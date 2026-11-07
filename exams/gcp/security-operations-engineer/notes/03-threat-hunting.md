---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 12 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 03 - Threat hunting

**Section 3: Threat hunting (~18%)** - tasks 3.1 and 3.2 of exam guide 2.0.

Hunting is the proactive half of detection. Instead of waiting for an alert, you assume an adversary may already be present, pick a hypothesis, and search the data. The exam tests which tool to use for which question, and how threat intelligence turns into searches.

---

## 3.1 Performing threat hunting across environments

**Start with a hypothesis.** A good one is specific and testable: "an attacker who stole a service account key will use it from an unusual network", or "a compromised identity will enumerate storage buckets". Guide 2.0 lists the inputs: behaviour, threat intelligence, **attack path exposures** and incident data (for example from SCC, Google SecOps and GTI). Attack path exposure is a useful input that people forget: a misconfiguration or exposure SCC has flagged tells you where an attacker is most likely to go first.

**Develop queries across environment logs.** Use the right search tool for the data and the question. The guide names these Google Cloud tools:

- **Logs Explorer**: interactive searching of Cloud Logging entries for recent events, good for fast checks on a known resource.
- **Log Analytics**: SQL queries over log data in log buckets, good for aggregation and trends across a large volume.
- **BigQuery**: SQL over large exported datasets, including long-retention logs, joins with other data and heavy statistical work.
- **Google SecOps**: UDM search and raw log search across normalised telemetry from all your sources, with entity views and the ability to pivot from one indicator to related assets and users. **Stats queries** aggregate the results, which suits hunting by user behaviour (count logins, distinct hosts or bytes per user and compare).

Hunting queries share a shape: restrict by time and source, filter to the behaviour of interest, group by entity, and look at the tail. For example, to find service accounts calling an unusual number of distinct APIs in Log Analytics or BigQuery, group audit log entries by principal and count distinct methods per day, then inspect the highest counts and the sudden changes.

**Analyse user behaviour.** Guide 2.0 gives stats queries as the example technique.

**Prompt AI in natural language.** Guide 2.0 adds using natural-language prompts to AI to conduct threat hunting, for example asking the platform to find unusual administrative activity and having it build the search. Treat the result as a draft query: read the generated search, check its time range and fields, and confirm it answers your hypothesis before trusting an empty or huge result.

**Search the right graph.** The guide asks you to evaluate when to search the **SCC security graph** and when the **Google SecOps Entity Context Graph**. Use the SCC graph for questions about cloud resources and exposure: which assets exist, which hold sensitive data classifications and which have known vulnerabilities. Use the Entity Context Graph for questions about the users, assets and indicators seen in your telemetry.

**Analyse user behaviour (continued).** Compare an identity's activity against its own history and its peers: time of day, geography, resources touched, volume and the sequence of actions. Signals include a first-time access to sensitive data, an impossible travel pattern, privilege changes followed by data access, and a burst of failed then successful authentications. Entity context from notes 02 turns "an odd login" into "an unusual login for a privileged finance user".

**Investigate network, endpoints and services.** Pivot across data types: from an IP address to the hosts that talked to it, from a host to its processes and files, from a file hash to every machine that has it. The aim is to identify threat patterns or **indicators of compromise (IOCs)**, observable artefacts such as domains, IP addresses, file hashes and URLs that suggest compromise.

**Collaborate with incident response.** Hunters and responders share findings both ways. A hunt that finds active compromise is handed to incident response immediately with scope, evidence and the query that produced it. Responders feed back the techniques used so the next hunt starts from them.

## 3.2 Leveraging threat intelligence for hunting

**Search for IOCs in historical logs.** New intelligence often arrives after the activity. When an indicator is published you must ask whether it appeared in your data before today. Search retained telemetry for the domain, IP or hash going back as far as retention allows.

**Retrohunt.** Guide 2.0 phrases it as comparing and performing a retrohunt of historical event data with newly enriched logs. A **retrohunt** runs an existing rule's logic over past data, so the same detection logic can find previously undiscovered threats. In Google SecOps you choose a start and end time (the default is one week), and for a multi-event rule the search range must be at least as large as the rule's match window. Running a retrohunt with alerting enabled creates an alert for every historical detection, so the documentation recommends running it with the rule's alerting status disabled. Retrohunts are subject to lookback limits that depend on your data retention. Curated detections cannot be run as retrohunts (per the unified rules page). The documentation also notes that SecOps does not delete detections that came from reference lists, so refreshing a rule will not update results it already produced. The guide phrases this as comparing and performing retrohunt of historical event data with newly enriched logs, using the SecOps rules engine, BigQuery and Cloud Logging, so be ready to choose between them: SecOps retrohunt for rules over UDM data, BigQuery or Cloud Logging for queries over data not in SecOps.

**Identify new attack patterns in real time.** Intelligence and risk assessments (Google Threat Intelligence, detection rules, SCC **toxic combinations**) show what attackers are doing now and where your environment is exposed to it. Toxic combinations, as SCC names them, flag combinations of issues that together create high-risk paths; prioritise hunting where intelligence and exposure overlap.

**Entity risk score.** Analysing entity risk score helps surface anomalous behaviour: entities whose detections accumulate risk over time rise to the top of the list. Use the score to decide whom to hunt first, but verify, since a high score can come from noisy rules.

**Triage and Investigation Agent results.** Guide 2.0 asks you to analyse the results of the **Triage and Investigation Agent**, the AI investigation assistant in Google SecOps. Per Google's documentation it assesses whether an alert is a true or false positive and explains why, using dynamic searches, GTI enrichment, command-line analysis and process tree reconstruction. Its output is a summary with a disposition, a confidence level and an explanation, an investigation timeline and suggested next steps. Read it as a well-organised lead: check the evidence it cites, and use the timeline to decide what to hunt next. It runs only on SecOps SIEM data.

**Proactive search using intelligence.** Turn intelligence into hunts: take a threat actor's known techniques, write searches for them against your telemetry and look for hits even if no alert has fired. When a hunt works, convert it into a detection rule (notes 04) so it runs continuously.

---

## Key terms

- **Threat hunting** - proactively searching data for adversary activity based on a hypothesis, without waiting for an alert
- **Indicator of compromise** - an observable artefact, such as a domain, IP address or file hash, that suggests a system has been compromised
- **Logs Explorer** - the Cloud Logging interface for interactively searching log entries
- **Log Analytics** - SQL-based analysis of log data stored in Cloud Logging log buckets
- **Retrohunt** - running an existing detection rule's logic over historical data to find previously undiscovered threats
- **Match window** - the time window over which a multi-event rule groups related events
- **Toxic combination** - an SCC grouping of issues that together create a high-risk path to an asset
- **Entity risk score** - a score that accumulates from an entity's detections to highlight anomalous behaviour
- **Hypothesis** - a specific, testable statement about adversary behaviour that guides a hunt
- **Triage and Investigation Agent** - the SecOps AI assistant that assesses alerts, explains its reasoning and suggests next steps
- **Stats query** - a search that aggregates results, such as counts per user, to reveal patterns
- **Attack path exposure** - a route an attacker could take to an asset, found by SCC, used to prioritise hunts
- **Pivot** - moving an investigation from one indicator or entity to related ones, such as from an IP address to the hosts that contacted it

---

## Related

- [Notes 02: data management](./02-data-management.md)
- [Notes 04: detection engineering](./04-detection-engineering.md)
- [Detection and response topic](../../../../topics/detection-and-response.md)
- **[📖 Run a rule against historical data](https://docs.cloud.google.com/chronicle/docs/detection/run-rule-historical-data)** - retrohunt behaviour, ranges and limits
- **[📖 Detect threats with unified rules](https://docs.cloud.google.com/chronicle/docs/detection/unified-rules/get-started)** - curated detections and retrohunt limits
- **[📖 Toxic combinations and chokepoints overview](https://docs.cloud.google.com/security-command-center/docs/toxic-combinations-overview)** - the toxic combination finding class (Premium and Enterprise tiers)
- **[📖 Security Command Center overview](https://docs.cloud.google.com/security-command-center/docs/security-command-center-overview)** - tiers and posture management
- **[📖 What is Google Security Operations?](https://docs.cloud.google.com/chronicle/docs/overview)** - search and investigation views
- **[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** - section 3 considerations
