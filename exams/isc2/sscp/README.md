---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 5 min
---

# ISC2 SSCP - Systems Security Certified Practitioner

The practitioner credential for people who run security controls: administer access, monitor logs, respond to incidents, operate firewalls and harden endpoints. It sits between the entry-level [CC](../cc/) and the senior [CISSP](../cissp/). ISC2 asks for 1 year of work experience.

## Exam Details

- **Exam Code:** SSCP
- **Duration:** 2 hours
- **Questions:** 100-125, multiple choice and advanced item types, computerized adaptive testing (CAT)
- **Passing Score:** 700/1000
- **Cost:** not verified (the ISC2 page states no price)
- **Prerequisites:** 1 year of work experience in security operations
- **Outline effective:** October 1, 2025

Full detail, with sources, in the [fact sheet](./fact-sheet.md).

## Domains

| Domain | Weight | Notes |
|---|---:|---|
| 1. Security Concepts and Practices | 16% | [01](./notes/01-security-concepts-and-practices.md) |
| 2. Access Controls | 15% | [02](./notes/02-access-controls.md) |
| 3. Risk Identification, Monitoring and Analysis | 15% | [03](./notes/03-risk-identification-monitoring-and-analysis.md) |
| 4. Incident Response and Recovery | 14% | [04](./notes/04-incident-response-and-recovery.md) |
| 5. Cryptography | 9% | [05](./notes/05-cryptography.md) |
| 6. Network and Communications Security | 16% | [06](./notes/06-network-and-communications-security.md) |
| 7. Systems and Application Security | 15% | [07](./notes/07-systems-and-application-security.md) |

## How the exam thinks

SSCP questions are written from the point of view of the person at the keyboard. The question is rarely "what is a SIEM" and usually "the SIEM shows X, what do you do first". Two habits help: always ask which control function the answer provides (prevent, detect, correct), and prefer the answer that fits the stated scope of a practitioner. A practitioner escalates a policy gap to management and fixes a configuration gap themselves.

Weights are close to even, so there is no domain to skip. Cryptography is the smallest at 9%, which makes it the best place to be efficient rather than to skip.

## Study sequence

1. **Security concepts and practices** (16%) - vocabulary, controls, asset and change management.
2. **Network and communications security** (16%) - the broadest technical domain; start early.
3. **Access controls** (15%) - authentication, trust, identity life cycle, access models.
4. **Risk, monitoring and analysis** (15%) - risk, assessments, SIEM and log analysis.
5. **Systems and application security** (15%) - malware, endpoint, mobile, cloud, virtualization.
6. **Incident response and recovery** (14%) - IR life cycle, forensics, BC/DR.
7. **Cryptography** (9%) - last, once the protocols in the network domain make sense.

Schedule in the [practice plan](./practice-plan.md).

## Study resources

- **[📖 ISC2 SSCP certification page](https://www.isc2.org/certifications/sscp)** - registration and experience requirement
- **[📖 ISC2 SSCP exam outline](https://www.isc2.org/certifications/sscp/sscp-certification-exam-outline)** - the authoritative domain list; study against this
- [Practice questions](../../../resources/practice-questions/isc2-sscp.md) - original question bank in this repo

## After SSCP

| Next | Why |
|---|---|
| [CISSP](../cissp/) | Senior generalist; needs 5 years of experience |
| [CCSP](../ccsp/) | Cloud specialist |
| [Security+](../../comptia/security-plus/) | Often the hiring baseline; overlaps heavily |
