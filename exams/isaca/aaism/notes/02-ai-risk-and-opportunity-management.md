---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 14 min
---

# 02 - AI risk and opportunity management

**Domain 2: AI Risk and Opportunity Management (31%)** - content areas 2A to 2C. ISACA's web page calls the domain "AI Risk Management"; the candidate guide adds "and Opportunity". The word matters: AI risk decisions weigh benefits too, so "do not use AI" is rarely the best answer.

Related tasks: oversee the AI risk life cycle including impact on enterprise risk, identify and assess the AI threat landscape, monitor internal and external factors that call for reassessment, design and implement testing and vulnerability management of AI solutions, conduct AI impact assessments, and embed, monitor and verify security requirements in vendor AI solutions.

---

## 2A AI risk assessment, thresholds and treatment

Start from the enterprise risk process you already know: identify, analyze, evaluate, treat, monitor. The AI twist is in what you assess.

**What makes AI risk different.** NIST lists the characteristics of trustworthy AI (valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed) and stresses that they trade off against each other. NIST also notes that the AI lifecycle has many interdependent activities and actors, so one team often lacks visibility into the others, and early decisions can change behavior later. Practically, this means the assessment must cover the whole life cycle and the deployment context, not only the model.

**The AI RMF map step** asks you to establish context: intended purpose, settings, laws and expectations; to categorize the system; to examine benefits and costs; to map risks for all components including third-party data and software; and to characterize impacts on individuals, groups, communities and society. That is your impact assessment template (task 8).

**Generative AI adds risks.** NIST AI 600-1 names twelve: CBRN information or capabilities, confabulation, dangerous, violent or hateful content, data privacy, environmental impacts, harmful bias and homogenization, human-AI configuration, information integrity, information security, intellectual property, obscene, degrading or abusive content, and value chain and component integration. Confabulation (confidently stated but false output) is the one every business user meets first.

**[📖 NIST AI 600-1 Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1)** - the twelve risk areas and suggested actions

**Thresholds.** A threshold is the point at which a measured risk indicator triggers action. Examples: a drift level that triggers retraining, a rate of harmful outputs that triggers rollback, an error rate that triggers human review. Thresholds come from risk appetite set by business owners, not from the model team alone. NIST MANAGE 1.1 frames the underlying question: whether the system achieves its intended purposes and objectives and whether development or deployment should proceed.

**Treatment** uses the usual options: mitigate (controls), transfer (insurance, contract), avoid (do not deploy the use case) and accept (formally, by the risk owner). MANAGE 2.1 reminds you to weigh viable non-AI alternatives, which is the "opportunity" side: sometimes a simpler method gives the benefit at less risk.

## 2B AI threat and vulnerability management

Identify and assess the AI threat landscape, then test and manage vulnerabilities. Three authoritative sources give you the vocabulary.

**NIST AI 100-2 (adversarial machine learning).** It organizes attacks by the attacker's goal against a predictive AI system: availability breakdown, integrity violation, and privacy compromise. Evasion attacks modify inputs at deployment time so the model misclassifies them while the change often stays imperceptible to humans. Poisoning attacks interfere at training time: targeted poisoning aims at specific samples, backdoor poisoning plants a trigger pattern, and model poisoning alters model parameters. Privacy compromise is leakage of restricted information including training data, weights or architecture. Energy-latency attacks are availability attacks that need only query access.

**[📖 NIST AI 100-2 E2025 Adversarial Machine Learning](https://doi.org/10.6028/NIST.AI.100-2e2025)** - taxonomy and terminology of attacks and mitigations

**NIST AI 600-1, information security.** It says generative AI both lowers barriers for offensive cyber operations and expands the attack surface, since the system itself is vulnerable to prompt injection and data poisoning. It distinguishes direct prompt injection (a crafted prompt entered directly) from indirect prompt injection, where adversaries inject prompts into data the application is likely to retrieve.

**OWASP Top 10 for LLM Applications (2025).** A community list of the most critical LLM application risks: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM03 Supply Chain, LLM04 Data and Model Poisoning, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM08 Vector and Embedding Weaknesses, LLM09 Misinformation and LLM10 Unbounded Consumption. Use it as a checklist for design review and testing of any application built around a language model.

**[📖 OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)** - the 2025 list with descriptions and mitigations

Defensive practice: threat model the system (what can an attacker influence: training data, retrieval content, prompts, tool inputs, the model supply chain); test before release and on a schedule with authorized adversarial testing (red teaming); track findings in the same vulnerability process as other assets; and watch for external developments (new attack techniques, vendor advisories) that trigger reassessment (task 6).

## 2C AI vendor and supply chain management

Most organizations consume AI. NIST GOVERN 6.1 asks for policies and procedures that address risks of third-party entities, including infringement of a third party's intellectual property or other rights. MAP 4.1 asks for approaches to map risks of components, including third-party data and software. MANAGE 3.1 asks that risks and benefits from third-party resources be regularly monitored and controls applied and documented.

NIST AI 600-1 explains why this is hard for generative AI: value chains involve many third-party components (datasets, pre-trained models, libraries) that might be improperly obtained or not properly vetted; the scale of training data may be too large for humans to vet; foundation models are heavily reused; and it can be hard to attribute an issue to a single source.

A vendor assessment should ask: what model and version, trained on what data and with what rights; whether your data is retained or used for training; where processing occurs; what security certification or audit evidence exists (ISO 42001, SOC reports); how changes are notified; how incidents are notified; what testing the vendor has done; and what the exit path is. Task 9 sums the discipline: embed, monitor and verify AI security requirements when using vendor AI-enabled solutions. Embed means written into the contract and requirements. Monitor means ongoing. Verify means you check evidence rather than relying on assurances.

Also treat the AI software supply chain like any other: pinned and verified model artifacts, scanned dependencies, controlled sources, and a record of what is in the system. OWASP lists Supply Chain as LLM03.

> **Exam habit:** when the stem mentions a vendor, the right answer usually adds contract terms and verification, not blind trust and not a ban.

---

## Key terms

- **Evasion attack** - modification of inputs at deployment time so a model misclassifies them, often imperceptibly (NIST AI 100-2)
- **Poisoning attack** - interference with training data or model parameters to alter model behavior (NIST AI 100-2)
- **Backdoor poisoning** - poisoning that plants a trigger pattern so inputs containing it are misclassified
- **Privacy compromise** - unintended leakage of restricted information from an AI system, including training data, weights or architecture
- **Prompt injection** - input that causes a language model to behave in unintended ways; direct when entered by the user, indirect when hidden in retrieved data
- **Confabulation** - confidently stated but erroneous or false content produced by a generative AI system (NIST AI 600-1)
- **Excessive agency** - the vulnerability that lets damaging actions occur in response to unexpected, ambiguous or manipulated LLM output, rooted in excessive functionality, permissions or autonomy (OWASP LLM06)
- **Risk threshold** - a defined level of a risk indicator at which action is triggered
- **Impact assessment** - structured analysis of how an AI system could affect individuals, groups and society
- **Value chain risk** - risk from third-party datasets, pre-trained models and libraries that are not properly vetted
