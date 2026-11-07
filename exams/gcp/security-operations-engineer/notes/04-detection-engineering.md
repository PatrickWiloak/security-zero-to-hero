---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 04 - Detection engineering

**Section 4: Detection engineering (~22%)** - tasks 4.1 and 4.2 of the exam guide. The largest section.

Detection engineering turns understanding of attacker behaviour into rules that run continuously, at an acceptable noise level. The tool at the centre is **YARA-L 2.0**, the rule language of Google SecOps.

---

## 4.1 Developing and implementing detections

### YARA-L rule structure

YARA-L 2.0 is the rule language used in Google SecOps to correlate UDM events, to detect threats, monitor entity behaviour and enrich detections with business logic. A rule has sections:

- `meta`: descriptive details such as author and description.
- `events`: filters that select UDM events and assign them to variables such as `$e`.
- `match`: groups events by variables over a time window, such as `$user over 5m`.
- `outcome`: calculates extra values for each detection, such as risk scores.
- `condition`: states which events or counts must be present to trigger a detection.
- `options`: optional settings for the rule.

A **single-event rule** flags individual occurrences, with no `match` section (or a condition that only requires one event). A **multi-event rule** uses `match` and the detection depends on the events within the window, such as counting at least ten logins with `#e >= 10`. The documentation's minimal example:

```
rule SingleEventRule {
meta:
  author = "noone@altostrat.com"

events:
  $e.metadata.event_type = "USER_LOGIN"

condition:
  $e
}
```

A multi-event rule for several failed logins followed by a success for the same user inside ten minutes:

```
rule failed_logins_then_success {
  meta:
    author = "detection-engineering"
    description = "Five or more blocked logins then an allowed login for one user in 10 minutes"
    severity = "MEDIUM"

  events:
    $fail.metadata.event_type = "USER_LOGIN"
    $fail.security_result.action = "BLOCK"
    $fail.target.user.userid = $user
    $ok.metadata.event_type = "USER_LOGIN"
    $ok.security_result.action = "ALLOW"
    $ok.target.user.userid = $user
    $fail.metadata.event_timestamp.seconds < $ok.metadata.event_timestamp.seconds

  match:
    $user over 10m

  outcome:
    $risk_score = 60

  condition:
    #fail >= 5 and $ok
}
```

Here `$user` is the match variable that groups events, `#fail` counts the failure events, and `outcome` assigns a risk value. Read rules for four things: what the events filter selects, what groups events, what must be true, and what value the detection carries.

### Reference lists, context and risk

**Reference lists** are generic lists of values used to analyse data. The type, set when the list is created, decides how values match: **string** lists require exact, case-sensitive matches, **regex** lists treat each line as a regular expression, and **CIDR** lists hold IPv4 or IPv6 ranges and test whether a field falls within them. In a rule you reference a list by name with a `%` prefix and test membership with `in`. The documentation says reference lists are being deprecated and replaced by data tables, with legacy functionality scheduled for retirement in July 2027, so check current guidance. (Exam guide 2.0 names data tables for risk-value rules.) Use lists for watch lists such as high-risk networks, privileged accounts or approved administrative hosts, so you can update values without editing rules.

```
events:
  $e.metadata.event_type = "NETWORK_CONNECTION"
  $e.principal.ip in %high_risk_networks
```

Designing rules that use risk values means building scores into detections so that alerts can be prioritised: a login from a high-risk network by a privileged account scores higher than a login from a normal network by a standard user. The guide names **Risk Analytics** and **curated detection rules** as sources of risk-assigning detections of anomalous behaviour by assets or users. Curated detections are prebuilt rule sets maintained by Google security experts that appear alongside your own rules, and they cannot be run as retrohunts.

**Use entity and context data to improve accuracy.** Using the entity graph (the guide's example), a rule can ask not only "did this login happen" but "was it by a user in a sensitive group on a laptop that is not managed". Context raises precision and lowers false positives.

### Detecting posture and risk-profile changes

Not every detection is about an attacker's action; some are about the environment's state changing. SCC **Security Health Analytics** detects misconfigurations, SCC posture management defines desired postures and flags drift, and SecOps rules can alert when, for example, a firewall rule opens a sensitive port or a new service account key is created. Design these to detect change from the baseline and route them to the owner.

### Finding rare and unseen items

New or low-prevalence processes, domains and IP addresses that do not appear in threat intelligence can be the most interesting, because attackers use fresh infrastructure. Methods named by the guide include writing YARA-L rules and building dashboards. A pattern is to count how many hosts have ever contacted a domain or run a binary, and alert when a never-before-seen item appears on a sensitive asset, then enrich with intelligence to decide.

### Event Threat Detection custom detectors

SCC **Event Threat Detection** is a built-in service of the Premium tier that monitors logs in near-real time using detection logic, threat intelligence, IOCs, anomaly detection and machine learning, and writes findings to SCC. For custom detections, it provides module templates; for threats with no template, you can export logs to BigQuery and write SQL queries. Configure custom detectors for IOCs (specific bad IPs, domains or identities) so SCC raises a finding when they appear in the logs it reads.

## 4.2 Threat intelligence for detection

- **Score alerts by IOC risk level.** Not all indicators are equal: a hash confirmed in active ransomware campaigns outweighs a stale scanning IP. Use confidence, recency and source to assign scores, and let those scores raise or lower alert priority.
- **Use the latest IOCs against ingested telemetry.** Match new indicators against live and historical data (retrohunt, notes 03), and keep feeds fresh because indicators decay.
- **Measure repetitive alerts to cut false positives.** Count how often a rule fires, per rule, per entity and per source. A rule that fires thousands of times for one backup server is a tuning candidate: exclude that known-good entity with a precise condition or reference list, never by deleting the rule. Track false positive rate as a metric and review it in your observability dashboards (notes 06).

---

## Key terms

- **YARA-L 2.0** - the rule language used in Google SecOps to correlate UDM events and generate detections
- **Single-event rule** - a rule that flags individual events and has no match window
- **Multi-event rule** - a rule that groups events over a match window and applies a condition to counts or combinations
- **Match section** - the part of a YARA-L rule that groups events by variables over a time window
- **Outcome section** - the part of a YARA-L rule that computes extra values, such as risk scores, for each detection
- **Reference list** - a list of values, of string, regex or CIDR type, used in rules to match fields
- **Data table** - the structure that is replacing reference lists in Google SecOps for lookup data
- **Curated detection** - a prebuilt rule set maintained by Google security experts that cannot be run as a retrohunt
- **Risk Analytics** - SecOps capability that assigns risk values to detections of anomalous behaviour by assets and users
- **Entity graph** - the context data about entities that rules can use to improve detection accuracy
- **Security Health Analytics** - the SCC service that detects misconfigurations used to build posture-change detections
- **Custom detector** - an Event Threat Detection module configured to detect specific IOCs or patterns
- **Low-prevalence item** - a process, domain or address seen on very few assets, worth investigating when absent from intelligence
- **False positive** - an alert raised for benign activity

---

## Related

- [Notes 03: threat hunting](./03-threat-hunting.md)
- [Notes 06: observability](./06-observability.md)
- **[📖 YARA-L 2.0 overview](https://docs.cloud.google.com/chronicle/docs/detection/yara-l-2-0-overview)** - rule sections, single and multi-event rules
- **[📖 Detect threats with unified rules](https://docs.cloud.google.com/chronicle/docs/detection/unified-rules/get-started)** - states that curated detections cannot be run as retrohunts
- **[📖 Reference lists](https://docs.cloud.google.com/chronicle/docs/reference/reference-lists)** - string, regex and CIDR lists in rules
- **[📖 Event Threat Detection overview](https://docs.cloud.google.com/security-command-center/docs/concepts-event-threat-detection-overview)** - detection sources and custom modules
- **[📖 Run a rule against historical data](https://docs.cloud.google.com/chronicle/docs/detection/run-rule-historical-data)** - retrohunt and curated detection limits
- **[📖 Exam guide (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_english.pdf)** - section 4 considerations
