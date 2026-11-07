---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 4 min
---

# Google Cloud Professional Security Operations Engineer Study Plan

Six weeks at 6-8 hours a week for someone with security operations experience. Study against the [exam guide 2.0](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf). Google offers free usage tiers and new-customer credits; use a sandbox project and never practise in a production or client environment.

## Week 1: Data management (Section 2, ~20%)

- [ ] Read `notes/02-data-management.md`
- [ ] Explain event data versus entity data with three examples of each
- [ ] Describe what a parser does and when you would write a parser extension
- [ ] Create a log sink to BigQuery and fix the writer identity permission
- [ ] List the logs you would ingest to detect credential theft and cloud misuse
- [ ] Describe how Bindplane collects Windows Event logs and what `raw` does
- [ ] Explain why an IOC feed must be re-ingested daily into the Entity Context Graph
- [ ] Say what LiveHunt, Digital Threat Monitoring and URL Scanning each do

## Week 2: Platform operations (Section 1, ~13%)

- [ ] Read `notes/01-platform-operations.md`
- [ ] Say what SecOps, Security Command Center and Google Threat Intelligence each own
- [ ] Explain Workforce Identity Federation in one paragraph
- [ ] List the four Cloud Audit Log types and which are off by default
- [ ] Justify an overlapping tool pair using requirements

## Week 3: Detection engineering (Section 4, ~20%)

- [ ] Read `notes/04-detection-engineering.md`
- [ ] Read the two YARA-L rules and say what each matches
- [ ] Write a single-event rule and a multi-event rule for scenarios of your own
- [ ] Choose string, regex or CIDR for five reference lists
- [ ] Explain why a curated detection cannot be run as a retrohunt
- [ ] Explain the difference between a reference list and a data table
- [ ] Describe a composite detection and its 14-day window
- [ ] Read the ATT&CK matrix idea: why a rule needs technique metadata to count

## Week 4: Threat hunting (Section 3, ~18%)

- [ ] Read `notes/03-threat-hunting.md`
- [ ] Write three hunt hypotheses and the tool you would use for each
- [ ] Choose between Logs Explorer, Log Analytics, BigQuery and SecOps for four questions
- [ ] Describe how to run a retrohunt safely
- [ ] Explain what a stats query adds to a UDM search
- [ ] Say what the Triage and Investigation Agent returns and how you would verify it

## Week 5: Incident response and observability (Sections 5 and 6, ~18% and ~11%)

- [ ] Read notes 05 and 06
- [ ] Sketch a playbook for a suspicious login: trigger, enrichments, branch and manual approval
- [ ] Define a case life cycle with stages, escalation triggers and a handoff template
- [ ] Define five health metrics and a silent source alert
- [ ] Work through the [cloud incident response tabletop](../../../resources/hands-on-projects/cloud-incident-response-tabletop.md)

## Week 6: Practice and review

- [ ] Work through the [practice questions](../../../resources/practice-questions/gcp-security-operations-engineer.md); read every explanation
- [ ] Try Google's own sample questions linked from the certification page
- [ ] Re-read the notes for any section below 70%
- [ ] Work through the [scenarios](./scenarios.md)

## Readiness check

You are ready when you can explain, without notes: parser versus parser extension, event versus entity data, single-event versus multi-event YARA-L, a retrohunt versus a hunt, which SCC service finds misconfiguration versus threats, and what a silent source alert protects against.
