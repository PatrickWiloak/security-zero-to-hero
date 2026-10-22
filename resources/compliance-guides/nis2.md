---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 15 min
---

# Compliance Guide - NIS2 Directive

## Overview

**NIS2** is the European Union's main cybersecurity law for organisations that society depends on: energy, transport, banking, health, water, digital infrastructure, cloud and managed service providers, public administration, manufacturing, food, chemicals, postal services and more. Its full name is **Directive (EU) 2022/2555** on measures for a high common level of cybersecurity across the Union. It replaced the first NIS Directive (2016/1148), which covered far fewer sectors and was applied very unevenly across member states.

Key dates:

| Date | What happened |
|------|---------------|
| 27 December 2022 | Published in the Official Journal |
| 16 January 2023 | Entered into force |
| 17 October 2024 | Deadline for member states to transpose it into national law |
| 17 October 2024 | Commission Implementing Regulation (EU) 2024/2690 adopted: detailed technical measures for digital infrastructure and digital service providers |
| 18 October 2024 | National measures apply; NIS1 repealed |
| 17 April 2025 | Deadline for member states to establish their lists of essential and important entities |
| 20 January 2026 | Commission proposed targeted amendments to NIS2 alongside a revised Cybersecurity Act (simplification, ransomware reporting, jurisdiction). **A proposal, not yet law at the time of writing** - check its status before relying on it |

Because NIS2 is a **directive**, it does not apply directly. Each member state writes it into its own law, so the exact obligations, registration process, authority and fines depend on the country. Many member states missed the October 2024 deadline and the Commission opened infringement procedures; most had transposed by 2026 but not all **[unconfirmed from an official source at the time of writing - check the Commission's NIS2 page for current transposition status]**. Always read the national law of each country you operate in.

The key ideas that separate NIS2 from its predecessor: **far wider scope** decided mostly by sector and size rather than government designation, **management accountability** (boards must approve and oversee cyber risk measures and can be held liable), **strict incident reporting deadlines**, and **supply chain security** as an explicit duty.

---

## NIS2 at a glance

```mermaid
flowchart LR
  scope[Am I in scope?<br/>sector in Annex I or II<br/>plus size threshold]
  class[Essential or<br/>important entity?]
  reg[Register with the<br/>national authority]
  gov[Management body approves<br/>and oversees measures,<br/>takes training]
  meas[Implement Article 21<br/>risk-management measures]
  rep[Report significant incidents:<br/>24h early warning,<br/>72h notification, 1 month final]
  sup[Supervision: proactive for essential,<br/>reactive for important]

  scope --> class --> reg --> gov --> meas --> rep
  meas --> sup
  rep --> sup
```

The NIS2 journey: work out whether and how you are in scope, register, put management in charge, implement the Article 21 measures, report incidents on deadline, and expect supervision matched to your category.

---

## Who is in scope

### Sectors

| Annex I: sectors of high criticality | Annex II: other critical sectors |
|--------------------------------------|----------------------------------|
| Energy (electricity, district heating and cooling, oil, gas, hydrogen) | Postal and courier services |
| Transport (air, rail, water, road) | Waste management |
| Banking | Manufacture, production and distribution of chemicals |
| Financial market infrastructures | Production, processing and distribution of food |
| Health (including some medical and pharmaceutical manufacturers) | Manufacturing (medical devices, computers and electronics, electrical equipment, machinery, motor vehicles, other transport equipment) |
| Drinking water and waste water | Digital providers (online marketplaces, search engines, social networking platforms) |
| Digital infrastructure (internet exchange points, DNS, TLD registries, cloud computing, data centres, content delivery networks, trust services, public electronic communications) | Research organisations |
| ICT service management, business to business (managed service providers and managed security service providers) | |
| Public administration (central and regional government) | |
| Space | |

### Size

As a rule, NIS2 applies to **medium and large** organisations in these sectors. Under the EU definition, a medium enterprise has **50 or more employees, or more than EUR 10 million annual turnover and balance sheet total**. Small and micro organisations are out of scope **unless** a specific rule pulls them in: for example, DNS service providers, TLD name registries and qualified trust service providers are covered regardless of size, and member states can designate smaller entities that are the sole provider of a critical service.

### Essential vs important

| | Essential entities | Important entities |
|---|---|---|
| Who | Mostly **large** organisations in Annex I sectors, plus some entities regardless of size (for example qualified trust service providers, TLD registries, DNS providers) and those designated by member states | **Medium** organisations in Annex I sectors, and medium or large ones in Annex II sectors |
| Obligations | The same Article 21 measures and Article 23 reporting | The same Article 21 measures and Article 23 reporting |
| Supervision | **Ex ante and ex post**: proactive audits, inspections and security scans at any time | **Ex post**: action after evidence or an indication of non-compliance |
| Maximum fines (Article 34) | At least **EUR 10 million or 2%** of total worldwide annual turnover, whichever is higher | At least **EUR 7 million or 1.4%** of total worldwide annual turnover, whichever is higher |

"At least" matters: the directive sets the minimum ceiling member states must allow; national law can go higher.

### Relationship with DORA

For financial entities covered by [DORA](./dora.md), DORA is **lex specialis**: its ICT risk management, incident reporting and testing rules apply instead of the equivalent NIS2 rules. Banks and financial market infrastructures still appear in NIS2's Annex I, but in practice they comply with DORA for these topics.

---

## The obligations

### Article 20: governance

- The **management body** (the board or equivalent) must **approve** the cybersecurity risk-management measures and **oversee** their implementation.
- Management can be **held liable** for infringements, under national law.
- Members of the management body must **follow training**, and entities are encouraged to offer similar training to employees regularly.

This is the clause that moved cybersecurity onto board agendas across Europe. "IT handles that" is no longer a defensible answer.

### Article 21: cybersecurity risk-management measures

Measures must be **appropriate and proportionate**, take an **all-hazards approach** (not just cyber attacks: also fire, power loss, physical threats) and cover at least these ten areas:

| Article 21(2) | Measure | In practice |
|---|---|---|
| (a) | Policies on risk analysis and information system security | A documented risk assessment and security policy; see [Risk management basics](../../learn/concepts/risk-management-basics.md) |
| (b) | Incident handling | Detection, response and reporting process; see [Incident response basics](../../learn/concepts/incident-response-basics.md) |
| (c) | Business continuity: backup management, disaster recovery, crisis management | Tested backups and recovery; see [Backup and ransomware resilience](../../learn/concepts/backup-and-ransomware-resilience.md) |
| (d) | Supply chain security, including security aspects of relationships with direct suppliers and service providers | Supplier inventory, risk tiering, contract clauses, assessments |
| (e) | Security in acquisition, development and maintenance of systems, including vulnerability handling and disclosure | Secure SDLC, [vulnerability management](../../learn/concepts/vulnerability-management.md), a vulnerability disclosure policy |
| (f) | Policies and procedures to assess the effectiveness of the measures | Internal audits, metrics, testing |
| (g) | Basic cyber hygiene practices and cybersecurity training | Patching, secure configuration, awareness training |
| (h) | Policies and procedures on cryptography and, where appropriate, encryption | Encryption standards and key management; see [Encryption explained](../../learn/concepts/encryption-explained.md) |
| (i) | Human resources security, access control policies and asset management | Joiner-mover-leaver process, least privilege, asset inventory |
| (j) | Multi-factor or continuous authentication, secured voice, video and text communications, and secured emergency communications where appropriate | [MFA](../../learn/concepts/mfa-and-passkeys.md) everywhere it matters, secure out-of-band channels for crises |

For digital infrastructure and digital service providers (DNS, TLD, cloud, data centres, CDNs, managed and managed security service providers, online marketplaces, search engines, social networks, trust services), **Implementing Regulation (EU) 2024/2690** spells out the technical and methodological requirements in detail and defines when an incident counts as significant. Because it is a regulation, it applies directly and identically in every member state.

### Article 23: incident reporting

A **significant incident** is one that has caused or can cause severe operational disruption or financial loss to the entity, or considerable damage to other people or organisations. For each one, report to the national CSIRT or competent authority:

| Deadline (from becoming aware) | Report | Contents |
|---|---|---|
| **24 hours** | Early warning | Whether it is suspected to be caused by unlawful or malicious acts, and whether it could have cross-border impact |
| **72 hours** | Incident notification | Update of the early warning, initial assessment of severity and impact, indicators of compromise where available |
| On request | Intermediate report | Status updates |
| **One month** after the incident notification | Final report | Detailed description, root cause or threat type, mitigation applied, cross-border impact (a progress report if the incident is still ongoing) |

Entities must also inform **recipients of their services** of significant incidents likely to affect them, and of measures they can take in response to significant cyber threats.

These deadlines run in parallel with others: a personal-data breach also triggers [GDPR](./gdpr.md)'s 72-hour notification to the data protection authority. Plan one process that feeds every report.

### Registration

Entities generally must register with their national authority, providing name, address, sector, contact details and the member states where they provide services. Certain digital providers register in the member state of their **main establishment**, and ENISA keeps a registry of them. Check the national process: in several countries registration is how the authority learns you exist.

---

## Cloud Provider NIS2 Support

The large cloud providers are themselves in scope (cloud computing and data centre services are Annex I digital infrastructure), and each publishes material on how its services help customers meet Article 21. Using them does not make you compliant; as always, how you configure and use them is yours.

### AWS

| Article 21 area | AWS service |
|-----------------|-------------|
| (a) Risk analysis, (f) effectiveness | AWS Security Hub, AWS Config conformance packs, AWS Audit Manager |
| (b) Incident handling | Amazon GuardDuty, Amazon Detective, AWS Security Incident Response |
| (c) Business continuity | AWS Backup (with Vault Lock), AWS Elastic Disaster Recovery, multi-AZ and multi-region designs |
| (e) Vulnerability handling | Amazon Inspector, AWS Systems Manager Patch Manager |
| (h) Cryptography | AWS KMS, AWS CloudHSM, AWS Certificate Manager |
| (i) Access control, (j) MFA | IAM Identity Center, IAM, MFA and passkey enforcement |

### Azure

| Article 21 area | Azure service |
|-----------------|---------------|
| (a) Risk analysis, (f) effectiveness | Microsoft Defender for Cloud regulatory compliance, Microsoft Purview Compliance Manager |
| (b) Incident handling | Microsoft Sentinel, Microsoft Defender XDR |
| (c) Business continuity | Azure Backup (immutable vaults), Azure Site Recovery |
| (e) Vulnerability handling | Defender for Cloud vulnerability assessment, Azure Update Manager |
| (h) Cryptography | Azure Key Vault, Managed HSM |
| (i) Access control, (j) MFA | Microsoft Entra ID, Conditional Access, Privileged Identity Management |

### Google Cloud

| Article 21 area | GCP service |
|-----------------|-------------|
| (a) Risk analysis, (f) effectiveness | Security Command Center compliance monitoring, Assured Workloads |
| (b) Incident handling | Google Security Operations, Security Command Center threat detection |
| (c) Business continuity | Backup and DR Service, multi-region storage and databases |
| (e) Vulnerability handling | Artifact Analysis, VM Manager patch management |
| (h) Cryptography | Cloud KMS, Cloud HSM, Cloud External Key Manager |
| (i) Access control, (j) MFA | Cloud IAM, Cloud Identity with 2-step verification enforcement, Privileged Access Manager |

---

## NIS2 vs other frameworks

| Aspect | NIS2 | ISO 27001 | DORA |
|--------|------|-----------|------|
| Type | EU directive (national law) | Voluntary international standard | EU regulation (directly applicable) |
| Who | Medium and large entities in 18 sectors | Anyone who chooses to certify | EU financial entities and their critical ICT providers |
| Proof | Supervision by national authority; no certificate | Certificate after an accredited audit | Supervision by financial regulators |
| Incident reporting | 24h / 72h / 1 month | Not mandated | Major ICT incidents: 4h after classification (24h max) / 72h / 1 month |
| Management duty | Explicit approval, oversight, training, liability | Leadership clause 5 | Management body bears ultimate responsibility |

An [ISO 27001](./iso-27001.md) ISMS covers most of Article 21 and is the most common way organisations organise their NIS2 programme, but a certificate is not proof of NIS2 compliance: reporting deadlines, registration and management liability are legal obligations ISO does not test. The [NIST CSF 2.0](./nist-csf.md) is a useful outside-the-EU mapping target.

---

## Preparation Checklist

### Scoping

- [ ] Determine, for each EU country you operate in, whether you are in an Annex I or II sector and over the size threshold
- [ ] Decide essential vs important, and check whether any size-independent rule or national designation applies
- [ ] Register with each relevant national authority
- [ ] Identify whether Implementing Regulation (EU) 2024/2690 applies (digital infrastructure and digital providers)

### Governance

- [ ] Management body formally approves the risk-management measures (minutes as evidence)
- [ ] Management body training completed and recorded
- [ ] Named accountable owners for each Article 21 area

### Measures

- [ ] Risk assessment covering all hazards, reviewed at least annually
- [ ] Incident response plan with the 24h / 72h / 1-month reporting steps and the authority's contact route
- [ ] Tested backups and disaster recovery
- [ ] Supplier inventory with risk tiers, contract security clauses and assessments of critical suppliers
- [ ] Vulnerability management and a coordinated vulnerability disclosure policy
- [ ] Cyber hygiene baseline and staff awareness training
- [ ] Cryptography policy
- [ ] Access control, joiner-mover-leaver process and asset inventory
- [ ] MFA for remote access, administrators and critical systems; secured emergency communications

### Evidence Collection

| Evidence type | Source | Automation |
|--------------|--------|------------|
| Board approval and training | Board minutes, training records | LMS exports |
| Risk assessment | Risk register | GRC tool |
| Incident reporting readiness | IR plan, exercise reports, report templates | Ticketing workflow with deadline timers |
| Backup and recovery | Restore test results | Scheduled restore jobs |
| Supply chain | Supplier register, assessments, contracts | Vendor risk platform |
| Vulnerability handling | Scan reports, patch SLAs, disclosure policy | Scanner dashboards |
| Access control and MFA | IdP reports, access reviews | IdP policies and access review tooling |

### Common gaps

- Management approval treated as a one-off signature, not ongoing oversight.
- No rehearsed way to produce a 24-hour early warning on a weekend.
- Supplier risk limited to a questionnaire at onboarding, never reassessed.
- Scoping done for the head office country only, missing subsidiaries elsewhere in the EU.
- MFA in place for staff but not for service providers with remote access.

---

## Certification Exam Relevance

NIS2 knowledge is relevant for:
- [ISACA CISM](../../exams/isaca/cism/) and [CISA](../../exams/isaca/cisa/) - governance, legal and regulatory requirements, management accountability
- [ISC2 CISSP](../../exams/isc2/cissp/) and [CCSP](../../exams/isc2/ccsp/) - legal and regulatory compliance, including EU regulation
- [CCSK v5](../../exams/cloud-security-alliance/ccsk/) - cloud compliance and jurisdiction
- [Microsoft SC-100](../../exams/azure/sc-100/) - regulatory compliance in a security strategy

Expect concepts (who is covered, management accountability, reporting deadlines) rather than article numbers.

---

## Documentation Links

**[📖 Directive (EU) 2022/2555 (NIS2) on EUR-Lex](https://eur-lex.europa.eu/eli/dir/2022/2555/oj/eng)** - the official text

**[📖 European Commission: NIS2 Directive](https://digital-strategy.ec.europa.eu/en/policies/nis2-directive)** - policy page, implementing acts and transposition updates

**[📖 Commission Implementing Regulation (EU) 2024/2690](https://eur-lex.europa.eu/eli/reg_impl/2024/2690/oj/eng)** - technical and methodological requirements for digital infrastructure and digital providers

**[📖 ENISA: NIS2 Technical Implementation Guidance](https://www.enisa.europa.eu/publications/nis2-technical-implementation-guidance)** - ENISA guidance on implementing the measures in Implementing Regulation (EU) 2024/2690
