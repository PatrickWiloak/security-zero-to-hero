---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 13 min
applies-to: AWS docs as read 2026-11-07
---

# 06 - Security foundations and governance

**Domain 6: Security Foundations and Governance (14%)** - SCS-C03 tasks 6.1 to 6.3.

Renamed from "Management and Security Governance". The theme is that security is a property of how accounts are organised and deployed, not of any single service.

---

## 6.1 Centrally deploy and manage AWS accounts

**AWS Organizations** groups accounts into organizational units (OUs) under a management account. Keep the management account nearly empty: no workloads, tightly controlled, because SCPs do not restrict it. Put workloads in member accounts by environment and sensitivity, and dedicate accounts to security tooling (security tooling and log archive accounts are standard).

**AWS Control Tower** builds a landing zone on top of Organizations with preventive controls (SCPs), detective controls (Config rules) and proactive controls, and an Account Factory to vend new accounts that start compliant. You can enable it in new and existing environments and deploy optional and custom controls.

**Organization policies** govern permissions at scale. From the SCP documentation:

- SCPs set the maximum available permissions for IAM users and roles in member accounts; they never grant permissions, and the effective permissions are the intersection of SCPs, RCPs and the identity and resource policies.
- They affect member accounts, including the member account's root user, and do not affect the management account or service-linked roles.
- They are available only in an organization with all features enabled.
- Do not remove the `FullAWSAccess` policy unless you replace it, or every action from member accounts fails. AWS recommends testing on a separate OU, moving accounts in a few at a time, rather than attaching an SCP to the root without testing.
- **Resource control policies (RCPs)** limit permissions on resources; **declarative policies** enforce a baseline configuration for a service (for example blocking public access) regardless of API calls; **AI service opt-out policies** control data use.

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "DenyOutsideApprovedRegions",
    "Effect": "Deny",
    "NotAction": ["iam:*", "organizations:*", "support:*", "sts:*"],
    "Resource": "*",
    "Condition": {
      "StringNotEquals": {"aws:RequestedRegion": ["us-east-1", "us-west-2"]}
    }
  }]
}
```

This deny-list SCP blocks activity outside two Regions while leaving global services working. `NotAction` with a deny excludes those actions from the deny.

**Centrally manage security services** with **delegated administrator** accounts: designate a security account as administrator for GuardDuty, Security Hub, Inspector, Config, Macie, IAM Access Analyzer and others, so you manage them without using the management account, and new accounts join automatically.

**Root user credentials.** Root is the most powerful identity and cannot be restricted by IAM policy in its own account. Give member accounts no root credentials where possible by **centralising root access** for member accounts, enable MFA on any root user you keep, and design **break-glass** procedures: sealed credentials, hardware MFA in a safe, alarms on any use, and a documented approval and review.

## 6.2 Secure, consistent deployment

**Infrastructure as code** makes security repeatable. **CloudFormation StackSets** deploy the same template to many accounts and Regions; third-party IaC tools work as well. Scan templates before deploy with **CloudFormation Guard** (policy-as-code rules) and **cfn-lint** (syntax and best-practice linting), failing the pipeline on violations.

**Tags** group resources by department, cost centre and environment, and drive ABAC (domain 4) and cost reporting. Enforce tagging with tag policies and Config rules.

**Deploy and enforce from a central source.** **AWS Firewall Manager** applies WAF, Shield Advanced, security group, Network Firewall and DNS firewall policies across accounts and enrolls new accounts automatically. **AWS Service Catalog** lets teams launch only approved, pre-secured products. **AWS Resource Access Manager** shares resources (subnets, transit gateways, rule groups) across accounts or the organization without copying them.

## 6.3 Evaluate compliance

**AWS Config** records resource configuration over time and evaluates it against rules. Detect and remediate noncompliant resources with **Config rules and remediation actions** (Systems Manager Automation), aggregate across accounts and Regions in an **aggregator**, and package rules as **conformance packs** (a conformance pack is a collection of rules and remediation actions deployed as one entity to an account or across an organization).

```bash
aws configservice put-organization-conformance-pack \
  --organization-conformance-pack-name org-baseline \
  --template-s3-uri s3://example-config-templates/org-baseline.yaml
```

**Security Hub** adds standards (AWS Foundational Security Best Practices, CIS, PCI DSS, NIST) and a security score. **AWS Audit Manager** continuously collects evidence mapped to frameworks and builds assessment reports for auditors. **AWS Artifact** is the portal for AWS's own compliance reports and agreements, which you hand to auditors as evidence for the provider's part of the shared responsibility model. The **AWS Well-Architected Tool** and its Security pillar review architectures against best practices.

Remember the division of duty: Artifact proves AWS's controls; Config, Security Hub and Audit Manager prove yours.

---

## Key terms

- **AWS Organizations** - the service that groups accounts into organizational units under a management account with central policies
- **Management account** - the organization's root account; SCPs do not restrict it
- **AWS Control Tower** - a service that sets up a governed multi-account landing zone with preventive and detective controls
- **Service control policy** - an organization policy defining maximum permissions for IAM users and roles in member accounts
- **Resource control policy** - an organization policy defining maximum permissions on resources in member accounts
- **Declarative policy** - an organization policy that enforces a baseline configuration for a service
- **Delegated administrator** - a member account designated to administer a service on behalf of the organization
- **Break-glass access** - emergency access using sealed credentials with alarms and review
- **CloudFormation StackSets** - a feature that deploys CloudFormation stacks to multiple accounts and Regions
- **CloudFormation Guard** - a policy-as-code tool that evaluates templates against rules
- **AWS Firewall Manager** - a service that centrally applies firewall and protection policies across accounts
- **AWS Service Catalog** - a service for offering approved, preconfigured products for self-service launch
- **AWS Resource Access Manager** - a service for sharing resources across accounts without copying them
- **AWS Config aggregator** - a collection of Config data from multiple accounts and Regions in one place
- **AWS Audit Manager** - a service that continuously gathers evidence mapped to compliance frameworks
- **AWS Artifact** - the portal for AWS compliance reports and agreements

---

## Related

- [Notes 04: identity and access management](./04-identity-and-access-management.md)
- [Notes 01: detection](./01-detection.md)
- [Governance and compliance topic](../../../../../topics/governance-and-compliance.md)
- **[📖 Service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)** - what SCPs do and do not affect, and testing advice
- **[📖 Conformance packs for AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/conformance-packs.html)** - rule and remediation bundles
- **[📖 SCS-C03 exam guide, Domain 6](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03-domain6.html)** - task statements and skills
