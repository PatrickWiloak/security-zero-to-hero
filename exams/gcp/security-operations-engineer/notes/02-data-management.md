---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 12 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 02 - Data management

**Section 2: Data management (~20%)** - tasks 2.1, 2.2 and 2.3 of exam guide 2.0. This section grew from about 14% to about 20% and gained a new task, so it is now one of the heaviest.

Detection quality is capped by data quality. This section covers getting the right logs in, in a usable shape, at a cost you can sustain, and attaching context so a bare event becomes meaningful.

---

## 2.1 Ingesting logs for security tooling

**Decide what to ingest.** Assess the logs you need for detection and response, including automated sources, per the guide. Work backwards from threats: for credential theft you need identity provider and authentication logs; for cloud misuse you need Cloud Audit Logs (including Data Access logs for sensitive services, notes 01); for lateral movement you need network and endpoint telemetry; for data exfiltration you need storage, DNS and proxy logs. SCC **Event Threat Detection** consumes Cloud Logging streams itself, including Cloud Audit Logs and, with organization-level activation, Google Workspace logs, plus Cloud DNS, VPC flow, firewall rules, Cloud NAT, load balancing and Cloud IDS logs, database, GKE, Backup and DR and AI agent logs depending on the rule. Know which sources SCC reads automatically so you do not pay to ingest the same data twice without a reason.

**Choose an ingestion approach.** Google SecOps ingests through forwarders, collectors, ingestion APIs and third-party integrations. Guide 2.0 gives two concrete pipelines to be able to architect: configuring **Bindplane** to collect Microsoft Windows Event logs and route them to Google SecOps, and configuring direct ingestion of SCC findings into Google SecOps.

**Bindplane.** Per Google's documentation, the Bindplane agent is an open-source, OpenTelemetry-based collector. For Windows it uses a `windowseventlog` receiver per channel (Security, Application, System, and Sysmon if you run it) and a `chronicle` exporter that sends to Google SecOps. The Windows Event parser expects raw, unrendered events, so the channel is configured with `raw: true`, and the exporter authenticates with an ingestion authentication file downloaded from the SecOps collection agents settings. Google recommends its built-in ingestion instead when the Windows server runs on Google Cloud. Reasoning to practise: where is the data, which collector fits, and what breaks if the format is wrong (the parser quietly fails to map fields).

**SCC findings.** Because SCC already reads Cloud Logging for threats, ingesting its findings into SecOps lets you correlate them with endpoint, identity and network events in one place instead of working two consoles.

Choose by where the data lives: Google Cloud logs flow from Cloud Logging, SaaS applications through API-based feeds, on-premises systems through a forwarder or collector, and custom sources through the ingestion API. A Cloud Logging sink can route Google Cloud logs to a destination such as BigQuery:

```bash
gcloud logging sinks create secops-audit-to-bq \
  bigquery.googleapis.com/projects/PROJECT_ID/datasets/audit_logs \
  --organization=ORG_ID --include-children \
  --log-filter='logName:"cloudaudit.googleapis.com"'
```

After creating a sink, grant its writer identity permission on the destination, or nothing will arrive.

**Parsers and normalisation.** A **parser** is a component that normalises raw log data into the Unified Data Model (UDM) structure, so that events from different products are searched and analysed uniformly. Evaluate whether a prebuilt parser exists for a source and whether it maps the fields you need. When it does not, use a **parser extension** to add or adjust mappings rather than replacing the whole parser, and test with representative samples. The Health Hub shows failed sources and parsers and reports normalisation problems; parser alerts trigger when the proportion of parser errors in ingested events rises by 5 percentage points or more compared with the previous day. A drop in a field's population after a vendor update is a classic sign that a parser needs attention.

**Normalisation techniques.** Normalisation means consistent field names, types and values, for example one representation of a username regardless of whether the source logged `DOMAIN\user` or `user@domain`. Evaluate whether mappings preserve what a detection needs, such as the acting principal, target resource, source IP and outcome. Inconsistent normalisation produces missed detections without any visible error.

**Labels.** Evaluate new labels for ingestion: tags that identify the environment, business unit, data source or sensitivity. Labels let you route, scope access and filter detections, for instance to apply stricter rules to production.

**Manage log and ingestion costs.** Volume drives cost. Ingest what supports a detection, investigation or compliance need and justify the rest. Filter noisy, low-value events at the source or at the sink, keep verbose logs in cheaper storage and search them with BigQuery when needed, set retention by purpose, and watch ingestion volume by source for sudden spikes. Remember that Data Access audit logs and flow logs can be very large.

## 2.2 Implementing a baseline of user, asset and entity context

Raw events say that something happened. Context says to whom and whether it is unusual.

**Identify relevant threat intelligence.** Know which intelligence applies to your environment (sector, technology, geography) and where it comes from: Google Threat Intelligence, open feeds, ISAC feeds and your own incident history. Intelligence is only useful if it is matched against your telemetry.

**Event data versus entity data.** The guide asks you to differentiate the two. **Event data** records things that happened: a login, a process start, an API call (Cloud Audit Logs are event data). **Entity data** describes the things events are about: users, assets and groups, with attributes such as department, manager, privilege level, criticality and location (Active Directory organisational context is entity data). A detection that knows only the event can say "someone logged in from a new country"; with entity data it can say "a domain administrator on the finance team did".

**Enrichment through aliasing.** Different sources identify the same entity differently: a laptop is a hostname in one log, an IP address in another and an asset tag in a third. **Aliasing** fields lets the platform match event and entity data across these identifiers so that all activity for one asset or user is stitched into one picture. Evaluate matches carefully: a reused IP address or a shared service account can produce wrong merges, which makes investigations misleading. Check that each important source has at least one field that links to the entity data you hold.

## 2.3 Ingesting and configuring threat intelligence

This task is new in guide 2.0 and is where intelligence stops being a report and becomes data in the platform.

**Ingest GTI or third-party IOCs into the Entity Context Graph.** Google SecOps parses indicator feeds (for example MISP, STIX/TAXII or CSV and JSON lists, or Google Threat Intelligence content) into UDM entities in the **Entity Context Graph**. Once there, indicators can be matched against event telemetry, searched across retained history and used in YARA-L rules. Two details from the documentation are worth knowing. Customer-ingested IOCs use the ENTITY_CONTEXT source type, and giving a feed the wrong log type at setup means raw indicator payloads never parse into entity fields. Graph entries are also time-bound: by default an entry is valid for roughly five days either side of its ingestion time, so feeds must be re-ingested at least daily for live rules and retrohunts to keep working (an entity with a `metadata.threat` field is exempt from that expiry).

**Configure and use GTI capabilities.** The guide names GTI threat hunting, **LiveHunt**, **Digital Threat Monitoring (DTM)**, Google Insights and URL Scanning. Treat them by job. Hunting and LiveHunt search for files and indicators matching patterns you define. DTM watches for your organisation's exposure outside your perimeter, such as mentions on the dark web and leaked material, and its alerts need a response (task 5.1). Insights and URL Scanning give context about an indicator and what a URL does. I could not find Google documentation tying DTM or LiveHunt directly into SecOps ingestion, so learn them as GTI capabilities and check the GTI documentation before the exam.

Good context is what makes later work cheaper: hunts can ask about "privileged users" instead of lists of names (notes 03), detection rules can weigh risk by asset criticality (notes 04) and responders can see ownership immediately (notes 05).

---

## Key terms

- **Unified Data Model** - Google SecOps' common schema into which parsers normalise events from all sources
- **Parser** - a component that normalises raw log data into the Unified Data Model
- **Parser extension** - an addition to a parser that maps extra or changed fields without replacing the whole parser
- **Normalization** - converting events into consistent field names, types and values so they can be searched and detected uniformly
- **Event data** - records of things that happened, such as logins, process starts and API calls
- **Entity data** - descriptive context about users, assets and groups, such as role, department and criticality
- **Aliasing** - matching different identifiers for the same entity across sources so activity can be stitched together
- **Health Hub** - the SecOps view that shows failed sources and parsers and normalization problems
- **Log sink** - a Cloud Logging configuration that routes matching log entries to a destination
- **Label** - a tag attached to ingested data to identify its environment, source or sensitivity for routing and filtering
- **Forwarder** - an on-premises component that collects logs and sends them to the security platform
- **Bindplane** - an open-source, OpenTelemetry-based collector used to send logs such as Windows Event logs to Google SecOps
- **Entity Context Graph** - the SecOps store of entity and indicator context that events are matched against
- **LiveHunt** - a GTI capability that searches for files matching rules you define
- **Digital Threat Monitoring** - a GTI capability that watches for an organisation's exposure outside its perimeter

---

## Related

- [Notes 01: platform operations](./01-platform-operations.md)
- [Notes 03: threat hunting](./03-threat-hunting.md)
- [Centralized logging and alerting project](../../../../resources/hands-on-projects/centralized-logging-and-alerting.md)
- **[📖 Event Threat Detection overview](https://docs.cloud.google.com/security-command-center/docs/concepts-event-threat-detection-overview)** - the log sources Event Threat Detection reads
- **[📖 Ingestion overview for Google SecOps](https://docs.cloud.google.com/chronicle/docs/ingestion/ingestion-overview)** - parsers and Health Hub monitoring
- **[📖 What is Google Security Operations?](https://docs.cloud.google.com/chronicle/docs/overview)** - ingestion methods and normalisation
- **[📖 Deploy the Bindplane agent for collection](https://docs.cloud.google.com/chronicle/docs/ingestion/use-bindplane-agent)** - Windows Event log collection
- **[📖 Entity Context Graph overview](https://docs.cloud.google.com/chronicle/docs/event-processing/entity-graph)** - entity and indicator context
- **[📖 Integrate your own threat intelligence feeds](https://docs.cloud.google.com/chronicle/docs/detection/integrate-threat-intel-feeds)** - feed ingestion into SecOps
- **[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** - section 2 considerations
