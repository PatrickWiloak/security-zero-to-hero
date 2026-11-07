---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 10 min
---

# 05 - Data security and privacy; continuous learning

**Modules 9 and 10 of 10 (6 exam questions each).** CSA's titles: "Data Security and Privacy AI Systems" and "Continuous Learning and Adaption".

---

## Module 9: Data security and privacy in AI systems

**Why data is central.** Data trains, tunes and feeds AI systems, and sits in prompts, retrieval stores and logs. Protecting it covers the whole life cycle.

**Privacy risks (NIST AI 600-1).** Generative AI training needs large volumes of data that can include personal data, which raises risks to widely accepted privacy principles including transparency, individual participation (including consent) and purpose specification. Models may leak, generate or correctly infer sensitive information about individuals. During adversarial attacks, language models have revealed sensitive information from their training data, a problem called data memorization. Models can also infer personal information not in their training data by stitching sources together, and wrong inferences can harm people too.

**Attack framing (NIST AI 100-2).** Privacy compromise covers leakage of restricted information including training data, weights or architecture. OWASP's LLM02, Sensitive Information Disclosure, addresses sensitive information affecting both the model and the application using it.

**Controls.**

- **Classification and minimization**: use only the data necessary; keep sensitive data out of prompts and training unless justified.
- **Provenance and lineage**: record where data came from, the lawful basis and permissions, and each transformation.
- **Access control and encryption** for datasets, vector stores, checkpoints and logs; enforce permissions at retrieval.
- **Integrity checks** against poisoning (OWASP LLM04; NIST AI 100-2).
- **Retention and deletion** aligned to law and contract; plan for how rights requests reach derived data.
- **Privacy review** for each AI use: lawful basis, notices, impact assessment where required.
- **Protect the telemetry**: prompt and output logs often contain sensitive data.

EU AI Act Article 10 gives a data governance checklist for high-risk systems: design choices, collection processes and origin (and the original purpose for personal data), preparation operations, assumptions, availability and suitability, examination for biases and gaps. Use it as a model even outside the EU.

## Module 10: Continuous learning and adaption

AI systems and their threats change, so safety is not a one-time sign-off.

**Monitoring and feedback.** NIST MANAGE 4 asks for post-deployment monitoring plans with mechanisms to capture and evaluate input from users and other AI actors, appeal and override, decommissioning, incident response, recovery and change management. MANAGE 4.2 asks for measurable activities for continual improvement, integrated into AI system updates, including regular engagement with interested parties. MEASURE asks that systems be tested before deployment and regularly while in operation.

**Drift and degradation.** Performance can decline as data or conditions change. Define thresholds and alerts, schedule maintenance and retraining, and re-validate after any change, including vendor model updates.

**Learning from incidents.** Root cause analysis, shared lessons and updated controls close the loop. The EU AI Act expects the same discipline for high-risk systems: post-market monitoring by providers (Article 72) and reporting of serious incidents (Article 73).

**Keeping the program current.** Track new threats (NIST AI 100-2 and OWASP update their lists), new regulation and standards, and new capabilities. NIST notes AI RMF 1.0 is being revised, and CSA notes AICM v1.1 supersedes v1, so check versions. Train staff continuously: AI-specific awareness and acceptable use guidance reduce risky behavior that technical controls cannot catch.

**Continuous improvement as a management system.** ISO/IEC 42001's abstract describes establishing, implementing, maintaining and continually improving an AI management system, which is the same loop applied to the organization.

> **Exam habit:** answers about the long term mention monitoring, feedback, review cycles and updating controls, not one-off fixes.

---

## Key terms

- **Data memorization** - a model reproducing sensitive information from its training data when queried or attacked
- **Purpose specification** - stating the purpose for which data is collected and used
- **Data minimization** - using only the data necessary for the stated purpose
- **Data lineage** - the documented path of data from origin through every transformation
- **Sensitive information disclosure** - an LLM or its application revealing sensitive data it should not (OWASP LLM02)
- **Post-deployment monitoring** - ongoing collection and evaluation of performance and user input after release
- **Appeal and override** - mechanisms letting people contest or reverse an AI-supported outcome
- **Model drift** - decline in model performance as real-world conditions change
- **Decommissioning** - retiring an AI system, its models and data in a controlled way
- **Continual improvement** - repeated cycles of measurement and update to raise performance and safety over time
