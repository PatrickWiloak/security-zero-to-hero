# AWS Security Specialty (SCS-C02) Practice Questions

> **Retired exam.** SCS-C02 closed on December 1, 2025. These questions are kept for reference. For the current exam see the [SCS-C03 practice questions](./aws-security-specialty-scs-c03.md).

40 scenario-based questions weighted by exam domain.

## Exam Domain Breakdown
| Domain | Weight | Questions |
|--------|--------|-----------|
| Threat Detection and Incident Response | 14% | 6 |
| Security Logging and Monitoring | 18% | 7 |
| Infrastructure Security | 20% | 8 |
| Identity and Access Management | 16% | 6 |
| Data Protection | 18% | 7 |
| Management and Security Governance | 14% | 6 |

> **Cert page:** [exams/aws/specialty/security-scs-c02/](../../exams/aws/specialty/security-scs-c02/)

---

## Domain 1: Threat Detection and Incident Response (Questions 1-6)

### Question 1
**Scenario:** Your company's security team received an alert from Amazon GuardDuty indicating "UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.OutsideAWS". An EC2 instance's credentials appear to be used from an external IP address. What is the MOST appropriate immediate response?

A. Terminate the EC2 instance immediately, then launch a clean replacement from the AMI
B. Isolate the instance with a security group change, preserve evidence
C. Stop and start the instance so its IAM role credentials rotate, then resume normal operation once new credentials are issued
D. Delete the IAM role attached to the instance and recreate it with the same name

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The proper incident response is to isolate the compromised resource while preserving forensic evidence. Modifying security groups to restrict all traffic isolates the instance without destroying evidence. Terminating (A) or stopping (C) destroys volatile memory evidence. Deleting the IAM role (D) doesn't stop the attacker who already has the credentials and destroys audit trails.

**Key Concept:** [AWS Security Incident Response Guide](https://docs.aws.amazon.com/whitepapers/latest/aws-security-incident-response-guide/welcome.html)
</details>

### Question 2
**Scenario:** A company needs to automatically remediate GuardDuty findings for compromised EC2 instances. The remediation should isolate instances, capture memory dumps, and notify the security team. What architecture provides this automation?

A. GuardDuty → CloudWatch Events → Step Functions (orchestrate isolation, forensics, notification)
B. GuardDuty → S3 export → Athena analysis → manual remediation
C. GuardDuty → SNS → Lambda → SSM Run Command and a security group change, with one Lambda handling the whole flow in sequence
D. GuardDuty → Security Hub → AWS Config auto-remediation

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Step Functions provides orchestration for multi-step incident response workflows including parallel execution of isolation (security group changes), forensics (memory capture via SSM), and notification (SNS/SES). EventBridge (CloudWatch Events) triggers on GuardDuty findings. Option C lacks orchestration for complex workflows. Option B is not automated. Option D doesn't support custom remediation workflows for this use case.

**Key Concept:** [Automated Incident Response with Step Functions](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/automate-incident-response-and-forensics.html)
</details>

### Question 3
**Scenario:** During a security incident investigation, you need to analyze VPC Flow Logs to identify data exfiltration patterns. The logs are stored in S3 in their default format. You need to query terabytes of logs quickly and cost-effectively. Which approach is BEST?

A. Download logs to an EC2 instance and use grep/awk for analysis
B. Use Athena with partition projection
C. Import logs into Amazon OpenSearch Service for analysis
D. Use Amazon Macie to analyze the flow logs for sensitive data and anomalies

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Athena with partition projection provides serverless, cost-effective querying of S3 data without infrastructure management. Partition projection automatically handles the time-based partitioning of flow logs. You pay only for data scanned. Option A doesn't scale. Option C requires provisioning and is expensive for ad-hoc analysis. Option D is for sensitive data discovery, not network analysis.

**Key Concept:** [Querying VPC Flow Logs with Athena](https://docs.aws.amazon.com/athena/latest/ug/vpc-flow-logs.html)
</details>

### Question 4
**Scenario:** An organization wants to detect when IAM credentials are used from IP addresses outside their corporate network range. They also need alerts for API calls from Tor exit nodes and known malicious IPs. Which solution provides this detection?

A. Use AWS Config rules to evaluate IAM policy compliance
B. Create CloudWatch Logs metric filters on CloudTrail logs for source IP patterns, with an alarm on each
C. Enable GuardDuty with threat intelligence feeds and create custom threat lists
D. Implement VPC Flow Logs analysis with custom Lambda functions that flag traffic from known bad IP addresses

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** GuardDuty provides built-in threat intelligence including Tor exit nodes and known malicious IPs. Custom threat lists allow adding your own IP allow/deny lists. GuardDuty analyzes CloudTrail, VPC Flow Logs, and DNS logs automatically. CloudWatch metric filters (B) require complex regex and don't include threat intelligence. Config (A) is for resource compliance. VPC Flow Logs (D) don't capture IAM credential usage.

**Key Concept:** [GuardDuty Trusted IP and Threat Lists](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_upload-lists.html)
</details>

### Question 5
**Scenario:** Your security team needs to investigate a potential data breach that occurred 45 days ago. They need to analyze CloudTrail logs, VPC Flow Logs, and GuardDuty findings from that time period. How should you ensure this data is available?

A. Configure CloudTrail to log to S3, Flow Logs to S3/CloudWatch Logs, and export GuardDuty findings to S3
B. Use AWS Backup to retain security logs
C. CloudTrail, Flow Logs, and GuardDuty retain 90 days of data by default
D. Enable long-term retention in each service's console settings

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Default retention varies: CloudTrail Event History is 90 days but limited, GuardDuty findings are 90 days but archives after that, VPC Flow Logs in CloudWatch default to never expire but cost increases. For reliable long-term retention and analysis, all logs should be exported to S3 with appropriate lifecycle policies. This enables Athena queries and meets compliance requirements. AWS Backup (B) doesn't support these log types.

**Key Concept:** [AWS Security Logging Best Practices](https://docs.aws.amazon.com/prescriptive-guidance/latest/logging-monitoring-for-application-owners/aws-services-logging-monitoring.html)
</details>

### Question 6
**Scenario:** Amazon Detective shows that an IAM user has been making unusual API calls to download S3 objects at 3 AM, which is outside normal business hours. The user's regular pattern shows activity only during business hours. What additional context does Detective provide that GuardDuty does not?

A. Real-time alerting on the suspicious activity as it happens, which Detective generates from the behavior graph
B. Automatic remediation of the threat
C. The specific S3 objects that were accessed
D. Visualization of the user's historical behavior patterns and entity relationships

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Amazon Detective provides behavior graphs and entity relationship visualizations that show historical patterns, related resources, and the context around findings. It helps answer "what happened" and "why" during investigations. GuardDuty provides the alert (A), but Detective provides investigation context. Detective doesn't show specific object names (C) or provide remediation (B).

**Key Concept:** [Amazon Detective Investigation Flow](https://docs.aws.amazon.com/detective/latest/userguide/detective-investigation-flow.html)
</details>

---

## Domain 2: Security Logging and Monitoring (Questions 7-13)

### Question 7
**Scenario:** A company needs to aggregate security findings from GuardDuty, Inspector, Macie, IAM Access Analyzer, and Firewall Manager across 200 AWS accounts. They need a single dashboard for prioritization and automated response. Which solution provides this?

A. Build a custom EventBridge and Lambda aggregator
B. Use AWS Security Hub with organization-wide enablement and custom insights
C. Create a centralized CloudWatch dashboard pulling metrics from all accounts and every service
D. Deploy third-party SIEM and configure each service in each account to export its findings

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Security Hub provides native integration with AWS security services, organization-wide deployment via AWS Organizations, automated finding aggregation, compliance standards (CIS, PCI DSS), and custom insights for prioritization. It supports automated response via EventBridge integration. CloudWatch (C) doesn't aggregate security findings. Custom solution (A) requires significant development. Third-party SIEM (D) adds cost and complexity.

**Key Concept:** [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)
</details>

### Question 8
**Scenario:** Your organization requires that all API activity across all accounts be logged, protected from tampering, and retained for 7 years for compliance. Logs must be queryable for security investigations. How should you architect this?

A. Enable CloudTrail in each account logging to local S3 buckets with Object Lock, with each account team managing its own retention rules, bucket policies, and log access for its own account
B. Create an organization trail logging to a central S3 bucket with S3 Object Lock (Governance mode), a 7-year retention period, and a lifecycle rule moving logs to Glacier after 1 year
C. Enable CloudTrail Insights in each account with extended retention
D. Create an organization trail to a central S3 bucket in a dedicated log archive account with Object Lock (Compliance mode) and SCPs preventing log deletion

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Organization trails provide centralized logging across all accounts. A dedicated log archive account with restricted access follows AWS best practices. S3 Object Lock in Compliance mode (not Governance) provides WORM protection that even the root user cannot override. SCPs prevent deletion attempts. Glacier lifecycle reduces long-term costs while maintaining compliance. Option B uses Governance mode which can be overridden.

**Key Concept:** [AWS Log Archive Account](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/log-archive.html)
</details>

### Question 9
**Scenario:** A security team needs real-time alerts when root user credentials are used in any account across their AWS Organization. The alerts should include the source IP, user agent, and which API was called. What is the MOST efficient solution?

A. Configure EventBridge rules in each account forwarding to a central SNS topic
B. Use an organization trail with an EventBridge rule in the management account matching root user events
C. Enable GuardDuty root user monitoring across the organization
D. Create CloudWatch Alarms on CloudTrail metrics in each account

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** An organization trail centralizes all CloudTrail events to one location. A single EventBridge rule in the management account can match root user events from any account with access to source IP, user agent, and API details from the CloudTrail event. This is simpler than rules in each account (A). CloudWatch Alarms (D) don't provide event details. GuardDuty (C) detects anomalies but doesn't alert on all root usage.

**Key Concept:** [Monitoring Root User Activity](https://docs.aws.amazon.com/IAM/latest/UserGuide/cloudtrail-integration.html)
</details>

### Question 10
**Scenario:** An application team wants to log access to sensitive DynamoDB tables containing PII. They need to capture who accessed which items, when, and from where. Standard CloudTrail only shows API calls, not item-level access. What solution provides this granularity?

A. Implement application-level logging using X-Ray and custom annotations
B. Enable CloudTrail data events for DynamoDB and deliver them to a trail bucket
C. Enable DynamoDB Streams and process with Lambda to log access
D. DynamoDB doesn't support item-level access logging; use a different database that records reads, such as Amazon RDS

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** CloudTrail data events for DynamoDB capture item-level API activity including GetItem, PutItem, Query, and Scan operations. Events include the table name, key attributes accessed, and IAM identity. This provides the audit trail without application changes. DynamoDB Streams (C) captures changes, not reads. X-Ray (A) is for performance tracing, not security auditing.

**Key Concept:** [CloudTrail DynamoDB Data Events](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/logging-using-cloudtrail.html)
</details>

### Question 11
**Scenario:** You need to monitor for changes to security-critical resources (security groups, NACLs, IAM policies) across all accounts and receive alerts promptly when changes occur. Changes should be automatically reverted if they violate security policies. Which solution provides this?

A. CloudTrail log files in S3 scanned by a Lambda that reverts violating changes
B. AWS Config rules with automatic remediation using SSM Automation documents across accounts
C. GuardDuty detecting configuration changes
D. Security Hub with automated response playbooks

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** AWS Config records configuration changes and evaluates rules when a resource changes. Managed and custom rules flag violations, and automatic remediation runs SSM Automation documents. This covers security groups, NACLs, and IAM policies natively, and an aggregator or conformance packs extend it across accounts. CloudTrail/Lambda (A) requires custom development, and log files in S3 arrive with a delay. GuardDuty (C) detects threats, not general config changes. Security Hub (D) aggregates findings but does not provide config-level remediation.

**Key Concept:** [AWS Config Auto Remediation](https://docs.aws.amazon.com/config/latest/developerguide/remediation.html)
</details>

### Question 12
**Scenario:** A company is using AWS WAF to protect their web applications. Security requires that all blocked requests be logged with full request details for forensic analysis, but they want to minimize costs for allowed traffic logging. How should they configure WAF logging?

A. Enable WAF logging to CloudWatch Logs for all requests, then delete the allowed ones with a daily Lambda function
B. Use CloudFront access logs instead of WAF logging, and keep them for a year
C. WAF logging to Firehose with a BLOCK filter, delivered to S3
D. Enable WAF logging to an S3 bucket named waf-logs with a logging filter for BLOCK actions only

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** WAF logging filters let you keep only BLOCK actions, and Firehose can deliver the filtered stream to S3 for cost-effective storage and Athena analysis. This reduces log volume and costs significantly. Logging everything to CloudWatch and deleting later (A) pays for all the traffic first. A direct S3 destination (D) must be a bucket whose name starts with aws-waf-logs-, which this one does not. CloudFront logs (B) don't include WAF rule details.

**Key Concept:** [AWS WAF Logging](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html)
</details>

### Question 13
**Scenario:** Your organization needs to ensure all CloudWatch Log Groups containing security logs are encrypted with customer-managed KMS keys and have retention periods of at least 1 year. How can you continuously monitor and enforce this?

A. Run a daily Lambda to check log groups
B. Use Service Control Policies to require encryption on log group creation in every account
C. Use AWS Config custom rules evaluating log group encryption and retention
D. Enable CloudTrail and alert on CreateLogGroup events that are missing encryption settings

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** AWS Config custom rules can continuously evaluate CloudWatch Log Groups for both encryption status and retention period settings. Non-compliant resources are flagged and can trigger remediation. Lambda (A) provides point-in-time checks, not continuous monitoring. CloudTrail (D) only catches creation, not existing non-compliant resources. SCPs (B) can't enforce specific retention periods.

**Key Concept:** [AWS Config Custom Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html)
</details>

---

## Domain 3: Infrastructure Security (Questions 14-21)

### Question 14
**Scenario:** A company needs to allow HTTPS traffic from the internet to their application load balancer while ensuring all traffic between the ALB and EC2 instances in private subnets is also encrypted. The EC2 instances should not be directly accessible from the internet. How should this be architected?

A. ALB in public subnet with HTTPS listener, HTTPS to instances using ACM certificates, instance security groups allowing only the ALB
B. NLB in public subnet with TLS passthrough to instances
C. ALB in public subnet with HTTPS listener, HTTP to instances in private subnets, with security groups restricting instance access to the ALB
D. ALB in private subnet using AWS PrivateLink for internet access

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** ALB in public subnets handles internet traffic. HTTPS listeners terminate TLS, then re-encrypt to instances using certificates (ACM for ALB, self-signed or ACM-issued for instances). Security groups on instances allow traffic only from ALB's security group. Private subnets with no direct internet route ensure isolation. Option C doesn't encrypt ALB-to-instance traffic. NLB TLS passthrough (B) doesn't allow ALB-level security features. ALB can't be in private subnets for public traffic (D).

**Key Concept:** [End-to-End Encryption with ALB](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html)
</details>

### Question 15
**Scenario:** An organization wants to ensure that EC2 instances can only be launched using approved, hardened AMIs that have been scanned and approved by the security team. How should they enforce this?

A. Implement IAM policies with conditions restricting ec2:RunInstances to AMIs with specific tags
B. Create an SCP that allows ec2:RunInstances only for specific AMI IDs
C. Use EC2 Image Builder with automatic distribution and deprecate old AMIs once new hardened ones are published
D. Use an AWS Config rule to detect instances launched from unapproved AMIs and terminate them automatically within minutes

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** IAM policies (or SCPs) with conditions on ec2:RunInstances can restrict launches to AMIs matching specific tags (e.g., "approved:true") or owner (e.g., account ID of security team). This is preventive and flexible - new approved AMIs don't require policy updates. SCP with specific IDs (B) requires updates for each new AMI. Config (D) is detective, not preventive. Image Builder (C) helps create AMIs but doesn't prevent use of unapproved ones.

**Key Concept:** [IAM Condition Keys for EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-policy-structure.html#amazon-ec2-keys)
</details>

### Question 16
**Scenario:** A security team needs to ensure no security group in their VPCs has inbound rules allowing SSH (port 22) from 0.0.0.0/0. They want automatic remediation that removes such rules while preserving other rules in the security group. What solution provides this?

A. AWS Config managed rule "restricted-ssh" with SSM Automation remediation that deletes the security group
B. AWS Config managed rule "restricted-ssh" with custom Lambda remediation that removes every inbound rule from the group
C. GuardDuty detecting open security groups with EventBridge remediation
D. AWS Firewall Manager security group policy with auto-remediation

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** AWS Firewall Manager security group policies can audit and auto-remediate security groups across accounts and VPCs. It can specifically remove rules allowing 0.0.0.0/0 on specified ports while preserving other rules. This is purpose-built for this use case. Option B would strip every inbound rule, not only the offending one. Option A's remediation would delete the entire group. GuardDuty (C) doesn't detect security group configurations.

**Key Concept:** [AWS Firewall Manager Security Group Policies](https://docs.aws.amazon.com/waf/latest/developerguide/security-group-policies.html)
</details>

### Question 17
**Scenario:** An organization uses AWS Network Firewall to inspect traffic between VPCs in their Transit Gateway architecture. They need to ensure all east-west traffic between production and development VPCs is inspected, but traffic within the same environment bypasses inspection for performance. How should routing be configured?

A. Use VPC peering for same-environment traffic and Transit Gateway for cross-environment flows
B. Deploy a Network Firewall in every VPC, inspecting both local and cross-environment traffic
C. Attach all VPCs directly to Transit Gateway with a single shared route table and rely on Network Firewall rules to pick out cross-environment flows
D. Separate prod and dev TGW route tables, routing cross traffic via an inspection VPC

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Transit Gateway route tables enable sophisticated routing policies. Create separate route tables for prod and dev VPC attachments. Configure routes so traffic destined for the other environment routes through the inspection VPC (containing Network Firewall), while same-environment traffic routes directly. This provides selective inspection without performance impact on internal traffic. Option A creates management complexity. Option B is expensive and redundant.

**Key Concept:** [Transit Gateway Network Firewall Architecture](https://docs.aws.amazon.com/network-firewall/latest/developerguide/arch-two-zone-igw.html)
</details>

### Question 18
**Scenario:** A company is running sensitive workloads on EC2 that require protection against hardware-level attacks, including protection of data in memory from AWS operators. Which EC2 feature provides this capability?

A. EC2 instances in a dedicated tenancy VPC
B. EC2 Dedicated Hosts, which give physical isolation on hardware only your account uses
C. AWS Nitro Enclaves for processing sensitive data
D. EC2 instances with encrypted EBS volumes

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** AWS Nitro Enclaves create isolated compute environments with no persistent storage, no external networking, and cryptographic attestation. Even AWS operators and the parent instance cannot access data inside an enclave. This protects against hardware-level and privileged access attacks. Dedicated Hosts (B) provide physical isolation but not memory protection from operators. EBS encryption (D) protects data at rest. Dedicated tenancy (A) isolates from other customers, not AWS operators.

**Key Concept:** [AWS Nitro Enclaves](https://docs.aws.amazon.com/enclaves/latest/user/nitro-enclave.html)
</details>

### Question 19
**Scenario:** An application running on EC2 needs to access an S3 bucket containing sensitive data. Security requires that the traffic never traverses the public internet and that access be restricted to only this specific application. How should this be implemented?

A. Use an S3 gateway VPC endpoint with a bucket policy naming the endpoint, which any instance in the VPC can use through the route table
B. S3 interface endpoint with security groups and a bucket policy on the endpoint ID
C. Configure S3 Transfer Acceleration for private connectivity from the instances to the bucket
D. Use AWS PrivateLink for S3 over a Direct Connect link from the VPC to the bucket and back

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Interface endpoints (powered by PrivateLink) provide private IP addresses in your VPC that can be controlled with security groups, allowing restriction to specific EC2 instances. Bucket policies can further restrict access to the vpc endpoint ID. Gateway endpoints (A) don't support security groups and use route tables for access control, making application-specific restriction harder. Transfer Acceleration (C) uses public internet. PrivateLink with Direct Connect (D) is for hybrid connectivity.

**Key Concept:** [S3 Interface Endpoints](https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html)
</details>

### Question 20
**Scenario:** A web application protected by AWS WAF is experiencing a Layer 7 DDoS attack with requests that appear legitimate but are overwhelming the application. The attack is using multiple IP addresses that rotate frequently. Which WAF feature helps mitigate this?

A. IP reputation rule group blocking known bad IP addresses from Amazon threat intelligence feeds
B. Rate-based rule with custom aggregation keys plus Bot Control
C. Rate-based rule with the IP address aggregation key, set to a low threshold so that each rotating address is blocked quickly
D. Geo-blocking rules for suspicious countries, applied at the web ACL for all requests

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** When attackers rotate IPs, IP-based rate limiting is ineffective. Custom aggregation keys allow rate limiting based on other request attributes like session tokens, URI paths, or header values that remain constant across the attack. Combined with Bot Control's ML-based detection, this identifies and blocks sophisticated application-layer attacks. IP reputation (A) and IP-based rate limiting (C) don't work with rotating IPs. Geo-blocking (D) causes collateral damage to legitimate users.

**Key Concept:** [WAF Rate-Based Rules](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based.html)
</details>

### Question 21
**Scenario:** An organization needs to enforce that all new VPCs across all accounts have flow logs enabled and sent to a centralized log archive bucket. What is the MOST effective enforcement mechanism?

A. Training developers to always enable flow logs
B. CloudFormation StackSets deploying flow logs to all VPCs nightly
C. AWS Config rule with auto-remediation that creates flow logs when missing
D. SCP preventing VPC creation except through a Service Catalog product that creates VPCs with flow logs

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** SCPs provide preventive controls - denying ec2:CreateVpc except via Service Catalog ensures all VPCs are created through the approved product that includes flow log configuration. This prevents non-compliant resources from ever being created. Config auto-remediation (C) is reactive and creates a window of non-compliance. StackSets (B) are periodic, not continuous. Training (A) doesn't provide technical enforcement.

**Key Concept:** [Service Catalog for Governance](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/introduction.html)
</details>

---

## Domain 4: Identity and Access Management (Questions 22-27)

### Question 22
**Scenario:** A company is federating their on-premises Active Directory with AWS using AWS IAM Identity Center (successor to AWS SSO). They have 500+ employees who need different levels of access to 50 AWS accounts based on their AD group membership. What is the MOST scalable approach?

A. Sync AD users to Cognito and use Cognito identity pools to give them AWS console access across the 50 accounts
B. Configure IAM Identity Center with AD integration, create permission sets, and assign them to AD groups per account
C. Create IAM users in each account matched to AD users
D. Use SAML 2.0 federation with an IAM role in each account mapped to AD groups, maintaining the trust and role definitions per account

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** IAM Identity Center provides centralized management of multi-account access with AD integration. Permission sets define access levels, and these are assigned to AD groups for specific accounts. Users authenticate via AD, and Identity Center handles temporary credential generation. This scales to hundreds of accounts and thousands of users. IAM users (C) don't federate. SAML federation (D) requires role management in each account. Cognito (A) isn't designed for AWS console federation.

**Key Concept:** [IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)
</details>

### Question 23
**Scenario:** An application needs to access AWS services from both EC2 instances and on-premises servers. The on-premises servers cannot use IAM roles. The credentials must be short-lived and automatically rotated. What solution meets these requirements?

A. Use AWS STS directly from on-premises servers with hard-coded credentials embedded in the application configuration files
B. Store long-term credentials in Secrets Manager with automatic rotation
C. Use IAM Roles Anywhere with a private CA for on-premises servers, and IAM roles for EC2
D. Create IAM users with programmatic access and rotate access keys monthly by a scheduled script

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** IAM Roles Anywhere allows workloads outside AWS to obtain temporary credentials by presenting X.509 certificates issued by your CA. This provides the same short-lived, automatically rotated credentials as IAM roles without storing long-term secrets. EC2 instances use instance roles. Option D has long-lived credentials. Secrets Manager (B) still stores credentials. STS requires existing credentials to call (A).

**Key Concept:** [IAM Roles Anywhere](https://docs.aws.amazon.com/rolesanywhere/latest/userguide/introduction.html)
</details>

### Question 24
**Scenario:** A company wants to implement the principle of least privilege for their Lambda functions. Each function should only have access to the specific DynamoDB tables and S3 buckets it needs. Currently, all functions share a single IAM role with broad permissions. What is the BEST approach to remediate this?

A. Keep the single shared role and use resource-based policies on the tables and buckets to tell the functions apart
B. Implement application-level access controls in the Lambda code
C. Add IAM policy conditions based on the Lambda function name
D. Create separate IAM roles for each Lambda function with resource-level permissions

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Each Lambda function should have its own execution role with permissions scoped to only the resources it needs. This follows least privilege and blast radius reduction. Resource-level permissions specify exact table/bucket ARNs. Policy conditions (C) are complex and error-prone. Resource-based policies (A) cannot tell the functions apart while they all share one role, because the role is the principal. Application controls (B) don't restrict IAM permissions.

**Key Concept:** [Lambda Execution Role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html)
</details>

### Question 25
**Scenario:** An IAM policy is attached to a user granting full S3 access, but the user cannot access a specific bucket. The bucket has no bucket policy. The user is in an account that's part of AWS Organizations with SCPs applied. What is the MOST likely cause?

A. The IAM policy has a typo in the bucket name
B. S3 Block Public Access is preventing access
C. An SCP is denying S3 access
D. The bucket has server-side encryption that the user cannot access

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** SCPs set maximum permissions for accounts in an organization. Even if the IAM policy grants full S3 access, an SCP denying S3 actions would prevent access. SCPs are evaluated before IAM policies. Check SCPs at the OU level, parent OUs, and the organization root. Block Public Access (B) doesn't affect authenticated IAM users. Encryption (D) would show a different error. Typos (A) are possible but less common with existing buckets.

**Key Concept:** [SCP Evaluation Logic](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
</details>

### Question 26
**Scenario:** A security audit revealed that several IAM users have not used their credentials in over 90 days. Some have both console and programmatic access. The security team wants to automatically identify and disable inactive credentials without manual review of each user. What is the MOST efficient solution?

A. Use the access-keys-rotated Config rule, which only checks key age
B. Create a Lambda function that calls GetAccessKeyLastUsed and the disable API weekly, scanning every IAM user in the account
C. Use IAM credential reports, reviewed and acted on manually by a security analyst each month
D. Use IAM Access Analyzer unused access findings with automated remediation via Lambda

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** IAM Access Analyzer's unused access analysis continuously identifies credentials (passwords and access keys) not used within a specified period. Findings can trigger EventBridge rules for automated remediation (disabling credentials via Lambda). This is a managed service approach. Credential reports (C) are manual. Custom Lambda (B) duplicates Access Analyzer functionality. The access-keys-rotated Config rule (A) flags keys by age since creation, not by last use, and has no built-in disable step.

**Key Concept:** [IAM Access Analyzer Unused Access](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-unused-access.html)
</details>

### Question 27
**Scenario:** A cross-account setup requires Account A's Lambda function to write to Account B's DynamoDB table. Account B's security team wants to ensure only this specific Lambda function from Account A can access the table, not any other resources from Account A. How should this be configured?

A. Create an IAM user in Account B with a DynamoDB policy and share its access keys with Account A's Lambda function configuration
B. Enable cross-account access in DynamoDB table settings
C. Use a DynamoDB resource-based policy allowing Account A's root principal to write, then rely on Account A's IAM policy to limit which function uses it
D. Create an IAM role in Account B that Account A's Lambda assumes, with a trust policy naming the Lambda execution role ARN

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The trust policy on Account B's IAM role should specify the exact ARN of Account A's Lambda execution role as the principal. This ensures only that specific Lambda function can assume the role. The role's permissions policy grants DynamoDB write access. Allowing the Account A root principal in a resource-based policy (C) would let any identity in Account A that its own IAM policies permit reach the table, so Account B could not guarantee that only this function gets in. Shared credentials (A) violate security best practices. There's no cross-account setting (B) in DynamoDB.

**Key Concept:** [Cross-Account IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)
</details>

---

## Domain 5: Data Protection (Questions 28-34)

### Question 28
**Scenario:** A healthcare application stores PHI in DynamoDB. Compliance requires that all data be encrypted with customer-managed keys, the keys must be rotated annually, and key usage must be audited. Which configuration meets all requirements?

A. Enable DynamoDB encryption with a customer managed KMS key, enable automatic rotation, and log key usage in CloudTrail
B. Encrypt data in the application before storing in DynamoDB
C. Use DynamoDB default encryption with AWS managed keys
D. Use DynamoDB encryption with AWS owned keys and application-level encryption

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Customer managed KMS keys (CMKs) provide full control over key policies, rotation schedules, and usage auditing via CloudTrail. DynamoDB encryption with CMKs encrypts all table data at rest transparently. Automatic rotation creates new key material annually while maintaining access to data encrypted with previous versions. AWS managed keys (C) don't allow custom rotation or access policies. Application-level (B) adds complexity and doesn't encrypt indexes. AWS owned keys (D) provide no visibility.

**Key Concept:** [DynamoDB Encryption at Rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html)
</details>

### Question 29
**Scenario:** An application needs to store database credentials that will be used by multiple Lambda functions. The credentials should be automatically rotated every 30 days, and rotation should not cause application downtime. Which solution provides this?

A. Store credentials in Secrets Manager with automatic rotation using alternating users strategy
B. Use IAM database authentication instead of credentials
C. Store credentials in Lambda environment variables and update every function's configuration each time the password rotates
D. Store credentials in Parameter Store SecureString with manual rotation

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Secrets Manager with automatic rotation handles the complexity of credential rotation. The alternating users strategy creates two database users and rotates between them, ensuring one set of credentials is always valid during rotation (zero downtime). Lambda functions using the Secrets Manager SDK automatically get current credentials. Parameter Store (D) requires custom rotation logic. Environment variables (C) require redeployment. IAM auth (B) is ideal when supported, but isn't available for all databases.

**Key Concept:** [Secrets Manager Rotation Strategies](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html)
</details>

### Question 30
**Scenario:** A company needs to encrypt S3 objects with different keys for different customers' data within the same bucket. Each customer should only be able to decrypt their own data. How should this be implemented?

A. Use SSE-KMS with a separate customer managed key per customer, with key policies granting access to that customer only
B. Create separate S3 buckets for each customer with SSE-S3
C. Use SSE-S3 with different prefixes for each customer
D. Use client-side encryption with customer-provided keys

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** SSE-KMS allows specifying different KMS keys for different objects. Creating a CMK per customer with key policies restricting access to that customer's IAM principals ensures cryptographic separation. Even if a customer can access the S3 object, they cannot decrypt another customer's data without their KMS key. SSE-S3 (C) uses a single key per bucket. Client-side (D) adds application complexity. Separate buckets (B) don't scale well.

**Key Concept:** [S3 Server-Side Encryption with KMS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingKMSEncryption.html)
</details>

### Question 31
**Scenario:** An organization needs to share encrypted EBS snapshots with a partner AWS account. The snapshots are encrypted with a customer managed KMS key. What steps are required to enable the partner to use these snapshots?

A. Share the snapshot and share the KMS key by adding the partner account to the key policy, with no further steps
B. Share the snapshot, allow the partner in the key policy, and add a grant
C. Export the snapshot to S3 as an encrypted object, then share it through cross-account bucket access and a bucket policy
D. Copy the snapshot using an AWS managed key, then share the copy with the partner account

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Sharing encrypted snapshots requires both sharing the snapshot (ModifySnapshotAttribute) and providing access to the KMS key. The key policy must allow the partner account as a principal, and a grant should be created specifying the partner account with permissions to use the key for EBS operations. Option A is incomplete without the grant. Option D loses the original encryption. Snapshots can't be exported to S3 (C).

**Key Concept:** [Sharing Encrypted Snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html)
</details>

### Question 32
**Scenario:** A security team needs to discover and classify sensitive data (PII, financial data) across hundreds of S3 buckets. They need ongoing monitoring for new sensitive data uploads and integration with their security workflow. Which service provides this?

A. AWS Config rules checking S3 object tags that your team applies after reviewing each bucket's contents
B. S3 Storage Lens with custom metrics
C. Amazon Macie with automated sensitive data discovery and Security Hub integration
D. Amazon Inspector scanning S3 buckets

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Amazon Macie is purpose-built for sensitive data discovery in S3. It uses ML and pattern matching to identify PII, PHI, financial data, and credentials. Automated discovery jobs continuously scan for sensitive data. Findings integrate with Security Hub for centralized security workflow. Storage Lens (B) is for storage analytics. Config (A) requires manual tagging. Inspector (D) scans for vulnerabilities, not data classification.

**Key Concept:** [Amazon Macie](https://docs.aws.amazon.com/macie/latest/user/what-is-macie.html)
</details>

### Question 33
**Scenario:** An application uses AWS KMS for encryption. The security team wants to ensure that specific KMS operations (like ScheduleKeyDeletion and DisableKey) can only be performed by a senior administrator role, even if other administrators have full KMS permissions. How can this be enforced?

A. Use IAM permission boundaries to restrict KMS operations for the other administrators
B. Enable MFA delete on KMS keys, and require a hardware token for key deletion
C. Create an SCP that denies these operations to every principal in every account in the organization
D. A key policy deny for all but the senior admin role

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** KMS key policies are resource-based policies that have explicit precedence. A policy statement explicitly denying ScheduleKeyDeletion and DisableKey to all principals except the senior admin role ARN will be enforced regardless of IAM permissions. The key policy is the primary authorization mechanism for KMS keys. An SCP that denies the operations for everyone (C) would block the senior administrator as well. Permission boundaries (A) apply to users/roles, not resources. MFA delete (B) isn't a KMS feature.

**Key Concept:** [KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)
</details>

### Question 34
**Scenario:** A company needs to encrypt data with keys that have never been and will never be accessible to AWS, including during encryption/decryption operations. The keys must remain in their on-premises HSM. How can they achieve this?

A. Use AWS KMS customer managed keys with key material imported from the on-premises HSM
B. Use client-side encryption with the AWS Encryption SDK, using data keys generated by AWS KMS
C. Use AWS CloudHSM clusters
D. Use AWS KMS with external key store (XKS) connected to their HSM

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** KMS External Key Store (XKS) allows you to use KMS with keys stored in HSMs outside of AWS. All cryptographic operations are performed by your external HSM - the key material never enters AWS. This meets "hold your own key" (HYOK) requirements. CloudHSM (C) keys are in AWS-hosted hardware. Client-side encryption with KMS-generated data keys (B) exposes the keys to AWS. Imported key material (A) copies keys into KMS.

**Key Concept:** [KMS External Key Store](https://docs.aws.amazon.com/kms/latest/developerguide/keystore-external.html)
</details>

---

## Domain 6: Management and Security Governance (Questions 35-40)

### Question 35
**Scenario:** An organization is implementing a multi-account strategy using AWS Control Tower. They need to ensure all accounts have a consistent security baseline including CloudTrail logging, Config enabled, and GuardDuty active. New accounts should automatically receive this configuration. What is the MOST efficient approach?

A. Use Control Tower Account Factory with custom blueprints and mandatory guardrails
B. Create CloudFormation templates and deploy via StackSets to all accounts
C. Manually configure each new account following a runbook
D. Write Lambda functions triggered by account creation events

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Control Tower Account Factory with customizations (Account Factory for Terraform or Customizations for Control Tower) allows defining a baseline that's automatically applied to new accounts. Mandatory guardrails enforce security controls. Account Factory integrates with Service Catalog for self-service provisioning with guardrails. StackSets (B) require management and don't integrate with Account Factory. Lambda (D) adds complexity. Manual (C) doesn't scale.

**Key Concept:** [Control Tower Account Factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html)
</details>

### Question 36
**Scenario:** A compliance audit requires documentation that all EC2 instances have been patched within 30 days of critical security patches being released. The organization uses AWS Systems Manager for patch management. How can they generate this compliance documentation?

A. Use Systems Manager Patch Manager compliance reports and AWS Config conformance packs
B. Export CloudTrail logs showing patch commands
C. Create custom CloudWatch dashboards showing patch status for each instance, with alarms when a patch is missing for 30 days
D. Manually document patches in a spreadsheet, filled in by each system owner after every patch window

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Patch Manager provides compliance reports showing patch status per instance, including which patches are missing and for how long. AWS Config can record patch compliance state over time. Conformance packs can validate instances meet the 30-day patching requirement. This provides auditable, historical compliance data. CloudTrail (B) shows actions, not compliance state. CloudWatch (C) is for metrics, not compliance. Manual documentation (D) isn't reliable.

**Key Concept:** [Systems Manager Patch Compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-compliance-about.html)
</details>

### Question 37
**Scenario:** A security team needs to evaluate their AWS environment against CIS AWS Foundations Benchmark and PCI DSS requirements. They want automated checks, centralized findings, and the ability to track remediation progress. What solution provides this?

A. Enable Security Hub with CIS AWS Foundations and PCI DSS security standards
B. Use AWS Audit Manager to assess CIS and PCI compliance
C. Deploy third-party compliance scanning tools
D. Create custom AWS Config rules for each control

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Security Hub provides pre-built security standards including CIS AWS Foundations Benchmark and PCI DSS. It automatically runs checks, aggregates findings with severity ratings, and tracks compliance scores over time. Findings can be integrated with ticketing systems for remediation tracking. Audit Manager (B) is for audit evidence collection, not automated compliance checks. Custom Config rules (D) require significant development effort. Third-party (C) adds cost.

**Key Concept:** [Security Hub Security Standards](https://docs.aws.amazon.com/securityhub/latest/userguide/standards-reference.html)
</details>

### Question 38
**Scenario:** An organization wants to implement a "break glass" process allowing emergency access to production accounts that bypasses normal approval workflows. The access should be heavily logged and automatically revoked after 4 hours. How should this be implemented?

A. Store root account credentials in a sealed envelope
B. Create a break glass IAM role with a 4-hour session duration, require MFA to assume it, and enable CloudTrail logging of all its activity
C. Use IAM Identity Center with a permission set that opens only after a manager approves each request, and remove the assignment by hand afterwards
D. Provide production credentials to on-call engineers

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A dedicated break glass IAM role can be assumed without an approval step, MFA protects it, the session ends at the 4-hour maximum session duration, and CloudTrail records every call (add an alarm on its use). Root credentials in an envelope are too powerful and do not expire. A manager approval step conflicts with bypassing approval, and manual removal is not automatic revocation (C). Sharing production credentials (D) is unsafe.

**Key Concept:** [Implement break-glass procedures](https://docs.aws.amazon.com/wellarchitected/latest/devops-guidance/ag.sad.5-implement-break-glass-procedures.html)
</details>

### Question 39
**Scenario:** A company uses multiple AWS services that each have their own logging capabilities (CloudTrail, VPC Flow Logs, ALB access logs, S3 access logs, RDS logs). They need a unified security analysis platform that allows correlation across all log types for threat detection. What architecture should they implement?

A. Send all logs to CloudWatch Logs and use Logs Insights for queries
B. Send all logs to S3, catalog with Glue, and query with Athena
C. Send all logs to Amazon OpenSearch Service with SIEM capabilities and dashboards
D. Send all logs to Security Hub for analysis

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** OpenSearch Service with SIEM (Security Information and Event Management) capabilities provides log aggregation, correlation, real-time analysis, alerting, and dashboards. It can ingest all AWS log types and correlate events across services for threat detection. This is the standard architecture for security operations centers. CloudWatch Insights (A) has query limits and isn't designed for SIEM workloads. Athena (B) is good for ad-hoc but not real-time correlation. Security Hub (D) aggregates findings, not raw logs.

**Key Concept:** [SIEM on AWS](https://aws.amazon.com/solutions/implementations/centralized-logging-with-opensearch/)
</details>

### Question 40
**Scenario:** An AWS environment has accumulated over 5 years of configuration drift, undocumented changes, and potential security misconfigurations. The security team wants to assess the current state against security best practices and identify the highest-risk findings to prioritize remediation. What is the fastest path to this assessment?

A. Run AWS Trusted Advisor and review security checks
B. Hire a third-party penetration testing firm
C. Enable Security Hub with all security standards and review findings sorted by severity
D. Manually review all resources in the AWS console

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Security Hub provides immediate, automated assessment against multiple security standards (CIS, PCI DSS, AWS Foundational Security Best Practices). Findings are prioritized by severity, enabling the team to focus on critical issues first. It aggregates findings from other AWS security services (GuardDuty, Inspector, Macie) for comprehensive view. Trusted Advisor (A) has limited security checks. Manual review (D) doesn't scale. Pen testing (B) focuses on exploitability, not configuration compliance.

**Key Concept:** [AWS Security Hub Best Practices](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-fsbp.html)
</details>
