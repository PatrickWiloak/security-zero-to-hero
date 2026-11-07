---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 7 min
---

# AWS Security Specialty (SCS-C03) Scenarios

Worked situations for the design and troubleshooting tasks the exam leans on.

---

## Scenario 1: A role cannot use a key

**Scenario**: A role has an IAM policy allowing `kms:Decrypt` on a customer managed key, but decryption fails with access denied. The key was created from the CLI with a custom key policy naming only a deleted administrator role.

**Solution Pattern**:
- A key policy does not grant access to the account by default; IAM policies only work if the key policy includes the statement that enables them
- Contact AWS Support to regain control of an unmanageable key, then add the account root statement
- Prevent recurrence: always include the "enable IAM policies" statement and separate key administrators from key users

**Key Takeaway**: With KMS, check the key policy first, then IAM, then grants and conditions.

---

## Scenario 2: Guardrails for a new business unit

**Scenario**: A new business unit will run workloads in several accounts. Leadership wants no use of unapproved Regions, no one able to disable logging, and new accounts to start compliant.

**Solution Pattern**:
- Create an OU for the unit; test SCPs on a single account before attaching to the OU
- SCP denying actions outside approved Regions with a `NotAction` list for global services
- SCP denying `cloudtrail:StopLogging` and `cloudtrail:DeleteTrail`
- Control Tower Account Factory for new accounts, with detective controls and conformance packs

**Key Takeaway**: Preventive guardrails belong in organization policies; remember SCPs do not touch the management account.

---

## Scenario 3: Exposed access key

**Scenario**: GuardDuty reports API calls using a developer's access key from an unfamiliar country.

**Solution Pattern**:
- Validate: compare with CloudTrail for that key and check with the developer
- Contain: deactivate the key, attach a deny policy to the user and review active sessions
- Scope: Athena over CloudTrail for every action by the key; Detective for the activity timeline
- Eradicate and recover: remove resources the attacker created, rotate secrets the key could read
- Prevent: replace the user with IAM Identity Center and short-lived credentials

**Key Takeaway**: Validate, contain, scope using logs, then remove long-term credentials.

---

## Scenario 4: Logs missing from member accounts

**Scenario**: An organization trail exists, but a security analyst sees no events for one member account in the central bucket.

**Solution Pattern**:
- Check trail status for delivery errors (bucket policy, KMS key policy)
- Confirm the account is a member and the trail is multi-Region if events come from other Regions
- Check whether the account's Region is an opt-in Region not enabled for the trail
- Fix the policy and verify with `validate-logs` and new test events

**Key Takeaway**: Organization trails can be created in members even when delivery validation fails; check status.

---

## Scenario 5: Immutable audit log bucket

**Scenario**: Auditors require that audit logs cannot be deleted or altered for seven years, even by administrators.

**Solution Pattern**:
- New bucket in the log archive account with Object Lock enabled
- Default retention in compliance mode of seven years
- KMS encryption with a key policy limited to the logging service and auditors
- SCP denying changes to the bucket's configuration outside the security role

**Key Takeaway**: Compliance mode is the only mode that blocks root; governance mode can be bypassed with permission.

---

## Scenario 6: Private path to S3

**Scenario**: Workloads in private subnets with no internet access need to reach S3 only for the company's own buckets.

**Solution Pattern**:
- Gateway endpoint for S3 (route-table based, no PrivateLink)
- Endpoint policy limiting access to company buckets or the organization
- Bucket policy requiring requests to come through the endpoint (`aws:SourceVpce`)

**Key Takeaway**: Combine the endpoint policy (what the VPC can reach) with the bucket policy (who may reach the bucket).
