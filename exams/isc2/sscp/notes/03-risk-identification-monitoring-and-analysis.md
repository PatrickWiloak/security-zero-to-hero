---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 15 min
---

# 03 - Risk identification, monitoring and analysis

**Domain 3: Risk Identification, Monitoring and Analysis (15%)** - objectives 3.1 to 3.5.

Risk work decides what to protect and how much to spend. Monitoring work tells you whether the protections hold. This domain joins the two.

---

## 3.1 Risk management

**Risk** is the combination of how likely a threat is to exploit a vulnerability and how bad the impact would be. An **asset** has value, a **threat** is something that could cause harm, a **vulnerability** is the weakness, and a **control** reduces likelihood or impact. Lose track of which word is which and the questions turn into traps.

NIST SP 800-30 Rev. 1 is the standard guide to conducting risk assessments, and says they feed decisions made by leaders at every tier of the organisation. Assessments can be **qualitative** (high, medium, low) or **quantitative** (money). The quantitative formulas are worth knowing cold:

- **Single loss expectancy (SLE)** = asset value x exposure factor
- **Annualized rate of occurrence (ARO)** = how many times a year it is expected
- **Annualized loss expectancy (ALE)** = SLE x ARO

A control is worth buying if the ALE it removes is larger than its yearly cost. Example: a server worth 100,000 with a 40% exposure factor to a flood gives an SLE of 40,000; at a 0.1 yearly rate the ALE is 4,000, so a 10,000 a year flood control is poor value.

**Risk treatment** has four options: **mitigate** (apply controls), **transfer** (insure or contract it out), **avoid** (stop the activity) and **accept** (document and live with it). What remains afterwards is **residual risk**, and **risk tolerance** (or appetite) is the amount management will accept. Accepting risk is a management decision, never a practitioner's. Your job is to describe the risk clearly enough that the right person can decide.

Frameworks give structure: the NIST Risk Management Framework, ISO/IEC 27005, and the NIST Cybersecurity Framework for organising outcomes. Know that frameworks guide and standards are measured against; do not memorise their steps over understanding them.

## 3.2 Legal and regulatory concerns

Different laws apply by **jurisdiction**: where the data subject, the company and the data live. Practitioners need enough awareness to ask the right question, not to be lawyers. Know the families: privacy law (personal data rights and breach notification), sector rules (payment card data, health records, financial reporting) and contractual obligations. **Limitations** include the reach of law across borders, the duty to preserve evidence and the need to involve legal counsel before acting on anything touching personal data or an investigation. When the question mentions a legal duty, the answer involves legal or compliance staff early.

## 3.3 Security assessments and vulnerability management

An **assessment** looks for weakness; a **penetration test** goes further and tries to exploit it under agreed rules. A **vulnerability scan** is automated discovery; it finds candidates, not proof.

The vulnerability management cycle is: maintain an asset inventory, scan, **prioritise** (severity, exploitability, asset criticality and exposure), remediate or mitigate, verify and report. Prioritising by score alone misleads; a medium flaw on an internet-facing system holding sensitive data can outrank a critical flaw on an isolated test box. **Credentialed scans** log in and see far more than unauthenticated ones, with fewer false positives. Expect **false positives** (reported but not real) and **false negatives** (real but missed), and the latter are the more dangerous.

Scan only what you are authorised to scan, at agreed times, and handle the results as sensitive: a list of unpatched systems is a map for attackers. Patching follows change management (see [notes 01](./01-security-concepts-and-practices.md)).

## 3.4 Operating and monitoring security platforms

Monitoring needs sources, collection and analysis.

- **Source systems**: firewalls, servers, endpoints, authentication systems, cloud audit logs, applications, DNS and proxy logs.
- **Events of interest**: failed and unusual logins, privilege changes, new accounts, policy changes, log clearing, large outbound transfers, connections to bad destinations, and changes to critical files.
- **Log management**: NIST SP 800-92 describes building the infrastructure to collect and manage logs and running the processes around it. The practical rules are: send logs off the source system promptly so an intruder cannot erase them, synchronise clocks (time sync is what lets events from different systems be lined up), protect log integrity, and set retention to meet legal and investigative needs.
- **SIEM**: a security information and event management platform collects, normalises, correlates and alerts across sources. Its value is correlation: a failed login on one host is noise, a failed login followed by a success and a new admin account is a story. A SIEM is only as good as its sources and its tuning.

Tune alerts. Too many false alarms train analysts to ignore the console; too few means missed attacks. Run rules against a baseline of normal behaviour.

## 3.5 Analyzing monitoring results

**Baselines** define normal; an **anomaly** is a departure from it, though not necessarily an attack. Analysis moves from alert to triage (is this real, how bad, how widespread), to **event analysis** (what happened, in what order, with what accounts), to a decision to escalate. Visualisations such as dashboards and timelines help spot patterns across large volumes.

Report in language fit for the reader: operators get indicators and next steps, management gets impact, trend and decision needed. **Escalation** follows the defined path and thresholds; if you are unsure whether it is an incident, the safe action is to follow the escalation procedure and let the incident process decide. Keep what you collected unaltered, because it may become evidence (see [notes 04](./04-incident-response-and-recovery.md)).

---

## Key terms

- **Risk** - the combination of the likelihood of a threat exploiting a vulnerability and the impact if it does
- **Single loss expectancy** - the expected monetary loss from one occurrence, asset value times exposure factor
- **Annualized loss expectancy** - the expected yearly loss, single loss expectancy times annualized rate of occurrence
- **Residual risk** - the risk that remains after controls are applied
- **Risk tolerance** - the level of risk management is willing to accept
- **Risk transfer** - shifting the financial consequence of a risk to another party, such as through insurance
- **Credentialed scan** - a vulnerability scan that logs in to the target and sees configuration and patch state directly
- **False negative** - a real problem that a scanner or detector fails to report
- **SIEM** - a platform that collects, normalises, correlates and alerts on security events from many sources
- **Baseline** - a record of normal behaviour or configuration used to spot departures
- **Time synchronisation** - keeping system clocks aligned so events from different sources can be correlated
- **Escalation** - passing an event to a higher level of authority under defined thresholds

---

## Related

- [Notes 04: incident response and recovery](./04-incident-response-and-recovery.md)
- [Detection and response topic](../../../../topics/detection-and-response.md)
- **[📖 NIST SP 800-30 Rev. 1: Guide for Conducting Risk Assessments](https://csrc.nist.gov/pubs/sp/800/30/r1/final)** - risk assessment guidance for leaders at all tiers (September 2012)
- **[📖 NIST SP 800-92: Guide to Computer Security Log Management](https://csrc.nist.gov/pubs/sp/800/92/final)** - building log infrastructure and running log management processes
