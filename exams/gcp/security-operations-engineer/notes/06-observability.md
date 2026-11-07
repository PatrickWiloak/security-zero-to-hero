---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 9 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 06 - Observability

**Section 6: Observability (~10%)** - tasks 6.1 and 6.2 of the exam guide.

Observability answers two questions about the security operation itself: is it working, and is it improving? The first is health monitoring (are logs arriving, are parsers running); the second is metrics and reporting.

---

## 6.1 Dashboards and reports

**Identify key security analytics.** Choose metrics that drive decisions. For detection: alert volume by rule, false positive rate, detections by technique coverage. For response: mean time to acknowledge, contain and resolve, cases by stage, handoff rework. For data: ingestion volume and cost by source, parser error rate, coverage of critical assets. For exposure: open critical findings, time to fix, posture drift. Put targets next to the numbers (a **KPI** is a metric with a target) and show trends, because a single value hides direction.

**Implement dashboards.** The guide lists dashboards that visualise security telemetry, ingestion metrics, detections, alerts and IOCs, using Google SecOps SOAR and SIEM dashboards and **Looker Studio** for broader reporting. Match audience to content: analysts need live queues and recent detections; engineers need rule performance and ingestion health; leadership needs trends, risk and cost. Avoid dashboards nobody owns; every one needs an owner and a question it answers.

**Generate and customise reports.** SOAR and SIEM both produce reports for scheduled review and for stakeholders. Customise them for the reader: executives want a one-page summary of risk and trend, auditors want evidence of control operation, and operations teams want detail. Reports built from the same data as the dashboards keep numbers consistent.

## 6.2 Health monitoring and alerting

A detection platform that silently stops receiving logs gives false comfort, which is worse than no platform.

**Identify important health metrics.** Ingestion rate per source, the age of the newest event per source, parser error rate, rule execution failures, API quota use and playbook failures. The Health Hub in SecOps shows failed sources and parsers, and parser alerts trigger when parser errors rise by 5 percentage points or more as a share of ingested events compared with the previous day.

**Centralise metrics in dashboards.** Use Cloud Monitoring dashboards to pull platform and pipeline metrics together, so one screen shows whether the operation is healthy.

**Create alerts with thresholds.** Alert on conditions that need human action: ingestion for a critical source drops below a threshold for a period, the parser error rate crosses a limit, or a playbook fails repeatedly. Use thresholds with durations to avoid flapping, and avoid alerting on conditions nobody can act on.

**Configure notifications.** Send notifications through Cloud Monitoring notification channels (email, chat, paging and webhook integrations), routed by severity and owner, and test them. An alert that goes to a mailbox nobody reads is not an alert.

**Identify health issues with logging tools.** Use Cloud Logging to find errors from forwarders, ingestion pipelines and functions, for example permission denied on a log sink destination, or quota exceeded.

**Configure silent source detection.** A **silent source** is a log source that has stopped sending data. Detection compares each source's expected rhythm with reality and alerts when no events arrive within the expected interval. Set the interval per source, since a firewall emits constantly while a quarterly-use system legitimately does not. Silence in a critical source, such as authentication or audit logs, is an incident until proven otherwise, because an attacker may have disabled logging.

---

## Key terms

- **Observability** - the ability to understand the health and performance of a system from its metrics, logs and traces
- **KPI** - a key performance indicator: a metric measured against a target
- **Mean time to respond** - the average time from detection to response or containment
- **Looker Studio** - Google's reporting and dashboard tool used for security analytics
- **Cloud Monitoring** - the Google Cloud service for metrics, dashboards, alerting policies and notifications
- **Silent source** - a log source that has stopped sending events when it is expected to be active
- **Health Hub** - the SecOps view of failed sources and parsers and normalization problems
- **Parser error rate** - the share of ingested events that a parser fails to normalise correctly
- **Alerting policy** - a rule that notifies people when a monitored metric crosses a threshold
- **Notification channel** - a destination, such as email or a chat tool, to which alerts are delivered

---

## Related

- [Notes 02: data management](./02-data-management.md)
- [Notes 05: incident response](./05-incident-response.md)
- **[📖 Ingestion overview for Google SecOps](https://docs.cloud.google.com/chronicle/docs/ingestion/ingestion-overview)** - Health Hub and parser alerts
- **[📖 Cloud Audit Logs](https://docs.cloud.google.com/logging/docs/audit)** - audit log types to monitor
- **[📖 Exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - section 6 considerations
