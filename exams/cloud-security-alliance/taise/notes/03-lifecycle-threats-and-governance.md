---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 14 min
---

# 03 - Model life cycle and threat taxonomy; governance, risk and compliance

**Modules 5 and 6 of 10 (6 exam questions each).** CSA's titles: "AI Model Lifecycle and Threat Taxonomy" and "Model Governance, Risk Management, and Compliance".

---

## Module 5: AI model life cycle and threat taxonomy

**Life cycle.** A model passes through requirements and design, data collection and preparation, training, validation and testing, deployment, operation and monitoring, and retirement. Attacks and failures can target any stage, which is why NIST places test, evaluation, verification and validation (TEVV) throughout the life cycle.

**Threat taxonomy (predictive AI).** NIST AI 100-2 (adversarial machine learning) organizes attacks by the attacker's objective:

- **Availability breakdown**: interference that disrupts timely and reliable access to the system's services, including energy-latency attacks that need only query access.
- **Integrity violation**: forcing the system to misperform against its intended objectives. It is achieved by **evasion** at deployment time (modified inputs that are misclassified, often imperceptibly) or by **poisoning** at training time (targeted poisoning, backdoor poisoning with a trigger pattern, and model poisoning that changes parameters).
- **Privacy compromise**: unintended leakage of restricted or proprietary information, including training data, weights or architecture.

**[📖 NIST AI 100-2 E2025 Adversarial Machine Learning](https://doi.org/10.6028/NIST.AI.100-2e2025)** - the taxonomy and terminology of attacks and mitigations

**Threat taxonomy (language-model applications).** The OWASP Top 10 for LLM Applications (2025) lists: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM03 Supply Chain, LLM04 Data and Model Poisoning, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM08 Vector and Embedding Weaknesses, LLM09 Misinformation, and LLM10 Unbounded Consumption. NIST AI 600-1 adds that prompt injection comes in two forms: direct, where an attacker enters a crafted prompt, and indirect, where adversaries inject prompts into data likely to be retrieved.

**[📖 OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)** - the 2025 list with descriptions and mitigations

Match threat to stage: poisoning and supply chain risks hit data and training; evasion and prompt injection hit deployment; extraction and leakage hit operation; consumption attacks hit availability.

## Module 6: Model governance, risk management and compliance

**Risk management frameworks.** The NIST AI RMF organizes work into GOVERN (policies, accountability, culture, third-party risk), MAP (context and impacts), MEASURE (analysis, testing, monitoring) and MANAGE (prioritization, treatment, response, recovery). GOVERN is cross-cutting.

**Management system standard.** ISO/IEC 42001:2023 specifies requirements and provides guidance for establishing, implementing, maintaining and continually improving an AI management system within an organization that provides or uses products or services that utilize AI systems, regardless of size or type. It can be certified. (Abstract read from national standards bodies' catalog pages; the full text is paid.)

**[📖 ISO/IEC 42001:2023](https://www.iso.org/standard/42001)** - catalog entry for the AI management system standard

**Control framework.** CSA's AI Controls Matrix (AICM) is a vendor-neutral control framework: CSA's page describes 243 control objectives across 18 security domains, mapped to ISO 42001, ISO 27001, NIST AI RMF 1.0 and BSI AIC4 (and, in the download, to NIST AI 600-1 and the EU AI Act). It defines five roles, each with implementation and auditing guidance: model provider, orchestrated service provider, application provider, AI customer and cloud service provider. The page notes AICM v1.1 is newer than v1, so check the latest.

**[📖 CSA AI Controls Matrix](https://cloudsecurityalliance.org/artifacts/ai-controls-matrix)** - the control objectives, domains, mappings and roles

**Law and compliance.** The EU AI Act classifies AI by risk. Prohibited practices (Article 5) are banned. High-risk systems must meet requirements including a risk management system (Article 9), data governance (Article 10), technical documentation (Article 11), record-keeping (Article 12), human oversight (Article 14) and accuracy, robustness and cybersecurity (Article 15). General-purpose model providers have separate duties (Article 53). Fines reach EUR 35,000,000 or 7% of worldwide annual turnover for breaches of the Article 5 prohibitions (Article 99). Article 113 sets staged application dates beginning 2 February 2025 and applying generally from 2 August 2026, as published; check for amendments.

**[📖 Regulation (EU) 2024/1689 (AI Act)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)** - the primary text on EUR-Lex

Governance in practice: an inventory of AI systems with owners, a policy set, risk assessments before deployment, documented approvals, monitoring, incident handling and periodic review. Compliance is evidence that these controls exist and work.

> **Exam habit:** know which items are binding (law), voluntary (NIST, OECD), certifiable (ISO 42001) and a control catalog (AICM). Questions often depend on that.

---

## Key terms

- **Availability breakdown** - an attack that disrupts timely and reliable access to an AI system (NIST AI 100-2)
- **Integrity violation** - an attack that forces an AI system to misperform against its intended objectives (NIST AI 100-2)
- **Privacy compromise** - an attack causing unintended leakage of restricted information from an AI system (NIST AI 100-2)
- **Evasion attack** - modified inputs at deployment time that cause misclassification
- **Poisoning attack** - interference with training data or model parameters
- **Direct prompt injection** - a crafted prompt entered directly into a generative AI system
- **Indirect prompt injection** - prompts injected into data the application is likely to retrieve
- **AI Controls Matrix (AICM)** - CSA's control framework for trustworthy AI with 243 control objectives across 18 domains
- **ISO/IEC 42001** - the certifiable AI management system standard
- **High-risk AI system** - a system in an Annex III area, or a safety component of a regulated product, subject to the AI Act's Chapter III requirements
