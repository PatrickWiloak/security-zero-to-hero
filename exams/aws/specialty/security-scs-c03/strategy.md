---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 5 min
---

# AWS Security Specialty (SCS-C03) Study Strategy

## What kind of exam this is

Sixty-five questions in 170 minutes, of which 50 are scored. Question types include multiple choice, multiple response, ordering and matching. Multiple response has two or more correct answers out of five or more options, and ordering and matching need every item correct for credit. Unanswered questions score zero, with no penalty for guessing, so answer everything.

## Reading questions

1. Find the constraint words: "least operational overhead", "across all accounts", "without changing the application", "must be tamper-proof", "cannot be disabled by account administrators".
2. Find where the control must live. Organization-wide and cannot-be-disabled points to SCPs, delegated administrators and Control Tower. Per-resource points to resource policies. Per-network points to endpoints and firewalls.
3. Prefer managed, automated, least-privilege answers. Strike answers that use long-term keys, wildcard actions, shared accounts or a human doing a repeatable job.
4. Check Region: many services (Security Hub, Access Analyzer external analyzers, GuardDuty) are per-Region.

## Distinctions to own

- **Detect, aggregate, investigate**: GuardDuty finds, Security Hub aggregates and scores, Detective investigates.
- **SCP, boundary, session policy**: three limiting policies at three scopes.
- **Key policy, IAM policy, grant**: all three can authorise KMS use; the key policy must allow IAM first.
- **Compliance mode versus governance mode**.
- **Security group versus network ACL versus Network Firewall**.
- **Gateway versus interface endpoint**.
- **Secrets Manager versus Parameter Store versus KMS**.
- **Artifact versus Audit Manager versus Config**.

## Weights

| Domain | Weight | Time share |
|---|---:|---|
| Identity and Access Management | 20% | Largest; give extra time |
| Infrastructure Security | 18% | Steady |
| Data Protection | 18% | Steady |
| Detection | 16% | Steady |
| Incident Response | 14% | Steady |
| Security Foundations and Governance | 14% | Steady |

## Resources

Use the [exam guide](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03.html) as the checklist, the [notes](./notes/01-detection.md) for explanation and the [practice questions](../../../../resources/practice-questions/aws-security-specialty-scs-c03.md) for gaps. The retired [SCS-C02 guide](../security-scs-c02/) is reference only and its domain weights are out of date.
