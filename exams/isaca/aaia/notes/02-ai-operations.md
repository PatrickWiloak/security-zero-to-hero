---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 20 min
---

# 02 - AI operations

**Domain 2: AI Operations (46%)** - content areas 2A to 2G, the largest domain at nearly half the exam. The supporting tasks read like an audit program: evaluate data input requirements, the AI solution life cycle, algorithms and models, change and configuration management, identity and access management, threat and vulnerability management, problem and incident management, and the design and effectiveness of AI controls.

For each area, think in three steps: the objective, the control that should exist, and the evidence you would test.

---

## 2A Data management specific to AI

**Objective:** data used by the AI is appropriate, lawful, accurate, protected and traceable.

**Controls to expect:** data inventory and classification; documented sources and lineage; quality checks; bias examination; access control and encryption for datasets, vector stores and logs; retention and deletion rules.

**Evidence:** data catalog entries, lineage records, data quality reports, access lists, approvals for data use, and sampling of datasets against requirements. Task 18 asks you to evaluate data input requirements for AI models, including data appropriateness, bias and privacy.

Two AI-specific points. First, data defects become model defects: biased or unrepresentative data produces biased decisions. EU AI Act Article 10 says training, validation and testing data sets must be relevant, sufficiently representative and, to the best extent possible, free of errors and complete for the intended purpose. Second, integrity of training data is a security matter. NIST AI 100-2 describes poisoning attacks at training time, and OWASP lists Data and Model Poisoning (LLM04).

## 2B AI solution development methodologies and life cycle

**Objective:** the AI solution is designed, built, validated, deployed, operated and retired in a controlled way aligned to business needs and enterprise architecture (tasks 19, 20 and 21).

Follow the life cycle and ask what gate exists at each stage:

```mermaid
flowchart LR
  A["Requirements and design"] --> B["Data preparation"]
  B --> C["Build and train"]
  C --> D["Validate and test"]
  D --> E["Approve and deploy"]
  E --> F["Operate and monitor"]
  F --> G["Retire"]
  F -.->|"drift, incidents"| A
```

The diagram shows a loop: operational findings flow back into design.

- **Requirements and design:** business objective documented, impact assessment done, risk classification, human oversight designed in.
- **Build and train:** controlled environments, versioned code, data and models; documentation of choices.
- **Validate:** test against defined thresholds with independent review where possible. NIST MEASURE says systems should be tested before deployment and regularly while operating, with documented test sets and metrics.
- **Deploy:** formal approval, release readiness, rollback plan.
- **Operate:** monitoring, maintenance, retraining schedule.
- **Retire:** decommissioning of models, data and access.

Task 21 asks you to evaluate algorithms and models so that AI solutions align with business objectives, policies and procedures. In practice, trace from the stated objective to the chosen model and the validation evidence, and confirm it is the model in production.

For high-risk systems under the EU AI Act, the life cycle is regulated: a quality management system (Article 17), technical documentation (Article 11), record-keeping (Article 12), and post-market monitoring (Article 72) are among the duties auditors can use as criteria.

## 2C Change management specific to AI

**Objective:** changes to models, data, prompts, configuration and infrastructure are authorized, tested and traceable (tasks 12 and 13).

AI widens what counts as a change: retraining, fine-tuning, a new base model version from a vendor, prompt or system instruction edits, retrieval corpus updates, and tool or permission changes. Controls: change request and approval, impact and risk assessment, testing against thresholds, version control, segregation of duties, rollback, and emergency change handling. Configuration management should track model versions, parameters, prompts and dependencies so the production state is known.

**Evidence:** change tickets sampled and traced to approval and test results; version history; comparison of deployed artifacts to approved ones; and detection of unauthorized changes. A model that changes without an approval trail is a classic finding.

## 2D Supervision of AI solutions (outputs, impacts and decisions)

**Objective:** the organization oversees what the AI produces and the effects it has (tasks 4 and 5).

Supervision includes human oversight, output monitoring, performance and drift tracking, complaint and override analysis, and review of the impact on people. EU AI Act Article 14 requires high-risk systems to be designed so natural persons can effectively oversee them, with measures commensurate with risks, autonomy and context. For deployers, Article 26 requires assigning human oversight to people with necessary competence, training and authority, monitoring operation, and keeping logs under their control for at least six months.

Audit the quality of oversight, not only its existence. Are reviewers trained? Do they have time and authority to override? Is the override rate tracked, and does a near-zero rate suggest rubber-stamping? Are decisions that significantly affect people explainable and contestable?

Also evaluate the effect on the organization and stakeholders (task 5) and on system interactions, the environment and humans (task 4): downstream systems that rely on the output, and affected groups.

## 2E Testing techniques for AI solutions

**Objective:** testing is sufficient to give confidence in performance, robustness, fairness, security and safety.

Know the techniques and what each shows:

- **Performance testing** against metrics and thresholds on held-out data.
- **Robustness testing**: behavior under noisy, unusual or adversarial input.
- **Bias and fairness testing**: outcomes compared across groups.
- **Explainability and interpretability testing**.
- **Security testing** including authorized adversarial testing (red teaming) and prompt injection testing for language model applications.
- **Regression testing** after any change.
- **Ongoing monitoring** as continuous testing in production.

From an auditor's view, evaluate the test design (are objectives, metrics and thresholds set in advance?), data (are test sets independent of training data?), independence of the tester, coverage and repeatability, and whether results drove decisions. NIST MEASURE 2.1 asks that test sets, metrics and tool details used in testing, evaluation, verification and validation be documented, and MEASURE as a whole notes that independent review improves testing and mitigates internal bias.

## 2F Threats and vulnerabilities specific to AI

**Objective:** AI-specific threats are identified and managed within the vulnerability and access programs (tasks 14 and 15).

Learn the vocabulary from the primary sources.

NIST AI 100-2 groups attacks on predictive AI by goal: availability breakdown, integrity violation and privacy compromise. Evasion attacks alter inputs at deployment to cause misclassification; poisoning attacks interfere at training time (targeted, backdoor and model poisoning); privacy compromise leaks training data, weights or architecture.

**[📖 NIST AI 100-2 E2025 Adversarial Machine Learning](https://doi.org/10.6028/NIST.AI.100-2e2025)** - taxonomy and terminology of attacks and mitigations

NIST AI 600-1 notes generative AI both lowers barriers to offensive cyber operations and expands the attack surface through prompt injection (direct and indirect) and data poisoning.

The OWASP Top 10 for LLM Applications (2025) lists: Prompt Injection, Sensitive Information Disclosure, Supply Chain, Data and Model Poisoning, Improper Output Handling, Excessive Agency, System Prompt Leakage, Vector and Embedding Weaknesses, Misinformation, and Unbounded Consumption. Use it as a checklist when auditing a language model application.

**[📖 OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)** - 2025 list of critical LLM application risks

Audit questions: is there a threat model for each AI system; are AI assets in the vulnerability management process; is adversarial testing performed; are model artifacts, datasets and prompts protected by identity and access management (least privilege, separation of duties, privileged access reviews); are secrets kept out of prompts; and is agent and tool authority limited? Excessive Agency (LLM06) is rooted in excessive functionality, permissions or autonomy, so check the permissions granted to tools and agents against need.

## 2G Incident response management specific to AI

**Objective:** AI incidents are detected, classified, handled, reported and learned from (task 11).

Evaluate whether the incident and problem management programs recognize AI failure modes: harmful or wrong outputs at scale, data leakage through prompts or outputs, model compromise, poisoned data discovered after release, biased outcomes, and vendor model changes. Check that there is a classification scheme, escalation paths, containment options including disabling the system, evidence preservation (prompts, outputs, model version, retrieval results, logs), communication to affected parties and regulators, root cause analysis, and lessons learned.

EU AI Act Article 73 requires providers of high-risk systems to report serious incidents, and the Act defines a serious incident by its consequences: death or serious harm to health, serious and irreversible disruption of critical infrastructure, infringement of fundamental-rights obligations under Union law, or serious harm to property or the environment. Contracts with vendors may impose their own notification duties; test whether they are met.

> **Exam habit:** in Domain 2 look for the answer that evaluates a control's design and its operating effectiveness with evidence, and that treats AI as a change and incident subject like other systems, with AI-specific twists.

---

## Key terms

- **Design effectiveness** - whether a control, if operated as described, would meet its objective
- **Operating effectiveness** - whether the control actually operated as designed over the period tested
- **Data lineage** - the documented path of data from origin through every transformation
- **Poisoning attack** - interference with training data or model parameters to alter model behavior (NIST AI 100-2)
- **Evasion attack** - alteration of inputs at deployment time so a model misclassifies them (NIST AI 100-2)
- **Prompt injection** - input that causes a language model to behave in unintended ways, direct or indirect
- **Excessive agency** - the vulnerability that lets damaging actions occur in response to unexpected, ambiguous or manipulated LLM output, rooted in excessive functionality, permissions or autonomy (OWASP LLM06)
- **Human oversight** - arrangements that let people monitor, interpret and intervene in an AI system's operation
- **Regression testing** - re-testing after a change to confirm existing behavior still meets requirements
- **Rollback** - returning a system to a previous approved state after a failed change
- **Serious incident (EU AI Act)** - an incident or malfunction of an AI system that leads to death or serious harm to health, serious and irreversible disruption of critical infrastructure, infringement of fundamental-rights obligations under Union law, or serious harm to property or the environment
