---
last-updated: 2026-11-07
---

# ISACA AAISM - Practice Questions

26 original scenario questions weighted to the three domains of the AAISM exam content outline (June 2025): Domain 1 (31%) 8 questions, Domain 2 (31%) 8, Domain 3 (38%) 10. These are original questions, not ISACA exam content.

> **Cert page:** [exams/isaca/aaism/](../../exams/isaca/aaism/)

---

### Question 1 - Domain 1: AI Governance and Program Management
**Scenario:** A business unit has started using several AI tools on its own. The security manager must first understand the exposure. What is the best first step?

A. Publish an ethics statement and wait for staff to comply
B. Build an inventory of AI tools, models and data with owners
C. Buy an AI monitoring product before knowing what needs monitoring
D. Block every AI domain at the firewall and close the issue

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** You cannot govern or protect what you have not identified. An inventory with owners comes before blocking, tooling or statements, and it feeds risk assessment and policy.
</details>

---

### Question 2 - Domain 1: AI Governance and Program Management
**Scenario:** Which framework is a certifiable standard for an AI management system?

A. OWASP Top 10 for LLM Applications
B. OECD AI Principles
C. ISO/IEC 42001
D. NIST AI RMF

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** ISO/IEC 42001 specifies requirements for an AI management system and can be audited. The NIST AI RMF and OECD principles are voluntary guidance, and the OWASP list is a risk catalog.
</details>

---

### Question 3 - Domain 1: AI Governance and Program Management
**Scenario:** In the NIST AI RMF, which function is described as cross-cutting and infused throughout risk management?

A. MEASURE
B. MAP
C. GOVERN
D. MANAGE

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** GOVERN sets policy, accountability and culture and supports the other three functions. MAP, MEASURE and MANAGE address context, assessment and treatment.
</details>

---

### Question 4 - Domain 1: AI Governance and Program Management
**Scenario:** Employees are pasting customer data into an unapproved chatbot. Which policy addition most directly addresses this?

A. An AI acceptable use policy defining approved tools and permitted data
B. A stronger password policy for the identity provider and all accounts
C. A data loss prevention rule for outbound email attachments only
D. A backup retention schedule covering all production databases

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** An AI acceptable use policy tells staff which tools and data are allowed. Pair it with approved alternatives and training. The other options do not address the behavior.
</details>

---

### Question 5 - Domain 1: AI Governance and Program Management
**Scenario:** An AI incident involves a retrieval assistant exposing confidential HR content. Which first action best fits the incident handling life cycle?

A. Contain by restricting the assistant's retrieval scope or disabling it
B. Delete the conversation logs so the content cannot be retrieved again
C. Notify all customers publicly before the scope is understood
D. Retrain the model immediately on a larger and cleaner dataset

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Containment limits further exposure while evidence is preserved. Retraining is not the fix for an access control gap, early public statements skip assessment, and deleting logs destroys evidence.
</details>

---

### Question 6 - Domain 1: AI Governance and Program Management
**Scenario:** Business continuity planning for an AI-enabled process should most specifically address which question?

A. Which team owns the visual design of the monitoring dashboard
B. What the business does if the AI is unavailable or unreliable
C. Which vendor brand is shown to customers on the AI interface
D. How many licenses the company bought for the AI service this year

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Continuity planning defines fallback processes when the AI is down or wrong. The other options do not affect resilience.
</details>

---

### Question 7 - Domain 1: AI Governance and Program Management
**Scenario:** Which statement about the EU AI Act is most accurate for a security manager?

A. It replaces privacy law wherever AI processes personal data
B. It sets risk-based duties for providers and deployers
C. It applies only to consumer chatbots sold to the public
D. It has no fines and relies only on voluntary codes of conduct

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The Act uses risk tiers, assigns duties by role, and requires accuracy, robustness and cybersecurity for high-risk systems (Article 15). It sets fines in Article 99 and does not replace privacy law.
</details>

---

### Question 8 - Domain 1: AI Governance and Program Management
**Scenario:** Which metric is most useful to management for judging the maturity of an AI security program?

A. Total hours employees spend using approved AI tools
B. Number of AI vendor demonstrations attended by staff
C. Share of AI systems inventoried, owned and risk-assessed
D. Number of AI-related pages in the security policy library

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Coverage of inventory, ownership and assessment shows control over exposure. Activity counts without outcomes mislead.
</details>

---

### Question 9 - Domain 2: AI Risk and Opportunity Management
**Scenario:** An attacker alters pixels in an image so a classifier mislabels it, with the change barely visible to people. Which attack class is this?

A. Backdoor poisoning of the training set
B. Model extraction through repeated queries
C. Energy-latency attack on availability
D. Evasion

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Evasion modifies inputs at deployment time to cause misclassification. Poisoning acts at training time, and energy-latency attacks target availability.
</details>

---

### Question 10 - Domain 2: AI Risk and Opportunity Management
**Scenario:** Hidden text on a web page tells a summarization tool to send the user's data elsewhere. What is this?

A. A denial of service against the web server
B. Model drift caused by changing data
C. Indirect prompt injection
D. Backdoor poisoning of the training set

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Instructions injected into data the application retrieves are indirect prompt injection. The right response reduces what the tool can do and adds approval for data egress.
</details>

---

### Question 11 - Domain 2: AI Risk and Opportunity Management
**Scenario:** A team proposes deploying a model whose error rate exceeds the business's stated tolerance. What should the security manager do?

A. Accept the risk on the team's behalf to keep the project moving
B. Escalate to the risk owner for treatment or a formal decision
C. Leave the error rate out of the project status report
D. Deploy now and plan to fix the error rate in a later release

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Risk acceptance belongs to the risk owner within appetite. The manager makes the risk visible and recommends treatment.
</details>

---

### Question 12 - Domain 2: AI Risk and Opportunity Management
**Scenario:** The term 'opportunity' in AI risk management most nearly means which of the following?

A. Selling AI-enabled products to new customers
B. Choosing the AI vendor that has the lowest price
C. Ignoring risk entirely whenever the expected benefit is large
D. Weighing AI benefits against risks and non-AI alternatives

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** AI risk management weighs benefits and risks together, and considers whether a simpler non-AI approach would give the benefit with less risk.
</details>

---

### Question 13 - Domain 2: AI Risk and Opportunity Management
**Scenario:** A vendor refuses to say whether customer inputs are used for model training. What is the best response?

A. Accept the vendor's marketing summary as sufficient assurance
B. Cancel every AI project in the company
C. Require contract terms on data use and verify the evidence
D. Proceed because most vendors are assumed not to train on inputs

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Embed requirements in the contract and verify them. Assumptions and blanket bans are both poor answers.
</details>

---

### Question 14 - Domain 2: AI Risk and Opportunity Management
**Scenario:** Which activity best identifies weaknesses in an AI application before attackers do?

A. Reducing logging to cut storage costs and noise
B. Relying on the vendor's published security brochure
C. Waiting for users to report problems after release
D. Authorized red teaming and threat modeling

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Authorized adversarial testing and threat modeling find weaknesses proactively. Waiting or removing logs reduces visibility.
</details>

---

### Question 15 - Domain 2: AI Risk and Opportunity Management
**Scenario:** Which NIST AI 100-2 attack goal covers leakage of training data or model weights?

A. Energy-latency attack
B. Privacy compromise
C. Availability breakdown
D. Integrity violation

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Privacy compromise is the unintended leakage of restricted information, including training data, weights or architecture.
</details>

---

### Question 16 - Domain 2: AI Risk and Opportunity Management
**Scenario:** A model supplier updates its model without notice and downstream quality drops. Which contract term would have helped most?

A. A clause granting the buyer on-site visits to vendor offices
B. Change notification and version pinning
C. A longer payment term of ninety days on invoices
D. A clause giving the vendor co-marketing rights on reports

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Notice of changes and version pinning let you re-validate before the change reaches production.
</details>

---

### Question 17 - Domain 3: AI Technologies and Controls
**Scenario:** Which design choice best limits damage if an LLM-based agent is manipulated?

A. Least-privilege tools with human approval for high-impact actions
B. Grant administrator rights so the agent is never blocked by permissions
C. Let it call any internal API it decides is useful
D. Disable action logging to protect user privacy

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Limiting functionality, permissions and autonomy reduces what a manipulated model can do. This is the core mitigation for excessive agency.
</details>

---

### Question 18 - Domain 3: AI Technologies and Controls
**Scenario:** Model output is inserted directly into a web page and a database query. Which principle is being violated?

A. Rotate the encryption keys protecting the model more often
B. Encrypt all application data at rest in the database
C. Treat model output as untrusted input and validate it
D. Require strong passwords for every user of the application

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Improper output handling occurs when model output goes downstream without validation or sanitization. Treat it like any untrusted input.
</details>

---

### Question 19 - Domain 3: AI Technologies and Controls
**Scenario:** A retrieval assistant must not show a user documents they cannot normally open. Where should the control be enforced?

A. At retrieval, filtering by the requesting user's permissions
B. After the answer has already been displayed to the user
C. By hiding links in the layout of the user interface
D. Only by wording the system prompt carefully

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Access control belongs in the retrieval layer. A prompt instruction is not a security boundary.
</details>

---

### Question 20 - Domain 3: AI Technologies and Controls
**Scenario:** Training data for a fine-tune comes from an unknown source. Which control best reduces poisoning risk?

A. Train first and check the data quality afterwards
B. Skip validation steps to meet the project deadline
C. Assume data from public sources is always safe to use
D. Verify provenance and integrity and record lineage before use

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Provenance and integrity checks guard against manipulated data, and lineage supports investigation.
</details>

---

### Question 21 - Domain 3: AI Technologies and Controls
**Scenario:** Which monitoring signal best indicates possible abuse of an LLM application's availability or cost?

A. Monthly count of pages printed in the office
B. Number of employee accounts created per quarter
C. Number of languages the interface is translated into
D. Spikes in token or compute use per user

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Unbounded consumption shows up as excessive, uncontrolled inference. Usage anomalies are the signal.
</details>

---

### Question 22 - Domain 3: AI Technologies and Controls
**Scenario:** A system prompt contains database credentials. What is the right correction?

A. Move secrets to a secrets store and enforce access outside the model
B. Rename the prompt file to something obscure and restrict the folder
C. Instruct the model never to reveal the credentials to users
D. Make the prompt longer so the credentials are harder to find

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** System prompts can be leaked, so they must not hold secrets. Enforce access outside the model.
</details>

---

### Question 23 - Domain 3: AI Technologies and Controls
**Scenario:** Which statement about human oversight of AI is best?

A. It should be risk-based, with reviewers who can actually intervene
B. It means a person must personally read every output before use
C. It is unnecessary whenever the model reports high accuracy
D. It is the model vendor's responsibility, not the deployer's

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Oversight scales with risk and only works if reviewers can actually intervene.
</details>

---

### Question 24 - Domain 3: AI Technologies and Controls
**Scenario:** After a model memorizes and reveals personal data from its training set, which risk area is primarily involved?

A. Intellectual property of the user interface
B. Data privacy
C. Obscene or abusive content
D. Environmental impact of training

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Memorization leading to disclosure of personal information is a data privacy risk described in NIST AI 600-1.
</details>

---

### Question 25 - Domain 3: AI Technologies and Controls
**Scenario:** Which action best protects the integrity of a deployed model's weights?

A. Restrict access, verify artifacts and log changes
B. Email copies of the weights to developers for convenience
C. Rename the weight files regularly to confuse attackers
D. Store them in a shared network folder open to all staff

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Weights are sensitive assets. Access control, artifact verification and change logging protect integrity.
</details>

---

### Question 26 - Domain 3: AI Technologies and Controls
**Scenario:** Prompt injection continues despite an input filter. What is the best conclusion?

A. Add a second identical filter and consider the risk closed
B. Disable the affected business function permanently
C. Accept it because no filter can ever be perfect
D. Layer controls: limit privileges, isolate content, add approvals

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** No single filter solves prompt injection. Controls that limit impact and detect abuse work together.
</details>

---
