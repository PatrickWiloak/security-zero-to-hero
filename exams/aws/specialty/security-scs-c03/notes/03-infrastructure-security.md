---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
applies-to: AWS docs as read 2026-11-07
---

# 03 - Infrastructure security

**Domain 3: Infrastructure Security (18%)** - SCS-C03 tasks 3.1 to 3.3.

This is where traffic and compute are protected: the edge, the workload, and the network between. The C03 guide dropped host-based security and TCP/IP fundamentals and added OCSF-format edge integration and generative AI guardrails.

---

## 3.1 Network edge services

Pick edge defences from the threat. Volumetric denial of service points to **AWS Shield** (Standard is automatic; Advanced adds detection, response support and cost protection). Application-layer attacks and the OWASP Top 10 point to **AWS WAF** on CloudFront, an Application Load Balancer, API Gateway or AppSync. Content delivery points to **Amazon CloudFront**, which can restrict access by geography, require signed URLs or cookies, add security headers through response header policies, and keep origins private.

WAF is built from web ACLs containing rules and rule groups. Use AWS managed rule groups for common attack classes, then add your own:

- **Rate-based rules** limit requests per client over a window, the standard answer to brute force and scraping.
- **Geographic match** rules allow or block countries.
- **Bot Control and fingerprinting** distinguish automated clients (client fingerprinting is named in the guide).
- **Logging** to S3, CloudWatch Logs or Kinesis for analysis; Security Lake can ingest WAF logs.

Other edge points the guide lists: **S3 cross-origin resource sharing (CORS)** configured narrowly, **AWS IoT policies** for device access, and **Firewall Manager** to apply WAF and Shield policies across accounts. Integrations (skill 3.1.4) include ingesting data in OCSF format and using third-party WAF rules.

Design principle: protect the origin as well as the edge. A CloudFront distribution does nothing for security if the origin load balancer accepts traffic from the whole internet; restrict the origin to CloudFront (managed prefix list or a secret header checked by WAF).

## 3.2 Compute workloads

**Hardened images.** Build golden **AMIs** and container images that embed controls: minimal packages, the Systems Manager agent, logging agent, CIS-style configuration. **EC2 Image Builder** automates build, test and distribution pipelines. Scan images before use and rebuild rather than patching in place.

**Instance profiles and execution roles.** Compute never carries long-term keys. An EC2 **instance profile** passes an IAM role to the instance; Lambda uses an **execution role**; ECS uses task roles; services use **service roles** to act on your behalf. Scope each to exactly what the workload needs, and restrict `iam:PassRole` so a user cannot hand a more powerful role to a service.

**Vulnerability scanning.** Amazon Inspector is a vulnerability management service that automatically discovers workloads and continually scans EC2 instances, container images in ECR and Lambda functions for software vulnerabilities and unintended network exposure. It rescans automatically when a package is installed, a patch is applied or a new CVE is published, produces a risk score adjusted to your environment (for example lowering a finding when no internet path exists), closes findings when you remediate, and can be activated across an organization with a delegated administrator. GuardDuty Runtime Monitoring watches runtime behaviour on EKS, EC2 and ECS.

**Patching.** Systems Manager **Patch Manager** applies patches by baseline and maintenance window; Inspector validates the result. Automate it and report compliance.

**Administrative access.** Prefer **Systems Manager Session Manager** (no inbound ports, no SSH keys, IAM-controlled, logged to CloudWatch Logs or S3) or **EC2 Instance Connect** (short-lived keys) over bastion hosts with open port 22.

**Pipeline security.** Scan code and dependencies in the pipeline: Amazon Q Developer and Amazon CodeGuru Security are the guide's examples.

**Generative AI guardrails (new in C03).** Apply protections for generative AI applications by following the GenAI OWASP Top 10 for LLM Applications: prompt injection, sensitive information disclosure, excessive agency and similar. Practical controls include Amazon Bedrock Guardrails for content and sensitive-information filtering, least-privilege roles for agents, input and output validation, and GuardDuty AI Protection for Bedrock and SageMaker AI workloads.

## 3.3 Network security controls

**Security groups** are stateful, attach to network interfaces, support allow rules only, and can reference other security groups. **Network ACLs** are stateless, attach to subnets, support allow and deny, and evaluate rules in number order. Use security groups as the primary control and network ACLs as a coarse subnet-level backstop or for explicit denies.

**AWS Network Firewall** is a stateful, managed network firewall and intrusion detection and prevention service for a VPC. It uses the Suricata open-source IPS for stateful inspection and supports Suricata-compatible rules, domain filtering and deep packet inspection. Resources: a **firewall** (with endpoints in dedicated firewall subnets), a **firewall policy**, and **rule groups** that are stateless (single packets, no flow context) or stateful (in context of the flow). Traffic is steered to the firewall endpoints with route tables, and a firewall endpoint cannot inspect traffic in its own subnet, so use dedicated subnets. Firewall Manager can deploy it across accounts.

```
drop tls $HOME_NET any -> $EXTERNAL_NET any (tls.sni; dotprefix; content:".blocked.example"; endswith; nocase; msg:"Block TLS to listed domain"; flow:to_server; sid:1000001; rev:1;)
```

This Suricata-style stateful rule drops TLS connections whose server name ends in a listed domain. The exam asks when to use it, not to write rules: choose Network Firewall for deep inspection, domain filtering and IPS in the VPC, and security groups for simple port rules.

**Hybrid connectivity.** **Site-to-Site VPN** is quick and encrypted over the internet; **Direct Connect** gives a dedicated link that is not encrypted by default, so add **MACsec** (layer 2, on supported dedicated connections) or run a VPN over it. **AWS Verified Access** gives zero-trust access to applications without a VPN, evaluating identity and device posture per request.

**Segmentation.** Separate workloads into VPCs and subnets: public, private and isolated subnets (no route to the internet). Plan north/south traffic (in and out of the VPC) and east/west traffic (between workloads). Use transit gateway route tables to segment VPCs, and Network Firewall in an inspection VPC for central east/west inspection.

**Find unnecessary access.** **Network Access Analyzer** identifies unintended network paths; **Inspector network reachability findings** and **Verified Access** help trim exposure. Review security groups for 0.0.0.0/0 on administrative ports.

**Private access to AWS services (domain 5 overlaps).** A **gateway endpoint** (S3 and DynamoDB only) uses route tables and is not PrivateLink; **interface endpoints** (PrivateLink) put an elastic network interface in your subnet. VPC endpoint policies are IAM resource policies attached to the endpoint; the default policy allows everything, so tighten it, for example to your own organization:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": "*",
    "Action": "*",
    "Resource": "*",
    "Condition": {"StringEquals": {"aws:PrincipalOrgID": "o-exampleorgid"}}
  }]
}
```

---

## Key terms

- **AWS WAF** - a web application firewall that filters HTTP requests to CloudFront, load balancers, API Gateway and AppSync using web ACLs
- **Rate-based rule** - a WAF rule that limits requests per client over a time window
- **AWS Shield Advanced** - an optional DDoS protection tier with enhanced detection, response support and cost protection
- **Instance profile** - the container that passes an IAM role to an EC2 instance
- **EC2 Image Builder** - a service that automates building, testing and distributing hardened images
- **Amazon Inspector** - a vulnerability management service that continuously scans EC2, ECR images and Lambda functions
- **Session Manager** - a Systems Manager capability for shell access without inbound ports or SSH keys
- **Security group** - a stateful, allow-only firewall attached to network interfaces
- **Network ACL** - a stateless subnet-level filter with ordered allow and deny rules
- **AWS Network Firewall** - a managed stateful firewall and intrusion prevention service for a VPC that uses Suricata-compatible rules
- **Gateway endpoint** - a VPC endpoint type for S3 and DynamoDB that uses route tables rather than PrivateLink
- **Interface endpoint** - a PrivateLink endpoint that places an elastic network interface in your subnet
- **VPC endpoint policy** - an IAM resource policy attached to a VPC endpoint that controls which principals can use it
- **MACsec** - layer 2 encryption available on supported Direct Connect dedicated connections
- **AWS Verified Access** - a service giving zero-trust access to applications based on per-request identity and device checks

---

## Related

- [Notes 05: data protection](./05-data-protection.md)
- [Implement zero trust](../../../../../resources/hands-on-projects/implement-zero-trust.md)
- **[📖 What is AWS Network Firewall?](https://docs.aws.amazon.com/network-firewall/latest/developerguide/what-is-aws-network-firewall.html)** - Suricata rules, firewall, policy and rule groups
- **[📖 What is Amazon Inspector?](https://docs.aws.amazon.com/inspector/latest/user/what-is-inspector.html)** - continuous scanning and risk score
- **[📖 AWS PrivateLink concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html)** - endpoint types and endpoint policies
- **[📖 SCS-C03 exam guide, Domain 3](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03-domain3.html)** - task statements and skills
