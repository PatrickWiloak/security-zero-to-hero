---
last-updated: 2026-10-22
difficulty: advanced
---

# CCSP - Certified Cloud Security Professional - Practice Questions

30 questions across the six CCSP domains: cloud concepts and architecture, cloud data security, cloud platform and infrastructure security, cloud application security, cloud security operations, and legal, risk and compliance.

CCSP rewards vendor-neutral thinking. Answers describe concepts and processes rather than a specific provider's service names.

> **Cert page:** [exams/isc2/ccsp/](../../exams/isc2/ccsp/)

---

### Question 1
**Scenario:** What are the phases of the cloud secure data lifecycle?

A. Ingest, process, output, the three stages a data pipeline uses to move records through a cloud analytics platform
B. Collect, analyze, report
C. Create, store, use, share, archive, destroy
D. Create, store, use, and delete, with no separate share, archive, or destroy phases

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The lifecycle is a CCSP staple because controls differ per phase, and the question is usually which control belongs where. Destroy in cloud typically means cryptographic erasure, since you cannot physically destroy media you do not own.
</details>

---

### Question 2
**Scenario:** Data must be rendered unrecoverable on a cloud provider's multi-tenant storage.

A. Overwriting the volumes several times with random patterns, which the provider's replication guarantees reaches every copy
B. Physical destruction of the drives by shredding them in the provider's data center
C. Cryptoshredding: destroy the keys so the ciphertext is unrecoverable
D. Degaussing the drives before they return to the provider's shared storage pool

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Physical media methods are unavailable to a tenant and overwriting cannot guarantee coverage of every replica. Cryptographic erasure is the recognized cloud answer, and it only works if the data was encrypted with keys you control.
</details>

---

### Question 3
**Scenario:** Which technique replaces sensitive values with non-sensitive surrogates that can be reversed by an authorized system?

A. Hashing, which turns each value into a fixed-length digest that a stored key can convert back
B. Tokenization, with a token vault mapping each token back to the original value for authorized systems
C. Anonymization
D. Masking

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Tokenization is reversible through the vault, which is what makes it work for payment card scope reduction. Hashing is one-way, masking obscures for display, and anonymization is meant to be irreversible.
</details>

---

### Question 4
**Scenario:** Which cloud deployment model serves a group of organizations with shared concerns?

A. Private cloud, provisioned for exclusive use by a single organization, whether on its premises or hosted by a third party
B. Community cloud
C. Public cloud open to any customer
D. Hybrid cloud joining two cloud types

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The four NIST models are public, private, community, and hybrid. Community is the one candidates forget: a shared infrastructure for organizations with common compliance or mission requirements, such as a government or healthcare consortium.
</details>

---

### Question 5
**Scenario:** What does a Type 2 SOC 2 report add over a Type 1?

A. Nothing beyond Type 1, other than a newer date on the cover page
B. A different scope
C. A financial audit
D. Testing of operating effectiveness over a period, not design at a point in time

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Type 1 answers whether the controls are designed appropriately as of a date; Type 2 answers whether they actually worked across a period, typically 6 to 12 months. SOC 1 covers financial reporting controls and SOC 3 is the public summary.
</details>

---

### Question 6
**Scenario:** A cloud application must be assessed for vulnerabilities during development.

A. Runtime monitoring in production, using the provider's logs to find injection attempts and unpatched libraries as they occur
B. A code review only
C. Penetration testing only, run once after release by an outside firm against the live production site
D. SAST on source, SCA on dependencies, DAST on the running app, and threat modeling in design

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The techniques find different classes of defect, which is why they are layered rather than alternatives. Software composition analysis matters disproportionately in cloud applications, where most of the code is third-party dependencies.
</details>

---

### Question 7
**Scenario:** Which best describes a cloud access security broker?

A. A control point between users and cloud services enforcing policy and visibility
B. An identity provider that issues tokens and federates sign-on, giving users single sign-on to every SaaS application
C. A load balancer
D. A firewall at the network edge that filters traffic by port and protocol and drops unwanted connections

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** CASBs address shadow IT discovery and consistent policy across SaaS that individual applications cannot provide. API-based deployment inspects data at rest in the service; proxy-based deployment sits inline and sees traffic in real time.
</details>

---

### Question 8
**Scenario:** Virtualization introduces which distinctive risk?

A. Hypervisor escape, inter-VM attacks, VM sprawl, and snapshot data leakage
B. None, because the hypervisor isolates tenants completely and the main concern is only guest operating system patching
C. Only physical risk, such as theft of servers from the provider's data centers or sites
D. Only network risk, such as denial of service against the provider's public endpoints

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The hypervisor is a shared trust boundary, so a compromise there crosses every tenant on the host. Snapshots are the quieter risk: they capture memory and disk including secrets, and they are frequently stored with weaker controls than the running system.
</details>

---

### Question 9
**Scenario:** A business impact analysis is being performed for a cloud-hosted service.

A. Assume the provider handles continuity
B. Identify critical processes, maximum tolerable downtime, and dependencies including the provider's, then derive RTO and RPO
C. Copy the provider's published SLA into the plan and use its uptime commitment as the recovery objective
D. Focus on technical recovery only

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The BIA drives the recovery objectives, not the other way around. Provider dependency mapping is the cloud-specific addition, because a regional service outage can take down a component you never considered separately.
</details>

---

### Question 10
**Scenario:** Which key management approach gives the customer the most control in a cloud service?

A. Provider-managed keys
B. No encryption
C. Provider-generated customer-managed keys, created and rotated inside the provider's KMS under the customer's access policies
D. Hold Your Own Key: keys stay in customer-controlled infrastructure and the provider requests use

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Control escalates from provider-managed, to customer-managed within the provider's KMS, to bring your own key, to hold your own key. Each step increases control and increases the customer's operational burden and the risk of locking themselves out.
</details>

---

### Question 11
**Scenario:** An eDiscovery request covers data held by a cloud provider.

A. The customer remains responsible; the contract should cover preservation and collection
B. It cannot be fulfilled, because multi-tenant storage cannot be placed under legal hold by the customer or the provider
C. Only the provider's own data is discoverable, not the customer's data or backups in the service
D. The provider handles it entirely under its standard terms, since it controls the storage and so owns the legal hold

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Legal hold in a multi-tenant environment is a contractual capability rather than a technical one you can perform yourself. Agreeing it before the litigation is what makes it possible; negotiating it after is not a strong position.
</details>

---

### Question 12
**Scenario:** Which control best addresses the risk of a malicious insider at the cloud provider?

A. Customer-held keys, comprehensive logging, and contractual and audit assurance over provider personnel
B. Multi-factor authentication for customer staff and conditional access, which protects the customer's own console logins
C. Trusting the provider
D. Network segmentation

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** You cannot administer the provider's staff, so the durable technical control is making the data unreadable without your keys. The rest is assurance: background screening, separation of duties, and privileged access monitoring evidenced through audit reports.
</details>

---

### Question 13
**Scenario:** Which describes the correct approach to security in a DevOps pipeline?

A. Manual review before release
B. A single security gate at the end of the pipeline, where a dedicated team signs off each release candidate before production
C. Integrated security: threat modeling, automated scans, policy as code, managed secret store
D. Post-deployment scanning only

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A single gate at the end becomes the bottleneck teams route around, and it finds problems at their most expensive point. Secrets in code and in CI variables are the specific recurring failure, which is why a managed secret store is called out.
</details>

---

### Question 14
**Scenario:** Which logging capability is most important for cloud security operations?

A. Provider status pages
B. Management plane and API logs, centralized in tamper-resistant storage with retention, plus workload logs
C. Application logs only, because the services running in the workload are where an attack on customer data is seen first
D. Billing records

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The control plane is where an attacker with credentials does the most damage in the least time. Making those logs immutable and stored in an account the compromised identity cannot reach is what preserves them through an incident.
</details>

---

### Question 15
**Scenario:** How should a cloud provider's compliance certifications be used in a customer's own compliance program?

A. As a full transfer of the requirement, because the provider's certificate means the customer has no controls left to prove
B. As a replacement for the customer's own audit, since the provider's auditor has already examined the whole service and no further evidence is needed
C. As inherited controls for the provider's share, with the customer documenting its own and complementary controls
D. As irrelevant

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Inheritance is real and useful: you do not re-audit the provider's data centers. What remains is everything above the responsibility line plus the controls the provider's report assumes you implement, which is the part most often skipped.
</details>

---

### Question 16 - Domain 1: Cloud Concepts, Architecture and Design
**Scenario:** A team must run a legacy application that needs a custom hardened operating system build, its own host-based agents, and full control of OS patch timing. Which service model fits?

A. SaaS, because the provider patches everything and the team only manages users and data
B. IaaS, because the customer controls the guest OS, its hardening, agents, and patch schedule
C. PaaS, because the provider runs the runtime while the team still installs agents on the host
D. Serverless functions, because each invocation runs on a fresh OS image the team can harden

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Only IaaS hands the guest operating system to the customer, so custom hardening, host agents, and patch timing all stay in the customer's control. A is wrong because SaaS gives no OS access at all. C is wrong because in PaaS the provider owns the OS and runtime, so the team cannot install host agents or set patch timing. D is wrong because serverless hides the OS completely and the provider controls the execution image.
</details>

---

### Question 17 - Domain 1: Cloud Concepts, Architecture and Design
**Scenario:** Leadership worries that a new platform will be hard to move to another provider in five years. Which design choice does the most to keep that option open?

A. Use as many provider-native managed services as possible, because they reduce operating effort
B. Sign a longer contract, because a multi-year term guarantees the provider's prices and features
C. Replicate every workload to a second provider now, because a live copy proves the move works
D. Package workloads in portable formats, use open standards and APIs, and confirm data export terms

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Portability comes from formats and interfaces that another provider can run, plus a contractual right to get your data out in a usable form. A is wrong because proprietary managed services are the main source of lock-in, even though they cut effort. B is wrong because a longer term deepens commitment rather than easing exit. C is wrong because running two clouds at once is costly and complex, and it is not needed to keep the option of moving open.
</details>

---

### Question 18 - Domain 1: Cloud Concepts, Architecture and Design
**Scenario:** A regulated customer requires that encryption in a candidate provider's service uses independently validated cryptographic modules. What evidence should the security architect ask for?

A. A current FIPS 140-3 validation certificate for the modules the service actually uses
B. A Common Criteria evaluation of the provider's web console at any assurance level
C. The provider's marketing page stating that all data is encrypted with strong algorithms
D. A SOC 2 Type 2 report, because it tests every cryptographic module in the service

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** FIPS 140-3 is the program that validates cryptographic modules, and the certificate should match the modules in the service in scope. B is wrong because a Common Criteria evaluation of the console says nothing about the crypto modules. C is wrong because a marketing claim is not independent validation. D is wrong because SOC 2 tests controls against the trust services criteria, not the cryptographic implementation of each module.
</details>

---

### Question 19 - Domain 2: Cloud Data Security
**Scenario:** A company has years of unstructured files in cloud object storage and no idea which ones hold personal data. What should it do first to protect them?

A. Encrypt every bucket with a new key, because encryption removes the need to know what is stored
B. Delete files older than one year, because old data is the most likely to contain personal data
C. Run automated data discovery and classification, then apply controls based on what is found
D. Move all files to archive storage, because archived data is out of scope for privacy rules

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** You cannot apply the right controls to data you have not found and labeled, so discovery and classification come first. A is wrong because encryption at rest is useful but does not tell you where personal data is, who can read it, or what retention applies. B is wrong because deleting by age alone may breach retention duties and is not based on content. D is wrong because archived personal data is still in scope for privacy law.
</details>

---

### Question 20 - Domain 2: Cloud Data Security
**Scenario:** A legal team shares sensitive design documents with an outside partner through a cloud file service. They need to stop printing and be able to revoke access after the project ends, even for copies already downloaded. Which control fits?

A. A data loss prevention policy that blocks uploads of the documents to personal storage
B. Information rights management, which binds usage policy to the file and checks it on each open
C. Encryption at rest in the file service, with the keys held in the company's own key manager
D. A shared link that expires after 30 days and requires the partner to sign in first

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** IRM travels with the file, so print restrictions and revocation apply even after download, because each open checks the policy. A is wrong because DLP watches data moving through channels it controls and does not govern a copy the partner already holds. C is wrong because encryption at rest protects data in the service, but a downloaded copy is already decrypted. D is wrong because link expiry stops new downloads but not use of existing copies.
</details>

---

### Question 21 - Domain 2: Cloud Data Security
**Scenario:** Developers ask for a copy of the production customer database in a cloud test environment so they can debug realistic cases. What is the best way to meet the need?

A. Give them read-only access to production, because read access cannot change customer records
B. Copy production as is, but restrict the test account to the senior developers only
C. Hash every column, because hashed values look realistic and keep all relationships working
D. Create a statically masked copy that keeps format and relationships but replaces real values

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Static masking produces realistic, consistent test data without exposing real customer values outside production. A is wrong because read access still exposes all real personal data to people who do not need it. B is wrong because a full copy in a less controlled environment is a breach risk, however few people have access. C is wrong because hashing every column breaks formats, dates, and many application rules, so the data is often unusable for testing.
</details>

---

### Question 22 - Domain 3: Cloud Platform and Infrastructure Security
**Scenario:** An organization's cloud account has a root or top-level owner identity that can override every other permission. How should it be handled?

A. Protect it with phishing-resistant MFA, use it only for break-glass tasks, and alert on every use
B. Share it among the operations team so someone can always reach it in an emergency
C. Use it for daily administration, because it avoids permission errors that slow down the team
D. Delete its password entirely, because the provider can always restore access if it is needed

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The top-level identity is the highest value target in the management plane, so it gets the strongest authentication, almost no use, and an alert whenever it is used. B is wrong because a shared credential has no individual accountability and is easier to leak. C is wrong because daily use maximizes exposure and breaks least privilege. D is wrong because recovery through the provider can be slow and is not a reliable emergency path.
</details>

---

### Question 23 - Domain 3: Cloud Platform and Infrastructure Security
**Scenario:** A service has an RTO of 4 hours and an RPO of 15 minutes. Running a full second copy at all times is too expensive. Which recovery design best fits?

A. Nightly backups to another region, restored onto new infrastructure only after a disaster
B. An active-active deployment in two regions with traffic split evenly between them
C. Continuous data replication to a second region with minimal compute that scales up on failover
D. Backups kept in the same availability zone, because restoring nearby is the fastest option

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Continuous replication meets the 15 minute RPO, and a small standby that scales up on failover can meet a 4 hour RTO at a fraction of the cost of full duplication. A is wrong because nightly backups can lose up to a day of data. B is wrong because active-active meets the objectives but is the expensive full copy the scenario rules out. D is wrong because backups in the same zone fail with the zone they are meant to protect.
</details>

---

### Question 24 - Domain 4: Cloud Application Security
**Scenario:** A company is exposing a public API that partner applications call on behalf of their users. Which approach best protects it?

A. Give each partner one shared API key with full access, rotated every year
B. Put it behind an API gateway with OAuth 2.0 scoped tokens, input validation, and rate limits
C. Allow only partner IP addresses, because network filtering makes authentication unnecessary
D. Rely on TLS alone, because an encrypted connection proves who the caller is and what it may do

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A gateway gives one place to check scoped, short-lived tokens, validate input, and limit abuse, and OAuth scopes keep each partner to what each user approved. A is wrong because a long-lived key with full access is easy to leak and cannot tell users apart. C is wrong because IP filtering is a useful extra layer, but addresses change and do not identify the user. D is wrong because server-side TLS protects the connection but does not authenticate or authorize the caller.
</details>

---

### Question 25 - Domain 4: Cloud Application Security
**Scenario:** A code review finds that a cloud web application fetches any URL a user submits, and the workload can reach the instance metadata service that hands out temporary credentials. What should the team do?

A. Validate URLs against an allowlist, require the token-based metadata service, and limit egress
B. Hide the feature from the menu, because users cannot submit a URL they cannot find
C. Turn on encryption at rest for the instance disk, because the credentials are stored on it
D. Add a web application firewall rule for the word "metadata" and leave the feature unchanged

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** This is a server-side request forgery risk, and layered fixes close it: allow only expected destinations, require the session-token version of the metadata service, and restrict outbound traffic. B is wrong because hiding a feature does not remove the endpoint. C is wrong because the risk is the application fetching live credentials, not someone reading the disk. D is wrong because a keyword filter is easy to get around and leaves the root cause in place.
</details>

---

### Question 26 - Domain 5: Cloud Security Operations
**Scenario:** Monitoring shows a cloud virtual machine making outbound connections to a known malicious host. The incident handler needs to contain it while keeping evidence. What is the best first step?

A. Terminate the instance at once, because removing it is the fastest way to stop the traffic
B. Reboot the instance to clear the malware from memory, then watch whether the traffic returns
C. Leave it running untouched for a week to learn more about the attacker's goals
D. Isolate it with a restrictive network rule, then snapshot its disks and capture memory if possible

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Network isolation stops the harm while the instance still exists, so disk snapshots and volatile memory can be captured for analysis. A is wrong because termination can destroy ephemeral storage and memory, which may be the only evidence. B is wrong because a reboot wipes memory evidence and does not contain anything. C is wrong because letting a known compromise run unchecked risks more damage and data loss.
</details>

---

### Question 27 - Domain 5: Cloud Security Operations
**Scenario:** Infrastructure is defined as code, but engineers sometimes make urgent changes directly in the console. Over time the live environment no longer matches the approved templates. What is the best fix?

A. Block all console access permanently, including in emergencies, so drift can never happen
B. Rewrite the templates every quarter to match whatever is running in production
C. Detect drift continuously, and route every change, including emergency ones, back through code
D. Accept drift as normal, because the console is faster than the pipeline for urgent fixes

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Change management in the cloud means the approved definition is the source of truth, drift is detected and alerted on, and emergency changes are recorded and folded back into code. A is wrong because a total ban with no break-glass path blocks real incident response. B is wrong because copying production into templates approves unreviewed changes after the fact. D is wrong because unmanaged drift hides misconfigurations and breaks the audit trail.
</details>

---

### Question 28 - Domain 5: Cloud Security Operations
**Scenario:** A team runs an auto-scaling fleet of stateless web servers. A critical OS vulnerability is announced. Which patching approach fits this design best?

A. Log in to each running server and apply the patch by hand during the next maintenance window
B. Build a patched golden image, test it, then roll it out by replacing the running instances
C. Patch only the servers that are running now, since new ones will be started from them later
D. Wait for the provider to patch the guest operating systems as part of the shared responsibility

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** With immutable, auto-scaling infrastructure, the fix belongs in the image, so every new instance starts patched and old ones are replaced in a controlled rollout. A is wrong because manual patching does not scale, and new instances would still launch from the old image. C is wrong because new instances launch from the image, not from running servers. D is wrong because in IaaS the guest OS is the customer's to patch.
</details>

---

### Question 29 - Domain 6: Legal, Risk and Compliance
**Scenario:** A company in the EU plans to store customer personal data with a provider that will process it in a country without an EU adequacy decision. What should the company put in place?

A. A recognized transfer mechanism such as standard contractual clauses, backed by a transfer risk assessment
B. Nothing extra, because the provider's ISO 27001 certificate makes any transfer lawful
C. Customer consent hidden in the general terms of service, covering all future transfers
D. A promise from the provider that the data will be encrypted while it is in transit

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** GDPR allows transfers to countries without adequacy only with a valid safeguard such as standard contractual clauses, and the exporter must assess whether local law undermines them and add measures if needed. B is wrong because a security certification is not a legal transfer mechanism. C is wrong because consent must be specific and informed, and buried blanket consent is not valid. D is wrong because transit encryption protects the transfer but does not make it lawful.
</details>

---

### Question 30 - Domain 6: Legal, Risk and Compliance
**Scenario:** A SaaS provider processes personal data for a customer under GDPR. The provider discovers a breach affecting that data. How should the contract and the parties handle notification?

A. The provider notifies the regulator and the affected people directly, and the customer is told later
B. No one needs to notify anyone if the provider believes the data was probably not misused
C. The provider, as processor, tells the customer without undue delay; the customer, as controller, decides on notifying the regulator
D. The customer has no duty, because a breach on the provider's systems moves all liability to the provider

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Under GDPR the processor must inform the controller without undue delay, and the controller must notify the supervisory authority within 72 hours where the breach poses a risk, and tell individuals where the risk is high. The contract should set the processor's notice duties and timing. A is wrong because the regulator and individual notices are the controller's duty. B is wrong because the processor cannot decide on its own that a breach does not need reporting. D is wrong because the controller stays accountable even when the processor caused the breach.
</details>

---

## Where to go deeper

- [CCSP cert page](../../exams/isc2/ccsp/) - notes, practice plan, strategy
- [CISSP practice questions](./isc2-cissp.md) - the broader prerequisite-level exam
- [CCSK practice questions](./cloud-security-alliance-ccsk.md) - the CSA counterpart
- [Shared responsibility model](../../learn/concepts/shared-responsibility-model.md) - plain-English foundation
- **[📖 ISC2 CCSP](https://www.isc2.org/certifications/ccsp)** - official exam outline
