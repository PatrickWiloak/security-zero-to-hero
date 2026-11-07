---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 10 min
---

# 03 - AI auditing tools and techniques

**Domain 3: AI Auditing Tools and Techniques (21%)** - content areas 3A to 3E. This domain covers how to run the audit, and how AI can itself help the audit. The tasks: evaluate impacts, opportunities and risk when integrating AI solutions within the audit process (task 1) and use AI solutions to enhance audit processes, including planning, execution and reporting (task 2).

The general audit method is the one you know from CISA: risk-based planning, evidence, conclusions, reporting. The AI-specific parts are what to test and how AI changes the tools.

---

## 3A Audit planning and design

Start with understanding the business and the AI use: what decisions does the system influence, who is affected, what is the risk? Then set objectives, scope, criteria and approach.

- **Scope** from the AI inventory and risk ranking. High-impact decisions (credit, hiring, safety) and high-exposure systems go first.
- **Criteria** from law (for example the EU AI Act where applicable), frameworks (NIST AI RMF), standards (ISO/IEC 42001), organizational policy and contracts. NIST's GOVERN, MAP, MEASURE and MANAGE functions make a workable audit program outline.
- **Skills and independence.** AI audits need technical competence. If the team lacks it, obtain specialist support while keeping the auditor's independence and responsibility for conclusions.
- **Approach**: combine control testing (governance, change, access, incident) with testing of the model's behavior (outputs, fairness, robustness).

## 3B Audit testing and sampling methodologies

Control testing for AI uses the usual methods: inquiry, observation, inspection and re-performance. Sampling needs thought because AI systems produce huge volumes of decisions.

- **Statistical sampling** supports projecting results to the population with a stated confidence; **judgmental sampling** uses auditor judgment to focus on risk.
- For control tests (such as change approvals), sample from the population of changes in the period.
- For outcome testing (such as fairness), consider stratified samples so that small groups are represented; a random sample may contain too few members of a minority group to detect a difference.
- **Substantive testing of model outputs** may use a labeled test set, independent re-computation, or comparison of decisions with a benchmark or human reviewers.
- Probabilistic outputs mean repeating a test can give different results; document the conditions and repeat where it matters.

State the population, the sampling method, sample size rationale and how exceptions were handled.

## 3C Audit evidence collection techniques

Evidence must be sufficient, reliable and relevant. For AI, sources include model documentation and cards, training and test records, data lineage, change tickets, version control history, system logs of prompts, outputs and decisions, monitoring dashboards, vendor reports, and interviews with owners and reviewers.

Rank reliability: evidence obtained directly by the auditor, from independent sources and in documentary form is stronger than representations from the auditee. A vendor statement that a model is unbiased is an assertion; the underlying test design and results are evidence.

Preserve integrity: use read-only access, timestamped extracts and a record of how data was obtained. Treat the evidence itself as sensitive when it includes personal data or proprietary model details.

## 3D Audit data quality and data analytics

Data analytics lets auditors test whole populations rather than samples. For AI audits, analytics can compare outcomes across groups, detect drift between training and live data, look for anomalies in override rates, and reconcile decision logs to approvals.

Quality of the audit data matters first: confirm completeness, accuracy and provenance of the extract (record counts, control totals, reconciliation to source) before relying on the results. NIST AI 600-1 and the EU AI Act both emphasize documentation and lineage, which makes the extract easier to validate.

**Using AI inside the audit** (tasks 1 and 2). AI tools can help with planning (risk scoring), execution (document review, anomaly detection) and reporting (drafting). The auditor must evaluate the impact, opportunity and risk: protect client and auditee data, verify outputs because generative tools can produce confidently stated errors (NIST calls this confabulation), keep a reviewer accountable for every conclusion, and document how outputs were verified. An AI summary is a lead, not evidence.

## 3E AI audit outputs and reports

A good AI audit report states scope, criteria, method, findings, risk rating, causes, recommendations and management responses, with enough precision that the finding can be acted on and re-tested. Practical points:

- Name the criterion behind each finding (a policy clause, an Act article, a framework subcategory).
- Describe limitations: the model's probabilistic behavior, test coverage, and any reliance on specialist work or third-party assurance.
- Report to the right level. Executives need risk and decisions; owners need specifics.
- Follow up on agreed actions and re-test.
- Keep independence: recommend what outcome is needed, and leave the design of the fix to management.

> **Exam habit:** in Domain 3 the best answer protects the integrity of evidence and the independence of the auditor, and uses AI as a tool whose outputs are verified.

---

## Key terms

- **Judgmental sampling** - choosing sample items by auditor judgment, usually focusing on higher-risk items
- **Statistical sampling** - random selection that allows results to be projected to the population with a stated confidence
- **Stratified sample** - a sample drawn so that each defined subgroup is represented
- **Audit evidence** - information used to support audit conclusions, which must be sufficient, reliable and relevant
- **Audit criteria** - the laws, standards, policies or frameworks against which a subject is evaluated
- **Data analytics** - automated analysis of whole populations of data to find exceptions and patterns
- **Population reconciliation** - checking that an extract is complete by tying record counts and totals to the source
- **Auditor independence** - freedom from conditions that threaten objectivity, so findings are not influenced by involvement in operating the subject
- **Confabulation** - confidently stated but false content produced by a generative AI system
