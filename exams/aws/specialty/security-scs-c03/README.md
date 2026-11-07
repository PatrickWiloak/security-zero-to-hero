---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 6 min
---

# AWS Certified Security - Specialty (SCS-C03)

The specialty exam for people who secure AWS workloads: logging and detection, incident response, edge and network controls, identity, encryption and multi-account governance. It is the current exam; SCS-C02 closed on December 1, 2025 and its [guide](../security-scs-c02/) is kept only as reference.

## Exam Details

- **Exam Code:** SCS-C03
- **Duration:** 170 minutes
- **Questions:** 65 (50 scored, 15 unscored); multiple choice, multiple response, ordering and matching
- **Passing Score:** 750 on a 100-1,000 scale
- **Cost:** $300 USD (AWS page, checked 2026-11-07)
- **Validity:** 3 years
- **Recommended experience:** five years of IT security and two or more years securing AWS workloads (AWS certification page)

Full detail and sources in the [fact sheet](./fact-sheet.md).

## Domains

| Domain | Weight | Notes |
|---|---:|---|
| 1. Detection | 16% | [01](./notes/01-detection.md) |
| 2. Incident Response | 14% | [02](./notes/02-incident-response.md) |
| 3. Infrastructure Security | 18% | [03](./notes/03-infrastructure-security.md) |
| 4. Identity and Access Management | 20% | [04](./notes/04-identity-and-access-management.md) |
| 5. Data Protection | 18% | [05](./notes/05-data-protection.md) |
| 6. Security Foundations and Governance | 14% | [06](./notes/06-security-foundations-and-governance.md) |

## How this exam differs from Associate and Professional exams

The specialty exam assumes you know AWS and asks which security design fits a constraint: lowest operational effort, least privilege, works across accounts, survives a compromised administrator. The task statements start with verbs like "design", "implement" and "troubleshoot", and the troubleshooting tasks are real: a trail that is not delivering, a key policy that locks out a role, an SCP that blocks a service. Learn the services by what they prove or prevent, and always ask where the control lives (account, organization, resource, network).

IAM is the largest domain at 20%, and almost every other domain depends on it, so give it extra time.

## Study sequence

1. **Identity and access management** (20%) - policy evaluation, roles and trust, ABAC, Access Analyzer.
2. **Security foundations and governance** (14%) - Organizations, SCPs, Control Tower, Config. It sets the guardrails the other domains sit inside.
3. **Data protection** (18%) - KMS, secrets, Object Lock, backups, TLS.
4. **Infrastructure security** (18%) - WAF, Network Firewall, security groups, endpoints, hardened images.
5. **Detection** (16%) - CloudTrail, GuardDuty, Security Hub, Security Lake.
6. **Incident response** (14%) - runbooks, forensics, containment, Detective.

Schedule in the [practice plan](./practice-plan.md).

## Study resources

- **[📖 SCS-C03 exam guide](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03.html)** - the authoritative outline; study against this
- **[📖 AWS Certified Security - Specialty](https://aws.amazon.com/certification/certified-security-specialty/)** - registration, price and validity
- [Practice questions](../../../../resources/practice-questions/aws-security-specialty-scs-c03.md) - original question bank in this repo

## Related

- [Retired SCS-C02 guide](../security-scs-c02/) - reference only
- [AWS exams index](../../README.md)
- Cloud depth: [cloud.noblerworks.com](https://cloud.noblerworks.com/)
