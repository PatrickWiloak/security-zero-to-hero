---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 8 min
---

# Google Cloud Professional Security Operations Engineer Fact Sheet

## Exam Overview

**Exam Code:** None published (checked 2026-11-07)
**Exam Name:** Professional Security Operations Engineer
**Level:** Professional
**Duration:** 2 hours
**Format:** 50-60 multiple choice and multiple select questions
**Questions:** 50-60
**Passing Score:** Not published by Google
**Cost:** $200 (plus tax where applicable), per the Google Cloud certification page on 2026-11-07
**Valid For:** Not verified; see Google's Renewal FAQs
**Delivery:** Online-proctored from a remote location, or onsite-proctored at a testing center
**Languages:** English, Japanese
**Prerequisites:** None. Recommended: 3+ years of security industry experience including 1+ years using Google Cloud security tooling

> **Verify before booking.** The certification page defers validity to the Renewal FAQs. The FAQs say renewing by exam adds 2 years to the inactive date for most professional certifications and that the exam renewal window opens 60 days before the inactive date, but they do not state the base validity period. Read from the Google Cloud certification page and the exam guide (PDF dated August 26, 2025 in its file metadata) on 2026-11-07. Price and renewal terms change.

> **Exam guide 2.0 exists.** A second PDF, "Professional Security Operations Engineer Exam Guide 2.0" (file metadata dated November 6, 2026), is published beside the original but is not yet linked from the certification page, which still links the August 2025 guide used for this sheet. The 2.0 guide uses different weights: Platform operations ~13%, Data management ~20%, Threat hunting ~18%, Detection engineering ~20%, Incident response ~18%, Observability ~11%. It also adds Google Threat Intelligence as a third assessed platform, a task 2.3 (ingesting and configuring threat intelligence), and topics such as Bindplane, MCP, data tables, AI-assisted hunting and rule writing, the Triage and Investigation Agent, composite detections and MITRE ATT&CK coverage analysis. Which guide the live exam follows is not stated; read **[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** before booking. The weights and notes in this guide follow the original guide.

**[📖 Professional Security Operations Engineer](https://cloud.google.com/learn/certification/security-operations-engineer)** - exam facts, price, recommended experience and renewal pointer
**[📖 Exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - the authoritative sections, weights and considerations
**[📖 Renewal FAQs](https://support.google.com/cloud-certification/answer/9907853)** - how renewal works

The exam guide says the exam assesses tasks in Google Security Operations (SecOps) and Security Command Center (SCC).

## Exam Domains

Six sections with approximate weights, in the exam guide's order.

| Section | Weight | Notes |
|---|---:|---|
| 1. Platform operations | ~14% | [01](./notes/01-platform-operations.md) |
| 2. Data management | ~14% | [02](./notes/02-data-management.md) |
| 3. Threat hunting | ~19% | [03](./notes/03-threat-hunting.md) |
| 4. Detection engineering | ~22% | [04](./notes/04-detection-engineering.md) |
| 5. Incident response | ~21% | [05](./notes/05-incident-response.md) |
| 6. Observability | ~10% | [06](./notes/06-observability.md) |

### Section 1: Platform operations (~14%)

1.1 enhancing detection and response (prioritising telemetry, integrating tools, justifying overlapping tools, finding coverage gaps, evaluating automation); 1.2 configuring access (authentication, IAM authorization for features and data, audit logs, API access, Workforce Identity Federation).

### Section 2: Data management (~14%)

2.1 ingesting logs for security tooling (ingestion approaches, parsers, normalization, labels, cost); 2.2 identifying a baseline of user, asset and entity context (threat intelligence, event versus entity data, aliasing for enrichment).

### Section 3: Threat hunting (~19%)

3.1 hunting across environments (queries, user behaviour, IOCs with Logs Explorer, Log Analytics, BigQuery and SecOps, hypotheses); 3.2 leveraging threat intelligence (IOCs in historical logs, new attack patterns, entity risk score, retrohunt).

### Section 4: Detection engineering (~22%)

4.1 developing detections (rules and searches, reference lists, Risk Analytics and curated rules, posture changes with Security Health Analytics, YARA-L for low-prevalence items, entity context, Event Threat Detection custom detectors); 4.2 threat intelligence for detection (alert scoring, IOC search, false-positive reduction).

### Section 5: Incident response (~21%)

5.1 containing and investigating incidents; 5.2 building and using response playbooks; 5.3 the case management life cycle.

### Section 6: Observability (~10%)

6.1 dashboards and reports; 6.2 health monitoring and alerting, including silent source detection.

## Related repo material

- [README](./README.md), [practice plan](./practice-plan.md), [scenarios](./scenarios.md), [strategy](./strategy.md)
- [Practice questions](../../../resources/practice-questions/gcp-security-operations-engineer.md)
- [Professional Cloud Security Engineer](../cloud-security-engineer/) - the design and configuration counterpart
- [Detection and response topic](../../../topics/detection-and-response.md)
