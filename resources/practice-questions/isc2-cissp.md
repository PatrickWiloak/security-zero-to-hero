# ISC2 CISSP - Practice Questions

30 scenario-based questions across the 8 CISSP domains. Questions 1 to 25 follow the April 2024 outline; questions 26 to 30 cover topics the 2027 outline adds (effective April 15, 2027), taught in [notes 09](../../exams/isc2/cissp/notes/09-2027-outline-changes.md). CISSP rewards "manager / risk-owner" thinking - read questions for that mindset.

> **Cert page:** [exams/isc2/cissp/](../../exams/isc2/cissp/)

---

### Question 1 - Domain 1: Security and Risk Management
**Scenario:** A Chief Risk Officer asks for a risk treatment for a vulnerability with low likelihood but catastrophic impact. The vulnerability cannot be remediated for 6 months. What's the BEST treatment?

A. Mitigate by adding a compensating control, such as extra monitoring or a firewall rule, while the fix waits
B. Accept the risk because the likelihood is low and the decision can be documented
C. Avoid the risk by retiring the affected system immediately, which removes the exposure but is not feasible when the business depends on that system
D. Transfer the risk by buying cyber insurance for the interim period, which covers financial loss but leaves the vulnerability open and unprotected

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** "Catastrophic impact" makes acceptance and transfer alone too weak; even with insurance, business continuity matters. A **compensating control** (firewall rule, additional monitoring, manual review) reduces likelihood while remediation is in progress. Avoidance via retirement is too costly without business approval. CISSP favors layered defense.
</details>

---

### Question 2 - Domain 1
**Scenario:** In ISC2 CISSP guidance on business continuity and impact decisions, what is the usual order of priorities?

A. They're equal, because a BIA assigns the same weight to every impact category
B. Safety of life > Critical business assets > Reputation > Cost, with human safety always ranked above any financial or operational impact
C. Compliance > Cost > Reputation > Safety, because regulators can fine the organization
D. Cost > Safety > Reputation > Compliance, because the BIA exists mainly to justify recovery spending

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** This is the standard CISSP convention, a judgment call rather than a formal BIA rule. **Safety of human life is always the top priority** in any security or BCP question. Critical business assets next, then reputation, then cost. CISSP repeatedly tests this - never pick "save money" over "save lives."
</details>

---

### Question 3 - Domain 2: Asset Security
**Scenario:** Personal Health Information (PHI) under HIPAA must be classified at what level minimum?

A. It depends on the organization's own classification scheme, because HIPAA sets safeguards but does not name a label
B. Public, because HIPAA protects data only once it is breached
C. Confidential / Restricted (highest standard tier the organization uses for sensitive data), because HIPAA names that exact tier as a minimum
D. Internal, because PHI is shared within the covered entity for treatment

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Classification schemes vary by organization, and HIPAA does not name a label. Most schemes have 3-4 tiers (Public, Internal, Confidential, Restricted). In practice PHI belongs in one of the most sensitive tiers the org defines. The right answer recognizes that classification labels are organization-specific while the underlying control requirements (encryption, access controls, audit) are mandated by HIPAA.
</details>

---

### Question 4 - Domain 3: Security Architecture
**Scenario:** What's the primary purpose of a Trusted Platform Module (TPM)?

A. Storing cryptographic keys in tamper-resistant hardware tied to one machine, enabling attestation and disk encryption
B. Application sandboxing, which isolates a running program from the rest of the system
C. Network packet filtering, which allows or blocks packets by port and address
D. Providing physical security for the data center, such as locks, badge readers, and cameras that control who enters the facility

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** TPM is a hardware chip that stores keys securely, supports remote attestation, and enables full-disk encryption (BitLocker, dm-crypt). The key benefit is **bound to a specific physical machine** - keys can't be exfiltrated to another machine.
</details>

---

### Question 5 - Domain 3
**Scenario:** A defense-in-depth strategy adds firewall, IDS, EDR, and email filtering. What concept does this exemplify?

A. Layered controls / defense in depth, using several independent control types
B. Reactive security, adding controls only after an incident
C. Single point of failure, a design weakness where one component outage takes down the service, which layering is meant to avoid
D. Compliance theater, where controls are deployed to satisfy an audit checklist without any real effect on the organization's risk

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Layering different control types (network, host, email) so a single failure doesn't compromise the system. CISSP tests this concept repeatedly under names like "defense in depth," "layered controls," "diverse controls."
</details>

---

### Question 6 - Domain 4: Communication and Network Security
**Scenario:** Which TLS handshake step proves the server's identity to the client?

A. ClientHello with cipher suites, which lets the client offer the versions and algorithms it supports
B. The server's X.509 certificate signed by a trusted CA, which the client validates against its trust store and checks against the hostname
C. The pre-master secret exchange, which lets both sides derive session keys
D. Application data encryption, which protects data after the handshake is finished

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Server identity is proven by the X.509 certificate signed by a CA the client trusts. The client validates the chain, the certificate's CN/SAN matches the hostname, and the cert isn't revoked or expired.
</details>

---

### Question 7 - Domain 5: Identity and Access Management
**Scenario:** Type 1, Type 2, Type 3 authentication factors - which is which?

A. Something you know / something you have / something you are
B. Required / recommended / optional, which are priority labels used in policy language and not categories of authentication factor
C. Username / password / biometric, which lists three examples of credentials and mixes a claim of identity with two factors
D. Hardware / software / cloud, which describes where an authenticator runs and not the kind of evidence being offered

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Memorize: **Type 1 = something you KNOW** (password, PIN), **Type 2 = something you HAVE** (token, smart card, phone), **Type 3 = something you ARE** (biometric). Multi-factor auth requires factors from at least **two different types** - not two of the same type.
</details>

---

### Question 8 - Domain 5
**Scenario:** A federated identity model with SAML - what does the Identity Provider (IdP) provide?

A. Network access, such as an IP address and VLAN assignment for the user's device, which is the job of the network layer and not the IdP
B. The application itself, which the user wants to reach, hosted by the service provider and not by the identity provider
C. Authentication assertions about a user (the IdP says "yes, this is alice@example.com")
D. Audit logs of user activity inside every application in the federation, which each service provider keeps itself

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** In SAML federation, the IdP authenticates the user and sends a signed assertion to the Service Provider (SP / app). The SP trusts the assertion based on the IdP's signing certificate. OIDC works similarly with JWT tokens.
</details>

---

### Question 9 - Domain 6: Security Assessment and Testing
**Scenario:** A penetration test should be conducted with what authorization?

A. Implicit consent of management, assumed because the test helps
B. Explicit, written authorization (rules of engagement document) from senior management
C. Verbal approval from the CISO, which leaves no record of scope or limits
D. No authorization needed if internal, because employees on the security team already have access to the systems involved

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Written authorization (often called "Rules of Engagement" or "Get Out of Jail Free Letter") is essential. Without it, pen testing is criminal trespass under CFAA (US) or equivalent. Specifies scope, timing, escalation contacts, and what's off-limits.
</details>

---

### Question 10 - Domain 7: Security Operations
**Scenario:** During incident response, what's the first phase per the standard 6-step process?

A. Identification, in which the team detects and confirms an event, which can only happen well once tools and roles are in place
B. Preparation
C. Recovery, in which systems are restored and monitored, which comes near the end of the process after the threat is removed
D. Containment, in which the team limits the spread of an incident, which comes after the event has been identified

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Order: **Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned**. Preparation (policies, runbooks, training) happens before any incident.
</details>

---

### Question 11 - Domain 7
**Scenario:** RAID 5 vs RAID 6 - the key difference?

A. RAID 5 is always faster because it uses fewer parity disks
B. RAID 6 uses encryption on the extra parity disks, which protects data at rest, whereas RAID 5 stores blocks in plain form
C. They're the same, with the number only showing how many disks are in the array
D. RAID 5 has one parity disk and survives one failure; RAID 6 has two (tolerates two simultaneous disk failures)

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** RAID 5: striping with single parity (tolerates 1 failure). RAID 6: striping with double parity (tolerates 2 simultaneous failures, slower writes due to dual parity calculation). RAID 10 is mirrored stripes (fast, expensive).
</details>

---

### Question 12 - Domain 7
**Scenario:** RTO vs RPO?

A. RTO is the maximum acceptable data loss measured in time; RPO is the maximum acceptable outage duration, as agreed with the business owner during planning
B. RTO is how long the team has to detect an incident; RPO is how long it takes to close the incident after the investigation
C. RTO and RPO each measure outage duration and differ only in whether the outage was planned or unplanned
D. RTO is the maximum acceptable time to restore service; RPO is the maximum acceptable data loss, measured back from the incident

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** **RTO** = Recovery Time Objective = max acceptable outage duration. **RPO** = Recovery Point Objective = max acceptable data loss (measured backwards from incident). RTO of 4 hours + RPO of 1 hour means: bring the system back within 4 hours, lose at most 1 hour of data.
</details>

---

### Question 13 - Domain 8: Software Development Security
**Scenario:** SQL injection is mitigated primarily by:

A. Input validation alone, which rejects odd characters but can be bypassed
B. Web Application Firewall, which blocks known attack patterns but can be evaded
C. Parameterized queries (prepared statements) with bound parameters, so user input is always treated as data and never as SQL code
D. Output encoding, which is a defense for XSS and not for SQL injection

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Parameterized queries are the **primary** defense. They separate SQL code from data so user input can't be interpreted as code. Input validation is defense-in-depth but not sufficient alone (encoding bypasses, edge cases). WAF helps but is reactive.
</details>

---

### Question 14 - Domain 8
**Scenario:** A code review finds a hardcoded API key in source. What's the BEST remediation?

A. Encrypt the key in code with a symmetric key stored beside it, which obscures the value but leaves a recoverable secret in the repository
B. Use environment variables instead, which moves the value out of the source but leaves the leaked key valid and in the history
C. Comment it out and ship, which hides the line from the running program but leaves the key valid and readable in source control
D. Rotate the key, store in a secret manager, fix the code, audit version control history for prior leaks, and rotate any other credentials that may have been compromised

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A hardcoded credential in version control is **already leaked** if the repo has multiple eyes. Rotate first, then move to secret manager, then sweep history (`git log -p` or BFG Repo-Cleaner), then audit related credentials. CISSP favors comprehensive remediation over narrow fixes.
</details>

---

### Question 15 - Cross-domain
**Scenario:** A company hires a third-party SaaS for HR data. From a security perspective, what document is MOST important?

A. SLA + SOC 2 Type II report + Data Processing Agreement (DPA), covering availability, assurance, and data handling
B. NDA, which restricts what each party may disclose
C. Master Service Agreement, which sets commercial terms such as fees and term but not the security controls or audit evidence
D. Insurance certificate, which proves that the provider has coverage for losses but does not show what controls protect the data

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** SOC 2 Type II shows operational security controls work over time. SLA covers availability and breach notification timing. DPA (especially under GDPR/CCPA) defines data handling. NDA and MSA are baseline contractual but don't cover security operations.
</details>

---

### Question 16
**Scenario:** A new security control is proposed. What's the security manager's FIRST step before approving?

A. Buy the most expensive option, assuming price means strength
B. Skip the control if it is expensive, since the cost of a control should never be allowed to exceed the budget of the department
C. Conduct a risk assessment to determine if the control's cost is justified by the risk it mitigates
D. Implement immediately to close the gap quickly, then evaluate the effect on risk after the control is running in production

<details><summary>Answer</summary>

**Correct: C**

**Why:** CISSP rule: every control proposal goes through risk assessment. Cost of control should not exceed expected loss it mitigates. "Best" answer in CISSP is almost always the risk-based one.
</details>

---

### Question 17
**Scenario:** During incident response, the FIRST priority is:

A. Forensic analysis of the root cause
B. Restoration of services from clean backups, which is premature while the threat is still active on the network
C. Containment to prevent further damage while evidence is preserved
D. A public statement to customers and the press, which is managed by the communications team after the facts are known

<details><summary>Answer</summary>

**Correct: C**

**Why:** NIST IR lifecycle: Preparation → Detection → **Containment** → Eradication → Recovery → Lessons Learned. Containment first. Even before knowing root cause, stopping the bleeding is the priority.
</details>

---

### Question 18
**Scenario:** Best evidence in a fraud investigation:

A. Original / direct evidence (system logs, signed documents, video)
B. Eyewitness testimony, which can be useful but depends on memory and perception and is weaker than records created at the time
C. Hearsay, a statement made outside the court by someone who is not testifying, which is generally inadmissible as proof
D. Circumstantial evidence, which supports an inference but does not directly prove the fact in question without further links

<details><summary>Answer</summary>

**Correct: A**

**Why:** Evidence hierarchy: best (original / direct) > secondary > circumstantial > hearsay. System logs with chain of custody are the gold standard for digital forensics.
</details>

---

### Question 19
**Scenario:** RTO is 4 hours, RPO is 15 minutes. Which DR pattern fits?

A. Backup and restore
B. Pilot light, with the data replicated and the app tier switched off
C. Warm standby, with a scaled-down but fully running copy of the whole stack in the DR region
D. Multi-site active-active, with full capacity serving traffic in both sites at all times

<details><summary>Answer</summary>

**Correct: B (or C depending on cost tolerance)**

**Why:** RTO 4h means tens of minutes of warm-up are acceptable. RPO 15 min requires near-continuous replication. Pilot light (data tier replicated, app off) fits. Warm standby tightens RTO further at higher cost. Backup-restore (A) cannot meet the 15-minute RPO unless backups run every few minutes, and a cold restore is slow; active-active (D) is overkill.
</details>

---

### Question 20
**Scenario:** Defense in depth means:

A. One very strong control, such as a next-generation firewall, placed at the perimeter so that attackers cannot get into the network
B. Hiring more security staff so that each system is watched by a person, which adds oversight but is not a layering of controls
C. Buying expensive products from several vendors, which adds cost but does not make the controls work together as separate layers
D. Multiple layered controls so failure of any one doesn't compromise the system

<details><summary>Answer</summary>

**Correct: D**

**Why:** Defense in depth = layered defenses (perimeter + network + host + app + data + identity + monitoring) so an attacker must defeat multiple controls to reach assets. Single-control strategies are brittle.
</details>

---

### Question 21
**Scenario:** Most secure password storage:

A. SHA-256 fast hash without a salt, which is one-way but lets attackers test billions of guesses per second and use rainbow tables
B. Reversible encryption with a key held by the application, which allows recovery of the password if the key is ever stolen
C. Plain text stored in a restricted database table, protected only by access controls and file permissions on the server
D. One-way hash with salt + slow KDF (bcrypt, scrypt, Argon2)

<details><summary>Answer</summary>

**Correct: D**

**Why:** Passwords should never be reversible. Salt prevents rainbow tables. Slow KDF (bcrypt / scrypt / Argon2) makes brute force computationally expensive. Fast hashes like SHA-256 are wrong - they're optimized for speed, which helps attackers.
</details>

---

### Question 22
**Scenario:** Bell-LaPadula model focuses on:

A. Availability, ensuring that systems and data are accessible when needed, which is the focus of redundancy and recovery models
B. Integrity, preventing improper changes to data, which is the focus of the Biba and Clark-Wilson models, not Bell-LaPadula
C. Non-repudiation, ensuring that a party cannot deny an action, which is provided by digital signatures and audit logs
D. Confidentiality (no read up, no write down)

<details><summary>Answer</summary>

**Correct: D**

**Why:** Bell-LaPadula = confidentiality. Biba = integrity (no write up, no read down). Clark-Wilson = integrity via well-formed transactions. Brewer-Nash (Chinese Wall) = conflict-of-interest. Memorize the model-to-property mapping for CISSP.
</details>

---

### Question 23
**Scenario:** Which legal concept applies when an employee's actions cause harm and the employer is held responsible?

A. Strict liability, which holds a party responsible for harm regardless of fault
B. Vicarious liability, where the employer answers for acts an employee commits within the scope of employment
C. Comparative fault, which divides responsibility by each party's share of blame
D. Negligence per se, where violating a statute is treated as negligence

<details><summary>Answer</summary>

**Correct: B**

**Why:** Vicarious liability = employer responsible for employee actions within scope of employment. Implications: training, policies, accountability chains all matter for the security manager.
</details>

---

### Question 24
**Scenario:** A penetration test discovers a vulnerability that the team disagrees about exploiting in scope. The CORRECT response:

A. Inform a competitor about the vulnerability, which breaches confidentiality
B. Stop, refer to the rules of engagement, get written authorization to expand scope before exploiting
C. Test it anyway, because the finding may be serious
D. Ignore it and say nothing in the report, since any issue outside the agreed scope is not the tester's concern

<details><summary>Answer</summary>

**Correct: B**

**Why:** Pen testing requires written authorization. Anything outside scope without authorization risks legal liability and breach of contract. The professional response: pause, document, get sign-off, then proceed.
</details>

---

### Question 25
**Scenario:** Most important component of an effective security awareness program:

A. Posters displayed in common areas, which raise visibility for a short time but give no measured change in behavior
B. Email reminders sent each month, which are easy to ignore and give no evidence that staff know what to do
C. Continuous, role-relevant content + measured outcomes (phish simulation pass rates, time-to-report) + non-punitive culture for reporting
D. Annual mandatory training delivered to all staff, which satisfies a checklist but is quickly forgotten and not tied to roles

<details><summary>Answer</summary>

**Correct: C**

**Why:** Awareness is a program, not an event. Sustained, measured, role-relevant training with a non-punitive reporting culture is what changes behavior. Annual training is necessary but not sufficient. Punitive responses suppress reporting.
</details>

---

### Question 26 - Domain 3: Security Architecture and Engineering (2027 outline)
**Scenario:** A government contractor encrypts design documents that must remain confidential for 25 years. Its key exchange uses elliptic curve Diffie-Hellman. Leadership asks what risk quantum computing poses today.

A. None until a large quantum computer exists, so no action is needed yet
B. Symmetric encryption such as AES-256 is broken by quantum computers, so all data must be re-encrypted now
C. Hashing algorithms are the main exposure, so the contractor should replace SHA-256 first
D. Harvest now, decrypt later: recorded traffic could be decrypted in future, so long-lived data needs a crypto-agile plan toward post-quantum key exchange

<details><summary>Answer</summary>

**Correct: D**

**Why:** Shor's algorithm threatens the public-key algorithms used for key exchange, and an adversary can record traffic today to decrypt later. Data that must stay secret for decades is already exposed, so inventory and migration to post-quantum algorithms (such as NIST's ML-KEM) should start. AES-256 and SHA-256 are far less affected.
</details>

---

### Question 27 - Domain 5: Identity and Access Management (2027 outline)
**Scenario:** After repeated credential phishing, a CISO wants an authentication method that a look-alike website cannot reuse, and that leaves no shared secret on the server.

A. Passkeys based on FIDO2 and WebAuthn
B. Longer passwords with 90-day rotation
C. One-time codes sent by SMS
D. Security questions combined with a password

<details><summary>Answer</summary>

**Correct: A**

**Why:** A FIDO2 credential is a key pair bound to the legitimate site's origin, so a phishing domain cannot obtain a usable credential, and the server stores only a public key. Passwords, SMS codes, and security questions are all shared secrets that a phishing page can capture and replay.
</details>

---

### Question 28 - Domain 5: Identity and Access Management (2027 outline)
**Scenario:** During a declared emergency, a field medic must open a patient record she would normally be denied. The system weighs the operational need against the current risk, grants access, and flags the decision for review.

A. Mandatory access control
B. Risk-Adaptable Access Control (RAdAC)
C. Rule-based access control (RuBAC)
D. Discretionary access control

<details><summary>Answer</summary>

**Correct: B**

**Why:** RAdAC makes real-time decisions by balancing security risk against operational need, so it can allow access in an emergency that it would deny normally, and records the decision. MAC and RuBAC apply fixed labels or rules regardless of the situation, and DAC leaves access to the owner's discretion.
</details>

---

### Question 29 - Domain 1: Security Governance and Risk Management (2027 outline)
**Scenario:** A lending team deploys an AI model that approves loans faster and more profitably, but an internal review finds it rejects applicants from one postal region at twice the rate of others, and no one can explain why.

A. Keep the model running because it improves profitability and no regulator has complained
B. Quietly retrain the model on different data without telling anyone
C. Raise it through governance: suspend or restrict the model for those decisions, require an explainable and fair review under the AI policy, and assign a human owner accountable for outcomes
D. Replace the model with manual approvals permanently and ban AI use across the company

<details><summary>Answer</summary>

**Correct: C**

**Why:** Ethics in AI is about fairness, transparency, and accountability, handled through governance with a named owner. Ignoring bias or fixing it silently fails transparency and accountability, and a blanket ban overreacts instead of managing the risk.
</details>

---

### Question 30 - Domain 7: Security Operations (2027 outline)
**Scenario:** A ransomware group compromised a backup administrator's account and deleted the organization's backups before encrypting production. Which control would MOST directly have preserved the ability to recover?

A. Backups encrypted with keys stored on the backup server
B. More frequent backup schedules to the same backup system
C. A warm site with replicated servers
D. Immutable backups that cannot be altered or deleted during their retention period, even by administrators

<details><summary>Answer</summary>

**Correct: D**

**Why:** Immutability removes the attacker's ability to destroy backups with a privileged account. Encryption protects confidentiality, not availability; more frequent backups to the same system die with it; and a warm site with live replication can replicate the encrypted data too.
</details>

---

## Scoring guide

- **26-30 correct (or 22-25 of the first 25):** Strong; schedule the exam.
- **20-25 (17-21 of the first 25):** Re-read weak domains; CISSP is broad - know all 8 domains.
- **Below 20 (below 17 of the first 25):** More foundational study needed.

CISSP exam: 100-150 adaptive questions, 3 hours. Pass rate ~70%. The mindset is **manager-level / risk-based**, not technical-implementation. When in doubt, pick the answer that prioritizes safety, business continuity, and the formal process.
