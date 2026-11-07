---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 6 min
---

# Google Cloud Professional Security Operations Engineer

The Google Cloud credential for people who run a security operations centre on Google's tooling: ingest and normalise logs, hunt, write detection rules, respond to incidents and keep the pipeline healthy. It centres on **Google Security Operations (SecOps)** and **Security Command Center (SCC)**. It is the operations counterpart to the [Professional Cloud Security Engineer](../cloud-security-engineer/), which covers designing and configuring secure infrastructure.

## Exam Details

- **Duration:** 2 hours
- **Questions:** 50-60 multiple choice and multiple select
- **Cost:** $200 plus tax where applicable (Google page, checked 2026-11-07)
- **Languages:** English, Japanese
- **Recommended experience:** 3+ years in security including 1+ year with Google Cloud security tooling
- **Renewal:** see Google's Renewal FAQs; base validity not stated on the exam page

Full detail and sources in the [fact sheet](./fact-sheet.md).

## Sections

| Section | Weight | Notes |
|---|---:|---|
| 1. Platform operations | ~14% | [01](./notes/01-platform-operations.md) |
| 2. Data management | ~14% | [02](./notes/02-data-management.md) |
| 3. Threat hunting | ~19% | [03](./notes/03-threat-hunting.md) |
| 4. Detection engineering | ~22% | [04](./notes/04-detection-engineering.md) |
| 5. Incident response | ~21% | [05](./notes/05-incident-response.md) |
| 6. Observability | ~10% | [06](./notes/06-observability.md) |

## How the exam thinks

Most questions put you in an analyst or engineer seat with a symptom: a parser is dropping fields, a rule fires too often, a source went quiet, a hunt needs historical data. The answer is usually the SecOps or SCC feature built for that job, used in the right order: normalise data first, enrich it with context, then detect, then respond. Know which tool owns each layer: SCC finds posture and cloud threats and writes findings; SecOps ingests, normalises, detects with YARA-L, and runs cases and SOAR playbooks.

Detection engineering (about 22%) and incident response (about 21%) are the biggest sections together, so be able to read and write a YARA-L rule.

## Study sequence

1. **Data management** (14%) - everything downstream depends on good ingestion and context.
2. **Platform operations** (14%) - tools, access and identity.
3. **Detection engineering** (22%) - YARA-L, reference lists, risk values, curated detections.
4. **Threat hunting** (19%) - queries, retrohunt, threat intelligence.
5. **Incident response** (21%) - containment, playbooks, cases.
6. **Observability** (10%) - dashboards and health.

Schedule in the [practice plan](./practice-plan.md).

## Study resources

- **[📖 Professional Security Operations Engineer](https://cloud.google.com/learn/certification/security-operations-engineer)** - official page, training path and sample questions
- **[📖 Exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - the authoritative outline; study against this
- [Practice questions](../../../resources/practice-questions/gcp-security-operations-engineer.md) - original question bank in this repo

## Related

- [Professional Cloud Security Engineer](../cloud-security-engineer/)
- [GCP provider index](../README.md)
