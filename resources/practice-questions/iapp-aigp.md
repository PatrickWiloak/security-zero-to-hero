---
last-updated: 2026-11-07
---

# IAPP AIGP - Practice Questions

24 original scenario questions weighted to the four domains of the v2.1 body of knowledge (effective 2 February 2026): Domain I (16-20 of 100 exam questions) 5 questions, Domain II (19-23) 6, Domain III (21-25) 6, Domain IV (21-25) 7. These are original questions, not IAPP exam content.

> **Cert page:** [exams/iapp/aigp/](../../exams/iapp/aigp/)

---

### Question 1 - Domain I: Foundations of AI Governance
**Scenario:** A company's governance board has only lawyers. A recent model failure was a data pipeline fault nobody on the board could assess. Which improvement fits best?

A. Add technical, security, privacy and business roles to the board
B. Replace the board with the data science team and drop legal review
C. Move all governance decisions to the AI vendor's support team
D. Remove the board and rely on a written policy with no named owner

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Cross-functional collaboration brings diverse expertise and perspective. Replacing lawyers with engineers just reverses the gap, and outsourcing or removing oversight removes accountability.
</details>

---

### Question 2 - Domain I: Foundations of AI Governance
**Scenario:** Which characteristic of AI most directly explains why one error can reach millions of people before it is noticed?

A. Speed and scale
B. Probabilistic output
C. Opacity
D. Data dependency

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Speed and scale means a flaw repeats widely and fast. Opacity is about explaining decisions, data dependency about reliance on data quality, and probabilistic output about variable results.
</details>

---

### Question 3 - Domain I: Foundations of AI Governance
**Scenario:** A retailer buys a ready-made chatbot and uses it for customer support under its own brand name only in its app; the vendor developed and markets the chatbot under the vendor's name. In EU AI Act terms, what is the retailer?

A. Distributor that only resells the vendor's product unchanged
B. Importer bringing the system in from outside the EU
C. Provider
D. Deployer

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The retailer uses an AI system under its authority, which is a deployer. It would become a provider if it placed the system on the market under its own name or trademark as the developer.
</details>

---

### Question 4 - Domain I: Foundations of AI Governance
**Scenario:** A small non-profit uses one low-risk AI writing aid. A consultant proposes a full enterprise AI governance office with a dozen committees. What is the best response?

A. Adopt it in full to be safe
B. Ban the writing aid
C. Do nothing, because small organizations are exempt
D. Scale the approach to size, maturity and risk tolerance

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Approaches should differ by organization size, maturity, industry and risk tolerance. Proportionate governance is the expected answer, not maximal or none.
</details>

---

### Question 5 - Domain I: Foundations of AI Governance
**Scenario:** Security rules at a firm require a review for any new software, but AI use is not covered. What is the most efficient first step?

A. Wait for a law to require it
B. Evaluate and update existing data, security and IP policies for AI
C. Write an entirely new standalone policy suite ignoring existing ones
D. Delegate the question to employees

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The blueprint calls for updating existing policies for AI rather than starting from nothing. Waiting or delegating leaves a gap.
</details>

---

### Question 6 - Domain II: Laws, Standards and Frameworks
**Scenario:** A system scores job applicants for a European employer. Under the EU AI Act which category does it most likely fall into?

A. Minimal risk
B. Outside the Act
C. High-risk
D. Prohibited

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Recruitment and selection of people is an Annex III area, so the system is high-risk. It is not on the Article 5 prohibited list merely because it ranks candidates.
</details>

---

### Question 7 - Domain II: Laws, Standards and Frameworks
**Scenario:** Which of these practices is prohibited outright by Article 5 of the EU AI Act?

A. A spam filter that sorts incoming company email
B. Untargeted scraping of facial images to build a face recognition database
C. A customer chatbot that clearly tells users it is an AI system
D. A CV ranking tool whose output a recruiter reviews

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Article 5 bans AI systems that create or expand facial recognition databases through untargeted scraping of facial images from the internet or CCTV. The other uses are either allowed or regulated differently.
</details>

---

### Question 8 - Domain II: Laws, Standards and Frameworks
**Scenario:** Which NIST AI RMF function is described as cross-cutting and infused throughout risk management?

A. MANAGE
B. MAP
C. GOVERN
D. MEASURE

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** GOVERN cuts across and enables the other functions, covering policy, accountability and culture. MAP sets context, MEASURE assesses and monitors, MANAGE treats risk.
</details>

---

### Question 9 - Domain II: Laws, Standards and Frameworks
**Scenario:** A company wants a standard against which an external auditor could certify its AI program. Which fits?

A. NIST AI RMF
B. ISO/IEC 42001
C. A vendor white paper
D. OECD AI Principles

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** ISO/IEC 42001 is a management system standard organizations can be assessed against. NIST AI RMF and OECD Principles are voluntary guidance without certification.
</details>

---

### Question 10 - Domain II: Laws, Standards and Frameworks
**Scenario:** A lender uses a model that systematically gives worse terms to a protected group, though no one intended it. Which body of existing law is most directly engaged?

A. Trademark law on brand names
B. Product liability law for design defects
C. Nondiscrimination law
D. Antitrust law on market dominance

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Nondiscrimination law applies to AI in credit and lending, and can apply without intent. Product liability concerns defects in products, which is a weaker fit here.
</details>

---

### Question 11 - Domain II: Laws, Standards and Frameworks
**Scenario:** Under the EU AI Act, which statement about general-purpose AI model providers is correct?

A. Their obligations apply only to open-source models
B. Only deployers have duties
C. They have no obligations
D. They keep technical documentation and publish a training content summary

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Article 53 requires technical documentation, information for downstream providers, a copyright policy and a public training content summary. Certain duties are relaxed for some open-source models, but not removed entirely.
</details>

---

### Question 12 - Domain III: Governing AI Development
**Scenario:** Before building a loan approval model, the team wants to know who might be harmed and how likely it is. Which activity does this describe?

A. Performing an impact assessment
B. Red teaming the production model
C. Writing a model card
D. Retraining the model

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** An impact assessment asks who could be harmed, how likely and how badly. Red teaming and retraining happen later, and a model card documents a finished model.
</details>

---

### Question 13 - Domain III: Governing AI Development
**Scenario:** A team plans to train on a scraped dataset. The governance reviewer's first questions should be about which?

A. Which file format the dataset is stored in
B. Lawful rights to use the data and its provenance
C. The marketing name chosen for the finished model
D. The hourly cost of the training hardware

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Data governance requires assessing lawful rights to collect and use data and documenting lineage and provenance. Format and cost matter less than whether use is permitted.
</details>

---

### Question 14 - Domain III: Governing AI Development
**Scenario:** Which test is best suited to checking whether outcomes differ across demographic groups?

A. Integration test of connected components
B. Unit test of a single code function
C. Load test of peak request volume
D. Bias test

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Bias testing compares outcomes across groups. Unit and integration tests check code behavior and connections.
</details>

---

### Question 15 - Domain III: Governing AI Development
**Scenario:** A team sets its accuracy threshold only after seeing test results. What is the governance concern?

A. Only the vendor's sales team may set any thresholds
B. Higher thresholds are always unlawful under privacy rules
C. Thresholds are unnecessary if the team trusts the model
D. Thresholds should be defined before testing to avoid cherry-picking

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Metrics and thresholds define good enough before testing. Setting them afterwards lets results shape the standard.
</details>

---

### Question 16 - Domain III: Governing AI Development
**Scenario:** Six months after release a model's accuracy drops because customer behavior changed. Which control should have caught this?

A. Continuous monitoring with a retraining schedule
B. A one-time validation test run before launch only
C. A model card written once at release
D. A longer contract term with the model vendor

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Drift is found by ongoing monitoring and handled by scheduled maintenance and retraining. A pre-launch test cannot detect later change.
</details>

---

### Question 17 - Domain III: Governing AI Development
**Scenario:** Which document best describes a model's intended use, evaluation results and limitations for those who will rely on it?

A. Invoice listing the license fees paid
B. Model card
C. Backup log for the model storage bucket
D. Firewall rule set for the training network

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A model card summarises intended use, evaluation and limits. The others serve unrelated purposes.
</details>

---

### Question 18 - Domain IV: Governing AI Deployment and Use
**Scenario:** A company wants its chatbot to answer from internal documents. Which governance question is most specific to this retrieval design?

A. Whether retrieval respects the asking user's access rights
B. The number of parameters
C. The vendor's office location
D. The colour of the interface

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** With retrieval augmented generation, access control on retrieved content is key; otherwise the model can expose documents to users who should not see them.
</details>

---

### Question 19 - Domain IV: Governing AI Deployment and Use
**Scenario:** In a vendor contract review, which term most directly protects your confidential data from being used to improve the vendor's public model?

A. A clause about payment and invoice dates
B. A clause about joint marketing and co-branding
C. A clause about the vendor's support office hours
D. A clause prohibiting training on your inputs

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A no-training or opt-out clause controls reuse of your data. The others do not address data use.
</details>

---

### Question 20 - Domain IV: Governing AI Deployment and Use
**Scenario:** An AI agent can issue refunds. Which design is the strongest control?

A. Unlimited authority with after-the-fact review
B. Refund limits, approval above a threshold, and a way to deactivate
C. No logs, to save storage
D. Trust the vendor's default settings

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Limiting authority, requiring approval above a threshold and keeping a deactivation option are layered controls. Unlimited authority and no logs remove oversight.
</details>

---

### Question 21 - Domain IV: Governing AI Deployment and Use
**Scenario:** Your organization fine-tunes an open model and puts its own name on the product. What changes compared with only using a vendor's tool?

A. Only the original model vendor is liable
B. It takes on greater obligations and liability
C. It is exempt from AI regulation as a user
D. Nothing changes in its duties

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Building and branding your own model increases obligations and liability, and under the EU AI Act can make you a provider.
</details>

---

### Question 22 - Domain IV: Governing AI Deployment and Use
**Scenario:** A deployment policy says an AI system can be switched off for regulatory or performance reasons. What is needed for this to be a real control?

A. Nothing, because the vendor will switch it off if needed
B. A slogan on the intranet saying the system can be stopped
C. An owner with authority, a fallback process and periodic testing
D. A longer user manual describing the system

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A deactivation control must name who can invoke it, provide a fallback and be tested. A statement without these is not a control.
</details>

---

### Question 23 - Domain IV: Governing AI Deployment and Use
**Scenario:** A tool approved to draft emails is now being used by HR to screen candidates. Which concept does this illustrate?

A. Secondary or unintended use
B. Data minimization of the training set
C. Edge deployment on user devices
D. Model compression for faster inference

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Using a system for a purpose it was not approved for is a secondary use, which governance should forecast and control.
</details>

---

### Question 24 - Domain IV: Governing AI Deployment and Use
**Scenario:** Which action best fits a deployer's duty to be transparent that users are talking to a machine?

A. Hide the fact to improve conversion rates
B. Publish the notice only after users complain
C. Tell users at first interaction that they are talking to AI
D. Rely on users to guess it from the tone

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Transparency notices should be clear and given no later than first interaction. Hiding or delaying the information fails the duty.
</details>

---
