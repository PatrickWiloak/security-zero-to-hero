---
last-updated: 2026-11-07
---

# AWS Certified Security - Specialty (SCS-C03) - Practice Questions

29 original scenario questions weighted to the six SCS-C03 domains: Detection (16%) 4 questions, Incident Response (14%) 4, Infrastructure Security (18%) 5, Identity and Access Management (20%) 6, Data Protection (18%) 6 and Security Foundations and Governance (14%) 4. These are original questions, not vendor exam content.

> **Cert page:** [exams/aws/specialty/security-scs-c03/](../../exams/aws/specialty/security-scs-c03/)

---

### Question 1 - Domain 1: Detection
**Scenario:** A security team wants one trail that records API activity for every current and future account in the organization and that member-account administrators cannot switch off. What should they do?

A. Create an organization trail from the management or a delegated administrator account
B. Ask each account owner to create a trail pointing at the same S3 bucket name in the log archive account
C. Create a trail in each account and use an SCP to share the destination bucket across them
D. Turn on CloudTrail event history in every account console and export it once a month

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** An organization trail logs events for the management account and all member accounts, and member accounts can see it but cannot delete it, stop logging or change it. Per-account trails depend on every owner, and event history is a short, console-only view.
</details>

---

### Question 2 - Domain 1: Detection
**Scenario:** An organization wants to enable GuardDuty everywhere and have new accounts enrolled automatically without anyone using the management account day to day. Which design fits?

A. Enable GuardDuty by hand in each new account after it is created, using the console
B. Designate a security account as GuardDuty delegated administrator and enable it for the organization
C. Run GuardDuty only in the management account in the hope that it will see every workload
D. Use legacy invitations that the management account sends to each member account one by one

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** GuardDuty supports AWS Organizations with a delegated administrator, which centralises management and can auto-enable new accounts. Manual enablement and invitation-based linking do not scale, and GuardDuty monitors per account.
</details>

---

### Question 3 - Domain 1: Detection
**Scenario:** Security Hub controls for a newly onboarded account all show no findings, although the account has noncompliant resources. What is the most likely missing prerequisite?

A. Resource recording in AWS Config is not enabled in that account and Region
B. Nobody has created CloudWatch alarms for each Security Hub control in the account yet
C. The AWS Artifact reports for the quarter have not been downloaded by the compliance team
D. Amazon Macie has not been enabled in any Region for the account, so findings cannot be produced

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Security Hub uses service-linked AWS Config rules for most controls, so Config must be enabled and recording resources or most control findings are not generated. The other items do not feed control checks.
</details>

---

### Question 4 - Domain 1: Detection
**Scenario:** Analysts need to query VPC flow logs, CloudTrail and WAF logs together in a common schema and let a third-party tool subscribe to the data. Which service fits best?

A. AWS Artifact, which stores compliance reports and lets subscribers read them in one place
B. CloudWatch Logs Insights over three separate log groups, joined by hand in each query
C. A custom Lambda function that copies the logs between buckets every night and renames fields
D. Amazon Security Lake, which normalises sources to OCSF in S3 buckets you own

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Security Lake centralises security data into a data lake in your account, converts it to Parquet and OCSF, and supports subscribers. Logs Insights queries log groups but does not normalise or support subscribers.
</details>

---

### Question 5 - Domain 2: Incident Response
**Scenario:** GuardDuty reports API calls from an unfamiliar country using a developer's long-term access key. What should the responder do first after validating that the activity is not expected?

A. Wait for a second GuardDuty finding about the same key before taking any action at all
B. Rotate the account root password and leave the compromised access key active for now
C. Delete the developer's IAM user and every CloudTrail log that mentions the access key
D. Deactivate the access key and attach a deny policy while preserving CloudTrail evidence

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Containment disables the credential quickly without destroying evidence. Deleting logs destroys the investigation, waiting extends exposure and changing the root password does not stop the compromised key.
</details>

---

### Question 6 - Domain 2: Incident Response
**Scenario:** A compromised EC2 instance must be investigated. Which approach best preserves evidence and limits harm?

A. Install more investigation tools on it to find the malware before isolating it from the network
B. Reboot it so that all volatile data resets to a known state and the attacker loses access
C. Terminate the instance at once and build a replacement from the same compromised image
D. Isolate it with a no-traffic security group, snapshot its volumes, then rebuild from a clean image

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Isolation stops spread, snapshots preserve disk evidence for analysis in a forensics account, and rebuilding from a known-good image removes the compromise. Terminating or rebooting destroys evidence and tools installed on the host can alter it.
</details>

---

### Question 7 - Domain 2: Incident Response
**Scenario:** A team wants to confirm that its incident runbooks work under failure conditions before a real incident. Which action tests this?

A. Run a game day that injects controlled faults, for example with AWS Fault Injection Service
B. Raise the CloudTrail log retention to ten years and archive it in a locked bucket
C. Re-read the runbook text during the annual policy review and sign it off
D. Enable GuardDuty sample findings and leave them in the console without any follow-up

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Testing means exercising the plan under failure: controlled fault injection shows whether responders and automation actually behave. A document review, longer log retention or unattended sample findings do not exercise it. (Tabletop exercises are also a valid test, but this option is a review, not a rehearsal.)
</details>

---

### Question 8 - Domain 2: Incident Response
**Scenario:** After a suspected breach, analysts need to see how the activity of several principals, IP addresses and resources connects over time to find the root cause. Which service is designed for this?

A. Amazon Detective
B. Amazon Inspector
C. AWS Service Catalog
D. AWS Config conformance packs

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Detective collects log data and uses machine learning, statistical analysis and graph theory to build visualisations that help identify the root cause of findings. Config evaluates configuration, Service Catalog offers products and Inspector scans for vulnerabilities.
</details>

---

### Question 9 - Domain 3: Infrastructure Security
**Scenario:** Which design best defends a public web application behind CloudFront from request floods by individual clients and common web exploits?

A. Move the application into an isolated subnet that has no route to anything else
B. Attach AWS WAF with managed rule groups and rate-based rules to the distribution
C. Add more entries to the origin security group that allow traffic from every address
D. Enable VPC Flow Logs on the origin subnet and review the flow records every week

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** WAF web ACLs can combine managed rule groups for common attacks with rate-based rules that limit requests per client. Opening the security group or isolating the application does not protect it, and flow logs only observe.
</details>

---

### Question 10 - Domain 3: Infrastructure Security
**Scenario:** A team needs to block outbound TLS connections from a VPC to a list of known-bad domains and also needs intrusion prevention rules. Which service fits?

A. A security group with outbound deny rules for each domain name
B. A network ACL with entries for each domain name
C. Amazon Macie with a custom data identifier
D. AWS Network Firewall with a stateful rule group

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Network Firewall is a stateful managed firewall and intrusion prevention service using Suricata-compatible rules and domain filtering. Security groups have allow rules only and neither security groups nor network ACLs filter by domain name.
</details>

---

### Question 11 - Domain 3: Infrastructure Security
**Scenario:** Instances in private subnets must be administered without opening inbound ports or distributing SSH keys, and sessions must be logged. What should be used?

A. A bastion host with port 22 open to the internet and one set of shared SSH keys
B. AWS Systems Manager Session Manager with logging to CloudWatch Logs or S3
C. Elastic IP addresses on each instance with password logins enabled for administrators
D. A VPN connection to every instance, using a shared administrator account for all staff

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Session Manager needs no inbound ports or SSH keys, uses IAM for access and can log sessions. A public bastion with shared keys increases the attack surface and weakens accountability.
</details>

---

### Question 12 - Domain 3: Infrastructure Security
**Scenario:** Which statement about Amazon Inspector is correct?

A. It continually scans EC2 instances, ECR images and Lambda functions and rescans when new CVEs are published
B. A WAF web ACL with managed rule groups attached to the CloudFront distribution
C. AWS CloudTrail, which records every API call made across the organization
D. Amazon Macie sensitive data discovery that scans the buckets on a schedule and reports findings

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Inspector is a vulnerability management service that discovers and continually scans eligible workloads, rescanning on changes and new CVEs. Option B describes AWS WAF, C describes CloudTrail and D describes Macie, so none of them is Inspector.
</details>

---

### Question 13 - Domain 3: Infrastructure Security
**Scenario:** Private subnets must reach S3 without internet access and only for the organization's own buckets. Which combination meets this?

A. An interface endpoint with the default endpoint policy left exactly as it was created
B. A public subnet with a route to the internet gateway for the S3 address prefix
C. A NAT gateway with an allow rule for every S3 address range published by AWS
D. A gateway endpoint for S3 with an endpoint policy restricting access to the organization

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Gateway endpoints send S3 traffic privately over route tables, and an endpoint policy can restrict principals or resources, for example by organization. The default endpoint policy allows all actions by all principals, so it does not satisfy the restriction.
</details>

---

### Question 14 - Domain 4: Identity and Access Management
**Scenario:** An IAM user has an identity policy allowing s3:GetObject. An SCP applied to the account does not mention S3 and no FullAWSAccess policy is attached. What is the result?

A. The request is allowed only if the caller works from the management account
B. The request is allowed because identity policies override SCPs when they grant the action
C. The request is denied because the SCP must also allow the action
D. The request is allowed if the bucket is in the same Region as the calling user

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Effective permissions are the intersection of SCPs and identity policies, so both must allow. If FullAWSAccess has been removed and nothing allows S3, the action fails. SCPs never grant permissions.
</details>

---

### Question 15 - Domain 4: Identity and Access Management
**Scenario:** Developers should create their own IAM roles, but never grant those roles more than a defined set of permissions. Which feature enforces the cap?

A. An AWS Config rule that only emails the security team
B. A permissions boundary required on every role they create
C. A session policy attached to each console login
D. A resource policy on the IAM service itself

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A permissions boundary sets the maximum permissions an identity policy can grant, enabling delegated role creation when the boundary must be attached. Session policies limit a single session, and an email alert does not prevent the grant.
</details>

---

### Question 16 - Domain 4: Identity and Access Management
**Scenario:** A policy lets users start and stop only EC2 instances tagged with their own team. Which approach scales without a new role per team?

A. A network ACL that lists each team's instance addresses
B. One role per team with separately written instance ARNs
C. ABAC comparing aws:ResourceTag/team with aws:PrincipalTag/team
D. A single role with ec2:* on all resources

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** ABAC grants access when tags on the principal and the resource match, so one policy serves all teams. It depends on restricting who can change tags. The other options either multiply roles or over-grant.
</details>

---

### Question 17 - Domain 4: Identity and Access Management
**Scenario:** A partner's account needs to assume a role in your account to read audit data. How do you protect against the confused-deputy problem?

A. Give the partner a long-term access key for a dedicated IAM user in your own account
B. Allow the partner to assume the role without MFA or any other condition at all
C. Trust the partner's whole account with no condition and no further checks on callers
D. Add an external ID condition to the role's trust policy and give it to the partner

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** An external ID in the trust policy ensures the partner assumes the role only on behalf of the right customer. Sharing long-term keys or trusting the account unconditionally leaves the confused-deputy gap open.
</details>

---

### Question 18 - Domain 4: Identity and Access Management
**Scenario:** Security wants to find IAM roles and access keys that have not been used in 90 days across the organization. Which tool does this?

A. An external access analyzer created for the whole organization
B. The AWS Config managed rule iam-user-mfa-enabled in every account
C. An IAM credential report downloaded once a year and read by hand
D. An IAM Access Analyzer unused access analyzer for the organization

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Unused access analyzers report unused roles, access keys and passwords, and unused services and actions; the unused-access age is configurable (the default lookback is 90 days). External access analyzers report resources shared outside the zone of trust. Config and a manual credential report do not do this across an organization continuously.
</details>

---

### Question 19 - Domain 4: Identity and Access Management
**Scenario:** A user receives access denied on an action, and the identity policy allows it. CloudTrail shows the denial came from the organization. What is the most likely cause?

A. An AWS Config managed rule that checks S3 buckets for public read access settings
B. An SCP or RCP does not allow the action, for example restricting the Region
C. The Amazon Macie sensitive data discovery job that scans buckets for personal data
D. An external access analyzer, which reports resources shared outside the zone of trust

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** With organizations, the action must be allowed by the SCP and RCP as well as identity policies, and an explicit deny in any overrides. An SCP restricting Regions is a common cause.
</details>

---

### Question 20 - Domain 5: Data Protection
**Scenario:** A role's identity policy allows kms:Decrypt on a key, but access is denied. The key policy lacks any statement for the account root principal. What explains this?

A. Customer managed keys can only be used from the management account
B. The key must be multi-Region before IAM can allow it
C. The key policy must enable IAM policies for them to take effect
D. IAM policies override key policies for KMS only

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A KMS key policy does not automatically give permission to the account, and IAM policies that allow access are ineffective unless the key policy enables them, for example with the default account root statement.
</details>

---

### Question 21 - Domain 5: Data Protection
**Scenario:** Auditors require that log objects cannot be deleted or overwritten by anyone, including the account root user, for seven years. What meets the requirement?

A. Versioning with MFA delete on a bucket without Object Lock
B. S3 Object Lock in governance mode with a seven-year retention
C. S3 Object Lock in compliance mode with a seven-year default retention
D. A bucket policy denying delete for all roles except the security team

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** In compliance mode no user, including root, can delete or overwrite a protected version or shorten retention. Governance mode can be overridden with the bypass permission, and bucket policies can be changed.
</details>

---

### Question 22 - Domain 5: Data Protection
**Scenario:** A company must generate and hold key material itself and import it into AWS so it can prove control over generation. Which KMS capability applies?

A. Use AWS managed keys, which are generated by the service
B. Enable automatic rotation to make AWS generate the material
C. Create a KMS key with no key material and import your own
D. Use an S3 bucket key with the default encryption

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** KMS lets you create a key without key material and import your own. Imported material is not rotated automatically, so you manage rotation by importing into a new key. AWS managed keys are generated by AWS.
</details>

---

### Question 23 - Domain 5: Data Protection
**Scenario:** An application needs database credentials that rotate every 30 days without redeploying code. Which service is designed for this?

A. AWS Secrets Manager with a rotation schedule
B. A KMS key with automatic rotation enabled
C. An environment variable set at deploy time
D. A SecureString parameter in Systems Manager Parameter Store as a static value

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Secrets Manager rotates secrets by updating the credentials in both the secret and the database, and applications fetch the current value at runtime. Static parameters and environment variables do not rotate, and KMS rotates key material, not secrets.
</details>

---

### Question 24 - Domain 5: Data Protection
**Scenario:** A security policy requires all connections to an S3 bucket to use TLS. How is this enforced?

A. Turn on S3 versioning and MFA delete for the bucket so that old versions are kept
B. A lifecycle rule that expires every object in the bucket after thirty days
C. A bucket policy that denies requests when aws:SecureTransport is false
D. Enable S3 Bucket Keys on the bucket to reduce the number of KMS request charges

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A Deny with the condition aws:SecureTransport set to false rejects requests that do not use TLS. Versioning, action lists and lifecycle rules do not control transport encryption.
</details>

---

### Question 25 - Domain 5: Data Protection
**Scenario:** Which feature masks sensitive values in log events as they are ingested, so that principals without a special unmask permission see only asterisks?

A. CloudWatch Logs metric filters
B. CloudWatch Logs data protection policies
C. VPC endpoint policies
D. Route 53 Resolver query logging

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Data protection policies detect and mask sensitive data in log events; only principals with the logs:Unmask permission can view the original values. Metric filters create metrics, endpoint policies control endpoint use and resolver logs record DNS queries.
</details>

---

### Question 26 - Domain 6: Security Foundations and Governance
**Scenario:** An organization wants to ensure no member account can run workloads outside two approved Regions, while global services keep working. What fits?

A. A deny-list SCP using aws:RequestedRegion with NotAction for global services
B. Enabling versioning on the bucket so that earlier object versions stay available to readers
C. An IAM policy that allows only the s3:GetObject action to the application role
D. A lifecycle rule that expires any object that was uploaded without encryption

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** An SCP sets the maximum permissions for member accounts and can deny actions outside approved Regions with a NotAction list excluding global services. Option B (versioning), C (a narrow IAM allow) and D (a lifecycle rule) do not restrict Regions.
</details>

---

### Question 27 - Domain 6: Security Foundations and Governance
**Scenario:** Where should AWS Organizations workloads be run, and what do SCPs not affect?

A. Run workloads in the management account; SCPs apply to it fully
B. Run workloads in any account; SCPs affect service-linked roles
C. Run workloads in member accounts; SCPs do not affect the management account
D. Run workloads only in OUs without SCPs

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The management account should hold no workloads because SCPs do not restrict it. SCPs also do not affect service-linked roles.
</details>

---

### Question 28 - Domain 6: Security Foundations and Governance
**Scenario:** Auditors ask for evidence that AWS's own data centres meet a standard. Which service provides AWS's compliance reports?

A. AWS Config
B. AWS Artifact
C. AWS Security Hub
D. AWS Audit Manager

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Artifact is the portal for AWS compliance reports and agreements. Audit Manager gathers evidence about your own usage, Config records configuration and Security Hub checks standards on your resources.
</details>

---

### Question 29 - Domain 6: Security Foundations and Governance
**Scenario:** A platform team wants every new account to receive the same logging and security baseline from a template, and wants templates scanned for policy violations before deploy. What fits?

A. CloudFormation StackSets or Control Tower, with CloudFormation Guard in the pipeline
B. A manual review of every account by the security team once every six months
C. Separate untracked scripts that administrators keep and run from their laptops
D. Console clicks by each account owner following a wiki page in their own time

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Infrastructure as code with StackSets or Control Tower deploys consistently across accounts, and CloudFormation Guard evaluates templates against rules before deployment. Manual steps drift.
</details>

---
