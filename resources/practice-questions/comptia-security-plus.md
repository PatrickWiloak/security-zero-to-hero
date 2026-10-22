---
last-updated: 2026-10-22
difficulty: beginner
---

# CompTIA Security+ (SY0-701) - Practice Questions

20 questions for Security+ prep across general security concepts, threats and vulnerabilities, security architecture, operations, and program management. Questions 1 to 15 fit both SY0-701 and SY0-801; questions 16 to 20 cover objectives new in SY0-801 (V8, launching November 17, 2026), taught in [notes 06](../../exams/comptia/security-plus/notes/06-sy0-801-changes.md).

> **Cert page:** [exams/comptia/security-plus/](../../exams/comptia/security-plus/)

---

### Question 1
**Scenario:** The CIA triad's three components.

A. Control, Integrity, Access
B. Confidentiality, Integrity, Authentication, a variant often mistaken for the triad
C. Confidentiality, Integrity, Availability
D. Cryptography, Isolation, Auditing

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Confidentiality keeps data from unauthorized viewers, integrity keeps it unaltered, availability keeps it reachable. Most exam questions asking "which principle is affected" resolve by mapping the incident to one of the three: a leak is confidentiality, tampering is integrity, ransomware is availability.
</details>

---

### Question 2
**Scenario:** A control category question: a security guard, a firewall, and a policy document.

A. All technical, because each one enforces a rule on people or on systems
B. All administrative, since each is defined by the organization and applied to staff
C. All operational, because each is carried out day to day by security staff
D. Physical, technical, and managerial respectively

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** SY0-701 uses managerial, operational, technical, and physical as the categories, cut across by control types: preventive, deterrent, detective, corrective, compensating, and directive. A single control has one category and one type, and questions often ask for both.
</details>

---

### Question 3
**Scenario:** An attacker sends a targeted email to the CFO impersonating the CEO requesting a wire transfer.

A. Vishing
B. Smishing
C. Phishing sent as a mass mailing to a broad list with no attempt to target one person
D. Business email compromise, a form of spear phishing known as whaling when it targets executives

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Spear phishing is targeted, whaling targets high-value individuals, and BEC is the fraud pattern built on it. Vishing is voice and smishing is SMS. The exam distinguishes these by the channel and the targeting, so read for both.
</details>

---

### Question 4
**Scenario:** A user's password is stolen but the attacker still cannot log in.

A. Encryption of the password database at rest, which protects storage but not a stolen password
B. Antivirus on the endpoint, which detects malware but does not verify a login
C. A firewall at the network edge, which filters traffic but cannot check who is logging in
D. Multi-factor authentication requiring a second factor

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The factors are something you know, something you have, and something you are, with location and behavior as attributes. Two of the same category is not MFA: a password plus a security question is still one factor.
</details>

---

### Question 5
**Scenario:** Which cryptographic property does a hash provide?

A. Confidentiality, because the digest scrambles the original data so unauthorized readers cannot see it
B. Integrity, via a fixed-length digest that changes when the input changes
C. Availability, because a hash lets the system recover a damaged file
D. Non-repudiation on its own

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Hashing is one-way and provides no confidentiality. Non-repudiation needs a digital signature, which combines a hash with the signer's private key. Salting defends stored password hashes against precomputed rainbow tables.
</details>

---

### Question 6
**Scenario:** Symmetric versus asymmetric encryption.

A. Symmetric: one shared key, fast. Asymmetric: a key pair, easier key distribution, higher compute cost
B. Asymmetric is always faster, which is why it is preferred for encrypting large volumes of data such as full disk images
C. Symmetric cannot encrypt bulk data, because one shared key is only safe for messages of a few kilobytes at a time
D. They are the same

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The practical pattern combines both: asymmetric to exchange a symmetric session key, symmetric for the bulk data. TLS works this way, which is why it needs certificates for the handshake and a cipher for the payload.
</details>

---

### Question 7
**Scenario:** A certificate is presented and the client must verify it is not revoked.

A. Trust the certificate because it was signed by a CA that the browser already ships in its trust store
B. Check the hostname only, confirming the name in the certificate matches the site being visited
C. Check a certificate revocation list or use OCSP, ideally with stapling so the server supplies a signed status
D. Check the expiry date only, since an expired certificate is the only sign of a bad one

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Validation covers the chain to a trusted root, the hostname, the validity dates, and revocation. OCSP stapling has the server present a signed status response, avoiding a separate client lookup and the privacy leak that comes with it.
</details>

---

### Question 8
**Scenario:** Which describes a zero-day vulnerability?

A. A vulnerability disclosed publicly a year ago, for which patches exist but have not been applied
B. Any unpatched system exposed to the internet, regardless of whether a fix exists
C. A vulnerability with no vendor patch available at the time of exploitation
D. A misconfiguration, such as a default password or an open port, that attackers find on their own

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The defining property is the absence of a fix, which is why compensating controls matter: segmentation, monitoring, and least privilege limit the damage of something you cannot patch. An old unpatched vulnerability is a patch management failure, not a zero-day.
</details>

---

### Question 9
**Scenario:** A network is divided so that a compromised workstation cannot reach the database tier directly.

A. Load balancing, which spreads requests across servers for performance and availability
B. Network segmentation, limiting lateral movement by restricting which zones a compromised host can reach
C. Redundancy, which duplicates components so a single failure does not take the service down
D. Encryption, which protects data in transit but does not stop a workstation reaching the tier

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Segmentation assumes a breach will happen and constrains what happens next. Microsegmentation extends it to individual workloads, and a screened subnet (DMZ) is the classic form for internet-facing services.
</details>

---

### Question 10
**Scenario:** An organization must decide how to handle a risk it cannot cost-effectively mitigate.

A. Choose a response (accept, avoid, transfer, or mitigate) and document the decision
B. Always mitigate, even when the control costs more than the loss it would prevent, to keep the register clean
C. Always transfer the risk to an insurer or vendor, since the risk can then be ignored by the business owner
D. Ignore it

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Formal acceptance by an authorized owner is a legitimate outcome and is what the risk register records. The exam also tests the vocabulary around it: risk appetite, residual risk (what remains after controls), and inherent risk (before them).
</details>

---

### Question 11
**Scenario:** The incident response lifecycle order.

A. Preparation, detection and analysis, containment, eradication, recovery, lessons learned
B. Containment first, always, because stopping the spread must happen before anyone analyzes the incident
C. Detection, preparation, recovery, containment
D. Recovery, then detection

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Preparation comes first because it is what makes the rest possible, and lessons learned is where the organization actually improves. Containment precedes eradication: stop the spread before you remove the cause.
</details>

---

### Question 12
**Scenario:** RPO and RTO must be distinguished.

A. RPO is acceptable data loss and sets backup frequency; RTO is acceptable downtime and sets recovery design
B. RPO measures downtime, meaning how long systems may stay unavailable before the business suffers serious and lasting harm
C. RTO measures data loss, meaning how many hours of transactions can be lost
D. They are the same

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** RPO looks backward from the incident and RTO looks forward. A four-hour RPO means backups at least every four hours; a one-hour RTO usually rules out restoring from tape. MTTR and MTBF are the related availability metrics.
</details>

---

### Question 13
**Scenario:** Logs from many systems must be correlated to detect an attack pattern.

A. A firewall, which filters traffic by rule at a network boundary but does not correlate logs
B. A SIEM, correlating log data from many sources and alerting on attack patterns
C. A vulnerability scanner, which finds known weaknesses on hosts but does not watch for attacks
D. An IPS, which blocks matching traffic inline but does not correlate

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Correlation across sources is what reveals patterns invisible in any single log. SOAR adds automated response playbooks on top. An IPS blocks in line, and a scanner finds weaknesses rather than detecting active attacks.
</details>

---

### Question 14
**Scenario:** A penetration test where the tester has no prior knowledge of the environment.

A. Partially known (grey box), where the tester is given some credentials or diagrams
B. Unknown environment (black box)
C. A vulnerability scan, which is automated and only lists potential weaknesses
D. White box, where the tester is given full documentation and source access

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** SY0-701 uses known, partially known, and unknown environment terminology. The other distinction the exam tests is scanner versus test: a vulnerability scan identifies potential weaknesses, while a penetration test attempts to exploit them and demonstrate impact.
</details>

---

### Question 15
**Scenario:** Sensitive data must be replaced with a non-sensitive equivalent that can be reversed by an authorized system.

A. Hashing, which produces a fixed-length digest that cannot be reversed by any system
B. Encryption with a lost key, so nobody can recover it
C. Tokenization, with the token mapped back to the original in a secure vault
D. Masking, which hides part of a value such as the first digits of a card number, usually irreversibly

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Tokenization removes the sensitive value from the processing environment entirely, which is why it is common in payment systems for PCI scope reduction. Masking obscures for display, and hashing is one-way and therefore not reversible.
</details>

---

### Question 16
**Scenario:** A company's AI assistant can read the shared drive and send email on users' behalf. A document on the drive contains hidden text instructing the assistant to email the payroll folder to an outside address. When a user asks for a summary of recent files, the assistant sends the email.

A. Data poisoning of the model's training set
B. Indirect prompt injection through content the assistant processed
C. Model evasion by an input crafted to be misclassified
D. A hallucination caused by an ambiguous user request

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Instructions hidden in data the model reads, which it then follows, are indirect prompt injection. Poisoning corrupts what a model learns, evasion makes a classifier mislabel an input, and a hallucination is invented content rather than an attacker's instruction being obeyed. The fixes are least privilege for the assistant and user confirmation before actions such as sending email.
</details>

---

### Question 17
**Scenario:** A database schema migration has already transformed millions of rows when the application starts throwing errors. Restoring the old schema would lose six hours of customer orders, so the team ships a corrective code change instead.

A. Backout planning
B. A maintenance window extension
C. Failing forward
D. An emergency change advisory board rejection

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Failing forward fixes a failed change with a further change when rolling back is impossible or riskier, as with data already transformed. Backout planning is the opposite approach, restoring the prior state; extending the window or a CAB decision does not describe what the team did.
</details>

---

### Question 18
**Scenario:** An organization wants an alert whenever anyone authenticates with a specific account, because no legitimate user or service ever uses it.

A. A canary account
B. A group managed service account
C. An emergency access account
D. A just-in-time privileged account

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A canary account exists only as a tripwire, so any use is a high-fidelity alert. A gMSA runs services and is used constantly, an emergency access account is real and must work when needed, and just-in-time accounts are granted for real tasks.
</details>

---

### Question 19
**Scenario:** A recovery plan states the order system may be down for at most four hours and may lose at most fifteen minutes of transactions.

A. RPO is four hours and RTO is fifteen minutes
B. MTTR is four hours and MTBF is fifteen minutes
C. MTBF is four hours and RPO is fifteen minutes
D. RTO is four hours and RPO is fifteen minutes

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Recovery time objective is how long the system may be down; recovery point objective is how much data, measured in time, may be lost. MTTR and MTBF describe measured repair and failure behavior, not targets set in a recovery plan.
</details>

---

### Question 20
**Scenario:** Phishing simulations show the accounts payable team clicks at three times the company average, and one clerk entered credentials in two simulations. Which response best fits a security awareness program?

A. Repeat the same annual company-wide training module for all staff
B. Remove email access from the accounts payable team
C. Targeted training for accounts payable on business email compromise, corrective one-to-one training for the clerk, and tracking click and report rates by team
D. Stop running simulations because they embarrass staff and lower morale

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** SY0-801 objective 5.6 names targeted and corrective training and measuring effectiveness with metrics and managerial reports. A generic module ignores the measured risk, removing email is not workable for a payments team, and dropping simulations removes the measurement.
</details>

---

## Where to go deeper

- [Security+ cert page](../../exams/comptia/security-plus/) - notes, practice plan, strategy
- [CySA+ practice questions](./comptia-cysa-plus.md) - the analyst-level next step
- [ISC2 CC practice questions](./isc2-cc.md) - the entry-level security sibling
- [Security topic index](../../topics/security.md) - security across the repo
- **[📖 CompTIA Security+](https://www.comptia.org/certifications/security)** - official exam objectives
