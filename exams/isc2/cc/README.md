---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 5 min
---

# ISC2 Certified in Cybersecurity (CC)

The genuine entry point to security certification: **no prerequisites, no work experience required, and both the training and the exam are free** through the ISC2 One Million Certified in Cybersecurity initiative.

This repo is called "zero to hero". Until now its security path started at [Security+](../../comptia/security-plus/), which assumes some background and costs money. CC is the actual zero.

## Exam Details

- **Exam Code:** CC
- **Duration:** 120 minutes
- **Questions:** 100-125, multiple choice and advanced item types, computerized adaptive testing (CAT)
- **Passing Score:** 700/1000
- **Cost:** Free exam and training through the ISC2 initiative; an Annual Maintenance Fee applies after certification
- **Validity:** 3 years, maintained with CPE credits and the AMF
- **Prerequisites:** None

Full detail in the [fact sheet](./fact-sheet.md).

## Domains

ISC2 replaced the CC outline on September 1, 2026, the first major update since CC launched in 2022. The five domains are new: some were renamed, governance became a domain of its own, cloud moved into a domain title, and business continuity and disaster recovery moved into Security Governance. Foundational AI topics (AI assets, AI-driven threats, governing AI use) run through every domain.

| Domain | Weight | Notes |
|--------|-------:|-------|
| 1. Security Principles | 24% | [01](./notes/01-security-principles.md) |
| 2. Security Governance | 17.3% | [02](./notes/02-security-governance.md) |
| 3. Identity and Access Management (IAM) Concepts | 20% | [03](./notes/03-identity-and-access-management.md) |
| 4. Networking and Cloud Security Concepts | 21.3% | [04](./notes/04-networking-and-cloud-security.md) |
| 5. Security Operations and Incident Response | 17.3% | [05](./notes/05-security-operations-and-incident-response.md) |

Study material written for the 2022 outline (Security Principles, BC/DR/IR, Access Control Concepts, Network Security, Security Operations) still covers most definitions, but it misses GRC, security metrics and KRIs, identity life cycle management, wireless and IoT, threat intelligence and threat frameworks, red and purple teaming, application testing, and quantum-resistant cryptography.

## What to expect

CC tests **vocabulary and concepts**, not implementation. You are not asked to configure a firewall; you are asked what a firewall does, where it sits, and which control type it is.

That makes it very learnable in a few weeks, and it makes precision matter. The exam distinguishes carefully between terms that sound similar:

- Threat, vulnerability, and risk
- Authentication, authorization, and accounting
- Preventive, detective, corrective, deterrent, and compensating controls
- Technical, administrative, and physical controls
- Business continuity, disaster recovery, and incident response
- RTO and RPO
- Symmetric encryption, asymmetric encryption, and hashing
- Due care and due diligence
- Key performance indicators and key risk indicators
- Red, blue, and purple teams

If you can define each of those cleanly and give an example, you are most of the way there.

## Study sequence

1. **Security principles** - the vocabulary everything else uses: CIA, AAA, risk, governance documents, controls, and ethics. 24% of the exam.
2. **Networking and cloud security** - the hardest domain for beginners, and 21.3%. Start early.
3. **Identity and access management** - the identity life cycle, least privilege, separation of duties, and access control models. 20%.
4. **Security governance** - GRC, business continuity and disaster recovery, awareness and culture, and security metrics. 17.3%.
5. **Security operations and incident response** - data security, triage, threat intelligence, incident response, asset protection, and security testing. 17.3%.

Schedule in the [practice plan](./practice-plan.md).

## If the networking vocabulary is new

Domain 4 assumes you know what an IP address, a port, and a protocol are. If that is unfamiliar, work through the repo's beginner material first; it will save you time overall:

- [What is a server?](https://cloud.noblerworks.com/learn/day-one/what-is-a-server/)
- [HTTP and APIs](https://cloud.noblerworks.com/learn/day-one/http-and-apis/)
- [Networking troubleshooting](https://cloud.noblerworks.com/learn/day-one/networking-troubleshooting/)
- [DNS explained](https://cloud.noblerworks.com/learn/concepts/dns-explained/)
- [TLS and HTTPS](../../../learn/concepts/tls-and-https.md)

## Study resources

- **[📖 ISC2 CC certification page](https://www.isc2.org/certifications/cc)** - registration and the free training offer
- **[📖 ISC2 CC exam outline](https://www.isc2.org/certifications/cc/cc-certification-exam-outline)** - the authoritative domain list, effective September 1, 2026; study against this
- **[📖 ISC2: Inside the updated CC exam](https://www.isc2.org/insights/2026/08/inside-the-updated-isc2-cc-exam)** - what changed in the 2026 outline and why
- **[📖 ISC2 free online self-paced training](https://www.isc2.org/landing/1mcc)** - the official course, free
- [Practice questions](../../../resources/practice-questions/isc2-cc.md) - question bank in this repo

## After CC

| Next | Why |
|---|---|
| [Security+](../../comptia/security-plus/) | Broader and more technical; the common hiring baseline |
| [SC-900](../../azure/sc-900/) or [AZ-900](https://cloud.noblerworks.com/exams/azure/az-900/) | If your direction is cloud |
| [CCSK](../../cloud-security-alliance/ccsk/) | Cloud security specifically |
| [CCSP](../ccsp/) or [CISSP](../cissp/) | Later, once you have the experience requirement |

See the [Security Engineer roadmap](../../../resources/certification-roadmap-security-engineer.md) for the full path.
