---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 12 min
applies-to: Google Cloud docs as read 2026-11-07
---

# 01 - Platform operations

**Section 1: Platform operations (~13%)** - tasks 1.1 and 1.2 of exam guide 2.0.

This section is about the toolset itself: which sources of telemetry matter, how the tools fit together, and who is allowed to do what inside them.

---

## The two platforms

Exam guide 2.0 says the exam assesses tasks in **Google Security Operations (SecOps)**, **Security Command Center (SCC)** and **Google Threat Intelligence (GTI)**. The third platform is new in 2.0. Learn what each owns.

**Google Security Operations** is a cloud service built on Google's infrastructure that lets an enterprise privately retain, analyse and search large volumes of security and network telemetry going back months or longer. It ingests data through forwarders, collectors, ingestion APIs and third-party integrations, normalises and indexes it, and supports raw log scans and regular expression searches. Investigation views (asset, IP, domain, hash, user) help analysts judge whether systems are compromised, the Detection Engine runs rules across incoming data and alerts on potential and known threats, and VirusTotal integration adds context. Its SOAR side adds cases and playbooks (section 5).

**Security Command Center** is a cloud-based risk management platform that helps teams prevent, detect and respond to security issues in Google Cloud. It produces **findings**, records of threats or issues, from built-in services, integrated Google Cloud services and partners. Its areas: vulnerability detection (misconfigurations, exposure, leaked credentials, compliance gaps against benchmarks, with **Security Health Analytics** as a key service); threat detection (**Event Threat Detection**, **Container Threat Detection**, **Virtual Machine Threat Detection**); posture management (defining postures, flagging drift, checking for over-permissioned accounts); and toxic combinations. SCC comes in Standard, Premium and Enterprise service tiers. The overview page states that the Enterprise tier is deprecated and will shut down on May 21, 2027, with Enterprise organizations moving to Premium automatically; check the current tier details before relying on a feature.

**Google Threat Intelligence** is Google's source of intelligence on indicators, actors and campaigns. In this exam it matters in two ways: as a telemetry and context source you prioritise and integrate (task 1.1), and as a platform you ingest from and hunt in (tasks 2.3, 3.2 and 4.2).

## 1.1 Enhancing detection and response

**Prioritise telemetry sources.** The 2.0 guide names SCC, GTI, Cloud Logging and Chrome Enterprise as examples of sources to rank for detecting incidents or misconfigurations. (The earlier guide also listed Cloud IDS, which inspects network traffic and is still a fair example of a network source.) Ask what each tells you that the others do not: SCC shows misconfiguration and cloud threats from Google Cloud logs; SecOps correlates across everything you ingest, including endpoints, identity and network; Cloud IDS inspects network traffic; GTI supplies intelligence on indicators and actors. Prioritise by the threats you care about and the assets that matter, and by the quality of the signal rather than the volume of the data.

**Integrate prebuilt content and tools.** Guide 2.0 adds integrating and maintaining prebuilt security tools from the **Google SecOps Content Hub**. Prebuilt content saves you writing parsers, rules and playbook pieces from scratch, but it must be maintained: updates arrive, and a stale copy drifts from the sources it was built for. Treat it as part of the architecture with an owner, not a one-time install.

**Integrate multiple tools.** A single tool seldom covers the architecture. Findings from SCC can be exported (Event Threat Detection findings can be exported through Pub/Sub and Cloud Run functions, or investigated in Google SecOps), and downstream third-party systems such as ticketing or messaging receive alerts. Prefer integrations that keep an authoritative record in one place, so that analysts do not have to reconcile three consoles.

**Justify overlapping tools.** The exam asks you to defend overlap using requirements. Two tools may both detect threats on a VM, but one might provide agentless coverage and the other deeper runtime visibility, or one might alert and the other correlate. If no requirement separates them, the overlap is cost without benefit. Frame it as: what requirement does each satisfy, and what is the gap if one is removed?

**Evaluate coverage and automation.** Map your detections to the attacker techniques you must catch, list the log sources that make each possible, and identify gaps: sources not ingested, rules not enabled, assets unmonitored. Guide 2.0 asks you to enhance detection and response using AI, automation and cloud-based tools, so look for repeated analyst work, such as enrichment, summarising and containment, that these can take over.

**Searching the platform.** Guide 2.0 lists conducting searches in the platform, for example UDM searches and **stats searches**. A UDM search finds events matching field conditions; a stats search aggregates results (counts, distinct counts, grouping) so you can see patterns instead of rows. You will use both heavily in section 3.

**Judge and integrate intelligence.** Guide 2.0 also asks you to evaluate how effective surfaced IOCs and TTPs are (for example from GTI and SecOps) and to integrate only the GTI IOCs and TTPs that suit the use case. An indicator feed that matches nothing in your environment, or fires constantly on benign infrastructure, is noise; choose intelligence for the threats and technologies you actually face.

## 1.2 Configuring access for human and non-human identities

Access to security tools is itself a high-value target, so configure it with least privilege.

**Authentication.** Guide 2.0 names SCC, Google SecOps and the Model Context Protocol (MCP) as the tools to authenticate to. MCP is an open protocol that lets AI clients call tools, so an MCP connection to a security platform is another non-human path in, and it needs the same least-privilege identity as any API client. Humans sign in through your identity provider. **Workforce Identity Federation** lets your external identity provider authenticate employees, partners and contractors who then use single sign-on to reach Google Cloud; it works with any provider supporting OpenID Connect or SAML 2.0 (such as Microsoft Entra ID, AD FS and Okta), and because Google Cloud does not store the user accounts there is no need to synchronise identities with tools like Google Cloud Directory Sync. Access scope comes from allow policies and attributes received from the provider. Services authenticate with **service accounts**, preferably with short-lived credentials and attached service accounts rather than downloaded keys.

**Authorization for features and for data.** The guide separates two questions: may this principal use a feature (open the rule editor, run a playbook, change a parser) and may it see particular data (specific log types, a scope, a business unit)? Both are controlled through IAM roles and permissions, and SecOps additionally supports scoping access to data. Give analysts the narrowest role that lets them work, give detection engineers rule-editing rights without admin rights on ingestion, and separate who can change a parser from who can read sensitive logs.

**Audit logs.** Cloud Audit Logs have four types. Admin Activity logs record user-driven changes to configuration or metadata, are always written and cannot be disabled. System Event logs record configuration changes made by Google systems, and are always written. Policy Denied logs record access denials caused by security policy violations and are generated by default. **Data Access** logs record reads of configuration or metadata and the reading and writing of user-provided data; they are **off by default for all services except BigQuery** and may add log usage charges. A security operations team needs them enabled for sensitive services, because without them you cannot answer who read this data. Enable by setting audit configuration in the IAM policy:

```yaml
auditConfigs:
- service: allServices
  auditLogConfigs:
  - logType: ADMIN_READ
  - logType: DATA_READ
  - logType: DATA_WRITE
```

Apply this at the organization, folder or project level by editing the IAM policy (for example with `gcloud projects get-iam-policy` and `gcloud projects set-iam-policy`). Enabling everywhere is expensive, so enable by sensitivity, and analyse the audit logs for changes to the security tools themselves.

**API access for automation.** Playbooks and scripts call SecOps, SCC, GTI and MCP-connected tools using service accounts with narrowly scoped roles. Avoid API keys where an identity-bound credential works, restrict any key to the APIs and callers it needs, rotate it, and store it in a secret manager instead of in playbook text.

---

## Key terms

- **Google Security Operations** - Google's cloud service for retaining, searching and detecting over security telemetry, with SIEM and SOAR capabilities
- **Security Command Center** - Google Cloud's risk management platform that produces findings about vulnerabilities, misconfigurations and threats
- **Finding** - a record in Security Command Center of a threat or issue in an asset
- **Security Health Analytics** - the SCC service that detects misconfigurations and vulnerabilities in Google Cloud resources
- **Event Threat Detection** - the SCC Premium service that monitors logs in near-real time for threats and writes findings
- **Posture management** - defining a desired security posture and flagging drift from it
- **Google Threat Intelligence** - Google's source of threat intelligence on indicators, actors and campaigns, used for enrichment and detection; the third assessed platform in guide 2.0
- **Content Hub** - the Google SecOps source of prebuilt security content that you integrate and maintain
- **Stats search** - a SecOps search that aggregates results to show patterns instead of listing events
- **Model Context Protocol** - an open protocol through which AI clients call tools; a non-human access path to configure
- **Workforce Identity Federation** - federation that lets an external identity provider authenticate workforce users to Google Cloud without syncing accounts
- **Admin Activity audit log** - a Cloud Audit Log of user-driven configuration changes that is always written
- **Data Access audit log** - a Cloud Audit Log of reads and writes of data that is off by default except for BigQuery
- **Service account** - a non-human identity used by workloads and automations to call Google Cloud APIs

---

## Related

- [Notes 02: data management](./02-data-management.md)
- [Professional Cloud Security Engineer](../../cloud-security-engineer/) for IAM design depth
- **[📖 What is Google Security Operations?](https://docs.cloud.google.com/chronicle/docs/overview)** - platform capabilities
- **[📖 Security Command Center overview](https://docs.cloud.google.com/security-command-center/docs/security-command-center-overview)** - tiers, findings and services
- **[📖 Workforce Identity Federation](https://docs.cloud.google.com/iam/docs/workforce-identity-federation)** - external identity providers for workforce access
- **[📖 Cloud Audit Logs](https://docs.cloud.google.com/logging/docs/audit)** - log types and which are on by default
- **[📖 Exam guide 2.0 (PDF)](https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf)** - section 1 considerations
