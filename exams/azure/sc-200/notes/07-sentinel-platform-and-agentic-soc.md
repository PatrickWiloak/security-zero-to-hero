---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 30 min
---

# 07 - The Sentinel platform, attack disruption, and the agentic SOC

The SC-200 outline was restructured in 2026 into three domains, and it now names a set of capabilities that notes 01 to 06 predate: the Microsoft Sentinel data lake and its tiers, KQL jobs, summary rules, Sentinel graph, notebooks connected to the Sentinel MCP server, automatic attack disruption, case management, investigation with Security Copilot, SOC optimization, Windows Event Forwarding, and Microsoft Graph activity logs. This page teaches them. Read it after notes 02 (Sentinel) and 04 (incident response).

**[📖 SC-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-200)** - skills measured as of October 21, 2026, with the change log

## What the October 21, 2026 update changed

Almost nothing. The change log marks one minor change, in *Ingest data into the Microsoft Sentinel SIEM and platform*: "Configure collection of Azure activities by using Azure Policy and resource diagnostic settings" now reads "Configure collection of Azure activity logs by using Azure Policy and resource diagnostic settings". The wording is clearer; the skill is the same.

The bigger change happened earlier in 2026, when the outline moved from four domains to three:

| Domain | Weight |
|--------|-------:|
| Manage a security operations environment | 40-45% |
| Respond to security incidents | 35-40% |
| Perform threat hunting | 20-25% |

"Configure protections and detections" no longer stands alone; detections now sit inside the first domain, which is why it nearly doubled. Study guides and courses that still show four domains (including the 25-30% / 15-20% / 35-40% / 15-20% split) teach the old outline.

---

## The Sentinel data lake and data tiers

### Why tiers exist

A SIEM has always forced a trade: keep everything searchable and pay for it, or drop high-volume logs and lose them for investigations. Firewall, DNS, and proxy logs are the classic victims. They are huge, rarely queried, and exactly what you need when an incident turns out to be six months old.

Microsoft Sentinel now stores data in tiers so that trade is made per table rather than for the whole SIEM.

- **Analytics tier.** The "hot" tier: fully indexed, fast, and the only tier where analytics rules, hunting queries, workbooks, watchlists, and playbooks work in real time. Default analytics retention is 30 days; Microsoft Sentinel tables can be extended to 90 days without a storage charge, and any table up to two years at a long-term retention charge.
- **Data lake tier.** The "cold" tier: low-cost, long-term storage (up to 12 years) in open Parquet format. Data in the analytics tier is mirrored to the lake by default, so you hold a single copy that is hot for its analytics retention and cold after that. You can also send a table *only* to the lake. Lake data is slower to query, has no query price included, and does not support real-time analytics rules.
- **XDR default tier.** Defender XDR advanced hunting tables (such as `DeviceEvents` or `EmailEvents`) are kept for 30 days as part of the XDR license and are not in your Sentinel workspace at all by default. Extending a supported XDR table's retention beyond 30 days creates it in the Sentinel workspace, in the analytics tier, mirrored to the lake; up to 90 days carries ingestion cost but no storage cost.

The outline bullet "Manage data retention for XDR and Microsoft Sentinel tables, including Analytics, Data lake, and XDR tiers" tests exactly these rules.

### Getting value out of lake data

Cold data is only useful if you can bring it back when you need it. Three tools do that, and the exam distinguishes them:

- **KQL jobs** run a KQL query against the data lake, once or on a schedule, and write the result into a table in the analytics tier. Use them to promote the slice you need ("all DNS queries to this domain in the last year") so analytics rules and hunting can use it.
- **Summary rules** run on a schedule against a high-volume table and write aggregated results (counts per user per hour, bytes per destination per day) to a custom analytics table. Detections then run on the small summary instead of the raw firehose. They work on analytics tables and on lake-tier data with full KQL on a single table.
- **Search jobs** run a long query across large datasets and write the matches to a results table (suffix `_SRCH`), useful for one-off investigations.

**Worked scenario:** a company ingests 400 GB per day of firewall logs and cannot afford to keep them in the analytics tier. The design sends the firewall table to the data lake tier only, with three years of total retention for compliance. A summary rule aggregates outbound connections per source host per hour into an analytics table, and a scheduled analytics rule alerts on hosts whose outbound volume jumps sharply. When an investigation needs the raw rows for a specific host from eight months ago, an analyst runs a KQL job that promotes those rows into an analytics table for hunting.

**How the exam tests this:** match the need to the tier and tool. "Retain for years at the lowest cost; real-time detection not needed" is the data lake tier. "Detect on a high-volume source cheaply" is a summary rule. "Make last year's lake data available to hunting queries" is a KQL job. "Keep Defender for Endpoint events for 180 days" means extending the XDR table's retention, which moves it into the Sentinel workspace.

- **[📖 Microsoft Sentinel data lake overview](https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-lake-overview)** - architecture, tiers, KQL, and notebooks
- **[📖 Manage data tiers and retention](https://learn.microsoft.com/en-us/azure/sentinel/manage-data-overview)** - analytics, data lake, and XDR default tiers compared

---

## Sentinel graph, hunting graphs, and blast radius

Logs are rows; attacks are paths. An attacker who phishes a user, steals a token, and reaches a database moves along relationships between identities, devices, permissions, and resources. **Sentinel graph** builds those relationships from data in the Sentinel platform (assets, identities, activity, and threat intelligence) so defenders and AI agents can reason over connections rather than joining tables by hand. If you have the data lake, the graph is provisioned for you in the Defender portal.

Two experiences appear in the outline:

- **Hunting graphs** let an analyst start from an entity and visually traverse its relationships: which devices a user signs into, which privileged groups those lead to, which critical assets sit at the end of the path. They answer "how could an attacker get from here to there?" before anyone has.
- **Blast radius analysis** enriches the incident graph during an active attack: from the compromised entity, it shows the vulnerable paths to critical assets, so responders contain the paths that matter first.

**How the exam tests this:** "Visualize the paths from a compromised account to critical servers during an incident" is blast radius. "Proactively find privileged access paths to critical assets" is a hunting graph. "Analyze relationships between entities" names Sentinel graph directly.

---

## Notebooks and the Sentinel MCP server

**Jupyter notebooks** let analysts use Python against the Sentinel data lake for work KQL is poor at: machine learning, statistical baselining, large joins, and custom visualizations. Notebooks can be scheduled, and like KQL jobs they can promote results to the analytics tier.

The **Model Context Protocol (MCP)** is an open protocol that lets AI tools call external tools in a standard way. The **Sentinel MCP server** exposes collections of security tools to any compatible client: a data exploration collection that finds the right tables and queries the lake from a natural-language request (with graph tools for exposure and hunting graphs), a triage collection for incidents, and a collection for building Security Copilot agents. Connecting a notebook environment or coding assistant to the MCP server lets an analyst ask "which service principals signed in from new countries last month?" without knowing the table names or schema.

**Trade-off:** natural-language access lowers the skill barrier and speeds exploration, but generated queries can be wrong. The analyst still owns validating results, and the exam favors answers where AI assists rather than replaces verification.

**How the exam tests this:** "Hunt with Python and machine learning over a year of lake data" is notebooks. "Let an AI assistant search Sentinel data in natural language" is the Sentinel MCP server.

- **[📖 What is Microsoft Sentinel's support for MCP?](https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-overview)** - MCP collections and clients

---

## Automatic attack disruption

Some attacks move faster than any SOC can respond. Human-operated ransomware can go from first lateral movement to mass encryption in under an hour, and adversary-in-the-middle phishing can turn a stolen session cookie into a business email compromise in minutes. **Automatic attack disruption** is Defender XDR's answer: when correlated signals across endpoint, identity, email, and cloud apps give high confidence that one of these attacks is in progress, Defender acts on its own to contain it.

Typical actions are **contain device** (isolate a compromised endpoint from the rest of the network), **contain user** (block a compromised account's lateral movement from devices that support it), and **disable user** in Active Directory or Microsoft Entra ID. The incident is tagged as attack disruption so analysts can see what was done and release containment after investigation.

Configuration is mostly about prerequisites rather than switches: the relevant Defender workloads must be deployed, Defender for Endpoint and Defender for Identity must be able to take action (for example, Defender for Identity needs an action account to disable users in AD), and device groups can be excluded from automated containment. The outline places "Configure automatic attack disruption" in domain 1 and "Investigate and remediate incidents identified by automatic attack disruption" in domain 2, so you need both halves.

**How the exam tests this:** "Stop an in-progress ransomware attack automatically before an analyst can respond" is attack disruption. Watch for exclusions: a critical server excluded from automated containment will not be isolated, which is sometimes the point of the question.

- **[📖 Automatic attack disruption in Microsoft Defender XDR](https://learn.microsoft.com/en-us/defender-xdr/automatic-attack-disruption)** - scenarios, actions, and prerequisites

---

## Case management and investigation with Security Copilot

**Case management** in the Defender portal turns security work into tracked work items. A **case** brings together investigation context, tasks, evidence, notes, attachments, and activity history with ownership and status. Incident cases are created from correlated incident activity; generic cases track other SecOps work such as a hunt or a control review. The value is accountability and continuity: shift handovers, audits, and post-incident reviews read from the case rather than from chat threads.

**Microsoft Security Copilot** is embedded in the Defender portal. During an investigation it can summarize an incident, explain a suspicious script or command line, suggest response steps from guided response, write a KQL query from a description, and draft an incident report. Copilot **agents** go further and work a defined task autonomously, such as triaging user-reported phishing and closing false positives with an explanation the analyst can review. The outline calls this "agentic AI".

**Trade-off and exam angle:** AI speeds triage, but the analyst remains accountable for decisions. Correct answers use Copilot to summarize, explain, and draft, then verify against evidence; distractors let AI close incidents with no review in high-impact cases.

- **[📖 Case management in Microsoft Defender](https://learn.microsoft.com/en-us/defender-xdr/siem-defender-case-management)** - incident cases and generic cases
- **[📖 Microsoft Security Copilot in Microsoft Defender](https://learn.microsoft.com/en-us/defender-xdr/security-copilot-in-microsoft-365-defender)** - incident summaries, script analysis, guided response

---

## SOC optimization

**SOC optimization** gives recommendations, in the Defender and Azure portals, for getting more value from Sentinel. There are three kinds: **data value** recommendations flag tables you pay to ingest but never use in detections (move them to a cheaper tier, or start using them); **threat-based coverage** recommendations compare your detections against attack scenarios such as human-operated ransomware or AiTM and point to missing rules and data; and **similar organizations** recommendations suggest data sources that comparable organizations ingest. It is the outline's "Optimize the Microsoft Sentinel platform" bullet.

**How the exam tests this:** "Identify ingested tables that no analytics rule uses" or "find detection coverage gaps for a specific attack type" is SOC optimization.

- **[📖 SOC optimization](https://learn.microsoft.com/en-us/azure/sentinel/soc-optimization/soc-optimization-access)** - data value and coverage recommendations

---

## Data ingestion objectives the older notes miss

### Windows Event Forwarding

The preferred way to collect Windows Security events is the **Windows Security Events via AMA** connector with a data collection rule (DCR), which the older notes cover. The outline also names **Windows Event Forwarding (WEF)**: Windows' built-in mechanism in which source machines forward selected events to a collector server, configured through Group Policy and subscriptions. In Sentinel, you install the Azure Monitor Agent on the collector and use the **Windows Forwarded Events** connector to ingest the forwarded channel.

WEF fits when you cannot or will not install an agent on every server (domain controllers in a restricted tier, a large estate with limited change windows). The trade-off is a collector that becomes critical infrastructure and a forwarded channel that needs careful event filtering to avoid volume surprises.

### Syslog and CEF via AMA

Linux and network appliances send **Syslog**; many security appliances format their messages as **Common Event Format (CEF)** over syslog. Both now use AMA on a Linux log forwarder with a DCR that selects facilities and severities. The exam detail is which table the data lands in: plain syslog goes to `Syslog`, CEF to `CommonSecurityLog`. Filter in the DCR rather than after ingestion, because you pay for what you ingest.

### Azure activity logs by policy

Azure activity logs (control-plane operations such as creating a VM or changing an RBAC assignment) reach Sentinel through **diagnostic settings**. At scale, you assign the built-in **Azure Policy** that deploys diagnostic settings to every subscription, with a remediation task for existing subscriptions, so new subscriptions are covered automatically. This is the bullet the October update reworded.

### Microsoft Graph activity logs

Most cloud attacks after an identity compromise use the **Microsoft Graph API**: reading mailboxes, enumerating users, adding credentials to applications. **Microsoft Graph activity logs** record the HTTP requests made to Graph by apps and users, including the calling application, the request, and the IP address. You enable them through Microsoft Entra diagnostic settings and query the `MicrosoftGraphActivityLogs` table. The outline names them as a source for investigating Microsoft 365 threats, alongside Purview Audit and Content search in eDiscovery.

**Worked example:** an app registration was compromised and a client secret added. Entra audit logs show the secret being added; Graph activity logs show what the app then did with it, such as calling the mail endpoints for 300 mailboxes from one IP. Together they scope the incident.

- **[📖 Access Microsoft Graph activity logs](https://learn.microsoft.com/en-us/graph/microsoft-graph-activity-logs-overview)** - what is logged and how to enable it

---

## Related

- [Notes 02: Microsoft Sentinel fundamentals](./02-microsoft-sentinel-fundamentals.md) - workspaces, connectors, analytics rules
- [Notes 04: incident investigation and response](./04-incident-investigation-and-response.md) - triage and automation
- [Notes 05: threat hunting](./05-threat-hunting.md) - hypotheses, bookmarks, MITRE mapping
- [Logging and detection](../../../../learn/concepts/logging-and-detection.md) - the concepts behind SIEM design
