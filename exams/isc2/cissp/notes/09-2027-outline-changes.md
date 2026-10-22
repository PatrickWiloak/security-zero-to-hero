---
last-updated: 2026-10-22
difficulty: advanced
reading-time: 30 min
---

# CISSP 2027 Exam Outline - What Changes on April 15, 2027

ISC2 has published the next CISSP exam outline. **Effective April 15, 2027, the CISSP exam is based on the new outline**; until then, the April 2024 outline that notes 01 to 08 follow is the one tested. The exam format does not change.

This page compares the two outlines line by line and teaches the content that is new. If your exam is before April 15, 2027, treat it as optional reading (most of the new topics are good security practice anyway). If it is on or after that date, study it alongside notes 01 to 08.

**[📖 CISSP exam outline page](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline)** - both the current and the 2027 outlines
**[📖 CISSP 2027 exam outline (PDF)](https://edge.sitecorecloud.io/internationf173-xmc4e73-prodbc0f-9660/media/Project/ISC2/Main/Media/documents/exam-outlines/2027/EXAMS-CISSP-Exam-Outline-English-RB-Revised-1016-ENU-2.pdf)** - the full 2027 outline

## Domain weights

| Domain | 2024 outline | 2027 outline | Change |
|--------|------------:|-------------:|-------:|
| 1. Security and Risk Management, renamed **Security Governance and Risk Management** | 16% | 13.6% | -2.4 |
| 2. Asset Security | 10% | 12% | +2.0 |
| 3. Security Architecture and Engineering | 13% | 12.8% | -0.2 |
| 4. Communication and Network Security | 13% | 12.8% | -0.2 |
| 5. Identity and Access Management (IAM) | 13% | 13.6% | +0.6 |
| 6. Security Assessment and Testing | 12% | 11.2% | -0.8 |
| 7. Security Operations | 13% | 12.8% | -0.2 |
| 8. Software Development Security | 10% | 11.2% | +1.2 |

The weights flatten: no domain is now worth more than 13.6%, so the exam rewards breadth more than ever. The biggest moves are Domain 1 shrinking and Domains 2 and 8 growing. Domain 1's new name signals the emphasis: governance is the frame, risk management sits inside it.

The overall pattern of the content changes is modernization rather than restructuring: AI, quantum, passwordless authentication, cloud-native protection, current endpoint and SOC tooling, and secure software supply chain practice. Most objective numbers stay the same.

---

## Domain 1 - Security Governance and Risk Management

### What changed

- **1.1 adds "Ethics in Artificial Intelligence (AI)"** alongside the ISC2 Code of Ethics and organizational ethics.
- **1.3 becomes "Evaluate, apply, and sustain security governance principles"** (adding *sustain*). PCI is now named **PCI DSS**.
- **1.4 adds HIPAA** to the named privacy laws; **1.5** drops "industry standards" from the investigation types, leaving administrative, criminal, civil, and regulatory.
- **1.8 personnel policies** now give **service-level agreements** as the example of vendor and contractor controls.
- **1.9 risk management** adds "risk mitigation strategies" as a risk response example, adds HIPAA to the named frameworks, and broadens "risk maturity modeling" to **maturity modeling** under continuous improvement.
- **1.11 supply chain risk** adds **reputational** risk and spells out **SBOM**.
- **1.12 becomes "Establish, maintain, and measure"** a security awareness program, adds **stakeholder engagement** to effectiveness evaluation, and drops social engineering and phishing as named training methods (security champions and gamification remain).

### Ethics in AI

AI ethics is about using AI in ways that are fair, transparent, accountable, and respectful of privacy. For a security professional, it becomes concrete in a few recurring questions:

- **Fairness and bias.** Is a model making decisions that disadvantage groups of people because of skewed training data? A fraud model that flags one demographic more often is an ethical and legal risk.
- **Transparency and explainability.** Can the organization explain an AI-driven decision to the person affected, a regulator, or a court?
- **Accountability.** A named human owner is responsible for each AI system's outcomes. "The model decided" is not an answer.
- **Privacy and consent.** Was personal data used to train or prompt the model with a lawful basis and within the purpose people agreed to?
- **Safety and misuse.** Could the system cause harm if it is wrong, or be turned to harmful use?

The CISSP lens is the professional one: the ISC2 Code of Ethics asks members to protect society and act honorably. When a question presents an AI deployment that is profitable but unfair or opaque, the ethical answer raises it through governance (an AI policy, an ethics or risk review, human oversight) rather than quietly approving or unilaterally blocking it.

### Measuring awareness programs

"Measure" is now in the objective title. Effective programs track behavior, not attendance: phishing simulation report rates (not only click rates), incidents caused by human error, time to report, and results trended by team. **Stakeholder engagement** means involving business leaders in setting goals and reading results, so awareness becomes part of how the business manages risk rather than an annual compliance module.

---

## Domain 2 - Asset Security (now 12%)

### What changed

- **2.3 provision information and assets securely** gains explicit examples for physical and digital/electronic assets: **data encryption at rest and in transit**, **secure media destruction**, a **data management policy**, and data maintenance.
- **2.4 data lifecycle** reorders roles and states.
- **2.5 becomes "Ensure appropriate asset management (e.g., End of Life (EOL), End of Support (EOS))"** (it was "asset retention") and adds **asset management policy**, **asset retention**, and **asset retirement**.
- **2.6** changes "standards selection" to **standards and controls selection** and adds **Cloud-Native Application Protection Platform (CNAPP)** to the data protection methods alongside DLP and CASB.

### Asset management through end of life

The domain grew two points, and the new 2.5 explains why: assets do not stop being risks when they stop being useful. **End of life (EOL)** means the vendor no longer sells or develops a product; **end of support (EOS)** means it no longer issues security patches. An EOS operating system on a network is a permanently unpatched vulnerability. An asset management policy defines ownership, inventory, tracking, and what happens at retirement: data sanitized to a standard that fits its classification, licenses and accounts revoked, and the asset removed from inventory and monitoring. Retention is the other half: keep assets and data as long as legal and business needs require, and no longer.

### CNAPP

A **Cloud-Native Application Protection Platform** combines posture management (cloud and Kubernetes misconfiguration), workload protection (runtime threats in VMs, containers, and serverless), identity entitlement analysis, and code-to-cloud scanning into one platform. Its value is context: it can see that a container image has a critical vulnerability, runs with an over-privileged identity, and is exposed to the internet, and rank that combination above three separate findings.

---

## Domain 3 - Security Architecture and Engineering

### What changed

- **3.1 secure design principles** adds **well-architected framework**, **rotation of duties**, and **two-person integrity**, renames secure access service edge to **SASE**, and adds privacy-enhancing technologies under privacy by design.
- **3.4** adds the **Hardware Security Module (HSM)** to information system security capabilities.
- **3.5** reorganizes system types and adds **supply chain risk**, **autonomous systems**, and **quantum computing**, folds serverless and **Function as a Service (FaaS)** into cloud models, and groups **OT and ICS** together.
- **3.6 cryptography** replaces "quantum" with **post-quantum** in the algorithm list, adds access management to key management practices, and changes "quantum key distribution" to "key distribution".
- **3.7 cryptanalytic attacks** renames man-in-the-middle to **adversary-in-the-middle** and adds **zero-day attacks** and **AI threats (e.g., adversarial AI, AI model poisoning, deepfake attacks)**.
- **3.10 information system lifecycle** adds **continuous security review** and **secure architectural design**, and **retirement/secure disposal**.

### Quantum computing and post-quantum cryptography

A sufficiently large quantum computer could run **Shor's algorithm** and break the public-key algorithms that protect key exchange and signatures today: RSA, Diffie-Hellman, and elliptic curve cryptography. Symmetric encryption and hashing are much less affected (Grover's algorithm roughly halves their effective strength, so AES-256 remains strong).

The near-term risk is **"harvest now, decrypt later"**: an adversary records encrypted traffic today and decrypts it once a capable quantum computer exists. Data that must stay confidential for many years is already exposed to that risk.

**Post-quantum cryptography (PQC)** means new public-key algorithms believed to resist quantum attack, running on ordinary computers. NIST published the first PQC standards in August 2024: **ML-KEM** (FIPS 203, key encapsulation), **ML-DSA** (FIPS 204, signatures), and **SLH-DSA** (FIPS 205, hash-based signatures). The manager's task is **crypto-agility**: inventory where public-key cryptography is used, prioritize long-lived sensitive data, and plan migration (often through hybrid schemes that combine a classical and a post-quantum algorithm during transition).

### AI threats

- **Adversarial AI** crafts inputs that cause a model to misbehave, for example an image altered imperceptibly so a classifier mislabels it, or malware modified to evade an AI detector.
- **Model poisoning** corrupts training data or the model itself so it learns attacker-chosen behavior.
- **Deepfake attacks** use synthetic audio or video to impersonate trusted people, usually to authorize payments or reset credentials.

Defenses combine data provenance and integrity for training data, adversarial testing, monitoring model behavior in production, and process controls that do not rely on recognizing a face or voice (out-of-band verification for payments and resets).

### Two-person integrity and rotation of duties

**Two-person integrity** requires two authorized people to be present or approve for a critical action, such as accessing a key ceremony or releasing a production change, so no single person can act alone. It is stronger than separation of duties, which divides a process between people but may let each act alone on their part. **Rotation of duties** moves people through roles periodically, which surfaces fraud that depends on one person hiding it and reduces key-person dependency.

### Autonomous systems

Systems that act without human intervention (self-driving vehicles, drones, industrial robots, autonomous software agents) raise security questions about integrity of sensor inputs, safe failure modes, the authority they hold, and how humans can override them. The principle to apply: an autonomous system's permissions and failure behavior must be designed for the case where its inputs are manipulated.

---

## Domain 4 - Communication and Network Security

Mostly editorial: acronyms expanded, **content delivery networks** replacing content distribution networks, **SD-WAN** named, "video meeting rooms" replacing a product name, and **remote working** added under remote access. **Software-defined security** moves here from Domain 8, under software-defined networking: security controls (firewalls, segmentation, policy) defined and deployed as code through APIs, so they scale and change with the infrastructure.

---

## Domain 5 - Identity and Access Management (now 13.6%)

### What changed

- **5.1 becomes "Manage physical and logical access to assets (e.g., provision, control, review, revoke)"** and adds **identities** as an asset type.
- **5.2** adds **passwordless authentication (e.g., FIDO, WebAuthn, passkeys, biometrics)** as its own item, separate from AAA.
- **5.4 authorization mechanisms** names **rule-based access control (RuBAC)** and replaces risk-based access control with **Risk-Adaptable Access Control (RAdAC)**.
- **5.5** adds administrator groups and **least privilege** to the privilege escalation example.
- **5.6 becomes "Implement authentication and authorization systems"**.

### Passwordless authentication

Passwords fail in predictable ways: reuse, phishing, and credential stuffing. **FIDO2** standards replace them with public-key cryptography. During registration, the authenticator (a security key, a phone, or a laptop's built-in authenticator) creates a key pair for that specific website; the private key never leaves the device. At sign-in, the site sends a challenge and the authenticator signs it after the user unlocks it with a PIN or biometric. **WebAuthn** is the browser API that makes this work on the web. A **passkey** is a FIDO2 credential, which may be synced across a user's devices by their platform provider or bound to one device.

Why it matters: the credential is bound to the site's origin, so a phishing site on a look-alike domain gets nothing usable. There is no shared secret on the server to steal. The trade-offs are recovery (what happens when a user loses every device) and legacy systems that cannot accept it.

### RAdAC

**Risk-Adaptable Access Control** makes access decisions by weighing the security risk of granting access against the operational need for it, in real time. It considers the user's trust level, device state, location, sensitivity of the resource, and current threat conditions, and may allow access in an emergency that it would deny in normal times, with that decision logged and reviewed. It is the logic behind modern conditional access engines. **RuBAC** (rule-based access control) applies fixed rules to all subjects, such as "no access outside business hours", and differs from role-based access control, which grants by job role.

---

## Domain 6 - Security Assessment and Testing

- **6.2** removes the red, blue, and purple team example from penetration testing, adds **misuse case testing**, and replaces "breach attack simulations" with **attack simulations**.
- **6.4 becomes "Analyze test/audit output and generate report"**, and "ethical disclosure" becomes **responsible disclosure**: reporting a discovered vulnerability privately to the vendor with time to fix it before publication.

Misuse case testing writes test cases from the attacker's point of view ("as a malicious user, I try to view another customer's order by changing the ID in the URL") and verifies the system refuses.

---

## Domain 7 - Security Operations

### What changed

- **7.2 logging and monitoring** adds **Security Orchestration, Automation, and Response (SOAR)** and gives DLP as the example of egress monitoring.
- **7.4 foundational concepts** adds defense in depth as an example and replaces "data at rest/data in transit" with **data states (in use, in transit, at rest)**; service-level agreements leave this list.
- **7.7 detective and preventive measures** replaces anti-malware with **endpoint protection (anti-malware, EDR, XDR)**, renames whitelisting and blacklisting to **allowlist and denylist**, and gives **DDoS scrubbing services** and **managed security service providers** as third-party security services.
- **7.10 recovery strategies** adds **immutable and encrypted** backups and **warm** sites.
- **7.11 disaster recovery** adds **metrics (baseline, MTTR, MTBF)**.
- **7.12 DR plan testing** simplifies communication to internal and external.
- **7.14 physical security** renames perimeter controls to **external security controls**; **7.15** drops the social media and 2FA fatigue examples.

### SOAR, EDR, and XDR

**EDR** records detailed endpoint telemetry (processes, files, network connections) and lets responders investigate and contain a device. **XDR** correlates signals across endpoints, identity, email, cloud, and network into single incidents. **SOAR** automates the response workflow: enrichment, ticketing, and containment steps defined as playbooks. Together they shorten detection and response; the CISSP-level point is that automation needs governance (which actions may run without approval, and how to roll them back).

### Immutable backups and recovery metrics

Ransomware operators delete or encrypt backups before they encrypt production. **Immutable** backups cannot be changed or deleted until their retention expires, even by an administrator, which removes that option. **Encrypted** backups protect confidentiality if the media is stolen. **MTTR** (mean time to repair or restore) and **MTBF** (mean time between failures) join RTO and RPO as the numbers that show whether DR capability meets the business's requirements.

---

## Domain 8 - Software Development Security (now 11.2%)

### What changed

- **8.1 SDLC** adds the **Secure Software Development Framework (SSDF)** and **SBOM requirements**, and **shift left**.
- **8.2 development ecosystems** adds **memory-safe** and object-oriented examples under programming languages; CI/CD stays.
- **8.3** lists SAST and DAST as the application security testing examples; **software composition analysis** moves to 8.4 under open source.
- **8.4 acquired software** adds **Function as a Service** to cloud services.
- **Software-defined security** moves out to Domain 4.

### SSDF, SBOM, and shift left

The **NIST Secure Software Development Framework (SP 800-218)** organizes secure development into four groups of practices: prepare the organization, protect the software, produce well-secured software, and respond to vulnerabilities. US federal procurement asks software suppliers to attest to it, which is why it reaches the CISSP outline. An **SBOM** lists every component in a software product so buyers and builders can find affected products quickly when a component vulnerability is announced. **Shift left** means moving security activities earlier in the life cycle (threat modeling in design, SAST in the IDE and pull request) where defects are cheapest to fix.

### Memory-safe languages

Memory corruption (buffer overflows, use-after-free) has historically caused a large share of serious vulnerabilities in software written in C and C++. **Memory-safe languages** such as Rust, Go, Java, and C# prevent those classes of bug by design. The security manager's decision is not "rewrite everything" but "write new components, and rewrite the most exposed ones, in memory-safe languages", with the trade-off of skills, performance, and migration cost.

---

## Related

- [Notes 01: security and risk management](./01-security-and-risk-management.md) through [notes 08: software development security](./08-software-development-security.md)
- [MFA and passkeys](../../../../learn/concepts/mfa-and-passkeys.md) and [software supply chain security](../../../../learn/concepts/software-supply-chain-security.md) - concept pages behind Domains 5 and 8
- [AI safety and security](https://ai.noblerworks.com/safety/) - AI threats and governance in more depth
