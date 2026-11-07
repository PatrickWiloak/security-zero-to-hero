---
last-updated: 2026-11-07
---

# ISC2 SSCP - Practice Questions

28 original scenario questions weighted to the seven SSCP domains of the outline effective October 1, 2025: Domain 1 (16%) 5 questions, Domain 2 (15%) 4, Domain 3 (15%) 4, Domain 4 (14%) 4, Domain 5 (9%) 2, Domain 6 (16%) 5, Domain 7 (15%) 4. These are original questions, not vendor exam content.

> **Cert page:** [exams/isc2/sscp/](../../exams/isc2/sscp/)

---

### Question 1 - Domain 1: Security Concepts and Practices
**Scenario:** A bank requires two different employees to approve any wire transfer over a set amount. Which principle does this enforce?

A. Need to know for payment data
B. Separation of duties
C. Defense in depth across layers
D. Least privilege for every account

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Separation of duties splits a sensitive task so one person cannot complete fraud alone. Least privilege limits what each identity can do, but not how a single task is split. Defense in depth is layering controls. Need to know limits information, not task completion.
</details>

---

### Question 2 - Domain 1: Security Concepts and Practices
**Scenario:** A legacy medical device cannot be patched. The security team places it on an isolated VLAN with extra logging. What kind of control is this?

A. Compensating
B. Corrective
C. Directive
D. Deterrent

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A compensating control stands in when the intended control (patching) is not feasible. It should be documented with the reason. A deterrent discourages attempts and a corrective control repairs after an event.
</details>

---

### Question 3 - Domain 1: Security Concepts and Practices
**Scenario:** A server is being retired. Its disks held encrypted customer data and the encryption key is held in a key management system. Which disposal approach is both sound and efficient?

A. Destroy the key under a documented process, then record the sanitization
B. Move the disks to a test environment where developers can reuse them
C. Delete the files and quick-format the disks before they are sold
D. Leave the disks in a storage cabinet until the space is needed again

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Cryptographic erase makes the data unrecoverable by destroying the only key, if the encryption was strong and the key had no other copies. Deleting and reformatting leaves recoverable data. Reuse and storage leave the data exposed. The sanitization should be recorded.
</details>

---

### Question 4 - Domain 1: Security Concepts and Practices
**Scenario:** A change request opens a firewall port for a new application. What should happen before approval?

A. Wait for the next audit to review it
B. Deploy to production to test it with real traffic
C. A security impact analysis and a rollback plan
D. Ask the vendor to approve the change

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Change management requires a security impact analysis (what does opening the port expose?), testing, approval and a rollback plan. Testing in production and waiting for an audit skip the control. The vendor does not own the organization's risk.
</details>

---

### Question 5 - Domain 1: Security Concepts and Practices
**Scenario:** A visitor follows an employee through a badge-controlled door without presenting a badge. Which physical control best reduces this?

A. Encrypted backups stored in a second region
B. A longer password policy for every account in the company
C. More firewall rules on the perimeter and the data centre edge
D. A mantrap with attentive reception

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Tailgating is a physical access problem. A mantrap lets only one person through at a time, and trained staff challenge strangers. The other controls address logical threats.
</details>

---

### Question 6 - Domain 2: Access Controls
**Scenario:** An organization requires users to approve a push notification and enter a password. How many authentication factors are in use, and which categories?

A. One factor, because both steps happen on the same phone
B. Two factors: something you know and something you have
C. Three factors, because there are three separate steps
D. Two factors, both in the something-you-know category

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The password is something you know and the registered phone approving the push is something you have. Two different categories make it multi-factor. (Push approval can still be vulnerable to fatigue attacks, so a phishing-resistant method is stronger.)
</details>

---

### Question 7 - Domain 2: Access Controls
**Scenario:** A partner company needs access to one internal application. Which design best follows sound trust principles?

A. Open the application to the internet with no authentication so the partner can reach it
B. Place the application in a controlled extranet segment with MFA, narrow access and logging
C. Give the partner a full VPN into the internal network for convenience
D. Share one employee account between the partner's staff

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Third-party access should be narrow, controlled, authenticated and logged. A full VPN gives the partner far more than needed, and shared accounts destroy accountability.
</details>

---

### Question 8 - Domain 2: Access Controls
**Scenario:** A user moves from accounts payable to purchasing and still has access to payment approval. What control failed?

A. Encryption in transit
B. Log retention
C. Access recertification
D. Network segmentation

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Privilege creep is caught by periodic access reviews, and role changes should trigger an immediate review. The other controls are unrelated to stale entitlements.
</details>

---

### Question 9 - Domain 2: Access Controls
**Scenario:** A system assigns access using classification labels on files and clearances on users, and owners cannot override it. Which model is this?

A. Mandatory access control
B. Rule-based access control
C. Role-based access control
D. Discretionary access control

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** In mandatory access control the system enforces access from labels and clearances and owners cannot change it. In discretionary control the owner decides. Role-based control uses job roles and rule-based control applies global rules.
</details>

---

### Question 10 - Domain 3: Risk Identification, Monitoring and Analysis
**Scenario:** A server is worth 200,000 and a fire would destroy 50% of its value. Fires are expected once every 10 years. What is the annualized loss expectancy?

A. 20,000
B. 100,000
C. 5,000
D. 10,000

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** SLE = 200,000 x 0.5 = 100,000. ARO = 0.1. ALE = SLE x ARO = 10,000. A control costing more than 10,000 a year to remove that loss would not pay for itself on this number alone.
</details>

---

### Question 11 - Domain 3: Risk Identification, Monitoring and Analysis
**Scenario:** Management reads a risk report and decides to live with a low-rated risk without further controls. Which treatment is this, and who must make the decision?

A. Mitigation, by the practitioner
B. Transfer, by the auditor
C. Acceptance, by management
D. Avoidance, by the vendor

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Acceptance means documenting the risk and carrying it, and it belongs to someone with authority over the business, not the practitioner. Mitigation applies controls, transfer shifts the loss and avoidance stops the activity.
</details>

---

### Question 12 - Domain 3: Risk Identification, Monitoring and Analysis
**Scenario:** Why should a vulnerability scan of servers usually be credentialed?

A. It runs faster than an unauthenticated scan on large networks
B. It sees configuration and patch state directly with fewer false positives
C. It replaces the need for any penetration testing programme
D. It avoids needing written authorization from the system owner

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A credentialed scan logs in and checks installed software and settings, so it is more accurate. It is not faster in general, still requires authorization and does not replace penetration testing.
</details>

---

### Question 13 - Domain 3: Risk Identification, Monitoring and Analysis
**Scenario:** Logs from a server and a firewall show events 7 minutes apart for what analysts believe is one action. What prevented clean correlation?

A. Excessive retention
B. Lack of encryption
C. Too many users
D. Unsynchronised clocks

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Time synchronisation lets events from separate systems be lined up. Without it, timelines and SIEM correlation are unreliable and evidence is weakened.
</details>

---

### Question 14 - Domain 4: Incident Response and Recovery
**Scenario:** An analyst confirms a workstation is compromised and still communicating with an attacker. Which action should come next in the incident response process?

A. Write the lessons learned report and close the ticket
B. Notify the press and customers before scoping the impact
C. Reimage the workstation immediately so the attacker loses access
D. Contain it, for example by isolating it from the network, while preserving evidence

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** After detection and analysis comes containment to stop the spread. Reimaging first destroys evidence and skips scoping. Lessons learned come last.
</details>

---

### Question 15 - Domain 4: Incident Response and Recovery
**Scenario:** During a forensic acquisition, which item should be collected first?

A. Printed documentation
B. The hard disk image
C. The contents of memory
D. Archived backups

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The order of volatility puts memory and running state first because they disappear on power loss. Disk, then logs and backups follow.
</details>

---

### Question 16 - Domain 4: Incident Response and Recovery
**Scenario:** A business impact analysis gives a maximum tolerable downtime of 8 hours. Which RTO is valid?

A. 4 hours
B. 24 hours
C. 12 hours
D. 8 hours exactly

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The recovery time objective must be shorter than the MTD so there is margin. A 12 or 24 hour RTO exceeds the tolerance, and exactly 8 hours leaves none.
</details>

---

### Question 17 - Domain 4: Incident Response and Recovery
**Scenario:** A ransomware outbreak encrypted the main file server and its nightly backups, which were on the same network share. What would have prevented the backup loss?

A. More frequent full backups to the same network share
B. Deleting old backups to reduce the number of targets
C. Offline or immutable backup copies kept separately
D. Longer passwords on the file server administrator account

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Backups reachable from the compromised network can be encrypted too. Offline or immutable copies, kept apart and tested, survive. Frequency alone does not help.
</details>

---

### Question 18 - Domain 5: Cryptography
**Scenario:** Alice wants to prove to Bob that a message came from her and was not altered. What does she use?

A. A digital signature using her private key
B. Bob's private key
C. A hash of the message alone
D. Her public key to encrypt it

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A digital signature made with the sender's private key gives integrity, authentication and non-repudiation. A hash alone can be recomputed by anyone, and encrypting with a public key gives confidentiality.
</details>

---

### Question 19 - Domain 5: Cryptography
**Scenario:** Why is a unique salt added to each password before hashing?

A. To make the hash reversible when users forget passwords
B. So identical passwords produce different hashes and precomputed tables fail
C. To shorten the stored hash and save database space
D. To encrypt the password while it travels over the network

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A salt is random data mixed into each password so equal passwords do not hash alike, which defeats rainbow tables. It does not make hashing reversible or protect transit.
</details>

---

### Question 20 - Domain 6: Network and Communications Security
**Scenario:** A switch port should admit a laptop only after the laptop authenticates with a certificate. Which technology provides this?

A. 802.1X with EAP-TLS
B. DNSSEC
C. NAT
D. SNMP

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** 802.1X is port-based network access control, and EAP-TLS uses certificates. NAT translates addresses, DNSSEC signs DNS data and SNMP manages devices.
</details>

---

### Question 21 - Domain 6: Network and Communications Security
**Scenario:** Which protocol is typically preferred for authorizing administrator commands on network devices?

A. SMTP
B. DHCP
C. TACACS+
D. ICMP

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** TACACS+ centralises device administration and separates authentication, authorisation and accounting. RADIUS is typical for end-user network access. The others are unrelated.
</details>

---

### Question 22 - Domain 6: Network and Communications Security
**Scenario:** An attacker sends forged ARP replies on a LAN so traffic passes through the attacker's machine. Which control best counters this?

A. Blocking port 443 at the perimeter firewall
B. A longer Wi-Fi passphrase on the corporate access points
C. Disabling DNS on the affected network segment
D. Dynamic ARP inspection on switches

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Dynamic ARP inspection validates ARP messages against known bindings. The other options do not address layer 2 address poisoning.
</details>

---

### Question 23 - Domain 6: Network and Communications Security
**Scenario:** An organization wants a device that sits inline and blocks traffic matching known attack patterns. Which device is this?

A. IPS
B. Proxy log
C. SIEM
D. IDS

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** An intrusion prevention system is inline and can block. An IDS only detects and alerts, and a SIEM correlates events but does not sit in the traffic path.
</details>

---

### Question 24 - Domain 6: Network and Communications Security
**Scenario:** Employees complain that the guest Wi-Fi shows two networks with the same name, one with a stronger signal in the lobby. Which attack is most likely?

A. Smurf attack
B. Evil twin
C. Replay
D. DNS amplification

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** An evil twin is a rogue access point impersonating a legitimate network. Wireless scanning, WPA-Enterprise with server certificate validation and user awareness reduce the risk.
</details>

---

### Question 25 - Domain 7: Systems and Application Security
**Scenario:** A program spreads across the network by itself, exploiting a flaw in a file-sharing service. What is it?

A. Rootkit
B. Worm
C. Logic bomb
D. Virus

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A worm self-propagates without user action. A virus needs a host file to be run, a rootkit hides itself and a logic bomb triggers on a condition.
</details>

---

### Question 26 - Domain 7: Systems and Application Security
**Scenario:** A company lets staff use personal phones for email but wants to wipe only business data on departure. Which approach supports this?

A. Banning email on phones and requiring office-only access
B. Sharing one account between all staff who use phones
C. Containerisation under MDM with a clear BYOD policy
D. Full device wipe by the help desk

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Containerisation separates corporate apps and data so a selective wipe is possible, backed by consent in policy. A full wipe destroys personal data.
</details>

---

### Question 27 - Domain 7: Systems and Application Security
**Scenario:** In an IaaS deployment, who is responsible for patching the guest operating system?

A. No one
B. The customer
C. The cloud provider
D. The internet service provider

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** In IaaS the provider secures the underlying platform and the customer secures the operating system, applications, data and identities. In SaaS the provider takes on most of the stack.
</details>

---

### Question 28 - Domain 7: Systems and Application Security
**Scenario:** Which risk is specific to virtual environments and means an attacker breaks out of a guest to reach the host?

A. Shoulder surfing
B. Tailgating
C. Phishing
D. VM escape

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** VM escape is the breakout from a guest virtual machine to the hypervisor or host. It is why hypervisor patching and management network isolation matter.
</details>

---
