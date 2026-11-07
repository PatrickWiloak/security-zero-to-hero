---
last-updated: 2026-11-07
---

# CompTIA SecurityX (CAS-005) - Practice Questions

27 original scenario questions weighted to the four CAS-005 domains: Governance, Risk, and Compliance (20%) 6 questions, Security Architecture (27%) 7, Security Engineering (31%) 8 and Security Operations (22%) 6. These are original questions, not vendor exam content.

> **Cert page:** [exams/comptia/securityx/](../../exams/comptia/securityx/)

---

### Question 1 - Domain 1: Governance, Risk, and Compliance
**Scenario:** A company must decide whether to buy a 40,000 a year control for an asset worth 500,000 that has a 20 percent exposure factor to an event expected once every five years. Which statement is correct?

A. The single loss expectancy is 20,000, so the control pays for itself immediately in the first year
B. The annualized loss expectancy is 100,000, so the control pays for itself clearly and should be bought
C. The annualized loss expectancy is 20,000, so the control costs more than the loss it removes
D. The annualized rate of occurrence is five, so any control priced under the asset value must be bought

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** SLE = 500,000 x 0.2 = 100,000. ARO = 1/5 = 0.2. ALE = 100,000 x 0.2 = 20,000. A 40,000 control exceeds the loss it removes, so on cost alone it is poor value (non-financial factors might still apply).
</details>

---

### Question 2 - Domain 1: Governance, Risk, and Compliance
**Scenario:** Developers copy a production customer database into a test environment that has weaker access controls. Which action best addresses the governance gap?

A. Move the test environment to a separate network segment but keep using the production data copies
B. Replace the copies with synthetic or masked data and apply data governance rules to every environment
C. Allow the copies but require every developer to sign an acknowledgement of the data handling policy first
D. Encrypt the test database with the same key that production uses so that the data is protected equally

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Data governance must cover production, development, test and QA. Using synthetic or masked data removes the sensitive content, whereas acknowledgements, shared keys or segmentation leave real data in a weakly controlled place.
</details>

---

### Question 3 - Domain 1: Governance, Risk, and Compliance
**Scenario:** A team wants to analyse what could go wrong with a new payment service before it is built. They list each component and data flow and classify threats as spoofing, tampering, repudiation, information disclosure, denial of service and elevation of privilege. What are they using?

A. A compliance gap analysis against a payment industry standard for each component
B. STRIDE threat modeling applied to the design's components and data flows
C. A configuration management audit using a CMDB export for each component
D. A quantitative risk assessment using annualized loss expectancy for each component

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** STRIDE classifies threats by those six categories and is applied per element and data flow in a design. ALE, CMDB audits and gap analyses do not classify threats this way.
</details>

---

### Question 4 - Domain 1: Governance, Risk, and Compliance
**Scenario:** An organization wants a single control set that satisfies PCI DSS and ISO/IEC 27001 and reduces duplicated audit evidence. What should it do?

A. Map one control set to both requirements using a GRC tool and collect evidence once
B. Run two separate programmes with independent evidence collection for each regime
C. Adopt only the framework with the shorter document and ignore the other one
D. Treat compliance with either regime as proof that the organization is secure

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A mapped control set with shared evidence avoids duplicated work, and GRC tools support this mapping. Separate programmes duplicate effort and compliance alone is a minimum, not proof of security.
</details>

---

### Question 5 - Domain 1: Governance, Risk, and Compliance
**Scenario:** Who must be assigned as accountable for each activity in a RACI matrix?

A. Exactly one party for each activity
B. All teams that perform the activity, jointly
C. No one, because consulted parties share the decision
D. The most senior person in the department, regardless of the activity

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A RACI matrix uses exactly one Accountable role per activity so that ownership is clear. Responsible parties may be several, but accountability is singular.
</details>

---

### Question 6 - Domain 1: Governance, Risk, and Compliance
**Scenario:** A vendor will process the organization's customer data. Which step best addresses third-party risk before signing?

A. Rely on the vendor's size and brand reputation as a sign that its security programme must be strong
B. Ask the vendor to sign the organization's acceptable use policy and nothing more before processing starts
C. Accept the vendor's marketing statements about its security as sufficient evidence and sign the contract today
D. Due diligence on the vendor's controls plus contract terms for security, breach notification and audit rights

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Third-party risk is managed through due diligence and contractual requirements, including breach notification and right to audit, followed by ongoing monitoring. Marketing claims and size are not evidence.
</details>

---

### Question 7 - Domain 2: Security Architecture
**Scenario:** Contractors use unmanaged laptops to reach a sanctioned SaaS file store. The company must find existing public shares and remediate them, with no agents on the laptops. Which solution fits best?

A. A forward proxy CASB that requires a certificate on every laptop
B. A host-based DLP agent installed on each contractor laptop
C. A site-to-site VPN between the contractors and the company
D. An API-based CASB connected to the SaaS provider

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** An API-based CASB inspects data at rest in the service, finds existing shares, remediates retroactively and does not need agents or traffic steering on unmanaged devices.
</details>

---

### Question 8 - Domain 2: Security Architecture
**Scenario:** Which approach makes data in a cloud provider's storage unrecoverable when physical overwrite is not possible?

A. Reformatting the virtual disk from inside the guest operating system
B. Deleting the objects and emptying the recycle bin of the storage console
C. Waiting for the provider's retention window to elapse on its own
D. Cryptographic erase by destroying the encryption key

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Cryptographic erase renders ciphertext useless by destroying the key, which addresses data remanence on storage you do not control. Deletion and formatting may leave recoverable data.
</details>

---

### Question 9 - Domain 2: Security Architecture
**Scenario:** Security wants east-west traffic between workloads in the same cloud network to be restricted per application, because perimeter firewalls never see it. What should be used?

A. An always-on VPN for the application servers
B. A bigger subnet so that workloads share one trust zone
C. A larger perimeter firewall at the internet gateway
D. Microsegmentation with workload-level policy

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Microsegmentation applies policy per workload and addresses lateral movement inside a network, where perimeter firewalls have no visibility.
</details>

---

### Question 10 - Domain 2: Security Architecture
**Scenario:** A design requires that every request be authenticated and authorized using identity, device posture and context, with no implicit trust from network location. Which architecture is this?

A. A DMZ architecture with two firewalls from different vendors
B. A flat network with VLANs for each department
C. Zero trust, with policy decision and enforcement points per request
D. A traditional perimeter model with a strong internet firewall

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Zero trust removes implicit trust from network location or asset ownership and evaluates each request. Perimeter, flat and DMZ models rely on location.
</details>

---

### Question 11 - Domain 2: Security Architecture
**Scenario:** Which statement best describes SASE?

A. It combines wide area networking with cloud-delivered security services so policy follows the user
B. A larger perimeter firewall at the internet gateway with a longer list of inbound rules for every port
C. An always-on VPN for the application servers so that all of their traffic is encrypted between hosts
D. A bigger subnet so that all of the workloads share one trust zone and need fewer rules to maintain

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** SASE combines network functions such as SD-WAN with security services such as secure web gateway, CASB, firewall and zero trust network access, delivered from the cloud.
</details>

---

### Question 12 - Domain 2: Security Architecture
**Scenario:** A pipeline deploys infrastructure from templates. Which control stops insecure configuration before it reaches the cloud?

A. A proactive control that scans templates and fails the pipeline on violations
B. A deterrent control such as a warning banner on the pipeline console
C. A detective control that reviews configuration after it is deployed each quarter
D. A corrective control that restores the previous version after an outage

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Proactive controls prevent bad configuration from deploying, such as infrastructure as code scanning and policy as code. Detective and corrective controls act later.
</details>

---

### Question 13 - Domain 2: Security Architecture
**Scenario:** An organization wants devices to be proven to be in a known good state before they can reach sensitive applications. Which concept applies?

A. Data remanence testing of the device storage each year
B. Shadow IT detection from proxy logs after the fact
C. Always-on VPN with a shared pre-shared key for all devices
D. Attestation of device state, used as a condition for access

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Attestation provides evidence that a device or workload is in a known good state and can gate access. The other options do not prove device state.
</details>

---

### Question 14 - Domain 3: Security Engineering
**Scenario:** An analyst writes a script that must connect to a remote host, read its certificate and report the days until expiry. Which language features are most appropriate for this task?

A. A PowerShell command that installs a new root certificate
B. A Bash loop that deletes certificates older than the current date
C. Python's ssl and socket modules to retrieve and parse the certificate
D. A SQL query against the host's certificate table

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Python's ssl and socket modules can open a TLS connection, read the peer certificate and compute the days remaining. The other options delete or install certificates or query something that does not exist.
</details>

---

### Question 15 - Domain 3: Security Engineering
**Scenario:** A SOAR playbook can isolate a production database server automatically when malware is suspected. What is the best practice?

A. A corrective control that restores the previous version of the template after an outage has been declared
B. Require human approval for disruptive actions on critical systems while automating enrichment
C. A deterrent control such as a warning banner shown on the pipeline console to anyone who logs in
D. A detective control that reviews the configuration after it is deployed, once each quarter by the audit team

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Automate low-risk, high-confidence steps and keep approval for disruptive actions on critical systems, since a wrong automated action can cause the outage the attacker wanted. AI output should be verified.
</details>

---

### Question 16 - Domain 3: Security Engineering
**Scenario:** Which component of SCAP expresses checklists and benchmarks for security configuration?

A. XCCDF
B. CVSS
C. CPE
D. CVE

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** XCCDF is the Extensible Configuration Checklist Description Format for checklists and benchmarks. CPE names platforms, CVE identifies vulnerabilities and CVSS scores severity.
</details>

---

### Question 17 - Domain 3: Security Engineering
**Scenario:** A scanner reports a medium CVSS flaw on an internet-facing system known to be exploited in the wild and a critical flaw on an isolated lab system. How should remediation be prioritised?

A. A traditional perimeter model in which a strong internet firewall decides who is inside the trusted network
B. A DMZ architecture in which two firewalls from different vendors protect the internal servers
C. A flat network with VLANs for each department and a single shared policy for everything inside them
D. Fix the exploited internet-facing flaw first, using exploitability and exposure as well as score

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Severity is not risk. Exploitation in the wild and exposure raise the priority of the internet-facing flaw above an isolated critical flaw.
</details>

---

### Question 18 - Domain 3: Security Engineering
**Scenario:** A company stores data that must remain confidential for 25 years and is concerned about adversaries recording today's encrypted traffic. What should it plan for?

A. Post-quantum key establishment such as ML-KEM, with crypto-agility and hybrid deployment
B. Hashing the data with a faster algorithm before it is transmitted
C. Removing encryption to reduce the performance cost of the connection
D. Longer RSA keys alone, because larger keys will resist any quantum computer

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Harvest now, decrypt later threatens public key exchange. NIST's FIPS 203 specifies ML-KEM, and organizations should plan crypto-agility and hybrid transition. Larger RSA keys do not resist a large quantum computer.
</details>

---

### Question 19 - Domain 3: Security Engineering
**Scenario:** Which technique replaces a card number with a surrogate value so that systems outside the vault never hold the real number?

A. Key stretching
B. Code signing
C. Tokenization
D. Forward secrecy

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Tokenization substitutes a surrogate and keeps the real value in a protected vault, which can reduce compliance scope. The other techniques solve different problems.
</details>

---

### Question 20 - Domain 3: Security Engineering
**Scenario:** What does forward secrecy provide?

A. The ability to compute on encrypted data without decrypting it
B. Faster encryption of stored files using hardware instructions
C. Compromise of a long-term key later does not expose past session traffic
D. Proof of which developer published a signed program

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Forward secrecy uses ephemeral key exchange so past sessions stay protected if a long-term key is later compromised. Speed is acceleration, computing on ciphertext is homomorphic encryption and publisher proof is code signing.
</details>

---

### Question 21 - Domain 3: Security Engineering
**Scenario:** Passwords are stored in a database. Which measure makes offline guessing expensive?

A. Encrypting the whole database with a key stored in the same server
B. Storing passwords in reversible form so they can be recovered
C. Key stretching with a slow salted function such as Argon2 or bcrypt
D. Using a fast general-purpose hash and a long database password

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Key stretching uses a deliberately slow, salted function so each guess is costly. Fast hashes and reversible storage make guessing cheaper or passwords recoverable.
</details>

---

### Question 22 - Domain 4: Security Operations
**Scenario:** A SIEM alert rule produces thousands of benign alerts a day, and analysts have started to ignore the console. What is the best response?

A. Disable all alerting until a quiet period arrives and then switch the rules back on one at a time
B. Tune the rule with context and allow-lists and measure false positive and false negative rates
C. Increase the severity of the rule so that analysts pay attention to it whenever it fires on the console
D. Delete the logs that generate the noisy alerts so that analysts no longer see the benign events

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Tuning reduces false positives without hiding real attacks, and measuring both error rates avoids over-tuning. Disabling or deleting data creates blind spots.
</details>

---

### Question 23 - Domain 4: Security Operations
**Scenario:** A hunter assumes an adversary uses scheduled tasks for persistence and searches endpoint logs for rare tasks created by office applications. What is this activity?

A. Proactive threat hunting based on a hypothesis
B. A penetration test of the endpoint
C. Alert triage of an existing high-severity alert
D. A compliance audit of scheduled task policy

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Hunting is proactive: form a hypothesis, search data for evidence, then turn findings into detections. Triage reacts to something already flagged.
</details>

---

### Question 24 - Domain 4: Security Operations
**Scenario:** Which tool is a decoy that no legitimate user should access, so any interaction is a strong signal of malicious activity?

A. A baseline
B. A honeypot
C. A playbook
D. A CMDB

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A honeypot is a decoy system, and any access is suspicious, which gives high-fidelity internal intelligence. A baseline records normal behaviour, a CMDB records assets and a playbook automates response.
</details>

---

### Question 25 - Domain 4: Security Operations
**Scenario:** An analyst runs a suspicious file in an isolated environment and records its file, registry, process and network behaviour. What is this?

A. Data recovery from a forensic image
B. Static analysis of strings and headers without execution
C. Dynamic malware analysis in a sandbox
D. Code stylometry of the author's writing habits

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Running the file and observing behaviour in a sandbox is dynamic analysis. Static analysis examines the file without running it.
</details>

---

### Question 26 - Domain 4: Security Operations
**Scenario:** A user input field allows an attacker to run database commands through the web form. Which mitigation is primary?

A. Parameterised queries and input validation with a least-privilege database account
B. Longer TLS session timeouts on the web server so that fewer connections need to be negotiated
C. A longer password policy for database administrators with a rotation schedule every ninety days
D. More frequent daily backups of the web server and the database to a second storage location

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Injection is prevented by keeping untrusted input separate from code: parameterised queries, validation and least privilege. TLS, passwords and backups do not stop injection.
</details>

---

### Question 27 - Domain 4: Security Operations
**Scenario:** After containing an incident, the team asks how the adversary got in, which control failed and what change would prevent a repeat. Which activity is this?

A. Root cause analysis
B. Indicator extraction
C. Reverse engineering of the malware
D. Threat intelligence sharing

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Root cause analysis determines why the incident was possible and which change prevents recurrence. The other activities examine samples or share indicators.
</details>

---
