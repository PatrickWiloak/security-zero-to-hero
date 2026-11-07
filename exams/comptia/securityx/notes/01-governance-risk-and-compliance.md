---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 16 min
---

# 01 - Governance, risk, and compliance

**Domain 1: Governance, Risk, and Compliance (20%)** - CAS-005. Sections follow the order of CompTIA's published objectives summary.

At this level the exam wants you to connect technical choices to business reasons. A control is justified by a risk, a risk is defined against an asset and its impact, and the whole thing is organised by a framework and documented in a policy. Know each link in that chain.

---

## Security program documentation

Documents form a hierarchy, from broad to specific:

- **Policies** state management intent in general terms ("data must be classified and protected"). They are mandatory and approved at the top.
- **Standards** set mandatory, measurable requirements ("AES-256 for data at rest").
- **Procedures** give the step-by-step method ("how to rotate a key").
- **Guidelines** are recommended practice and are not enforced.

Exceptions need a documented process with an owner, a reason, a compensating control and an expiry date. A permanent exception is a policy change in disguise.

## Program management

A security program needs ownership and rhythm. **Training** covers phishing, security and privacy awareness, and measures behaviour (simulation reporting rates) rather than attendance. **Communication** gives each audience what it needs: technical staff get indicators, executives get risk and decisions. **Reporting** uses metrics tied to risk: mean time to detect and remediate, patch latency on critical assets, percentage of assets with an owner. A **RACI matrix** assigns Responsible, Accountable, Consulted and Informed roles for each activity; exactly one party is accountable. Use it to remove the usual failure mode where everybody assumes somebody else owns a task.

## Frameworks

Frameworks give a common language and a baseline. **COBIT** is an IT governance framework that links IT goals to business goals. **ITIL** is an IT service management framework covering change, incident and configuration processes that security depends on. For security control selection and risk, common references are the NIST Cybersecurity Framework (CSF), NIST SP 800-53 controls and the NIST Risk Management Framework. NIST SP 800-37 Rev. 2 describes the RMF as a structured, flexible process for managing security and privacy risk across the system life cycle, with steps that categorize information, select, implement and assess controls, authorize systems and monitor continuously. A framework is chosen for fit with the business (sector, geography, customers), not because it is popular, and is then tailored.

## Configuration management

Know what you own. The **asset life cycle** runs from planning and acquisition through deployment and operation to retirement, and security must act at each stage, including secure disposal. A **configuration management database (CMDB)** holds the configuration items and their relationships, so you can ask what depends on this server. An accurate **inventory** is the foundation for patching, vulnerability management and incident scoping, and it fails when shadow IT or untagged cloud resources are missing from it. Link the inventory to change management so that every approved change updates the record, and unapproved changes show up as drift.

## GRC tools

Governance, risk and compliance tools map controls to multiple frameworks (one control, many requirements), automate evidence collection and track compliance state over time. Their value is in reducing duplicated audit work and in surfacing control failures continuously rather than annually. Their limit is the data: a tool that reports on an incomplete inventory produces confident wrong answers.

## Data governance

Data governance defines who may use data, for what, and how long. It must cover every environment, not just production. **Production** data carries the real sensitivity. **Development, test and QA** environments often get copies of production data with weaker controls, which is a common breach path. The fix is to use synthetic data or masked, tokenised copies, keep non-production access narrower than production would suggest, and apply retention rules everywhere. Data classification (public, internal, confidential, restricted), ownership and lineage underpin every control decision.

## Risk management

**Impact analysis** estimates the consequence to confidentiality, integrity and availability, and to the business (financial, legal, reputational, safety). **Risk assessment** combines likelihood and impact.

- **Qualitative** assessment ranks risks (high, medium, low) using expert judgement. It is fast and works when numbers are unavailable.
- **Quantitative** assessment uses money: single loss expectancy = asset value x exposure factor; annualized loss expectancy = SLE x annualized rate of occurrence. It supports cost-benefit decisions and insurance, but depends on estimates that are easy to get wrong.

A control is worth buying if the reduction in annualized loss exceeds its annual cost. Treatments are mitigate, transfer, avoid and accept; what is left is **residual risk**, which must be accepted by someone with authority. **Third-party risk** extends all of this to suppliers: due diligence before contract, contractual security and breach-notification terms, right to audit, continuous monitoring and an exit plan. NIST SP 800-161 Rev. 1 (May 2022; the record page shows it as superseded) addressed supply chain risk as risk from products or services that may be malicious, counterfeit or poorly made, to be integrated with existing risk activities. A software bill of materials and signed artefacts apply the same idea to software.

## Threat modeling

Threat modeling asks what can go wrong in a design, before it is built. Elements the objectives name:

- **Actor characteristics**: capability, motivation, resources and access (nation state, organised crime, hacktivist, insider, opportunist).
- **Attack patterns**: how adversaries behave. **MITRE ATT&CK** is a free knowledge base of adversary tactics and techniques drawn from real-world observations, with Enterprise, Mobile and ICS matrices; it is used to build threat models and to map detections. **CAPEC** catalogues attack patterns of weaknesses at design level.
- **STRIDE** classifies threats per element: Spoofing, Tampering, Repudiation, Information disclosure, Denial of service and Elevation of privilege. Apply it to each component and each data flow in a diagram, and map each threat to a mitigation.

## Attack surface

The attack surface is everything an adversary can reach. **Architecture reviews** find unnecessary exposure; **data flow diagrams** show where data moves and where it is processed; **trust boundaries** mark where the level of trust changes, such as the internet to the web tier, or a SaaS vendor to your tenant. Threats concentrate at trust boundaries, so review authentication, validation and logging there first. Reduce the surface by removing, not just protecting: close ports, delete unused services and accounts, and shut down forgotten test environments.

## Compliance strategies

Compliance is a minimum, not security. Industry-specific standards apply by sector: **PCI DSS** for payment card data and the **ISO/IEC 27000** family for information security management systems (27001 specifies the management system, 27002 gives control guidance). Build one control set that satisfies the strictest overlapping requirements and map it to each regime, instead of one programme per regulation. Plan for jurisdiction: data residency and cross-border transfer rules affect cloud region choices and vendor selection. Maintain evidence continuously so audits are routine.

## Security frameworks

NIST CSF organises cybersecurity outcomes and is described by NIST as helping organisations better understand and improve their management of cybersecurity risk, with Quick Start Guides, Profiles and informative references. Use a **profile** to describe current and target states and plan the gap. The Cloud Security Alliance (CSA) publishes cloud-specific guidance such as the Cloud Controls Matrix. Choose, map and measure; a framework adopted without measurement is decoration.

---

## Key terms

- **Policy** - a mandatory statement of management intent in general terms
- **Standard** - a mandatory, measurable requirement that supports a policy
- **RACI matrix** - a chart assigning Responsible, Accountable, Consulted and Informed roles for each activity
- **COBIT** - an IT governance framework that links IT goals to business goals
- **ITIL** - an IT service management framework covering processes such as change, incident and configuration management
- **CMDB** - a configuration management database holding configuration items and their relationships
- **Data governance** - the policies and accountability determining who may use data, for what, and for how long
- **Quantitative risk assessment** - risk assessment using monetary values such as single and annualized loss expectancy
- **Residual risk** - the risk remaining after controls are applied
- **Third-party risk** - risk arising from suppliers, partners and service providers
- **STRIDE** - a threat classification: spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege
- **MITRE ATT&CK** - a knowledge base of adversary tactics and techniques drawn from real-world observations
- **CAPEC** - a catalogue of common attack patterns used to reason about how weaknesses are exploited
- **Trust boundary** - a point in a system where the level of trust changes
- **Attack surface** - the set of points where an adversary can try to enter or extract data
- **PCI DSS** - the payment card industry standard for protecting cardholder data
- **Risk Management Framework** - the NIST process for managing security and privacy risk across the system life cycle

---

## Related

- [Notes 02: security architecture](./02-security-architecture.md)
- [Governance and compliance topic](../../../../topics/governance-and-compliance.md)
- [NIST CSF guide](../../../../resources/compliance-guides/nist-csf.md)
- [ISO 27001 guide](../../../../resources/compliance-guides/iso-27001.md)
- **[📖 NIST SP 800-37 Rev. 2: Risk Management Framework](https://csrc.nist.gov/pubs/sp/800/37/r2/final)** - the RMF steps (December 2018)
- **[📖 NIST SP 800-161 Rev. 1: Cybersecurity Supply Chain Risk Management](https://csrc.nist.gov/pubs/sp/800/161/r1/final)** - supply chain risk practices (May 2022; the page notes it was withdrawn and superseded)
- **[📖 MITRE ATT&CK](https://attack.mitre.org/)** - the adversary tactics and techniques knowledge base
- **[📖 NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)** - CSF 2.0, profiles and quick start guides
