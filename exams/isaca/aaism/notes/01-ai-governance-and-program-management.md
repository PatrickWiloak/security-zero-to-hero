---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
---

# 01 - AI governance and program management

**Domain 1: AI Governance and Program Management (31%)** - content areas 1A to 1E of the June 2025 outline. Supporting tasks include collaborating on the charter and roles for AI governance, maintaining AI-specific security policies, ensuring responsible use, keeping an AI asset and data inventory, handling AI incidents, and building AI security awareness and acceptable use guidelines.

For a security manager, governance is the structure that makes every later control possible: who decides, by what rules, with what visibility. The IAPP AIGP guide in this repo covers the legal and policy side in more depth: see [IAPP AIGP](../../../iapp/aigp/).

---

## 1A Stakeholder considerations, industry frameworks and regulatory requirements

AI touches more stakeholders than most systems: business owners, data science and engineering, security, privacy, legal, risk, audit, HR, vendors, customers and the people the system makes decisions about. Your task is to collaborate on a charter that sets roles and responsibilities so that AI use aligns with business objectives. Without that, AI adoption happens in pockets with no owner.

Three frameworks to know well, all from primary sources:

**NIST AI Risk Management Framework (AI 100-1).** Four functions. GOVERN is cross-cutting and sets policies, accountability structures, culture and third-party handling. MAP establishes context and characterizes impacts. MEASURE analyzes, benchmarks and monitors risk. MANAGE prioritizes and treats risk, including response and recovery. NIST says AI systems should be tested before deployment and regularly in operation.

**[📖 NIST AI RMF 1.0 (NIST AI 100-1)](https://doi.org/10.6028/NIST.AI.100-1)** - the four functions, categories and trustworthy AI characteristics
**[📖 NIST AI 600-1 Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1)** - twelve risks unique to or exacerbated by generative AI and suggested actions mapped to AI RMF subcategories

**ISO/IEC 42001:2023.** The AI management system standard. Its abstract describes requirements and guidance for establishing, implementing, maintaining and continually improving an AI management system within an organization that provides or uses products or services that utilize AI systems. It is certifiable, which suits organizations that need to show customers an audited program. (Abstract read from national standards bodies' catalog pages; the full text is paid.)

**[📖 ISO/IEC 42001:2023](https://www.iso.org/standard/42001)** - catalog entry for the AI management system standard

**Regulation.** The EU AI Act classifies AI by risk (prohibited practices in Article 5, high-risk systems in Article 6 and Annex III, transparency duties in Article 50) and puts duties on providers and deployers. For security managers, the key hooks are Article 15 (accuracy, robustness and cybersecurity of high-risk systems), Article 9 (risk management system), Article 12 (record-keeping) and Article 73 (reporting of serious incidents). Fines for the most serious infringements reach EUR 35,000,000 or 7% of worldwide annual turnover.

**[📖 Regulation (EU) 2024/1689 (AI Act) on EUR-Lex](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)** - primary text; see Articles 5, 6, 9, 12, 15, 50, 73, 99 and Annex III

The exam asks you to apply these, not recite them. Know which are binding (law), which are voluntary guidance (NIST, OECD) and which can be certified (ISO 42001).

## 1B AI-related strategies, policies and procedures

Policy is where "responsible use" becomes enforceable. The tasks ask you to establish and maintain AI-specific security policies and procedures that inform standards and guidelines, and to ensure responsible use through leading practices, ethical principles, regulatory requirements and frameworks.

A workable AI policy stack sits beside existing security policy rather than replacing it:

- An **AI acceptable use policy**: which tools staff may use, what data may be entered, what outputs need human review, and what is forbidden.
- **Data handling for AI**: classification limits on what may be used for prompts, fine-tuning or retrieval.
- **Development and procurement standards**: required assessments, testing, documentation and security requirements before something goes live.
- **Human oversight rules**: where a person must review or approve.
- **Incident and exception procedures**.

NIST's GOVERN function adds that policies should integrate the characteristics of trustworthy AI and that legal and regulatory requirements are understood, managed and documented. The OECD AI Principles (inclusive growth and well-being; human rights and democratic values; transparency and explainability; robustness, security and safety; accountability) are a good statement of the values behind those policies.

**[📖 OECD AI Principles](https://oecd.ai/en/ai-principles)** - values-based principles and the AI system definition

## 1C AI asset and data life cycle management

You cannot protect what you have not listed. The task is to establish and maintain processes to identify, inventory and classify data and assets related to AI. An AI asset inventory covers more than models:

- models (own, fine-tuned, third-party, API-based), their versions and owners
- training, validation and retrieval datasets, with source, license and sensitivity
- prompts, system instructions and configuration
- pipelines, vector stores, tools and plugins the model can call
- the business process and decision each supports
- shadow AI: tools staff use that nobody approved

Classification links the AI asset to the data it touches and the impact if compromised. **Life cycle** thinking asks what happens at each stage: acquire, prepare, train, validate, deploy, operate, retire. Retirement matters: models and datasets must be decommissioned with the same care as any asset, including deleting copies and revoking access. **Data lineage and provenance**, recording where data came from and what was done to it, is the control that lets you answer a regulator, a deletion request or a poisoning investigation.

## 1D AI security program development and management

A program turns policy into operating practice. Elements the outline expects: charter and roles, a governance body, risk-based control selection, metrics, tooling, training and continuous improvement. Tasks 18 and 19 mention defining and monitoring security metrics for AI solutions and reviewing and implementing AI security tools within the information security program.

Useful metrics are ones a manager can act on: share of AI systems inventoried and risk-assessed; share with a named owner; time to detect and respond to AI incidents; coverage of adversarial testing; vendor assessments completed; findings open past due; training completion. Treat vanity counts with caution.

Integrate AI into the existing program instead of building a second one. Enterprise architecture should include AI (task 11), security awareness should include AI (task 21), and the risk register should hold AI risks beside others.

## 1E Business continuity and incident response

AI systems fail in new ways: a model degrades, a vendor changes or withdraws a model, poisoned data is found after release, or a user extracts sensitive data through crafted input. The tasks ask you to:

- Address AI security risk in business continuity and disaster recovery planning. Ask what the business does when the AI is unavailable or wrong: a manual fallback, a prior model version, or a rule-based system.
- Establish AI-specific processes to investigate, document and report AI security incidents in line with regulatory and contractual requirements.
- Establish AI incident handling covering containment, notification, escalation, eradication and recovery.

AI incident handling follows the familiar life cycle with AI twists. Containment may mean disabling a tool the model can call, restricting retrieval scope, or switching to a fallback. Evidence includes prompts, outputs, model version, retrieval results and logs, so make sure they are retained. Eradication may mean removing poisoned data and retraining. EU AI Act Article 73 requires providers of high-risk systems to report serious incidents, and the Act defines a serious incident by the harm it causes, such as death, serious harm to health, serious and irreversible disruption of critical infrastructure, or infringement of fundamental rights obligations.

> **Exam habit:** governance answers usually name an owner, a document, a review cycle and a link to business objectives. Pick the answer that builds the structure before the tool.

---

## Key terms

- **AI governance** - the structure of roles, policies and decision rights that directs how an organization develops and uses AI
- **GOVERN** - the NIST AI RMF function that sets policy, accountability, culture and third-party handling across the other functions
- **ISO/IEC 42001** - the certifiable international standard for an AI management system
- **AI acceptable use policy** - rules stating which AI tools and data staff may use and what review is required
- **AI asset inventory** - a maintained list of models, datasets, prompts, pipelines, tools and the processes they support
- **Shadow AI** - AI tools used in an organization without approval or visibility
- **Data lineage** - the documented path of data from origin through every transformation
- **Serious incident (EU AI Act)** - an incident or malfunction of an AI system that leads to death or serious harm to health, serious and irreversible disruption of critical infrastructure, infringement of fundamental-rights obligations under Union law, or serious harm to property or the environment
- **Risk-based human oversight** - review of AI inputs and outputs proportionate to risk, covering trust and safety, quality, explainability and robustness
