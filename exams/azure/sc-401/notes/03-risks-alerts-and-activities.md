---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 12 min
---

# 03 - Risks, alerts, and activities

**Domain 3: Manage risks, alerts, and activities (30-35%)**

Detecting risky behavior, responding to alerts, proving what happened, and protecting data used by AI services.

---

## Insider Risk Management

Detects patterns of user behavior over time rather than single events.

**Policy templates** include data theft by departing users, data leaks, data leaks by priority users, security policy violations, patient data misuse, risky browser usage, and forensic evidence.

**Structure**:
- **Triggering event** starts the detection window. Commonly a termination date from the **HR connector**, a DLP policy match, or a security alert.
- **Indicators** are the signals scored: SharePoint downloads, USB copies, uploads to personal cloud, printing, renaming to obscure extensions, email to external recipients.
- **Sequence detection** identifies patterns such as download then rename then exfiltrate, which scores higher than any single event.
- **Risk score** accumulates, producing alerts, which analysts triage into **cases** with actions including notice, escalation for investigation, and escalation to eDiscovery.

**Privacy controls**: username anonymization by default, role-based access separating analysts from investigators, and configurable exclusions. These matter in works council and GDPR contexts and are directly testable.

---

## Communication Compliance

> Communication Compliance and Information Barriers are no longer named in the SC-401 skills measured (checked 2026-10-22). They stay here because they sit next to insider risk in the Purview portal and can still appear as distractors, but give them less time than the named skills.

Reviews message content in Exchange, Teams, Viva Engage, and connected third-party sources against policy: offensive language, sensitive information, regulatory compliance, and conflict of interest.

Structure: policy with conditions, a reviewer group, and a remediation workflow (resolve, notify the user, escalate, tag as a false positive). Supports sampling percentages and pre-trained classifiers.

It **reviews**; it does not prevent. Requirements to prevent communication point at Information Barriers.

---

## Information Barriers

Prevents communication and discovery between defined groups.

- **Segments** defined by an Entra attribute such as department or job title
- **Policies** between segments in **block** mode (these two cannot communicate) or **allow** mode (this segment may communicate only with those listed)
- Enforcement spans Teams, SharePoint, and OneDrive
- Users cannot search for, message, call, or share with blocked segments

Common in financial services (banking and trading separation) and legal (matter conflict walls).

---

## Purview Audit

| | Standard | Premium |
|---|---|---|
| Retention | 180 days by default | Longer, with configurable audit retention policies up to 10 years |
| High-value events | Not included | MailItemsAccessed, Send, SearchQueryInitiated |
| Bandwidth | Standard | Higher API throughput |

**Audit retention policies** let you keep specific record types longer than the default, scoped by workload, record type, or user.

Audit answers "who did what, when". It is the evidence layer for investigations, and increasingly for AI interactions, since Copilot prompts and responses are auditable events.

---

## eDiscovery

- **Content search** finds content across Microsoft 365 without a case structure. No hold, no export workflow beyond basics.
- **eDiscovery (Standard)** adds cases, legal holds that preserve content in place, search, and export.
- **eDiscovery (Premium)** adds custodian management, legal hold notifications, review sets, analytics such as near-duplicate detection and email threading, and predictive coding.

A hold **preserves**; it does not restrict access or classify. Deleted content covered by a hold moves to preservation storage rather than being removed.

---

## Responding to alerts across portals

The outline lists alert response in several places, and the question is usually "where do I look?" DLP alerts are triaged in the **Microsoft Purview portal** (the DLP alerts page), and Purview alerts also flow into **Microsoft Defender XDR** incidents, where a SOC analyst sees them next to endpoint and identity alerts. **Defender for Cloud Apps file policy alerts** are handled in the Defender portal. **Activity explorer** shows what happened to labeled and classified content over time (labels applied, changed, or removed, DLP matches, files copied to USB), which makes it the first stop for "how has this sensitive content been used?" Purview Audit is the deeper, per-event record behind it.

---

## Protect data used by AI services

The audience profile now says the administrator protects "data used by AI services", and the outline gives it its own section. The starting point is a principle that runs through all of Purview: Microsoft 365 Copilot and other AI assistants answer using the permissions of the person asking. AI does not create new access, but it makes over-broad access far easier to exploit, because a user can ask for "every salary file I can see" instead of hunting for it.

**Data Security Posture Management (DSPM) for AI** is the Purview hub for this. It reports which AI apps are in use, what sensitive data appears in prompts and responses, and which users are behaving riskily with AI. Its prerequisites are the things the reports are built from: Purview Audit must be on, and to see activity on third-party AI sites, devices must be onboarded to Purview and running the Purview browser extension. Without those, the dashboards are empty rather than reassuring.

Access to DSPM for AI is split by role, and the split matters: seeing summary reports is one permission, while seeing the actual text of prompts and responses is a more sensitive one that should go to few people. DSPM for AI also offers ready-made policies (DLP, insider risk, and communication monitoring for AI interactions) that you create from its recommendations and then tune like any other policy.

The controls themselves come from the rest of this exam. Sensitivity labels with encryption stop Copilot summarizing content the user cannot open. DLP policies for the Microsoft 365 Copilot location stop labeled content being processed at all. Oversharing assessments and SharePoint access reviews fix the permissions that AI would otherwise expose. A good exam answer to "prepare for a Copilot rollout" combines visibility (DSPM for AI), a permissions clean-up, and labels plus DLP, in that order.

**[📖 DSPM for AI](https://learn.microsoft.com/en-us/purview/dspm-for-ai)** - reports, prerequisites, and one-click policies
**[📖 Purview data security and compliance protections for generative AI apps](https://learn.microsoft.com/en-us/purview/ai-microsoft-purview)** - which Purview controls apply to Copilot and other AI apps

---

## Key terms

- **Insider Risk Management** - Purview solution scoring user behavior over time to detect data theft, leaks, and policy violations
- **Triggering event** - the event, often an HR termination date, that opens an insider risk detection window for a user
- **Sequence detection** - insider risk capability identifying multi-step exfiltration patterns rather than isolated actions
- **Username anonymization** - insider risk privacy control hiding user identities from analysts until a case is escalated
- **Communication Compliance** - Purview solution reviewing message content against policy with a reviewer remediation workflow
- **Information Barriers** - Purview capability preventing communication and discovery between defined user segments
- **Segment** - an Information Barriers grouping of users defined by a directory attribute
- **Purview Audit Premium** - the audit tier adding longer retention, configurable retention policies, and high-value events such as MailItemsAccessed
- **Audit retention policy** - configuration keeping selected audit record types longer than the default period
- **eDiscovery hold** - a legal hold preserving content in place without restricting access or altering classification
- **Review set** - the eDiscovery Premium working collection where collected content is analyzed and reviewed

---

## Related

- [Notes 01: information protection](./01-information-protection.md)
- [Notes 02: data loss prevention and retention](./02-data-loss-prevention.md) - retention, records, and precedence
- [Scenarios](../scenarios.md) - scenarios 5, 7, and 8
- [Compliance guides](../../../../resources/compliance-guides/)
- [GDPR](../../../../resources/compliance-guides/gdpr.md)
