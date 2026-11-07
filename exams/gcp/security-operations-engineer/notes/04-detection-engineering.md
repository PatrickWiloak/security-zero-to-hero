---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 04 - Detection engineering

**Section 4: Detection engineering (~20%)** - tasks 4.1 and 4.2 of exam guide 2.0. Tied with data management as the largest section.

Detection engineering turns understanding of attacker behaviour into rules that run continuously, at an acceptable noise level. The tool at the centre is **YARA-L 2.0**, the rule language of Google SecOps.

---

## 4.1 Developing and implementing mechanisms to detect risks and identify threats

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

**Reference lists** are generic lists of values used to analyse data. The type, set when the list is created, decides how values match: **string** lists require exact, case-sensitive matches, **regex** lists treat each line as a regular expression, and **CIDR** lists hold IPv4 or IPv6 ranges and test whether a field falls within them. In a rule you reference a list by name with a `%` prefix and test membership with `in`. The documentation says reference lists are being deprecated and replaced by data tables, with legacy functionality scheduled for retirement in July 2027, so check current guidance. Exam guide 2.0 names data tables in its risk-value task (below). Use lists for watch lists such as high-risk networks, privileged accounts or approved administrative hosts, so you can update values without editing rules.

```
events:
  $e.metadata.event_type = "NETWORK_CONNECTION"
  $e.principal.ip in %high_risk_networks
```

### Data tables

A **data table** is a multicolumn dataset you supply, which rules use as a lookup. A reference list holds one column of values; a data table spans several, so one lookup can filter on more than one field. You create tables in the web interface, through the API, or by writing rule results into them. In YARA-L a table is referenced as `%table_name.column_name`. A column-based test uses `in`, as with lists; a row-based test uses `=` and requires every condition to match the same row, which makes the rule a multi-event rule that needs a `match` section.

```
events:
  $e.principal.hostname = $host
  $e.target.hostname in %badApps.hostname
```

For risk values, store a score beside each entry (a host, user or application and its risk) and let the rule read it into `outcome`, so you tune risk by editing the table instead of the rule. Documented limits include up to 10 million rows per table (read from the data tables page on 2026-11-07), and no real-time run frequency for rules that use data tables, so a rule using them runs on a schedule, which matters for time-sensitive detections.

Designing rules that use risk values means building scores into detections so that alerts can be prioritised: a login from a high-risk network by a privileged account scores higher than a login from a normal network by a standard user. The guide names **Risk Analytics** and **curated detection rules** as sources of risk-assigning detections of anomalous behaviour by assets or users. Curated detections are prebuilt rule sets maintained by Google security experts that appear alongside your own rules, and they cannot be run as retrohunts.

**Use entity and context data to improve accuracy.** Using the entity graph (the guide's example), a rule can ask not only "did this login happen" but "was it by a user in a sensitive group on a laptop that is not managed". Context raises precision and lowers false positives.

### Detecting posture and risk-profile changes

Not every detection is about an attacker's action; some are about the environment's state changing. SCC **Security Health Analytics** detects misconfigurations, SCC posture management defines desired postures and flags drift, and SecOps rules can alert when, for example, a firewall rule opens a sensitive port or a new service account key is created. Design these to detect change from the baseline and route them to the owner.

### Finding rare and unseen items

New or low-prevalence processes, domains and IP addresses that do not appear in threat intelligence can be the most interesting, because attackers use fresh infrastructure. Methods named by the guide include writing YARA-L rules and building dashboards. A pattern is to count how many hosts have ever contacted a domain or run a binary, and alert when a never-before-seen item appears on a sensitive asset, then enrich with intelligence to decide.

### Composite detections

Guide 2.0 asks you to write **composite detections** to discover activity correlations over longer periods. A composite rule takes detections or alerts from other rules as its input, and must have a `match` section. Base rules produce detections, the composite rule correlates them, and its output can feed further rules in a chain. This is how you catch a multi-stage attack where no single rule is suspicious by itself, such as the same user tripping two different rules within two weeks.

```
rule Two_Rules_Same_User {
  events:
    $d1.metadata.event_type = "DETECTION"
    $d1.metadata.rule_name = "RULE_A"
    $user = $d1.detection.collection_elements.references.event.principal.user.userid
    $d2.metadata.event_type = "DETECTION"
    $d2.metadata.rule_name = "RULE_B"
    $user = $d2.detection.collection_elements.references.event.principal.user.userid
  match:
    $user over 14d
  condition:
    $d1 and $d2
}
```

The documentation's field paths for `$user` are illustrative, so check them before use. Facts to remember: the longest match window for detection rules is 14 days, chains can be up to 10 rules deep, joins are most reliable on outcome variables, meta labels and match variables, and exclusions belong on the underlying rules, not the composite. To test a chain, run a retrohunt on each rule in order. Long windows run less often, so they suit slow-moving threats rather than time-critical alerting.

### Coverage against MITRE ATT&CK

Guide 2.0 asks you to analyse detection coverage against **MITRE ATT&CK**. In Google SecOps the MITRE ATT&CK matrix tab (under Rules and Detections) shows tactics as columns and techniques as cards, coloured by how many rules cover each. A custom rule counts toward coverage only if its metadata carries the technique ID, such as `technique="T1548"`. A technique with zero rules may still show a count of related log types, which marks a detection opportunity. The matrix can be filtered by rule type and status and exported for the MITRE ATT&CK Navigator. This closes the loop with task 1.1: coverage gaps become the detection backlog.

### Natural-language rule creation

Guide 2.0 also lists prompting AI in natural language to create detection rules. The safe habit is the same as for hunting: treat the generated YARA-L as a first draft, read each section, test it against known events and a retrohunt, and check the technique metadata and severity before enabling.

### SCC detectors and Web Security Scanner

Guide 2.0 asks you to configure SCC threat detectors: Event Threat Detection, Cloud Run Threat Detection, Container Threat Detection and Virtual Machine Threat Detection. Pick by workload: logs for cloud activity, containers for GKE, VMs for agentless memory-level visibility, Cloud Run for serverless. It also asks you to configure SCC tooling such as **Web Security Scanner** to send run-time vulnerabilities to Google SecOps, so web application findings can be correlated with the rest of your telemetry. And the posture task now covers **AI infrastructure risks** and uses Compliance Manager alongside SecOps.

### Event Threat Detection custom detectors

SCC **Event Threat Detection** is a built-in service of the Premium tier that monitors logs in near-real time using detection logic, threat intelligence, IOCs, anomaly detection and machine learning, and writes findings to SCC. For custom detections, it provides module templates; for threats with no template, you can export logs to BigQuery and write SQL queries. Configure custom detectors for IOCs (specific bad IPs, domains or identities) so SCC raises a finding when they appear in the logs it reads.

## 4.2 Threat intelligence for detection

- **Score alerts by IOC risk level.** Not all indicators are equal: a hash confirmed in active ransomware campaigns outweighs a stale scanning IP. Use confidence, recency and source to assign scores, and let those scores raise or lower alert priority.
- **Use the latest IOCs against ingested telemetry.** Match new indicators against live and historical data (retrohunt, notes 03), and keep feeds fresh because indicators decay.
- **Configure rules from GTI.** Write detections from GTI TTPs and IOCs where they fit the use case, not wholesale: each rule is maintained work.
- **Applied Threat Intelligence.** Guide 2.0 names **Applied Threat Intelligence (ATI)** for understanding exposure, with the Emerging Threats Center and curated detections as examples. ATI matches Google's intelligence against your telemetry, and the Emerging Threats Center shows which active campaigns your environment may be exposed to and which rules cover them.
- **Measure repetitive alerts to cut false positives.** Count how often a rule fires, per rule, per entity and per source. A rule that fires thousands of times for one backup server is a tuning candidate: exclude that known-good entity with a precise condition or reference list, never by deleting the rule. Track false positive rate as a metric and review it in your observability dashboards (notes 06).

---

## Key terms

- **YARA-L 2.0** - the rule language used in Google SecOps to correlate UDM events and generate detections
- **Single-event rule** - a rule that flags individual events and has no match window
- **Multi-event rule** - a rule that groups events over a match window and applies a condition to counts or combinations
- **Match section** - the part of a YARA-L rule that groups events by variables over a time window
- **Outcome section** - the part of a YARA-L rule that computes extra values, such as risk scores, for each detection
- **Reference list** - a list of values, of string, regex or CIDR type, used in rules to match fields
- **Data table** - a multicolumn lookup dataset that is replacing reference lists in Google SecOps
- **Composite detection** - a detection made by a rule whose input is the detections of other rules, used to correlate over longer periods
- **Applied Threat Intelligence** - Google intelligence matched against your telemetry, with the Emerging Threats Center to show exposure
- **MITRE ATT&CK matrix** - the SecOps view of rule coverage by tactic and technique
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
- **[📖 Data tables](https://docs.cloud.google.com/chronicle/docs/investigation/data-tables)** - multicolumn lookups in rules
- **[📖 Composite detections](https://docs.cloud.google.com/chronicle/docs/detection/composite-detections)** - chaining rules
- **[📖 Monitor threat coverage (MITRE)](https://docs.cloud.google.com/chronicle/docs/detection/mitre-dashboard)** - the ATT&CK matrix
- **[📖 Event Threat Detection overview](https://docs.cloud.google.com/security-command-center/docs/concepts-event-threat-detection-overview)** - detection sources and custom modules
- **[📖 Run a rule against historical data](https://docs.cloud.google.com/chronicle/docs/detection/run-rule-historical-data)** - retrohunt and curated detection limits
- **[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** - section 4 considerations
