---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 14 min
---

# 04 - Incident response and recovery

**Domain 4: Incident Response and Recovery (14%)** - objectives 4.1 to 4.3.

When prevention fails, this domain decides how much it costs. The theme is preparation: a team that has rehearsed makes calm decisions; a team improvising makes expensive ones.

---

## 4.1 The incident response life cycle

An **event** is any observable occurrence; an **incident** is an event that actually or potentially harms confidentiality, integrity or availability, or violates policy. Most events are not incidents, and triage decides which are.

The classic life cycle, and the one ISC2 questions follow, runs: **preparation, detection and analysis, containment, eradication, recovery, and post-incident activity** (lessons learned). NIST SP 800-61 Rev. 3 (April 2025) restates incident response as part of cybersecurity risk management using the Cybersecurity Framework 2.0, aiming to help organisations prepare for incidents and improve detection, response and recovery. It supersedes Rev. 2, the source of the classic four-phase model; the phases above remain the working vocabulary.

```mermaid
flowchart LR
    P[Preparation] --> D[Detection and analysis]
    D --> C[Containment]
    C --> E[Eradication]
    E --> R[Recovery]
    R --> L[Post-incident activity]
    L --> P
```

The diagram shows the loop: lessons learned feed back into preparation.

- **Preparation**: the plan, the team with named roles, contact lists, tools, training and exercises. Authority to act (for example, to isolate a server) must be decided in advance.
- **Detection and analysis**: confirm that it is an incident, scope it, classify severity and start a timeline. Document everything with times.
- **Containment**: stop the spread. Short-term actions isolate (pull the host off the network, disable the account); long-term actions hold until a clean rebuild. Weigh the cost: pulling a live system loses volatile evidence and may take down a business service, so decide with the business owner.
- **Eradication**: remove the cause, such as malware, backdoors and the vulnerability used. Rebuilding from a known-good image is often safer than cleaning.
- **Recovery**: restore service, verify it is clean, and monitor closely for reinfection.
- **Post-incident activity**: a blameless review within days, with actions tracked to completion. This is where the incident repays its cost.

Order matters on the exam. If the question asks for the first step after confirming a compromise, it is usually containment; before it, you analyse enough to know what you are containing. Communication follows the plan: the incident commander controls internal and external messages, and legal counsel decides on notifications.

## 4.2 Forensic investigations

Forensics preserves and interprets evidence so it can stand up in a disciplinary or legal process. NIST SP 800-86 presents forensics from an IT perspective, with data sources including files, operating systems, network traffic and applications, and notes that it is not legal advice; involve counsel before acting.

The principles:

- **Order of volatility**: collect the most perishable evidence first. Memory and running processes, then network state, then disk, then logs and backups held elsewhere.
- **Chain of custody**: a written record of who held the evidence, when, and what they did with it. A broken chain makes evidence deniable.
- **Integrity**: work from forensic copies, and prove the copy matches the original with a cryptographic hash. Use write blockers when imaging disks so the original is never altered.
- **Legal hold** and preservation: once litigation is reasonably foreseeable, normal deletion must stop.
- **Reporting** is factual, repeatable and separates what was observed from what is concluded.

Types of investigation differ in standard of proof and authority: administrative, civil, criminal and regulatory. A practitioner's job is to preserve and support, then hand over to those authorised to lead.

## 4.3 Business continuity and disaster recovery

**Business continuity (BC)** keeps essential functions running through disruption. **Disaster recovery (DR)** restores IT after a major outage and is a subset of continuity. Planning starts with a **business impact analysis (BIA)** that identifies critical functions, their dependencies and what an outage costs over time. NIST SP 800-34 Rev. 1 is the contingency planning guide, and supplies a BIA template.

The BIA produces the numbers that drive design:

- **Maximum tolerable downtime (MTD)**: the longest the business can survive without the function.
- **Recovery time objective (RTO)**: the target time to restore service; it must be shorter than the MTD.
- **Recovery point objective (RPO)**: how much data loss, measured in time, is acceptable; it sets the backup frequency.

**Alternate processing sites**: a **hot site** is ready to run within minutes or hours at the highest cost; a **warm site** has hardware and connectivity but needs data restored; a **cold site** is just space and power. Cloud regions now often replace all three. **Backups** follow full, differential and incremental patterns: full copies everything, differential copies changes since the last full, and incremental copies changes since the last backup of any kind (the fastest to take, the slowest to restore). Keep copies offline or immutable so ransomware cannot encrypt them, store one off-site, and **test restores**, because an untested backup is a hope.

Testing escalates: read-through, tabletop, walk-through, simulation or parallel, and full interruption. Each test should produce updated plans. Emergency response puts **life safety first**, always, ahead of data or equipment.

---

## Key terms

- **Incident** - an event that actually or potentially harms confidentiality, integrity or availability, or violates policy
- **Containment** - actions that stop an incident spreading while preserving evidence and the ability to investigate
- **Eradication** - removing the cause of an incident, such as malware, backdoors and the exploited weakness
- **Order of volatility** - the rule to collect the most perishable evidence, such as memory, before more durable sources
- **Chain of custody** - the written record of who handled evidence, when, and what they did
- **Write blocker** - a device or software that prevents any change to a disk while it is being imaged
- **Business impact analysis** - the study of critical functions, their dependencies and the cost of their outage over time
- **Maximum tolerable downtime** - the longest a business function can be unavailable before survival is threatened
- **Recovery time objective** - the target time within which a service must be restored
- **Recovery point objective** - the maximum acceptable data loss, measured in time
- **Hot site** - an alternate site ready to take over within minutes or hours
- **Differential backup** - a backup of everything changed since the last full backup

---

## Related

- [Notes 03: risk, monitoring and analysis](./03-risk-identification-monitoring-and-analysis.md)
- [Cloud incident response tabletop](../../../../resources/hands-on-projects/cloud-incident-response-tabletop.md) - a worked exercise
- **[📖 NIST SP 800-61 Rev. 3: Incident Response Recommendations and Considerations](https://csrc.nist.gov/pubs/sp/800/61/r3/final)** - incident response within CSF 2.0 (April 2025)
- **[📖 NIST SP 800-86: Guide to Integrating Forensic Techniques into Incident Response](https://csrc.nist.gov/pubs/sp/800/86/final)** - forensics from an IT perspective
- **[📖 NIST SP 800-34 Rev. 1: Contingency Planning Guide](https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final)** - contingency planning and a BIA template
