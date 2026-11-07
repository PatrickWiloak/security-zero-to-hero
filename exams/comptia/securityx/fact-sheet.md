---
last-updated: 2026-11-07
exam-version: CAS-005
difficulty: advanced
reading-time: 8 min
---

# CompTIA SecurityX (CAS-005) Fact Sheet

SecurityX is the renamed CASP+, announced December 18, 2024 together with the V5 exam (CAS-005, released December 17, 2024). Current CASP+ holders keep their certification status and continuing education (CompTIA blog, read 2026-11-07).

## Exam Overview

**Exam Code:** CAS-005 (V5)
**Exam Name:** CompTIA SecurityX
**Level:** Advanced (CompTIA Xpert series)
**Duration:** Maximum of 165 minutes
**Format:** Multiple choice and performance-based questions
**Questions:** Maximum of 90
**Passing Score:** Pass/fail only; no scaled score
**Cost:** Not verified. The CompTIA SecurityX page states no price (checked 2026-11-07)
**Valid For:** Not verified. Neither the SecurityX page nor the SecurityX educational units page states the renewal cycle or CEU count (checked 2026-11-07)
**Delivery:** Not stated on the SecurityX page; see CompTIA
**Languages:** English and Japanese (other languages "to be determined")
**Prerequisites:** None required. Recommended: a minimum of 10 years of general hands-on IT experience including 5 years of hands-on security; Network+, Security+, CySA+, Cloud+ and PenTest+ knowledge or equivalent

> **Verify before booking.** Read from the CompTIA SecurityX page on 2026-11-07. The page says CompTIA exams are usually retired three years after launch (estimated 2027) but gives no retirement date, and CompTIA's "exam objectives under development" page lists a draft **SecurityX V6** objectives PDF with no code or launch date. Confirm the current version before you book.

**[📖 CompTIA SecurityX](https://www.comptia.org/en-us/certifications/securityx/)** - exam facts and the inline objectives summary used for this guide
**[📖 Introducing SecurityX: CASP+ gets an update and rebrand](https://www.comptia.org/en-us/blog/introducing-comptia-securityx/)** - the rename, V5 domain weights against V4, and 23 objectives
**[📖 CompTIA exam objectives under development](https://www.comptia.org/en-us/resources/comptia-exam-objectives-under-development/)** - lists the draft V6 objectives; not the current exam

## Exam Domains

Four domains. The SecurityX page publishes the weights and an inline objectives summary; it links no CAS-005 objectives PDF, so the numbered objectives and acronym list are not reproduced here (CompTIA says V5 has 23 objectives).

| Domain | Weight | Notes |
|---|---:|---|
| 1. Governance, Risk, and Compliance | 20% | [01](./notes/01-governance-risk-and-compliance.md) |
| 2. Security Architecture | 27% | [02](./notes/02-security-architecture.md) |
| 3. Security Engineering | 31% | [03](./notes/03-security-engineering.md) |
| 4. Security Operations | 22% | [04](./notes/04-security-operations.md) |

The CompTIA blog gives V4 (CASP+) weights for comparison: 15%, 29%, 26% (called "Security Engineering and Cryptography" in V4) and 30%. Security Operations shrank most; Governance, Risk, and Compliance grew.

### Domain 1: Governance, Risk, and Compliance (20%)

Security program documentation; program management (training, communication, reporting, RACI matrix); frameworks (COBIT, ITIL and others); configuration management (asset life cycle, CMDB, inventory); GRC tools; data governance; risk management (impact analysis, quantitative versus qualitative assessment, third-party risk); threat modeling (actors, attack patterns, ATT&CK, CAPEC, STRIDE); attack surface; compliance strategies (PCI DSS, ISO/IEC 27000); security frameworks (NIST, CSF, CSA).

### Domain 2: Security Architecture (27%)

Cloud capabilities (CASB, shadow IT detection, shared responsibility, CI/CD, IaC, containers, orchestration, serverless); cloud data security; cloud control strategies; network architecture (segmentation, microsegmentation, VPN, API integration); security boundaries; deperimeterization (SASE, SD-WAN, SDN); zero trust.

### Domain 3: Security Engineering (31%)

Automation (PowerShell, Bash, Python, event triggers, IaC, cloud APIs, generative AI, SOAR); vulnerability management (scanning, SCAP, CVE, CVSS); advanced cryptography (PQC, key stretching, homomorphic encryption, forward secrecy, hardware acceleration); cryptographic use cases and techniques.

### Domain 4: Security Operations (22%)

Monitoring and data analysis (SIEM); vulnerabilities and attack surface; threat hunting and threat intelligence; incident response (malware analysis, reverse engineering, metadata analysis, data recovery, root cause analysis).

## Related repo material

- [README](./README.md), [practice plan](./practice-plan.md), [scenarios](./scenarios.md), [strategy](./strategy.md)
- [Practice questions](../../../resources/practice-questions/comptia-securityx.md)
- [Security+](../security-plus/) and [CySA+](../cysa-plus/) - the CompTIA exams SecurityX builds on
- [CISSP](../../isc2/cissp/) - the comparable senior generalist credential
