---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 13 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 05 - Incident response

**Section 5: Incident response (~21%)** - tasks 5.1 to 5.3 of the exam guide.

Detection ends where an alert becomes a case. This section covers containing and investigating, automating with playbooks, and managing the case life cycle so that nothing is dropped between people.

---

## 5.1 Containing and investigating security incidents

**Collect evidence on scope.** Start by preserving: forensic images and artefacts of affected systems (disk snapshots, memory where possible), the relevant logs and the alerts themselves. Use cloud-native capabilities, such as disk snapshots shared to an isolated project, and record who collected what and when. Do not modify the originals.

**Observe and analyse alerts.** In SCC and Google SecOps, review the alerts and findings related to the incident: related detections on the same entities, timing, severity and the entity context from notes 02. Group related alerts so the team sees one incident rather than many.

**Analyse scope with log tools.** The guide names Logs Explorer, Log Analytics, BigQuery, Cloud Logging and Cloud Monitoring. Answer the scoping questions: which identities and credentials were used, which systems they touched, what data was accessed, how long it went on and whether other copies of the technique exist. Cloud Audit Logs are central here, which is why Data Access logs must have been enabled beforehand (notes 01).

**Collaborate with engineering teams.** Containment and remediation usually require the owners of the affected systems, who know the blast radius of a change, and long-term fixes (patches, redesign) belong to them. Agree on communication, decisions and who can approve disruptive actions.

**Isolate affected services and processes.** Contain to stop the spread while preserving evidence. Typical cloud actions: remove or restrict a compromised service account's roles or disable its keys, tighten firewall rules or network tags to quarantine a VM, stop or snapshot-and-stop an instance, revoke sessions, and block malicious indicators. Choose the least disruptive action that stops harm. Isolation should be reversible and logged.

**Analyse identified artefacts.** For hashes, IP addresses, URLs and binaries, use Google Threat Intelligence (the guide's example) to learn what the artefact is, who uses it and what else it connects to, and extract further IOCs for scoping.

**Root cause analysis.** Use SCC and the Google SecOps SIEM to establish the initial access point, the control that failed and the path the attacker took. The output is a fix, such as closing an exposure SCC flagged or tightening an over-permissioned account, not only a report.

## 5.2 Building, implementing and using response playbooks

**What a playbook is.** In Google SecOps SOAR, a playbook is built from a trigger, actions and flow logic: the flow commonly uses if-then-else branching so that later steps depend on earlier results. A **case** is the top-level container made of one or more **alerts** ingested from various sources, and an alert is a notification containing one or more security events. **Case playbooks** run at the case level, so one action can cover all alerts and entities, with reaction triggers such as a change of priority, assignee or stage, or the addition of a tag. A **manual action** pauses a playbook until an analyst completes or skips it, and appears in the Pending Actions widget (per the playbook actions documentation). These case-playbook features were marked pre-GA in the documentation I read, so confirm current behaviour.

**Determine which steps to automate.** Automate steps that are frequent, well understood and low risk: enrichment, reputation lookups, ticket creation, notifications, adding indicators to a watch list. Use a manual action or approval for disruptive steps such as disabling a production service account, since a wrong automated action can cause the outage the attacker wanted. Decide by asking how often the step is performed, how certain the trigger is, and the cost of getting it wrong.

**Prioritise high-value enrichments.** Choose enrichments by the threat profile of the alert: for a phishing alert, URL detonation and sender reputation; for a suspicious login, the user's role and recent travel; for malware, file reputation and other hosts with the same hash. Limit lookups to unique entities to save time and API quota (case playbooks can deduplicate entities across alerts).

**Evaluate integrations.** Playbooks reach other systems through integrations: threat intelligence, identity providers, endpoint tools, ticketing and messaging. Evaluate by the actions available, authentication method, rate limits and failure behaviour.

**Improve from incidents.** After incidents, design new processes for newly identified attack patterns and recommend new orchestrations where gaps show in the current implementation. If analysts do the same five manual steps for every alert of a type, that is the next playbook.

**Notify analysts and stakeholders.** Implement notifications to the right people with the right information: analysts for assignment, owners for containment approval, management for severity thresholds. Use channels that cannot be silently ignored for high severity.

## 5.3 Implementing the case management life cycle

Cases need a defined path, or incidents stall.

- **Assign cases into appropriate response stages.** Stages such as triage, investigation, containment, remediation and closure show what is happening and where bottlenecks are. Each stage has entry and exit criteria, so cases do not jump or linger.
- **Implement efficient escalation workflows.** Define what triggers escalation (severity, affected asset class, SLA breach, regulatory impact), who receives it and how fast. Escalation should be automatic where the trigger is clear.
- **Assess the effectiveness of handoffs.** Many failures occur between shifts and teams. Review whether a receiving analyst can continue without asking questions: summary, evidence, actions taken, open tasks and next owner. Measure rework after handoffs and fix the template.

Close the loop with metrics (time to acknowledge, contain and resolve) and a review of each significant case, feeding detection gaps back to notes 04 and playbook gaps back to this section.

---

## Key terms

- **Case** - the top-level container in SecOps SOAR holding one or more alerts and the work done on them
- **Alert** - a notification containing one or more security events
- **Playbook** - an automated workflow made of a trigger, actions and flow logic that responds to alerts or cases
- **Case playbook** - a playbook that runs at the case level and reacts to case events such as priority or stage changes
- **Manual action** - a playbook step that pauses until an analyst completes or skips it
- **Enrichment** - adding context, such as reputation or ownership, to an alert or entity
- **Containment** - limiting the spread and impact of an incident while preserving evidence
- **Forensic image** - a bit-for-bit copy of a disk or memory used for analysis without altering the original
- **Escalation** - passing a case to a higher level of authority or skill under defined triggers
- **Handoff** - the transfer of a case between analysts, shifts or teams
- **Root cause analysis** - determining how an incident became possible and which change prevents recurrence
- **Response stage** - a defined step in the case life cycle, such as triage, investigation, containment or closure

---

## Related

- [Notes 04: detection engineering](./04-detection-engineering.md)
- [Notes 06: observability](./06-observability.md)
- [Cloud incident response tabletop](../../../../resources/hands-on-projects/cloud-incident-response-tabletop.md)
- **[📖 Case playbooks overview](https://docs.cloud.google.com/chronicle/docs/soar/respond/working-with-playbooks/case-playbooks)** - triggers, deduplication and manual actions (pre-GA at time of reading)
- **[📖 Manage actions in playbooks](https://docs.cloud.google.com/chronicle/docs/soar/respond/working-with-playbooks/using-actions-in-playbooks)** - manual actions and the Pending Actions widget
- **[📖 Investigation and case management overview](https://docs.cloud.google.com/chronicle/docs/soar/investigate/working-with-cases/cases-overview)** - cases and alerts in SecOps SOAR
- **[📖 Cloud Audit Logs](https://docs.cloud.google.com/logging/docs/audit)** - the audit trail used to scope incidents
- **[📖 Exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - section 5 considerations
