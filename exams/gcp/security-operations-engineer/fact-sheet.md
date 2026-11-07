---
last-updated: 2026-11-07
difficulty: advanced
exam-version: Exam guide 2.0
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
>
> **This sheet follows exam guide 2.0.** Google publishes "Professional Security Operations Engineer Exam Guide 2.0" (a six-page PDF, read in full on 2026-11-07). The certification page's own text still links the original guide (file metadata dated August 26, 2025) and does not say which guide the live exam follows, so the 2.0 guide is linked below as the checklist and the original is kept only for comparison. 2.0 keeps the same six section titles and re-weights them, adds Google Threat Intelligence as a third assessed platform, adds task 2.3 (ingesting and configuring threat intelligence), and adds topics such as Bindplane, MCP, data tables, composite detections, MITRE ATT&CK coverage analysis, AI-assisted hunting and rule writing and the Triage and Investigation Agent.

**[📖 Professional Security Operations Engineer](https://cloud.google.com/learn/certification/security-operations-engineer)** - exam facts, price, recommended experience and renewal pointer
**[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** - the authoritative sections, weights and considerations (checklist for this repo)
**[📖 Original exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - the earlier outline, for comparison only
**[📖 Renewal FAQs](https://support.google.com/cloud-certification/answer/9907853)** - how renewal works

Guide 2.0 says the exam assesses tasks in Google Security Operations (SecOps), Security Command Center (SCC) and Google Threat Intelligence (GTI).

## Exam Domains

Six sections with approximate weights, in the exam guide 2.0 order. The weights sum to 100%.

| Section | Weight | Notes |
|---|---:|---|
| 1. Platform operations | ~13% | [01](./notes/01-platform-operations.md) |
| 2. Data management | ~20% | [02](./notes/02-data-management.md) |
| 3. Threat hunting | ~18% | [03](./notes/03-threat-hunting.md) |
| 4. Detection engineering | ~20% | [04](./notes/04-detection-engineering.md) |
| 5. Incident response | ~18% | [05](./notes/05-incident-response.md) |
| 6. Observability | ~11% | [06](./notes/06-observability.md) |

### Section 1: Platform operations (~13%)

1.1 enhancing detection and response (prioritising telemetry such as SCC, GTI, Cloud Logging and Chrome Enterprise; integrating Content Hub tools; justifying overlapping tools; finding coverage gaps; using AI and automation; UDM and stats searches; evaluating and integrating GTI IOCs and TTPs); 1.2 configuring access for human and non-human identities (authentication including MCP, IAM for features and data, audit logs, API access for automations, Workforce Identity Federation).

### Section 2: Data management (~20%)

2.1 ingesting logs for security tooling (Bindplane and direct SCC findings pipelines, required logs, parsers and extensions, normalization, labels, cost); 2.2 implementing a baseline of user, asset and entity context (threat intelligence, event versus entity data, aliasing for enrichment); 2.3 ingesting and configuring threat intelligence (GTI or third-party IOCs into the Entity Context Graph; GTI hunting, LiveHunt, Digital Threat Monitoring, Google Insights and URL Scanning). Task 2.3 is new in 2.0.

### Section 3: Threat hunting (~18%)

3.1 performing threat hunting across environments (queries, stats queries for user behaviour, Logs Explorer, BigQuery and SecOps, collaborating with incident response, hypotheses from attack path exposures, natural-language AI prompts, SCC security graph versus Entity Context Graph); 3.2 leveraging threat intelligence for hunting (historical IOC search, real-time patterns and toxic combinations, entity risk score, retrohunt, proactive search, Triage and Investigation Agent results).

### Section 4: Detection engineering (~20%)

4.1 developing and implementing mechanisms to detect risks and identify threats (rules and searches over timelines, data tables for risk values, Risk Analytics and curated detections, posture and AI infrastructure risk with Compliance Manager, Web Security Scanner findings into SecOps, YARA-L for low-prevalence items, entity context, SCC threat detectors, ATT&CK coverage, composite detections, natural-language rule creation); 4.2 leveraging threat intelligence for detection (IOC alert scoring, latest IOCs, repetitive alert frequency, GTI-based rules, Applied Threat Intelligence).

### Section 5: Incident response (~18%)

5.1 containing and investigating security incidents (evidence, scope and severity with posture and vulnerability context, isolation, root cause, responding to GTI alerts such as DTM, AI investigation tools); 5.2 building, implementing and using response playbooks (including updating SCC findings, notifications, invoking the Triage and Investigation Agent, custom transformers and logical operators); 5.3 implementing the case management lifecycle (metrics such as tags, SLAs, stages and closure reasons; escalation workflows).

### Section 6: Observability (~11%)

6.1 developing and maintaining dashboards (analytics and KPIs, dashboards, SOAR, SIEM, GTI and SCC reports); 6.2 configuring health monitoring and alerting (metrics, centralised dashboards, thresholds, Cloud Monitoring notifications, Cloud Logging and Gemini Cloud Assist, silent source detection).

## Related repo material

- [README](./README.md), [practice plan](./practice-plan.md), [scenarios](./scenarios.md), [strategy](./strategy.md)
- [Practice questions](../../../resources/practice-questions/gcp-security-operations-engineer.md)
- [Professional Cloud Security Engineer](../cloud-security-engineer/) - the design and configuration counterpart
- [Detection and response topic](../../../topics/detection-and-response.md)
