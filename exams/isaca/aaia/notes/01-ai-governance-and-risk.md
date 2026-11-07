---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
---

# 01 - AI governance and risk

**Domain 1: AI Governance and Risk (33%)** - content areas 1A to 1E of the June 2025 outline. Supporting tasks include evaluating the organization's AI policies and procedures and compliance with legal and regulatory requirements, evaluating monitoring and reporting of AI metrics (KPIs and KRIs), evaluating whether ownership of AI risk, controls, decisions and standards is defined, and evaluating the privacy and data governance programs for AI.

An auditor's question in this domain is always the same: what should exist, and is there evidence that it does?

---

## 1A AI models, considerations and requirements

You cannot audit what you cannot describe. Learn the building blocks:

- An **AI system** is, in the EU AI Act's words, a machine-based system designed to operate with varying levels of autonomy that infers from its input how to generate outputs such as predictions, content, recommendations or decisions that can influence physical or virtual environments. The OECD wording is nearly identical.
- A **model** is the trained component. Types an auditor meets: classic machine learning (classification, prediction), generative models (text, image, code), and agentic systems that call tools and take actions.
- **General-purpose AI models** are trained on large data and can perform many tasks; the EU AI Act sets separate duties for their providers.
- Key characteristics that drive audit risk: opacity (hard to explain), probabilistic outputs (same input, different outputs), data dependency, autonomy, and scale.

**[📖 Regulation (EU) 2024/1689 (AI Act), Article 3](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)** - definitions of AI system, provider, deployer, general-purpose AI model and serious incident
**[📖 OECD AI Principles](https://oecd.ai/en/ai-principles)** - values-based principles and the OECD definition of an AI system

NIST's characteristics of trustworthy AI give auditors a ready set of criteria: valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed. NIST adds that they involve trade-offs and that the decision to deploy should rest on a contextual assessment of trustworthiness, risks, impacts, costs and benefits.

**[📖 NIST AI RMF 1.0 (NIST AI 100-1)](https://doi.org/10.6028/NIST.AI.100-1)** - characteristics of trustworthy AI and the GOVERN, MAP, MEASURE and MANAGE functions

## 1B AI governance and program management

Governance is the first control area to audit, because it determines whether the rest exist. Evaluate whether:

- a charter or policy sets roles and responsibilities for AI, with executive sponsorship
- **ownership** of AI-related risk, controls, procedures, decisions and standards is defined (task 8)
- an **inventory** of AI systems exists and is current
- policies and procedures cover the life cycle and are communicated (tasks 6 and 23: awareness programs align with policy)
- **metrics** are defined and reported: KPIs show performance, KRIs signal rising risk (task 7). For AI, examples are model accuracy against threshold, drift indicators, rate of human overrides, number of AI incidents, and coverage of risk assessments
- the **workforce impact** is considered (task 22): training, education and role changes

NIST GOVERN is a good audit program skeleton. Its categories cover policies and processes (including legal and regulatory requirements understood, managed and documented), accountability structures, workforce diversity and inclusion, a critical-thinking and safety-first culture, engagement with outside parties, and third-party risk.

ISO/IEC 42001 is the AI management system standard, specifying requirements and guidance for establishing, implementing, maintaining and continually improving an AI management system. For an auditor it is a source of criteria and, where the organization is certified, a source of third-party assurance, whose scope you should read before relying on it. (Abstract read from national standards bodies' catalog pages; the full text is paid.)

**[📖 ISO/IEC 42001:2023](https://www.iso.org/standard/42001)** - catalog entry for the AI management system standard

## 1C AI risk management

Evaluate whether the organization runs a real AI risk process, integrated with enterprise risk:

- **Identification and assessment.** Is there an impact assessment before deployment covering individuals, groups and society? NIST MAP asks for context, categorization, benefits and costs, risks of third-party components, and impacts.
- **Treatment.** Are risk responses documented, with owners and dates? NIST MANAGE asks whether the system achieves its intended purpose and whether it should proceed, weighs non-AI alternatives, manages third-party risks and plans post-deployment monitoring, response and recovery.
- **Monitoring.** Are risks tracked over time, including emergent ones? MEASURE 3 asks for mechanisms to track identified risks.
- **Generative AI.** NIST AI 600-1 lists risks to look for: confabulation, data privacy, harmful bias and homogenization, information integrity, information security, intellectual property, value chain and component integration, human-AI configuration, and others.

**[📖 NIST AI 600-1 Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1)** - twelve generative AI risk areas and suggested actions

The EU AI Act supplies a regulatory risk lens. It prohibits certain practices (Article 5), regulates high-risk systems (Article 6 and Annex III) and imposes transparency duties for certain systems (Article 50). High-risk providers need a risk management system (Article 9), among other duties. Fines for breaching the Article 5 prohibitions reach EUR 35,000,000 or 7% of worldwide annual turnover, whichever is higher (Article 99). Task 3 asks you to evaluate AI solutions to advise on impact, opportunities and risk, so keep both sides in view.

## 1D Privacy and data governance programs

Tasks 9 and 10 ask you to evaluate the data governance and privacy programs specific to AI. Audit questions:

- **Lawful basis and purpose.** Was data used for training and use covered by the stated purpose and permissions? Is there a record?
- **Minimization and retention.** Is only the necessary data used, and for how long is it kept, including in prompts, logs and vector stores?
- **Data subject rights.** Is there a process for access, correction and deletion requests that reaches derived data?
- **Sensitive data.** Are special categories handled with extra controls?
- **Data quality and lineage.** Is origin documented, and is quality fit for purpose? EU AI Act Article 10 gives a good checklist for high-risk systems: design choices, collection and origin, preparation operations, assumptions, availability and suitability, bias examination and mitigation, and gaps.
- **Leakage.** NIST AI 600-1 describes models leaking, generating or inferring sensitive information about individuals, and training data memorization.
- **Cross-border and third-party processing** where relevant.

The specific privacy statute depends on the jurisdiction in the question. Use the principle (lawful basis, purpose, minimization, rights, security) and then the named law.

## 1E Leading practices, ethics, regulations and standards for AI

Task 3 and task 6 tie to compliance. The auditor should know the landscape well enough to identify criteria, not to give legal advice:

- **Regulation** (binding): the EU AI Act is the main comprehensive law; sectoral and national laws also apply. Role matters: provider, deployer, importer, distributor.
- **Frameworks** (voluntary): NIST AI RMF, OECD principles.
- **Standards** (certifiable): ISO/IEC 42001.
- **Ethics**: fairness, transparency, accountability, human oversight, privacy, safety. The OECD list is inclusive growth and well-being; human rights and democratic values; transparency and explainability; robustness, security and safety; accountability.

The EU AI Act applies in stages. Article 113 states that it applies from 2 August 2026 with exceptions: Chapters I and II from 2 February 2025; certain governance, general-purpose model, enforcement and penalty provisions from 2 August 2025; and Article 6(1) obligations from 2 August 2027. Those are the dates in the published text. Confirm current dates before testing compliance, as amendments have been proposed.

When you cite a criterion in a report, name the source and version. An audit finding is only as strong as the criterion behind it.

> **Exam habit:** If a question asks what the auditor should do first in a governance review, think scope, objectives and criteria: understand the AI inventory and the applicable requirements before testing anything.

---

## Key terms

- **AI system** - a machine-based system designed to operate with varying levels of autonomy that infers from its input how to generate outputs such as predictions, content, recommendations or decisions (EU AI Act, Article 3)
- **KRI (key risk indicator)** - a metric that signals increasing risk exposure, for AI for example rising drift or override rates
- **KPI (key performance indicator)** - a metric showing how well a process or system is performing
- **Trustworthy AI characteristics** - valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed (NIST AI RMF)
- **Model owner** - the person accountable for an AI model's risk, controls and performance
- **Impact assessment** - structured analysis of how an AI system could affect individuals, groups and society
- **Confabulation** - confidently stated but erroneous or false content produced by a generative AI system (NIST AI 600-1)
- **Data minimization** - using only the data necessary for the stated purpose
- **ISO/IEC 42001** - the certifiable standard for an AI management system
- **Criteria** - the standards, policies or laws against which an auditor evaluates a subject
