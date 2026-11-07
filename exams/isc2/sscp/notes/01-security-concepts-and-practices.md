---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 15 min
---

# 01 - Security concepts and practices

**Domain 1: Security Concepts and Practices (16%)** - outline effective October 1, 2025. Objectives 1.1 to 1.8.

This domain is the vocabulary and the habits of the job. The ideas are simple; the exam tests whether you can apply them to a situation without confusing neighbouring terms.

---

## 1.1 Codes of ethics

You are held to two codes: the ISC2 Code of Ethics and your employer's. When they conflict on a question, the exam's answer is almost always to protect society and the public first, act honourably and legally, serve your principals diligently, and advance the profession, in that order of priority. In practice this means you report a discovered crime or a safety problem through proper channels rather than quietly ignoring it, and you do not use access you were given for one purpose to satisfy curiosity.

## 1.2 Security concepts

**Confidentiality, integrity and availability** are the three goals. Confidentiality keeps data from people who should not see it, integrity keeps it from unauthorised or accidental change, and availability keeps it usable when needed. Every control exists to serve at least one of them, and every incident is a failure of at least one.

Around the triad sit the supporting ideas:

- **Accountability** means every action traces to one identity. Shared accounts destroy it.
- **Non-repudiation** means a person cannot credibly deny an action. A digital signature gives it; a plain hash or an encrypted file does not, because someone else could have produced those.
- **Least privilege** gives each identity only what its job needs, and **need to know** applies the same idea to information.
- **Separation of duties** splits a sensitive task between people so that one person cannot complete fraud alone. **Job rotation** and mandatory vacation help expose frauds that separation missed.
- **Defense in depth** layers controls so that failure of one does not expose the asset.
- **Fail secure** versus **fail open**: when a control breaks, does it block (secure) or allow (open)? A door to a vault fails secure; a fire exit fails open for safety. Life safety wins over confidentiality.

## 1.3 Technical, physical and administrative controls

Controls are classified two ways, and the exam asks for either.

By **type** (what the control is made of): technical (firewall, encryption), physical (lock, badge reader, camera) and administrative (policy, training, background check).

By **function** (what it does for you): preventive, detective, corrective, deterrent and compensating. Section 1.4 covers these.

Controls are only worth something if they work and are used. **Compliance assessment** checks that controls match the policy and the standard they are meant to meet. **Periodic audits** do it on a schedule, internally or by an outside party, and the audit trail from your logs is the evidence. As a practitioner you will mostly collect evidence and fix findings; the audit opinion belongs to the auditor.

## 1.4 Documenting and maintaining controls by type

Know the five functions precisely.

| Function | Job | Example |
|---|---|---|
| Deterrent | Discourage an attempt | Warning sign, visible camera |
| Preventive | Stop it happening | Firewall rule, door lock, MFA |
| Detective | Notice it happened | IDS alert, log review, CCTV recording |
| Corrective | Limit damage and restore | Restore from backup, patch, isolate host |
| Compensating | Stand in when the intended control is not feasible | Extra monitoring on a legacy system that cannot be patched |

A single control can serve more than one function (a camera deters and detects). Compensating controls must be documented together with the reason the primary control could not be used, because auditors will ask.

Maintaining controls means each has an owner, a documented configuration, a test schedule and a record of exceptions. A control that nobody tests is an assumption.

## 1.5 Asset life cycle

Assets, whether hardware, software or data, pass through planning, acquisition, deployment, operation and maintenance, and disposal. Security work belongs at each step. You cannot protect what you have not inventoried, so the **asset inventory** comes first, with an owner and a classification for each item.

At the end of life, disposal is a security event. **Media sanitization** makes the data on retired media infeasible to recover at a level of effort matched to how sensitive it is. NIST's media sanitization guidance describes this as a decision driven by the confidentiality of the information, and the current edition is SP 800-88 Rev. 2, which superseded Rev. 1 in September 2025. Choose the method by data sensitivity and by whether the media will be reused: overwriting suits reusable magnetic media, cryptographic erase suits encrypted devices where you can destroy the key, and physical destruction suits media that is failing or holds the most sensitive data. Record the sanitization for each asset.

Software assets have the same end-of-life problem: an unsupported operating system gets no patches, so retire it or wrap it in compensating controls.

## 1.6 Change and configuration management

**Configuration management** keeps a known-good baseline for each system class and records every deviation. **Change management** is the approval process that moves systems from one baseline to the next without surprises.

A well-formed change has a request, a **security impact analysis** (does this open a port, add a trust, remove a log?), approval by the right people, a test, a rollback plan and a record. Emergency changes still get recorded, after the fact if need be. The exam favours answers where the change is tested before production and where unauthorised changes are detected by comparing against the baseline.

Patching is change management applied at volume. NIST SP 800-40 Rev. 4 frames it as preventive maintenance and a continuous cycle of finding, ranking, obtaining, deploying and confirming fixes, rather than a one-off project.

## 1.7 Security awareness and training

People are both the biggest risk and a sensor network. Awareness training is general (spot phishing, protect passwords, report quickly) and training is role-specific (administrators learn secure configuration). Good programmes measure outcomes: phishing simulation click and report rates, time to report, and repeat offenders. **Tabletop exercises** walk decision makers through a scenario on paper, testing the plan and the people without touching systems. Reporting must be easy and blame-free, or people hide mistakes.

## 1.8 Collaboration with physical security

Logical security fails if someone can walk out with the server. Practitioners work with facilities on badge and visitor management, escorts, secured rooms, cable and rack locks, device controls such as USB port blocking, and clean-desk and media storage rules. **Tailgating** (following someone through a door) is the classic gap; **mantraps** and attentive staff close it. Camera footage and badge logs are also evidence, so retention and time synchronisation matter.

---

## Key terms

- **Non-repudiation** - assurance that a person cannot credibly deny having performed an action, typically provided by a digital signature
- **Least privilege** - giving an identity only the access its job requires
- **Separation of duties** - splitting a sensitive task between people so one person cannot complete abuse alone
- **Defense in depth** - layering controls so that the failure of one does not expose the asset
- **Deterrent control** - a control that discourages an attempt without physically stopping it
- **Compensating control** - an alternative control used when the intended control is not feasible
- **Corrective control** - a control that limits damage and restores normal operation after an event
- **Configuration baseline** - the approved, known-good configuration against which a system is compared
- **Security impact analysis** - the review of what a proposed change does to the security of a system
- **Media sanitization** - making access to data on storage media infeasible at a level of effort matched to its sensitivity
- **Tailgating** - following an authorised person through a controlled door without presenting credentials
- **Tabletop exercise** - a discussion-based walk-through of a scenario to test plans and decision makers

---

## Related

- [Notes 02: access controls](./02-access-controls.md)
- [Scenarios](../scenarios.md)
- **[📖 NIST SP 800-88 Rev. 1: Guidelines for Media Sanitization](https://csrc.nist.gov/pubs/sp/800/88/r1/final)** - the record page notes Rev. 1 was withdrawn on September 26, 2025 and superseded by Rev. 2
- **[📖 NIST SP 800-40 Rev. 4: Guide to Enterprise Patch Management Planning](https://csrc.nist.gov/pubs/sp/800/40/r4/final)** - patching as preventive maintenance and a continuous cycle
