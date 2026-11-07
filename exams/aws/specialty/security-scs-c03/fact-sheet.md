---
last-updated: 2026-11-07
exam-version: SCS-C03
---

# AWS Certified Security - Specialty (SCS-C03) - Fact Sheet

> **Current exam.** SCS-C03 replaced SCS-C02, which was in use until December 1, 2025; SCS-C03 has been in use since December 2, 2025 (AWS exam guide appendix). The retired [SCS-C02 guide](../security-scs-c02/) is kept as reference only.

## Exam Overview

**Exam Code:** SCS-C03
**Exam Name:** AWS Certified Security - Specialty
**Level:** Specialty
**Duration:** 170 minutes
**Format:** 65 questions (50 scored and 15 unscored); multiple choice, multiple response, ordering and matching
**Questions:** 65
**Passing Score:** 750 (scaled score of 100-1,000; compensatory scoring)
**Cost:** $300 USD (AWS certification page, checked 2026-11-07; additional costs may apply)
**Valid For:** 3 years
**Delivery:** Pearson VUE testing center or online proctored
**Languages:** English, Japanese, Korean, Portuguese (Brazil), Simplified Chinese, Spanish (Latin America)
**Prerequisites:** None required. AWS recommends five years of IT security experience and two or more years of hands-on experience securing AWS workloads; the exam guide describes the target candidate as having the equivalent of 3-5 years of experience securing cloud solutions.

> **Verify before booking.** Read from the AWS certification page and exam guide on 2026-11-07. The certification page notes that the exam in Simplified Chinese, Spanish (Latin America) and Portuguese (Brazil) will be retired after December 31, 2026. Price and languages change; confirm on the AWS page.

**[📖 AWS Certified Security - Specialty](https://aws.amazon.com/certification/certified-security-specialty/)** - exam facts, price, validity and languages
**[📖 SCS-C03 exam guide](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03.html)** - domains, weights, task statements and skills
**[📖 Appendix: comparison of SCS-C02 and SCS-C03](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03-appendix-b.html)** - what moved, was added and was removed

## Exam Domains

Six content domains, as percentages of scored content. The guide says unanswered questions score as incorrect and there is no penalty for guessing.

| Domain | Weight | Notes |
|---|---:|---|
| 1. Detection | 16% | [01](./notes/01-detection.md) |
| 2. Incident Response | 14% | [02](./notes/02-incident-response.md) |
| 3. Infrastructure Security | 18% | [03](./notes/03-infrastructure-security.md) |
| 4. Identity and Access Management | 20% | [04](./notes/04-identity-and-access-management.md) |
| 5. Data Protection | 18% | [05](./notes/05-data-protection.md) |
| 6. Security Foundations and Governance | 14% | [06](./notes/06-security-foundations-and-governance.md) |

### Domain 1: Detection (16%)

1.1 design and implement monitoring and alerting; 1.2 design and implement logging; 1.3 troubleshoot monitoring, logging and alerting.

### Domain 2: Incident Response (14%)

2.1 design and test an incident response plan; 2.2 respond to security events.

### Domain 3: Infrastructure Security (18%)

3.1 network edge services; 3.2 compute workloads (including generative AI guardrails); 3.3 network security controls.

### Domain 4: Identity and Access Management (20%)

4.1 authentication strategies; 4.2 authorization strategies.

### Domain 5: Data Protection (18%)

5.1 data in transit; 5.2 data at rest; 5.3 confidential data, credentials, secrets and key material.

### Domain 6: Security Foundations and Governance (14%)

6.1 centrally deploy and manage accounts; 6.2 secure and consistent deployment; 6.3 evaluate compliance.

## What changed from SCS-C02

Domains 1 and 2 of SCS-C02 (Threat Detection and Incident Response, Security Logging and Monitoring) were restructured into Detection and Incident Response. IAM grew from 16% to 20%; Infrastructure Security fell from 20% to 18%; Data Protection (18%) and Governance (14%) kept their weights, and Governance was renamed from "Management and Security Governance". Added content includes validating findings from security services, OCSF and third-party edge integration, generative AI application guardrails, inter-resource encryption in transit, imported key material, data masking and multi-Region keys and certificates. Removed content includes ASFF, host-based security, TCP/IP fundamentals and TLS concepts.

## Related repo material

- [README](./README.md), [practice plan](./practice-plan.md), [scenarios](./scenarios.md), [strategy](./strategy.md)
- [Practice questions](../../../../resources/practice-questions/aws-security-specialty-scs-c03.md)
- [SCS-C02 guide (retired, reference)](../security-scs-c02/)
- [Least-privilege IAM review lab](../../../../resources/hands-on-projects/least-privilege-iam-review.md)
