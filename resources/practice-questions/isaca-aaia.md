---
last-updated: 2026-11-07
---

# ISACA AAIA - Practice Questions

28 original scenario questions weighted to the three domains of the AAIA exam content outline: Domain 1 (33%) 9 questions, Domain 2 (46%) 13, Domain 3 (21%) 6. These are original questions, not ISACA exam content.

> **Cert page:** [exams/isaca/aaia/](../../exams/isaca/aaia/)

---

### Question 1 - Domain 1: AI Governance and Risk
**Scenario:** During an audit of a credit decision model, the data science team says the business owns it, the business says IT owns it, and nobody reviews performance. What is the primary finding?

A. An outdated network diagram in the architecture file
B. Excess cloud spending on model training runs beyond the approved budget
C. Undefined ownership of AI risk, controls and decisions
D. Insufficient volume of training data for the model

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Ownership of AI-related risk, controls, procedures and decisions is a governance expectation. The facts show no accountable owner and no performance review.
</details>

---

### Question 2 - Domain 1: AI Governance and Risk
**Scenario:** Which source of audit criteria is a certifiable management system standard for AI?

A. ISO/IEC 42001
B. OWASP Top 10 for LLM Applications list
C. NIST AI RMF applied by the organization
D. OECD AI Principles adopted by member governments

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** ISO/IEC 42001 specifies requirements for an AI management system that an organization can be assessed against. The others are principles, a voluntary framework and a risk catalog.
</details>

---

### Question 3 - Domain 1: AI Governance and Risk
**Scenario:** An auditor wants indicators that signal rising AI risk before an incident occurs. Which type of metric fits best?

A. Key risk indicators such as rising drift or override rates
B. Share of the AI budget spent on staff training courses each year
C. Number of employees in the data science team
D. Total revenue recognized in the quarter

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** KRIs are leading indicators of risk exposure. Training spend, headcount and revenue do not signal rising AI risk.
</details>

---

### Question 4 - Domain 1: AI Governance and Risk
**Scenario:** Which statement about the NIST AI Risk Management Framework is correct?

A. It applies only to generative AI systems
B. It is voluntary guidance with four functions
C. It is a binding law that carries fines for breaches
D. It is a certification standard audited by accredited bodies

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The AI RMF is a voluntary framework. Binding duties come from laws such as the EU AI Act, and certification is associated with ISO/IEC 42001.
</details>

---

### Question 5 - Domain 1: AI Governance and Risk
**Scenario:** A company used customer data for a new AI training purpose that was not in its notices. Which privacy principle is most directly in question?

A. Availability of the training environment
B. Purpose limitation
C. Fault tolerance of the training cluster
D. Non-repudiation of training job submissions

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Using data for a new purpose beyond what was stated raises purpose limitation and lawful basis. The other terms are security or resilience concepts.
</details>

---

### Question 6 - Domain 1: AI Governance and Risk
**Scenario:** Before testing any AI controls in a new engagement, what should the auditor do first?

A. Ask management to approve the conclusions in advance
B. Draft the final report conclusions early
C. Run technical tests on the models immediately
D. Understand the inventory, risks and requirements

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Risk-based planning comes first: understand the subject, set objectives, scope and criteria. Testing and reporting follow.
</details>

---

### Question 7 - Domain 1: AI Governance and Risk
**Scenario:** In the EU AI Act, which description best matches a provider?

A. A national regulator that supervises AI systems in the market
B. Anyone who uses an AI system in a personal non-professional activity
C. Someone who develops or commissions an AI system and sells it under its own name
D. A customer who reads a reply from a chatbot

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A provider develops or has an AI system developed and places it on the market or puts it into service under its own name or trademark. Deployers use systems under their authority.
</details>

---

### Question 8 - Domain 1: AI Governance and Risk
**Scenario:** An organization says its AI system is fair, citing a statement from the vendor. How should the auditor treat this?

A. As sufficient evidence on its own
B. As irrelevant to the audit because vendors are the experts here
C. As an assertion that needs supporting evidence
D. As proof that the regulator accepts the system

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Vendor or management statements are representations. Reliable evidence comes from underlying tests and independent analysis.
</details>

---

### Question 9 - Domain 1: AI Governance and Risk
**Scenario:** Which EU AI Act article lists practices that are prohibited outright?

A. Article 12 on record-keeping
B. Article 50 on transparency
C. Article 99 on penalties
D. Article 5

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Article 5 sets out prohibited AI practices. Article 50 covers transparency duties, Article 12 record-keeping, and Article 99 penalties.
</details>

---

### Question 10 - Domain 2: AI Operations
**Scenario:** A model was retrained and released with no record of approval or testing. Which program should the auditor primarily evaluate?

A. Change management as applied to AI
B. Facilities and physical access management
C. Payroll and human resources administration
D. Procurement of office equipment and supplies

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Retraining is a change to a production system. Approval, testing and rollback are change management controls.
</details>

---

### Question 11 - Domain 2: AI Operations
**Scenario:** Which dataset defect most directly leads to biased model decisions?

A. A short password on a service account
B. A slow network link between the two primary data centers
C. An expired certificate on the web server
D. Unrepresentative or biased training data

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Data defects become model defects. Training data that is not representative of the people affected produces biased decisions.
</details>

---

### Question 12 - Domain 2: AI Operations
**Scenario:** An attacker inserts a trigger pattern into training samples so inputs with the pattern are misclassified. What is this?

A. A denial of service on the model endpoint
B. Backdoor poisoning
C. A phishing attack on data scientists
D. An evasion attack at deployment time

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Backdoor poisoning plants a trigger during training so that inputs containing it are misclassified. Evasion alters inputs at deployment time.
</details>

---

### Question 13 - Domain 2: AI Operations
**Scenario:** Human reviewers of AI decisions override the system in almost zero percent of cases. What should the auditor consider?

A. That the reviewers are overstaffed and the team should be reduced
B. Whether oversight is effective or merely a rubber stamp
C. That the system must therefore be perfect
D. That oversight can be removed to save cost

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A near-zero override rate may mean the system is excellent or that reviewers lack time, training or authority. The auditor should test the quality of oversight.
</details>

---

### Question 14 - Domain 2: AI Operations
**Scenario:** Which test set best supports an unbiased assessment of a model's performance?

A. Data chosen by the developer to show good results
B. Only data from the previous calendar year
C. Held-out data independent of training data
D. The same data that was used for training

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Independent held-out data avoids overstating performance. Reusing training data or hand-picked samples hides weaknesses.
</details>

---

### Question 15 - Domain 2: AI Operations
**Scenario:** A language model application inserts model output directly into a database query. Which OWASP LLM risk is most relevant?

A. Improper Output Handling
B. Unbounded Consumption of resources
C. System Prompt Leakage to users
D. Misinformation in generated answers

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Improper output handling is insufficient validation and sanitization of model output before it is passed downstream.
</details>

---

### Question 16 - Domain 2: AI Operations
**Scenario:** An AI agent has permissions to approve payments, delete records and email customers, though its task is drafting replies. What is the auditor's concern?

A. Low accuracy on the drafting task
B. Excessive agency from excess functionality and permissions
C. Poor interface design that makes reviews take longer than needed
D. High operating cost of the agent

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Excessive agency arises from excessive functionality, permissions or autonomy. Least privilege should limit what the agent can do.
</details>

---

### Question 17 - Domain 2: AI Operations
**Scenario:** Which evidence best shows a change to an AI model was properly controlled?

A. The size of the model file before and after
B. A manager's verbal assurance that it was approved
C. The vendor's brochure describing its process
D. Sampled change tickets tied to approvals and test results

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Direct documentary evidence linking changes to approvals and tests is reliable. Verbal assurance and marketing material are weak.
</details>

---

### Question 18 - Domain 2: AI Operations
**Scenario:** During an AI incident the team wants to preserve what is needed for investigation. Which items should be retained?

A. Nothing at all, in order to protect the privacy of the users involved
B. Only a screenshot of the user interface
C. Prompts, outputs, model version and relevant logs
D. Only the final summary email to executives

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Investigation needs the inputs, outputs, version and logs. Retention should respect privacy and policy, but cannot be zero.
</details>

---

### Question 19 - Domain 2: AI Operations
**Scenario:** For deployers of high-risk systems under the EU AI Act, which duty is in Article 26?

A. Assign competent human oversight and keep the logs
B. Register as a general-purpose model provider
C. Publish the full source code of the system to the public
D. Develop the model from scratch themselves

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Article 26 requires deployers to use systems per instructions, assign competent human oversight, monitor operation and keep logs for an appropriate period of at least six months.
</details>

---

### Question 20 - Domain 2: AI Operations
**Scenario:** A vendor updates the underlying model without notice, and downstream quality falls. Which control gap is most direct?

A. Insufficient office space for the AI team
B. Late payroll processing for the contractors on the team
C. No policy on visitor parking
D. No change notification or version control for the vendor model

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Vendor changes need notification and version management so the organization can re-validate before relying on the new behavior.
</details>

---

### Question 21 - Domain 2: AI Operations
**Scenario:** Which statement about NIST AI 100-2 attack goals is correct?

A. It lists only physical attacks on the hardware in data centers
B. It sets pricing guidance for AI services
C. It covers only firewall rule design
D. It groups attacks by availability, integrity and privacy goals

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** NIST AI 100-2 organizes attacks on predictive AI by the attacker's goal: availability, integrity and privacy.
</details>

---

### Question 22 - Domain 2: AI Operations
**Scenario:** A privacy-minded team keeps full prompt logs forever. What is the auditor's best observation?

A. Logs may hold sensitive data and need retention limits and protection
B. Logs should always be kept forever for safety
C. Logs should never be created at all, because they are risky
D. Logs are not usable as audit evidence

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Logs support investigation but can contain personal or proprietary data, so retention and access controls are needed.
</details>

---

### Question 23 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** To test whether a model treats a small demographic group fairly, which sampling approach is most suitable?

A. A very small random sample of all records in the population
B. A stratified sample that ensures the group is represented
C. Whichever records the auditee finds easiest to provide
D. Only the first ten records in the file

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A plain random sample may include too few members of a small group to detect a difference. Stratification ensures coverage.
</details>

---

### Question 24 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** Auditors use a generative tool to summarize auditee documents. What is the right treatment of the summary?

A. As final audit evidence once it is produced
B. As a lead to be verified against source documents
C. As unnecessary to review because it is automated
D. As a substitute for the auditor's professional judgment

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Generative tools can produce confident errors. The summary points to areas to check, and a reviewer remains accountable.
</details>

---

### Question 25 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** Which evidence is generally the most reliable?

A. Unsigned notes taken at a prior meeting with the auditee
B. Marketing materials from the vendor
C. Evidence obtained directly by the auditor from independent sources
D. Verbal statements from the auditee in interviews

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Direct, independent, documentary evidence is the strongest. Representations and marketing materials are weaker.
</details>

---

### Question 26 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** Before relying on a data extract for analytics, what should the auditor do?

A. Reconcile record counts and totals to the source
B. Use it only if the file is large enough to look representative
C. Delete apparent duplicates without noting it
D. Assume it is complete if the system produced it

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Confirming completeness and accuracy of the data is the first step in analytics. Size does not prove quality.
</details>

---

### Question 27 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** Which practice best protects auditor independence when reporting an AI control weakness?

A. Implement the fix personally to speed things up
B. Leave the weakness out of the report to avoid conflict
C. Let the auditee reword the finding freely
D. Recommend the outcome and leave the fix design to management

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Auditors report and recommend; management owns remediation. Implementing the fix or letting auditees alter findings compromises independence.
</details>

---

### Question 28 - Domain 3: AI Auditing Tools and Techniques
**Scenario:** A good audit finding on an AI system should include which element?

A. A guess at the cause that has not been tested or confirmed
B. A list of the auditee's preferred suppliers
C. The criterion that was not met, such as a policy clause
D. Only the auditor's general opinion

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A finding is anchored in a criterion, evidence, cause and effect. The criterion explains why something is a deficiency.
</details>

---
