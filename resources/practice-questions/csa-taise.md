---
last-updated: 2026-11-07
---

# CSA TAISE - Practice Questions

30 original scenario questions, 3 per module across the 10 TAISE modules (CSA weights the exam equally, 6 questions per module). These are original questions, not CSA exam content.

> **Cert page:** [exams/cloud-security-alliance/taise/](../../exams/cloud-security-alliance/taise/)

---

### Question 1 - Module 1: Introduction to AI
**Scenario:** Which feature best distinguishes an AI system from conventional software in the OECD definition?

A. It always runs on specialized graphics hardware
B. It follows only fixed rules written by developers
C. It requires a continuous internet connection
D. It infers from its input how to generate outputs such as predictions

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The definition centers on inference: outputs such as predictions, content, recommendations or decisions are generated from input, with varying autonomy and adaptiveness.
</details>

---

### Question 2 - Module 1: Introduction to AI
**Scenario:** NIST says a highly secure system that treats groups unfairly is undesirable. Which idea does this illustrate?

A. Trustworthiness characteristics must be balanced
B. Accuracy is the single measure of trustworthiness
C. Security matters more than any other property
D. Fairness is only a legal concern, not a design one

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** NIST stresses trade-offs among characteristics such as secure, fair, accurate and transparent. A comprehensive approach balances them.
</details>

---

### Question 3 - Module 1: Introduction to AI
**Scenario:** Why is AI risk management usually cross-functional?

A. Only legal staff understand AI systems well enough
B. Different teams own different life cycle stages
C. AI systems have no technical owners to consult
D. Regulation forbids engineers from taking part

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** AI actors in charge of one stage often lack visibility into others, so risk management needs collaboration across functions.
</details>

---

### Question 4 - Module 2: Generative AI Architecture and Design
**Scenario:** A generative AI application answers questions from company documents by looking them up at query time. What is this pattern?

A. Federated login across the identity providers
B. Quantization of the model weights
C. Backdoor poisoning of the training set
D. Retrieval-augmented generation (RAG) over internal documents

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** RAG retrieves relevant documents at query time and supplies them to the model. The retrieval store becomes a data asset needing access control.
</details>

---

### Question 5 - Module 2: Generative AI Architecture and Design
**Scenario:** Which layer of a generative AI application usually holds the embeddings used for similarity search?

A. The identity provider that signs users in to the application
B. The application layer that stores the system prompt
C. The retrieval layer or vector store
D. The billing system that tracks token usage by team

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Embeddings are stored in a vector database in the retrieval layer, which OWASP flags for specific weaknesses.
</details>

---

### Question 6 - Module 2: Generative AI Architecture and Design
**Scenario:** Which description fits a foundation model?

A. A model trained on broad data and adapted to many tasks
B. A model trained for exactly one narrow task by one team
C. A database index used to speed up relational queries
D. A rule engine written entirely by hand with no training data

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Foundation models are trained on broad data, generally with self-supervision, and adapted to many tasks.
</details>

---

### Question 7 - Module 3: Generative AI Use Cases and Applications
**Scenario:** A team uses a generative assistant to draft customer replies. Which risk is most characteristic of generated text?

A. Expiry of the TLS certificate on the public website
B. Loss of the user's password hash from the identity store
C. Confabulation, meaning confident but false output
D. Overheating of the data center cooling units overnight

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Confabulation is the production of confidently stated but erroneous content, a risk NIST lists for generative AI.
</details>

---

### Question 8 - Module 3: Generative AI Use Cases and Applications
**Scenario:** Which use case most clearly falls in a high-risk category under the EU AI Act?

A. A spell checker in a word processor
B. A tool that formats code indentation
C. A system that ranks job applicants
D. A recommendation of songs on a music app

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Recruitment and selection is an Annex III area, so such systems are high-risk.
</details>

---

### Question 9 - Module 3: Generative AI Use Cases and Applications
**Scenario:** Employees accept every AI suggestion without checking. Which NIST risk area is most relevant?

A. CBRN information or capabilities
B. Human-AI configuration (over-reliance)
C. Obscene or abusive content
D. Environmental impacts of training

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Human-AI configuration covers risks from how people interact with and rely on AI, including over-reliance.
</details>

---

### Question 10 - Module 4: Ethics, Transparency, and Explainability in AI
**Scenario:** Under the EU AI Act, which transparency duty applies to a system designed to interact directly with people?

A. Conceal that it is an AI in order to build trust
B. Delete their messages after every single reply
C. Require them to pay a fee before they may chat with it
D. Inform them they are interacting with an AI system

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Article 50 requires providers to ensure people are informed they are interacting with an AI system unless this is obvious.
</details>

---

### Question 11 - Module 4: Ethics, Transparency, and Explainability in AI
**Scenario:** What distinguishes explainability from interpretability in the NIST AI RMF?

A. Mechanisms of operation versus meaning of output
B. Explainability applies to hardware components only
C. Interpretability applies only to legal contracts
D. They are two words for exactly the same idea

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** NIST defines explainability as a representation of the mechanisms underlying operation and interpretability as the meaning of output in the context of its designed functional purpose.
</details>

---

### Question 12 - Module 4: Ethics, Transparency, and Explainability in AI
**Scenario:** Which control makes the principle of accountability real?

A. A faster network link between the data centers
B. A longer privacy notice published on the website
C. A larger model with many more parameters
D. A named owner who is answerable for each system's outcomes

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Accountability requires clear ownership of outcomes and governance.
</details>

---

### Question 13 - Module 5: AI Model Lifecycle and Threat Taxonomy
**Scenario:** An attacker slightly alters an image so a classifier mislabels it at deployment. What is this?

A. Evasion attack at deployment time
B. Data minimization
C. Backdoor poisoning
D. Fine-tuning

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Evasion modifies inputs at deployment time to cause misclassification.
</details>

---

### Question 14 - Module 5: AI Model Lifecycle and Threat Taxonomy
**Scenario:** Which stage is most exposed to data poisoning?

A. Invoice processing for cloud spend
B. Data collection and the training stage
C. Hardware retirement and disposal
D. Office onboarding of new hires

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Poisoning interferes with training data or parameters, so data collection and training are the exposed stages.
</details>

---

### Question 15 - Module 5: AI Model Lifecycle and Threat Taxonomy
**Scenario:** Hidden instructions in a retrieved web page change an assistant's behavior. Which OWASP LLM risk is this?

A. LLM10 Unbounded Consumption of resources
B. System Prompt Leakage to end users
C. Misinformation in generated answers
D. LLM01 Prompt Injection

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Indirect prompt injection places instructions in data the application retrieves. OWASP lists Prompt Injection as LLM01.
</details>

---

### Question 16 - Module 6: Model Governance, Risk Management, and Compliance
**Scenario:** Which item is a certifiable management system standard for AI?

A. OECD AI Principles
B. ISO/IEC 42001 AI management system standard
C. OWASP LLM Top 10
D. NIST AI 100-2

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** ISO/IEC 42001 specifies requirements for an AI management system that can be audited and certified.
</details>

---

### Question 17 - Module 6: Model Governance, Risk Management, and Compliance
**Scenario:** How many control objectives and domains does CSA's AI Controls Matrix v1 page state?

A. 12 across 3 domains
B. 50 across 5 domains
C. 1,000 across 40 domains
D. 243 across 18 domains

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** CSA's page states 243 control objectives distributed across 18 security domains.
</details>

---

### Question 18 - Module 6: Model Governance, Risk Management, and Compliance
**Scenario:** Which describes the NIST AI RMF function GOVERN?

A. Only the model training step of the life cycle
B. Cross-cutting policy, accountability and culture
C. Only the purchase of hardware for the data center
D. Only incident response after a release has happened

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** GOVERN is cross-cutting and infused throughout risk management, enabling the other functions.
</details>

---

### Question 19 - Module 7: Introduction to AI Security and Safety
**Scenario:** What are the two primary information security risks NIST AI 600-1 notes for generative AI?

A. Lower electricity use and smaller models in production
B. Faster typing speeds and bigger monitor screens
C. Fewer users and less training data than before
D. Easier offensive cyber operations and a larger attack surface

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** NIST says generative AI can ease offensive cyber operations and also expands the attack surface through issues like prompt injection and data poisoning.
</details>

---

### Question 20 - Module 7: Introduction to AI Security and Safety
**Scenario:** An agent granted far more permissions than its task needs is most associated with which OWASP risk?

A. Vector and Embedding Weaknesses
B. LLM10 Unbounded Consumption of resources
C. LLM06 Excessive Agency
D. Misinformation in generated answers

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Excessive Agency is rooted in excessive functionality, permissions or autonomy.
</details>

---

### Question 21 - Module 7: Introduction to AI Security and Safety
**Scenario:** Which approach best reduces prompt injection impact?

A. Layered controls such as least privilege and approvals
B. Longer prompts that include more detailed instructions
C. A single input filter with no other controls at all
D. Turning off all logging to protect user privacy

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** No single filter is sufficient; limiting what a manipulated model can do and detecting abuse works better.
</details>

---

### Question 22 - Module 8: Cloud and AI Security
**Scenario:** A company builds an app on a cloud-hosted foundation model. What is the right first step to assign security duties?

A. Wait for an incident to reveal the split
B. Identify its role in the AI stack
C. Assume nothing is shared with the provider
D. Assume the provider handles everything

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The AICM defines roles by layer; each party covers controls within its layer, so identify your role and verify the rest.
</details>

---

### Question 23 - Module 8: Cloud and AI Security
**Scenario:** Which OWASP risk is a particular concern with pay-per-use cloud AI endpoints?

A. Supply Chain weaknesses in third-party models
B. System Prompt Leakage to end users
C. LLM10 Unbounded Consumption of resources
D. Misinformation in generated answers

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Unbounded consumption means excessive uncontrolled inference leading to denial of service and economic loss.
</details>

---

### Question 24 - Module 8: Cloud and AI Security
**Scenario:** Which cloud control best protects model endpoints?

A. Least-privilege identities and network controls
B. Shared long-lived administrator keys for every team
C. Disabling all logging in order to save cost
D. Open public access to the endpoint for convenience

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Cloud IAM and network controls apply to AI endpoints as to any workload.
</details>

---

### Question 25 - Module 9: Data Security and Privacy AI Systems
**Scenario:** A language model repeats personal data from its training set when attacked. Which phenomenon is this?

A. Model compression to reduce size
B. Data memorization of training examples
C. Batch scheduling of nightly jobs
D. Edge deployment on user devices

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** NIST AI 600-1 describes data memorization as models revealing sensitive training information during adversarial attacks.
</details>

---

### Question 26 - Module 9: Data Security and Privacy AI Systems
**Scenario:** Which control best addresses the use of personal data in a fine-tuning set?

A. Classify, approve and minimize the data before any use
B. Turn off access controls on the dataset to move faster
C. Add more personal data to the set to improve accuracy
D. Delete the model card so nobody asks questions

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Data governance before training: minimization, lawful basis, approval and lineage.
</details>

---

### Question 27 - Module 9: Data Security and Privacy AI Systems
**Scenario:** Why must prompt and output logs be protected?

A. They are published openly by law
B. They can hold sensitive personal or proprietary data
C. They are always empty after the session
D. They cannot be used in any investigation

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Logs support investigation but hold sensitive content, so they need retention limits and access control.
</details>

---

### Question 28 - Module 10: Continuous Learning and Adaption
**Scenario:** What does NIST MANAGE 4 call for after deployment?

A. No monitoring unless a regulator specifically asks for it
B. Removal of the user feedback channels to cut noise
C. Post-deployment monitoring with feedback and incident plans
D. A single review at launch and no checks afterward

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** MANAGE 4.1 asks for post-deployment monitoring plans with mechanisms for input, appeal and override, decommissioning, incident response, recovery and change management.
</details>

---

### Question 29 - Module 10: Continuous Learning and Adaption
**Scenario:** Model accuracy slowly declines as customer behavior changes. What is the best long-term response?

A. Increase the model's randomness setting to compensate
B. Delete the monitoring alerts to reduce noise
C. Monitor for drift and retrain under change control
D. Ignore it unless users complain very loudly

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Drift is addressed by monitoring thresholds and scheduled maintenance, then re-validation.
</details>

---

### Question 30 - Module 10: Continuous Learning and Adaption
**Scenario:** Which statement about keeping an AI program current is best?

A. Track new threats and rules, then update controls
B. Avoid version numbers in documents to prevent confusion
C. Stop training staff once they have passed the course
D. Lock the policy in place unchanged for several years

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Threat lists, laws and frameworks change; continual improvement keeps the program current.
</details>

---
