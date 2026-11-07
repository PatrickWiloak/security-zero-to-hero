---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 4 min
---

# AWS Security Specialty (SCS-C03) Study Plan

Six weeks at 6-8 hours a week for someone with working AWS experience. Study against the [exam guide](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03.html). Use a sandbox account you can afford to break; never practise in a production or client account.

## Week 1: Identity and access management (Domain 4, 20%)

- [ ] Read `notes/04-identity-and-access-management.md`
- [ ] Explain, in order, how an explicit deny, SCP, boundary, session policy and identity policy combine
- [ ] Write an ABAC policy and say what stops a user editing their own tags
- [ ] Create an Access Analyzer external and unused analyzer and read the findings
- [ ] Work through the [least-privilege IAM review lab](../../../../resources/hands-on-projects/least-privilege-iam-review.md)

## Week 2: Security foundations and governance (Domain 6, 14%)

- [ ] Read `notes/06-security-foundations-and-governance.md`
- [ ] Draw an OU layout with security tooling and log archive accounts
- [ ] Write a Region-restriction SCP and say which actions it must exclude
- [ ] State what SCPs do not affect
- [ ] List what a delegated administrator manages and why not the management account

## Week 3: Data protection (Domain 5, 18%)

- [ ] Read `notes/05-data-protection.md`
- [ ] Read a KMS default key policy and say what each statement allows
- [ ] Choose between KMS, CloudHSM, client-side and server-side encryption for four cases
- [ ] Explain compliance versus governance mode, and legal hold
- [ ] Rotate a Secrets Manager secret

## Week 4: Infrastructure security (Domain 3, 18%)

- [ ] Read `notes/03-infrastructure-security.md`
- [ ] Compare security groups, network ACLs and Network Firewall
- [ ] Put WAF rate-based and managed rules on a test distribution
- [ ] Decide between gateway and interface endpoints and write an endpoint policy

## Week 5: Detection and incident response (Domains 1 and 2, 16% and 14%)

- [ ] Read notes 01 and 02
- [ ] Create an organization trail and validate logs
- [ ] Enable GuardDuty and generate sample findings
- [ ] Write a runbook for an exposed access key and one for a compromised instance
- [ ] Read the [cloud incident response tabletop](../../../../resources/hands-on-projects/cloud-incident-response-tabletop.md) and talk it through

## Week 6: Practice and review

- [ ] Work through the [practice questions](../../../../resources/practice-questions/aws-security-specialty-scs-c03.md); read every explanation
- [ ] Re-read the notes for any domain below 70%
- [ ] Work through the [scenarios](./scenarios.md)

## Readiness check

You are ready when you can explain, without notes: why a key policy without the account statement breaks IAM access, the difference between an SCP and a permissions boundary, which service detects versus aggregates versus investigates, and where each log source comes from.
