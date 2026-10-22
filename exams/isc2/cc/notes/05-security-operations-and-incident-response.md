---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 18 min
---

# 05 - Security operations and incident response

**Domain 5: Security Operations and Incident Response (17.3%)** - in the outline effective September 1, 2026.

This domain is the day-to-day work of keeping an organization safe and handling things when they go wrong. It has five objectives: data security (5.1), security operations (5.2), incident response (5.3), asset protection (5.4), and security testing (5.5). Threat intelligence, threat frameworks, red and purple teaming, application testing, and quantum-resistant cryptography are new to the outline.

---

## 5.1 Data security

### Data handling

Data moves through a life cycle: **create, store, use, share, archive, destroy**. Handling rules follow the data through every stage, and the outline names four handling activities.

**Classification** assigns a sensitivity level so the right protection follows the data. Commercial schemes often use Public, Internal, Confidential, and Restricted; government schemes use levels such as Confidential, Secret, and Top Secret. The **data owner** (accountable for the data, usually a business leader) decides the classification; the **data custodian** (usually IT) applies the controls the owner specifies.

**Labeling** marks the data with its classification, as a visible header, a file property, or a tag, so that people and systems know how to handle it. Tools such as data loss prevention read the labels to enforce rules automatically.

**Masking** hides part of the data while keeping it usable: showing only the last four digits of a card number, or replacing real customer names with realistic fake ones in a test database. It lets developers, support staff, and analysts do their jobs without seeing the real sensitive values. Masking is also a control for AI: masking personal data before it goes into an AI tool or a training set keeps it out of the model.

**Sanitization** removes data from media so it cannot be recovered before the media is reused, sold, or thrown away. In rising order of assurance:

- **Deletion** removes the pointer to the data; the data itself is usually recoverable
- **Clearing** (overwriting) writes over the data so ordinary tools cannot recover it
- **Purging**, such as **degaussing** magnetic media or **cryptographic erasure** (destroying the encryption key so the stored ciphertext is useless), protects against laboratory recovery
- **Destruction** (shredding, pulverizing, incinerating) destroys the media itself and gives the highest assurance

Degaussing does not work on solid-state drives, which is why cryptographic erasure and physical destruction are the usual choices for SSDs. Retention rules decide **when** data is sanitized: keep it as long as law and business need require, and no longer, because data you keep is data you can lose.

### Encryption

| Type | Keys | Speed | Used for |
|---|---|---|---|
| **Symmetric** | One shared key | Fast | Bulk data encryption (AES) |
| **Asymmetric** | Public and private key pair | Slow | Key exchange, digital signatures (RSA, ECC) |
| **Hashing** | None | Fast | Integrity, password storage (SHA-256) |

**Symmetric** encryption is fast but has a key distribution problem: both sides need the same secret key, and you have to get it to the other side safely. **Asymmetric** encryption solves that: anyone can encrypt with your **public** key, and only your **private** key decrypts. A **digital signature** works the other way round: you sign with your private key, and anyone can verify with your public key, which gives authenticity, integrity, and non-repudiation. Real systems such as TLS combine the two: asymmetric to agree a symmetric key, then symmetric for the data.

**Hashing is not encryption.** It is one way, cannot be reversed, and provides integrity rather than confidentiality. Passwords are stored as salted hashes, not encrypted, so that even the system cannot recover them. A **salt** is random data added before hashing so that identical passwords produce different hashes.

### Quantum-resistant cryptography

The outline now names **quantum-resistant** (post-quantum) cryptography. A large enough quantum computer could break today's asymmetric algorithms, RSA and elliptic curve, because it can solve the maths problems they rely on far faster than a normal computer. Symmetric encryption and hashing are much less affected; longer keys, such as AES-256, are enough.

No such quantum computer exists yet, but the risk is already real because of **harvest now, decrypt later**: an attacker can record encrypted traffic today and decrypt it once quantum computers arrive. Data that must stay secret for many years, such as health records or state secrets, is exposed now.

The response is to move to new algorithms built on maths problems quantum computers are not known to solve. In 2024, NIST published the first post-quantum standards: **ML-KEM** for key exchange (FIPS 203), and **ML-DSA** (FIPS 204) and **SLH-DSA** (FIPS 205) for digital signatures. The practical first steps for an organization are an inventory of where it uses asymmetric cryptography and **crypto agility**: designing systems so algorithms can be swapped without rebuilding everything.

---

## 5.2 Security operations

### Logging and monitoring

You cannot respond to what you cannot see. Systems should log authentication attempts, authorization failures, administrative actions, configuration changes, and access to sensitive data. A **SIEM** (security information and event management) collects logs from across the organization, correlates them, and raises alerts. Logs must be protected from tampering, because attackers try to delete them, and clocks must be synchronized (with NTP) so events from different systems line up.

### Triage

A security team receives far more alerts than it can investigate in depth, so **triage** decides which alerts matter and in what order. The outline names three parts of it:

- **Incident use cases** define in advance what the team is watching for and what to do about it, such as "impossible travel: the same account signs in from two countries an hour apart". A use case turns a vague worry into a specific detection with a specific response.
- **Prioritization** ranks alerts by severity and by the value of what is affected. A malware alert on a domain controller outranks the same alert on a kiosk.
- **Correlation** links related events across sources: a phishing email, then a sign-in from a new country, then a large download is one incident, not three unrelated alerts.

AI and automation now do much of the first-pass triage, enriching and grouping alerts so analysts spend their time on the ones that need judgment.

### Threat actors

Knowing who might attack, and why, shapes which defenses matter.

| Type | Typical motivation | Typical capability |
|---|---|---|
| **Cybercriminals** | Money: ransomware, fraud, data theft for sale | Moderate to high, often organized as a business |
| **Nation-state actors** | Espionage, disruption, strategic advantage | Highest; long, patient campaigns (often called APTs) |
| **Hacktivists** | Ideology or protest | Varies; defacement, leaks, DDoS |
| **Insiders** | Grievance, money, or simple mistakes | Already have legitimate access |
| **Script kiddies** | Curiosity, notoriety | Low; use tools others wrote |
| **Competitors** | Commercial advantage | Varies; industrial espionage |

An **advanced persistent threat (APT)** is a well-resourced attacker, usually state-backed, who gets in and stays hidden for a long time. AI has lowered the skill needed for many attacks, from writing convincing phishing to automating reconnaissance, so the capability gap between actor types is narrowing.

### Cyber threat intelligence

**Cyber threat intelligence (CTI)** is evidence-based knowledge about threats: who is attacking, how, and what to look for. It comes at different levels. **Strategic** intelligence informs leaders about trends and risks. **Operational** intelligence describes specific campaigns and how actors operate. **Tactical** and technical intelligence gives defenders **indicators of compromise (IOCs)**, such as malicious IP addresses, domains, and file hashes, to load into their tools.

Sources include commercial feeds, government agencies, open-source intelligence, and industry sharing groups such as ISACs (information sharing and analysis centers). Intelligence is only useful if it is relevant to your organization and acted on; a feed nobody reads is just noise.

### Threat frameworks

Threat frameworks give defenders a shared language for how attacks unfold.

The **MITRE ATT&CK** framework is a knowledge base of real attacker behavior, organized as **tactics** (the attacker's goal at each stage, such as initial access, persistence, or exfiltration) and **techniques** (how they achieve it). Teams use it to check which techniques they can detect and to describe incidents consistently.

The **Cyber Kill Chain**, from Lockheed Martin, describes an attack as seven stages: reconnaissance, weaponization, delivery, exploitation, installation, command and control, and actions on objectives. Its lesson is that breaking any link stops the attack, so defenders should aim to disrupt it as early as possible.

**STRIDE** is a threat modeling framework rather than an attack model; it is covered under security testing below.

---

## 5.3 Incident response

### Events, incidents, and breaches

An **event** is any observable occurrence: a login, a file opened, a port scan. An **incident** is an event that harms or threatens to harm security. A **breach** is an incident in which data is accessed or disclosed without authorization, which often triggers legal notification duties.

### The incident response plan

An **incident response plan (IRP)** sets out in advance who does what when an incident happens: the team (technical responders plus legal, communications, HR, and management), how incidents are classified by severity, who must be told and when, and the steps for each phase. The phases, in order:

1. **Preparation** - the plan, the team, the tools, and the training. Everything done before an incident
2. **Detection and analysis** - recognizing that an incident is happening and working out its scope and severity
3. **Containment** - limiting the damage, for example isolating an infected machine
4. **Eradication** - removing the cause: the malware, the compromised account, the exploited vulnerability
5. **Recovery** - returning systems to normal and confirming they are clean
6. **Post-incident activity** - lessons learned, and improvements to controls and to the plan itself

### Data handling during an incident

The outline ties the data handling policy to the IRP, because an incident creates sensitive data of its own. Evidence (logs, disk images, memory captures) must be **preserved** before systems are cleaned, because containment can destroy the evidence needed to understand what happened. A **chain of custody** records who handled each piece of evidence and when, which is required if the matter reaches court. Incident data often includes the very personal data that was breached, so it must itself be classified, access-controlled, and retained according to policy. And the plan must say who may talk about the incident outside the team, since a careless message can create legal exposure.

### Incident response exercises

A plan nobody has practiced fails under pressure. **IR exercises** test it. A **tabletop exercise** walks the team through a scenario in discussion, such as "ransomware hits payroll on a Friday night", to find gaps in roles, contacts, and decisions without touching any system. **Functional exercises** and simulations practice specific actions. **Full-scale exercises** involve real systems and many teams. Every exercise should end with lessons learned and updates to the plan, exactly like a real incident.

---

## 5.4 Asset protection

### Asset life cycle management

You cannot protect what you do not know you have, so **asset management** starts with an inventory of hardware, software, cloud resources, data, and now AI models and services. Each asset is tracked through its life cycle: **acquire**, **deploy**, **maintain**, and **retire**, with its owner and classification recorded.

The outline calls out **end of life (EOL)**. When a vendor stops supporting a product, it stops issuing security patches, so every new vulnerability stays open for good. EOL software and devices should be replaced or upgraded before support ends. Where that is impossible, compensating controls apply: isolate the system on its own segment, restrict who can reach it, and monitor it closely. Retirement ends with sanitization of the media, as in 5.1.

### Configuration and change management

**Configuration management** keeps systems in a known, secure state. A **baseline** is the approved secure configuration for a type of system. **Hardening** removes what is not needed: unused services, default accounts, and default passwords. Systems are checked against their baseline so that **configuration drift** is caught. Patch management identifies, tests, deploys, and verifies updates.

**Change management** controls how changes are made: a change is requested, assessed for risk, approved, scheduled, implemented, and documented, with a rollback plan. It exists because most outages are caused by changes. Emergency changes follow a faster path but are still recorded and reviewed afterwards.

---

## 5.5 Security testing

### Red, blue, and purple teams

**Security readiness testing** checks whether defenses work against realistic attacks. A **red team** plays the attacker, using real adversary techniques to reach a goal without being caught. A **blue team** is the defense: the people who monitor, detect, and respond. A **purple team** is not a separate group so much as a way of working: red and blue collaborate openly, with the red team running a technique and the blue team checking whether it was detected, then improving detections on the spot. Red team exercises measure how good defenses are; purple teaming improves them fastest.

### Application testing

Applications are tested in several complementary ways:

- **Vulnerability scanning** checks systems and applications automatically for known vulnerabilities and missing patches. It is broad and frequent, but it finds only known issues and produces false positives that need checking.
- **Static analysis** (SAST) examines source code without running it, finding flaws such as injection or hard-coded secrets early, while the code is being written.
- **Dynamic analysis** (DAST) tests the running application from the outside, the way an attacker would, finding issues such as misconfigurations that only appear at run time.
- **Threat modeling** happens at design time. The team asks what could go wrong with the design before anything is built, often using **STRIDE**: spoofing, tampering, repudiation, information disclosure, denial of service, and elevation of privilege. Each letter is a category of threat to look for.

Fixing a flaw at design time is far cheaper than fixing it after release, which is the idea behind **shifting left**: moving testing earlier in development.

### Physical penetration testing

A **physical penetration test** checks whether people and physical controls can be beaten, always with written permission and agreed rules. The outline names three techniques. **Phishing** tests whether staff click or hand over credentials. **Tailgating** tests whether staff hold doors for strangers. **Impersonation** tests whether someone posing as a delivery driver, auditor, or IT technician is challenged. The results feed directly back into security awareness training in [notes 02](./02-security-governance.md#23-security-awareness).

---

## Key terms

- **Data classification** - assigning a sensitivity level so handling requirements follow the data
- **Data owner** - the role accountable for data, deciding its classification and who may access it
- **Data custodian** - the role implementing the controls the data owner specifies
- **Labeling** - marking data with its classification so people and systems can apply the right handling
- **Data masking** - hiding part or all of a sensitive value while keeping the data usable
- **Sanitization** - removing data from media so it cannot be recovered before reuse or disposal
- **Degaussing** - destroying data on magnetic media with a strong magnetic field
- **Cryptographic erasure** - rendering data unrecoverable by destroying the key that encrypts it
- **Symmetric encryption** - encryption using a single shared key, fast and suited to bulk data
- **Asymmetric encryption** - encryption using a public and private key pair, solving key distribution
- **Hashing** - a one-way function producing a fixed-length value, used for integrity and password storage
- **Salt** - random data added before hashing a password so identical passwords hash differently
- **Digital signature** - data signed with a private key, providing authenticity, integrity, and non-repudiation
- **Quantum-resistant cryptography** - algorithms designed to stay secure against attack by quantum computers
- **Harvest now, decrypt later** - recording encrypted data today to decrypt it once quantum computers can
- **Crypto agility** - designing systems so cryptographic algorithms can be replaced without rebuilding them
- **SIEM** - security information and event management, centralizing and correlating log data
- **Triage** - deciding which security alerts matter and in what order to handle them
- **Incident use case** - a predefined detection scenario with an agreed response
- **Correlation** - linking related events from different sources into a single incident
- **Threat actor** - the person or group behind a threat, such as a criminal, nation-state, hacktivist, or insider
- **APT** - advanced persistent threat, a well-resourced attacker who stays hidden in a network for a long time
- **Cyber threat intelligence** - evidence-based knowledge about threats, their methods, and indicators
- **Indicator of compromise** - an observable artifact, such as a malicious IP address or file hash, that signals an intrusion
- **MITRE ATT&CK** - a knowledge base of real attacker tactics and techniques
- **Cyber Kill Chain** - Lockheed Martin's seven-stage model of how an attack unfolds
- **Event** - any observable occurrence in a system or network
- **Incident** - an event that harms or threatens to harm security
- **Breach** - an incident involving unauthorized access to or disclosure of data
- **Incident response plan** - the documented approach to detecting, containing, and recovering from incidents
- **Containment** - the incident response phase that limits the damage of an ongoing incident
- **Eradication** - the incident response phase that removes the cause of the incident
- **Chain of custody** - documentation of who handled evidence, when, and how
- **End of life** - the point after which a vendor no longer supports a product or issues security patches
- **Baseline** - the approved secure configuration for a given system type
- **Hardening** - reducing a system's attack surface by removing unnecessary services and defaults
- **Configuration drift** - gradual divergence of a system from its approved baseline
- **Change management** - the controlled process for requesting, approving, and documenting changes
- **Red team** - testers who emulate real attackers to measure an organization's defenses
- **Blue team** - the defenders who monitor, detect, and respond to attacks
- **Purple team** - red and blue teams working together openly to improve detection
- **Vulnerability scanning** - automated checking of systems for known vulnerabilities and missing patches
- **Static analysis** - examining source code for security flaws without running it
- **Dynamic analysis** - testing a running application from the outside for security flaws
- **Threat modeling** - identifying what could go wrong with a design before it is built
- **STRIDE** - a threat modeling scheme: spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege
- **Physical penetration test** - an authorized test of physical and human controls using techniques such as tailgating and impersonation

---

## Related

- [Notes 01: security principles](./01-security-principles.md)
- [Scenarios](../scenarios.md) - scenarios 5, 7, and 10
- **[📖 NIST post-quantum cryptography standards](https://csrc.nist.gov/projects/post-quantum-cryptography)** - FIPS 203, 204, and 205
- **[📖 MITRE ATT&CK](https://attack.mitre.org/)** - attacker tactics and techniques
- **[📖 NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final)** - incident response recommendations
