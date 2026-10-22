# ISC2 Certified in Cybersecurity (CC) - Practice Questions

30 questions for ISC2 CC prep. Questions 16 to 30 are tagged with the domains of the ISC2 CC outline effective September 1, 2026. CC is a vocabulary exam: the textbook definition is almost always the correct answer.

> **Cert page:** [exams/isc2/cc/](../../exams/isc2/cc/)

---

### Question 1
**Scenario:** A web server runs an unpatched library with a known remote code execution flaw. Attack groups are actively scanning for it. The server holds payment records. Which term describes the unpatched library?

A. Asset, meaning the payment records an attacker would want to steal
B. Threat
C. Vulnerability
D. Risk, meaning the likelihood of exploitation combined with the business impact

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A vulnerability is the weakness. The attack groups are the threat, the payment records and server are assets, and the risk is the combination of the likelihood of exploitation and the impact if it happens.
</details>

---

### Question 2
**Scenario:** A company installs a visible warning sign stating that an area is under camera surveillance. What control function is the sign?

A. Detective (it records events as they happen)
B. Corrective (it repairs damage after an event)
C. Deterrent (discourages)
D. Preventive (it physically blocks the attempt)

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A sign discourages an attempt without physically stopping it, which is the definition of a deterrent. The camera recording is detective; a lock would be preventive; restoring from backup would be corrective.
</details>

---

### Question 3
**Scenario:** An organization buys cyber insurance to cover the financial consequence of a breach it cannot fully prevent. Which risk treatment is this?

A. Transfer, by shifting the loss
B. Avoid, by ending the risky activity altogether
C. Mitigate, by deploying monitoring and hardening so a breach becomes less likely
D. Accept, by documenting the residual exposure and carrying the loss internally

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Transfer moves the financial consequence to another party. Avoid means stopping the activity, mitigate means applying controls to reduce likelihood or impact, and accept means documenting and taking no further action.
</details>

---

### Question 4
**Scenario:** A government system labels documents Secret and Top Secret, and the system enforces clearance levels that users cannot override. Which access control model is this?

A. ABAC (attribute-based access)
B. RBAC (role-based access)
C. MAC (mandatory)
D. DAC (discretionary access)

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Mandatory access control is system-enforced from labels and clearances, and users cannot change it. DAC lets the data owner decide, RBAC attaches permissions to roles, and ABAC evaluates attributes at access time.
</details>

---

### Question 5
**Scenario:** An HR analyst can read employee records only for their own region, even though the system technically permits reading others. Which principle is this?

A. Least privilege
B. Need to know, because access follows the analyst's duties
C. Job rotation
D. Separation of duties, so that no one person controls a whole process end to end

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Need to know limits what a subject can see to what their duties require. Least privilege limits what they can do, such as read-only rather than read-write. Both often apply together, and the exam distinguishes them.
</details>

---

### Question 6
**Scenario:** A payments company can tolerate at most 15 minutes of lost transactions. Which objective does that define, and what does it drive?

A. SLA; it drives vendor selection
B. MTD; it drives the continuity plan
C. RTO; it drives recovery capability
D. RPO; it drives backup and replication frequency

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Recovery point objective is the maximum acceptable data loss measured in time, and it is satisfied by how often data is captured. Recovery time objective is the maximum acceptable downtime and is satisfied by recovery architecture.
</details>

---

### Question 7
**Scenario:** During a ransomware incident, clinical staff switch to paper forms so patient care continues. Which discipline owns this activity?

A. Disaster recovery
B. Business continuity planning
C. Incident response
D. Change management

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Business continuity keeps critical business functions running during a disruption. Incident response handles the security event itself, such as containment. Disaster recovery restores the technology.
</details>

---

### Question 8
**Scenario:** Which is the correct order of incident response phases?

A. Preparation, detection and analysis, containment, eradication, recovery, post-incident activity
B. Preparation, containment, detection, recovery, eradication
C. Detection, preparation, containment, recovery, eradication, lessons learned, restoring service before the cause is removed
D. Containment, detection, eradication, preparation, recovery

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Preparation comes first because it is everything done before an incident. Eradication removes the cause and must precede recovery, or you restore into the same compromise. Post-incident activity is where lessons learned improve both controls and the plan.
</details>

---

### Question 9
**Scenario:** A system must store user passwords so they cannot be recovered. Which cryptographic approach applies?

A. Asymmetric encryption with a protected private key
B. Symmetric encryption
C. Hashing with a unique salt
D. Digital signatures

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Hashing is one way, which is exactly the requirement. Encryption of any kind is reversible, so storing encrypted passwords is wrong. The salt ensures identical passwords do not produce identical hashes.
</details>

---

### Question 10
**Scenario:** In a SaaS deployment, who is responsible for configuring which users can access the application?

A. Vendor
B. Shared 50/50 with the provider
C. It depends on the SLA
D. The customer

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Two responsibilities never shift regardless of service model: physical datacenter security is always the provider's, and data and access configuration are always the customer's. Everything between them moves toward the provider from IaaS to SaaS.
</details>

---

### Question 11
**Scenario:** Which document type is recommended rather than mandatory?

A. Guideline, a recommendation that staff are encouraged to follow
B. Policy; it states management intent that staff may follow at their discretion
C. Procedure
D. Standard; it sets technical settings such as minimum password length that staff may adopt where convenient

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Guidelines are recommendations. Policies state mandatory intent, standards state mandatory specific requirements, and procedures are mandatory step-by-step instructions. This distinction appears reliably on the exam.
</details>

---

### Question 12
**Scenario:** A device sits inline and blocks traffic matching known attack signatures. What is it?

A. Load balancer appliance
B. Web proxy server
C. Network IDS sensor
D. Network IPS

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** An intrusion prevention system sits inline and blocks. An intrusion detection system observes and alerts without blocking. The IDS versus IPS distinction is one of the most reliably tested items in the network security domain.
</details>

---

### Question 13
**Scenario:** Which authentication combination constitutes multi-factor authentication?

A. A password and a security question
B. A password and a code from a hardware token
C. A password and a PIN
D. A fingerprint and a facial scan, because biometric checks are stronger than passwords

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** MFA requires factors from different categories: something you know, something you have, something you are. A password with a security question or PIN is two things you know. A fingerprint plus a face is two things you are.
</details>

---

### Question 14
**Scenario:** A small enclosed entry space has two interlocking doors. The second opens only after the first closes and the person is verified, so an unauthorized person cannot follow an authorized one. What is it, and what attack does it address?

A. A mantrap or access control vestibule; tailgating
B. A badge reader; shoulder surfing
C. CCTV; dumpster diving
D. A perimeter fence; eavesdropping

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A mantrap, also called an access control vestibule, is an enclosed space between two interlocking doors that admits one verified person at a time. A turnstile is a simpler one-at-a-time barrier. Tailgating is following an authorized person through without authenticating; piggybacking is being knowingly let through.
</details>

---

### Question 15
**Scenario:** Which backup type creates backups fastest but takes longest to restore?

A. Differential backup
B. Incremental
C. Full
D. Storage snapshot

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Incremental copies only changes since the last backup of any type, so each backup is small and fast, but a restore requires the full backup plus every incremental since. Differential copies changes since the last full backup, so it is slower to create and faster to restore, needing only the full plus the latest differential.
</details>

---

### Question 16 - Domain 1: Security Principles
**Scenario:** A finance manager approves wire transfers in a web app. Later, a manager denied approving a large transfer, and the company could not prove otherwise. Which control would best stop a repeat of this dispute?

A. Encrypting the approval records at rest with a strong key
B. Requiring each approval to carry the manager's digital signature
C. Backing up the approval database every hour to a second region
D. Hashing each approval record and storing the hash in the same table

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The goal is non-repudiation: proof that a specific person took an action, so they cannot credibly deny it. A digital signature made with a private key only that manager holds gives that proof. A is wrong because encryption protects confidentiality, not proof of origin. C is wrong because backups protect availability. D is wrong because a plain hash shows the record was not changed, but anyone can compute it, so it does not tie the approval to one person.
</details>

---

### Question 17 - Domain 1: Security Principles
**Scenario:** Before signing with a new payroll provider, a security analyst reviews the provider's audit reports, breach history, and contract terms. Which concept does this review demonstrate?

A. Due care, because the analyst is acting as a reasonable person would
B. Risk avoidance, because the review keeps the risk from arising
C. Non-repudiation, because the provider cannot deny its own audit findings
D. Due diligence, because the analyst is investigating before deciding

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Due diligence is the research and investigation done to understand a risk before acting. Due care is doing what a reasonable person would do once you know, such as applying the controls, so A describes the follow-through, not the research. B is wrong because avoidance means not doing the risky activity at all, and the company still plans to sign. C is wrong because non-repudiation is about proving who performed an action, not vendor assessment.
</details>

---

### Question 18 - Domain 1: Security Principles
**Scenario:** An ISC2-certified engineer is told by a manager to ship a medical device update that skips a safety test, to meet a deadline. The engineer believes the gap could harm patients. Which ISC2 Code of Ethics canon should guide the decision first?

A. Protect society, the common good, necessary public trust and confidence, and the infrastructure
B. Act honorably, honestly, justly, responsibly, and legally
C. Provide diligent and competent service to principals
D. Advance and protect the profession

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The four canons are applied in order, and protecting society comes first. Possible harm to patients is a harm to society, so it outranks the other duties. B is the second canon and still matters, but it ranks below the first. C is wrong because duty to the employer, the principal, is third and does not override public safety. D is the last canon and is not the deciding factor here.
</details>

---

### Question 19 - Domain 1: Security Principles
**Scenario:** A company writes a rule that all staff must lock their screens when they step away, and it trains every new hire on the rule. How is this control best classified by type?

A. Technical, because it applies to computer screens
B. Physical, because it relates to people leaving their desks
C. Administrative, because it is a policy enforced through training
D. Detective, because it reveals who leaves a screen unlocked

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Administrative, or managerial, controls are policies, procedures, and training that direct how people behave. A is wrong because a technical control would be the system itself forcing an automatic lock after a timeout. B is wrong because physical controls are things like locks, fences, and guards. D is wrong because detective is a control function, not a type, and the rule does not detect anything by itself.
</details>

---

### Question 20 - Domain 2: Security Governance
**Scenario:** The board wants one number that warns early when the chance of a breach is rising. Which measure is the best key risk indicator?

A. The number of security awareness courses published this quarter
B. The total security budget spent compared with the plan
C. The count of firewall rules added during the last month
D. The percentage of critical systems missing patches past their deadline

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A key risk indicator tracks exposure, so a change in the number signals that risk is growing. Overdue critical patches directly raise the likelihood of a breach. A is wrong because publishing courses measures activity, not risk, and says nothing about whether staff learned. B is a financial performance measure, not a risk signal. C is wrong because more firewall rules could mean better or worse security, so the number does not point to rising risk.
</details>

---

### Question 21 - Domain 2: Security Governance
**Scenario:** A phishing simulation shows that 30 percent of staff clicked the test link, but only 2 percent reported it. Leadership wants to build a stronger security culture. What is the best next step?

A. Make reporting simple, such as a one-click report button, and praise people who report
B. Name the employees who clicked in a company-wide email so others learn from it
C. Stop the simulations, since they upset staff and lower trust in the security team
D. Block all external email links so the click rate falls to zero

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A healthy security culture treats people as sensors. Easy reporting and positive feedback raise the report rate, which helps defenders find real phishing fast. B is wrong because public shaming discourages people from admitting mistakes and reporting. C is wrong because removing the measurement does not fix the behavior. D is wrong because blocking every link disrupts the business and does not build awareness for threats that use other channels.
</details>

---

### Question 22 - Domain 3: Identity And Access Management (IAM) Concepts
**Scenario:** A contractor's engagement ended on Friday. On Monday, logs show the contractor's account still signed in to the file server. Which identity life cycle stage failed?

A. Provisioning, because the account had too many rights at the start
B. Role definition, because contractors need their own role
C. Deprovisioning, because access was not removed when the work ended
D. Authentication, because the password should have expired

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Deprovisioning removes or disables access when a person leaves or no longer needs it, ideally triggered by the end date in the HR or vendor record. A is wrong because the problem is the timing of removal, not the rights granted at the start. B may be good practice but would not stop the account staying active. D is wrong because authentication worked as designed; the account should not have existed in an active state.
</details>

---

### Question 23 - Domain 3: Identity And Access Management (IAM) Concepts
**Scenario:** An employee has moved through three departments in five years. They still hold access from every past role. Which practice would best catch this?

A. Adding multi-factor authentication to the employee's account
B. Periodic access reviews where managers confirm each right is still needed
C. Moving the employee to a mandatory access control system
D. Requiring the employee to change their password every 30 days

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Collecting rights from past roles is called privilege creep. Regular access reviews, also called recertification, find and remove rights that are no longer needed, which restores least privilege. A is wrong because MFA makes sign-in stronger but does not reduce what the account can do. C is wrong because changing the access control model is a large redesign and is not how creep is found. D is wrong because password changes do not affect permissions.
</details>

---

### Question 24 - Domain 3: Identity And Access Management (IAM) Concepts
**Scenario:** In an accounts payable team, one clerk can both add a new vendor to the system and approve payments to that vendor. An auditor flags this. Which principle is being violated?

A. Need to know, because the clerk sees too much vendor data
B. Least privilege, because the clerk can read the payment history
C. Defense in depth, because there is only one control layer
D. Separation of duties, because one person controls both steps

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Separation of duties splits a sensitive process so no single person can complete it alone. Here one clerk could create a fake vendor and pay it. A is wrong because the issue is control over actions, not visibility of data. B is related, but the specific flaw is combining two conflicting duties in one role. C is a network and architecture concept about layered controls, not about splitting a business process.
</details>

---

### Question 25 - Domain 4: Networking and Cloud Security Concepts
**Scenario:** A factory adds smart sensors and building controllers that cannot run endpoint security software and rarely receive updates. They share a flat network with office laptops. What should the security team do first?

A. Place the devices on their own VLAN or zone, with firewall rules that allow only the traffic they need
B. Give each device a public IP address so the vendor can manage it directly
C. Disable logging on the devices to reduce load on the network
D. Replace the office laptops with thin clients so nothing can reach the devices

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** IoT and industrial control devices that cannot be hardened should be segmented, so a compromise in one zone cannot spread to the other. Firewall rules between zones limit traffic to what is required. B is wrong because exposing the devices to the internet greatly raises their risk. C is wrong because logging helps detection and should be kept. D is wrong because it is costly and still leaves the devices on a shared flat network.
</details>

---

### Question 26 - Domain 4: Networking and Cloud Security Concepts
**Scenario:** A company is moving to a Zero Trust model. A user on the office network asks why they now need to verify their identity to reach an internal app. What is the correct explanation?

A. Zero Trust means no one is trusted, so users are blocked until IT approves each request by hand
B. Zero Trust only applies to remote users, so the office request is a configuration error
C. Network location grants no trust, so each request is verified based on identity, device, and context
D. Zero Trust replaces firewalls, so the app now checks identity instead of the network

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Zero Trust removes implicit trust based on being inside the network. Every request is checked each time using identity, device health, and other signals, then given the least access needed. A is wrong because access is automated and policy based, not a manual approval for every request. B is wrong because Zero Trust applies the same rules inside and outside the office. D is wrong because firewalls and segmentation remain part of a layered design.
</details>

---

### Question 27 - Domain 4: Networking and Cloud Security Concepts
**Scenario:** An online retailer's traffic jumps tenfold on a holiday weekend. Its cloud service adds servers automatically during the spike and removes them afterward. Which cloud characteristic does this show?

A. Resource pooling
B. Rapid elasticity
C. Broad network access
D. Measured service

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Rapid elasticity means capacity grows and shrinks quickly to match demand, often automatically. A is wrong because resource pooling means the provider serves many customers from shared hardware. C is wrong because broad network access means the service is reachable over the network from many device types. D is wrong because measured service means usage is metered and billed, which happens here too but is not what the scenario describes.
</details>

---

### Question 28 - Domain 5: Security Operations and Incident Response
**Scenario:** A hospital is retiring laptops whose drives held patient records. The laptops will be sold to a recycler for reuse. What should happen to the drives first?

A. Delete the patient files and empty the recycle bin
B. Run a quick format so the drives appear empty
C. Remove the drive labels so no one knows what they held
D. Sanitize the drives with a verified purge method, such as cryptographic erase, and record it

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Sanitization makes data unrecoverable before media leaves the organization's control. A verified purge, such as cryptographic erase on an encrypted drive, plus a record of it, fits reuse. Physical destruction would be needed if the drives were not reused. A is wrong because deleted files can usually be recovered. B is wrong because a quick format leaves most data in place. C is wrong because removing labels hides nothing on the drive itself.
</details>

---

### Question 29 - Domain 5: Security Operations and Incident Response
**Scenario:** A company has just written its incident response plan. Leaders want to check that each team knows its role, without any risk to production systems. Which exercise fits best?

A. A tabletop exercise where teams talk through a realistic scenario step by step
B. A full interruption test that shuts down production to force the plan into use
C. A red team engagement that attacks live systems without warning
D. An external vulnerability scan of the public website

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A tabletop is a discussion-based exercise. It tests roles, communication, and decisions with no impact on systems, which makes it the right first test of a new plan. B is wrong because a full interruption test carries real business risk and is used only for mature plans. C is wrong because a red team tests defenses against live attack, not whether staff understand the plan. D is wrong because a scan finds technical weaknesses and does not exercise the response plan at all.
</details>

---

### Question 30 - Domain 5: Security Operations and Incident Response
**Scenario:** A development team wants to find security flaws in its source code before the application is ever built or run. Which testing approach should they add to the pipeline?

A. Dynamic analysis of the running application in a test environment
B. A physical penetration test of the developers' office
C. Static analysis of the source code
D. A purple team exercise against production

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Static analysis examines source code without running it, so it can flag flaws early in the pipeline. A is wrong because dynamic analysis needs a running application, which the team does not have yet. B is wrong because it tests building security, such as tailgating, not code. D is wrong because a purple team exercise is red and blue teams working together on live defenses, not a code review step.
</details>

---

## Scoring guide

- **26-30 correct (85%+):** Ready. The pass mark is 700/1000 on a scaled score.
- **20-25 correct (65-84%):** Drill the definition pairs in the [readiness check](../../exams/isc2/cc/practice-plan.md#readiness-check).
- **Below 20:** Work the [scenarios](../../exams/isc2/cc/scenarios.md) and the free ISC2 self-paced training.

CC rewards the standard textbook answer over the clever real-world nuance. If two options both seem defensible, pick the one a textbook would give.
