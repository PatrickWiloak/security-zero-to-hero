---
last-updated: 2026-10-22
difficulty: intermediate
---

# CCSK v5 - Certificate of Cloud Security Knowledge - Practice Questions

30 questions across the CCSK v5 domains, which follow the CSA Security Guidance v5: governance, risk and compliance, infrastructure and networking, identity and access management, cloud workload security, data security, application security, and incident response. The exam is open book against the Guidance, the Cloud Controls Matrix, and the ENISA report.

> **Cert page:** [exams/cloud-security-alliance/ccsk/](../../exams/cloud-security-alliance/ccsk/)

---

### Question 1
**Scenario:** How does the shared responsibility split change between IaaS and SaaS?

A. The provider's share grows from IaaS to PaaS to SaaS, but the customer always retains data, identity, and access responsibility
B. It is identical across service models, because the contract fixes one split regardless of what is consumed
C. The provider is responsible for everything in IaaS, including the guest operating system, the data, and user access
D. The customer is responsible for everything in SaaS, including the application code, the runtime platform, and the physical datacenter

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The constants are what CCSK emphasizes: data classification, identity, and entitlement stay with the customer at every service model. What moves is the operating system, runtime, and application layers.
</details>

---

### Question 2
**Scenario:** Which document establishes what a provider is actually contractually obliged to do?

A. The customer's internal policy, which binds the provider once it has been sent to the account manager
B. The provider's marketing material and website, which describe the features included in each service tier
C. The contract and its SLAs, since the contract is the primary governance tool in cloud
D. A certification badge on the provider's website, which proves the provider will meet every customer requirement

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** CSA's position is that in cloud you govern through the contract, because you cannot directly control the provider's operations. Certifications and audit reports are evidence supporting the contract rather than substitutes for it.
</details>

---

### Question 3
**Scenario:** What is the Cloud Controls Matrix?

A. A pricing model that predicts monthly cost from instance count and data volume
B. A cloud-specific control framework mapped to other standards, used with the CAIQ to assess providers
C. A network diagram that shows how workloads and gateways are connected inside the provider's data centers and regions
D. An encryption standard that defines approved key lengths and algorithms

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The mappings are the practical value: satisfying a CCM control lets you point at the corresponding ISO 27001 or NIST requirement. The Consensus Assessments Initiative Questionnaire is the CCM turned into questions a provider answers, published for many providers in the STAR registry.
</details>

---

### Question 4
**Scenario:** A cloud provider's data center is in another jurisdiction.

A. No law applies, because data stored in a cloud service sits outside the jurisdiction of any single country
B. Several jurisdictions can apply, such as where data resides and where each party operates, so residency is a contract term
C. Only the provider's country's law applies, since the provider operates the facility that holds the data
D. Only the customer's country's law applies, because the customer owns the data wherever the provider stores it

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Jurisdictional overlap is a first-order legal risk in cloud, and lawful access requests can come from any of them. Region selection, contractual residency commitments, and encryption with customer-held keys are the practical controls.
</details>

---

### Question 5
**Scenario:** Which is the most significant difference in cloud incident response?

A. Limited forensic access to infrastructure, dependence on provider logs, and escalation paths agreed in advance with the provider
B. The provider handles everything, including investigating and containing incidents
C. Nothing changes, because forensic acquisition works the same on a hypervisor the customer does not own
D. Incidents do not occur in major cloud providers, since their infrastructure is audited and certified continuously

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** You cannot image a hypervisor you do not own, so the provider's logging and support commitments become part of your response capability. Snapshot-based acquisition of your own instances is fast, which is a genuine cloud advantage in the other direction.
</details>

---

### Question 6
**Scenario:** Which access control model best fits dynamic cloud environments?

A. Individual local accounts on each system, created by the administrator of that system when a person asks for access
B. Shared credentials stored in a team password vault, rotated whenever someone leaves the group
C. Attribute-based access control with policy conditions, plus just-in-time elevation and federated identity
D. Static role assignments only, reviewed once a year, since a fixed role list is easier to audit than conditions

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Attributes such as tags, time, network path, and device posture express policy that a role list cannot. Federation keeps identity in one authoritative source, which is what avoids the account sprawl that makes deprovisioning unreliable.
</details>

---

### Question 7
**Scenario:** What is the primary security benefit of infrastructure as code?

A. It is faster, because a template runs quickly and a deployment needs less time than manual steps, which cuts the window for human error
B. It eliminates all risk, because templates are tested and a tested template cannot contain a misconfiguration or a vulnerable dependency
C. It removes the need for monitoring, because deployed resources never drift
D. Configuration that is consistent, reviewable, version-controlled, and scannable for violations before deployment

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Configuration becomes an artifact you can review, diff, and test, which is what makes prevention possible rather than detection after the fact. The corresponding risk is that a flawed template deploys the same flaw everywhere at once.
</details>

---

### Question 8
**Scenario:** Which encryption approach keeps the provider unable to read customer data?

A. Provider-managed keys, which keep the provider unable to read the data because it never sees the plaintext
B. Encryption at rest by default, which the provider applies and decrypts transparently whenever data is read
C. Customer-managed or customer-held keys, with client-side encryption being strongest
D. TLS only, which encrypts data in transit and so protects it from the provider as well as from eavesdroppers

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Provider-managed encryption protects against physical media loss but not against the provider itself. The trade-off with client-side encryption is loss of provider-side processing and search, plus the full weight of key management on the customer.
</details>

---

### Question 9
**Scenario:** Which describes the main risk of serverless functions from a security perspective?

A. The provider secures the code, so the customer's only task is to choose the memory size and timeout
B. They cannot be attacked, because each invocation runs in a short-lived isolated environment and then disappears entirely
C. There is no attack surface, because there is no server for an attacker to log in to or to patch
D. The attack surface shifts to code, dependencies, event sources, and over-permissive roles rather than hosts

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Removing the server removes patching but not application risk, and event-driven triggers widen the set of untrusted inputs. Function-level least privilege matters more than in a monolith, because each function's role is a separate blast radius.
</details>

---

### Question 10
**Scenario:** A container image must be trusted before deployment.

A. Scan images, sign them, verify signatures at admission, and build from minimal trusted base images
B. Use the latest tag, so each deployment automatically pulls the most recently patched version of the image
C. Scan at runtime only, because vulnerabilities found in running containers are the only ones that matter
D. Trust the registry, since any image stored in the organization's private registry has already been vetted

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Supply chain assurance runs from base image to admission control, and `latest` breaks it by making the deployed artifact unidentifiable. Runtime scanning alone finds the problem after it is already running.
</details>

---

### Question 11
**Scenario:** Which best describes cloud network security compared with traditional?

A. Only firewalls matter, because every cloud workload is protected by one perimeter firewall at the provider edge
B. No network controls exist, because the provider's network is shared
C. Software-defined and identity-aware: security groups and micro-segmentation replace the perimeter
D. Identical, since cloud networks use the same zones, appliances, and cabling-based segmentation as a data center

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Segmentation becomes cheap and granular because it is software, so per-workload policy replaces a small number of network zones. The trade is that a misconfigured rule propagates instantly across everything using that group.
</details>

---

### Question 12
**Scenario:** How should cloud misconfiguration be prevented at scale?

A. Training only, since misconfigurations come from people and a well-trained engineer will not make them, whatever the pace of change
B. Annual audits, performed by an external assessor who reviews a sample of the production configuration and issues a report
C. Manual review of every change by a second engineer before the change is approved to deploy, with sign-off recorded in a ticket
D. Preventive guardrails through policy as code and organization-level controls, plus posture management for drift

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Misconfiguration is the leading cause of cloud data exposure, and it appears faster than review cycles can catch it. Prevention at the control plane plus detection for what slips through is the two-layer answer.
</details>

---

### Question 13
**Scenario:** What is the significance of the cloud management plane?

A. It is the network layer, which carries customer traffic between workloads and the provider's routers and switches
B. It is the highest-value target, since controlling it means controlling every resource whatever the workload-level controls
C. It is unimportant, because it only handles billing and reporting and has no effect on workloads
D. It is the storage layer, which holds customer data and so is where encryption is applied by the provider

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** This is the structural difference from traditional data centers: an API credential can do what once required physical access. Strong authentication, minimal privileged accounts, and comprehensive logging of the management plane follow directly.
</details>

---

### Question 14
**Scenario:** A business unit must be prevented from creating resources in unapproved regions.

A. Preventive policy at the organization level, such as a service control policy, denying actions outside approved regions
B. A monthly report listing resources outside approved regions, reviewed by the cloud team and followed up by tickets to owners
C. Tagging every resource with its region, so finance can see where each business unit has deployed
D. A policy document stating which regions are approved, signed by every manager in the business unit and filed with compliance

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Preventive guardrails at the organization level cannot be overridden by an account administrator, which is what makes them a control rather than a guideline. Detective controls only tell you it already happened.
</details>

---

### Question 15
**Scenario:** How should a cloud exit or portability requirement be addressed?

A. Assume the provider will always be available, since major providers publish uptime figures that exceed typical on-premises results
B. Plan for it: know export formats and egress costs, limit proprietary coupling, and define exit terms contractually
C. Keep a copy on premises always, with a full second copy of every workload
D. Use multicloud for everything, running every workload on two providers at all times

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Lock-in is a business risk to manage deliberately rather than avoid absolutely, since managed services deliver real value in exchange for coupling. Egress cost and the practical time to move large data are the parts most often left out of an exit plan.
</details>

---

### Question 16 - Domain 1: Cloud Computing Concepts and Architectures
**Scenario:** A hosting vendor sells a "private cloud." Customers raise a ticket for each new server and wait three days while the vendor's staff build it. A buyer asks whether this meets the NIST definition of cloud.

A. Yes, because the servers are virtualized and share physical hosts with other customers
B. No, because on-demand self-service is missing when every request waits on vendor staff
C. Yes, because it is a private deployment model, which NIST exempts from the essential characteristics
D. No, because a private cloud can never be cloud computing unless it is operated by the customer

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** NIST SP 800-145 requires all five essential characteristics, and on-demand self-service means a consumer provisions capability without human interaction with the provider. A three-day ticket queue is managed hosting. A is wrong because virtualization alone is resource pooling, one characteristic out of five. C is wrong because the deployment model does not waive any characteristic. D is wrong because a private cloud can be operated by a third party and still be cloud.
</details>

---

### Question 17 - Domain 2: Cloud Governance
**Scenario:** A spend review finds 40 SaaS subscriptions paid on corporate cards that security never assessed. The CIO wants this under control without stopping the teams that rely on the tools.

A. Block every SaaS domain at the web proxy until each team has re-applied through a new approval form
B. Ask each team to sign a statement that their tool holds no sensitive data and close the review
C. Move all 40 subscriptions to one corporate card so finance can see the total monthly cost
D. Inventory existing use, then route cloud purchases through a risk-based intake by data sensitivity

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Cloud governance works by putting a light, risk-tiered gate on how services are adopted and by knowing what is already in use, so the riskiest tools get assessed first. A is wrong because a blanket block breaks working business processes and pushes use further out of sight. B is wrong because self-attestation is not an assessment and gives no evidence. C is wrong because it improves cost visibility but does nothing about security or data risk.
</details>

---

### Question 18 - Domain 3: Risk, Audit, and Compliance
**Scenario:** A retailer moves its card payment application to an IaaS provider that holds a PCI DSS attestation. The project manager says the retailer is now PCI compliant by inheritance.

A. The provider's attestation covers only its scope, so the retailer must confirm services used are in scope and meet its own duties
B. The retailer is compliant, because a PCI attestation transfers to every customer that runs on the attested platform
C. The retailer must audit the provider's data centers itself, because a provider attestation cannot be relied on at all
D. PCI DSS does not apply in IaaS, because the card data sits on infrastructure the retailer does not own

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Compliance inheritance is partial. The provider's report covers the controls it operates, for the services listed in its scope, and the customer still owns everything above that line. A is the right reading of shared responsibility. B is wrong because compliance does not transfer wholesale. C is wrong because the attestation is valid evidence for the provider's part, and on-site audits of hyperscalers are rarely possible. D is wrong because the standard follows the card data, not ownership of the hardware.
</details>

---

### Question 19 - Domain 4: Organization Management
**Scenario:** A company has set up a cloud organization with many member accounts. The top-level management account has full control over all of them. How should that account be handled?

A. Use it as the daily admin account for the cloud team, since it already holds every permission they need
B. Share its credentials among three senior engineers so it stays reachable during an outage
C. Run no workloads in it, enforce strong MFA, limit and log its use, and alert on any sign-in
D. Delete it after setup, because member accounts can manage themselves once their policies are set

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The top of the hierarchy can change or remove guardrails for every account below it, so it should be rarely used, tightly protected, and watched. A is wrong because daily use multiplies the exposure of the most powerful credential. B is wrong because shared credentials remove accountability and widen exposure. D is wrong because the management account cannot simply be deleted and is needed to run the organization.
</details>

---

### Question 20 - Domain 5: Identity and Access Management
**Scenario:** A CI/CD pipeline deploys to the cloud using a long-lived access key stored as a pipeline secret. The key has not been rotated in two years. What is the best fix?

A. Rotate the key every 90 days and store the new value in the same pipeline secret
B. Federate the pipeline's workload identity to the cloud and issue short-lived, scoped credentials per run
C. Encrypt the access key with a second key and keep that second key in the repository
D. Move the key into an environment variable on the build server so it is not visible in the pipeline UI

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Workload identity federation removes the standing secret entirely. Each run gets a token that expires quickly and can be scoped to that pipeline. A is wrong because rotation shrinks the exposure window but keeps a long-lived secret to steal. C is wrong because it just moves the secret to another key stored next to the code. D is wrong because the key is still long-lived and now sits on a shared host.
</details>

---

### Question 21 - Domain 6: Security Monitoring
**Scenario:** Management plane API logging is enabled in each account, and each account's admins can change or delete their own logs. An attacker with admin rights in one account could erase their tracks.

A. Send the logs from every account and region to a separate security account with write-once storage
B. Keep the logs in each account but review them once a month for signs of deletion
C. Turn off logging in low-risk accounts to cut cost and focus review on production accounts
D. Rely on the provider to keep a copy of the logs and request it after an incident

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Centralizing logs in an account the workload admins cannot control, with immutable storage, keeps the evidence intact even when one account is compromised. A is the standard design. B is wrong because a monthly review finds deletion after the evidence is gone. C is wrong because attackers often start in the less watched accounts. D is wrong because providers do not promise to keep or hand over a customer's deleted logs.
</details>

---

### Question 22 - Domain 7: Infrastructure and Networking
**Scenario:** Workloads in a private subnet call the provider's managed database and object storage services. Today that traffic leaves through a NAT gateway to the services' public endpoints.

A. Add a second NAT gateway so the traffic has a redundant path to the public endpoints
B. Move the workloads into a public subnet so they reach the services directly without the NAT
C. Encrypt the traffic with TLS, since TLS alone makes a public endpoint as safe as a private one
D. Use private endpoints for those services and apply endpoint policies that limit which resources can be reached

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Private endpoints keep the traffic on the provider's network, and endpoint policies can restrict access to the organization's own resources, which also blocks data being copied to an outside account. A is wrong because it adds resilience but not security. B is wrong because it exposes the workloads to the internet. C is wrong because TLS is needed but does not stop access to other tenants' resources through the public endpoint.
</details>

---

### Question 23 - Domain 7: Infrastructure and Networking
**Scenario:** Administrators reach cloud management hosts through a VPN that, once connected, places them on a network with open access to every subnet. Leadership wants a zero trust approach.

A. Keep the VPN and add a second VPN concentrator in another region for better availability
B. Replace the VPN with a jump host that has a public IP and password login for every admin
C. Grant access per user and per resource, checking identity and device posture each time
D. Allow admin access only from the office IP range and remove all other remote access

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Zero trust removes implicit trust from network location. Each connection is authorized to one resource based on who is asking and the state of their device, as in a software-defined perimeter. A is wrong because it keeps the flat access model. B is wrong because a public jump host with passwords is a weaker control. D is wrong because a source IP range is still location-based trust and anyone inside the office gets full reach.
</details>

---

### Question 24 - Domain 8: Cloud Workload Security
**Scenario:** A team runs 200 VMs in auto-scaling groups. Admins log in to patch them by hand, and the fleet has drifted so no two servers are configured the same.

A. Build patched images in a pipeline and replace instances with new ones rather than changing them in place
B. Give more admins login access so the manual patching finishes faster each month
C. Turn off auto-scaling so the number of servers stays fixed and is easier to patch by hand
D. Install a remote shell agent on every VM so admins can patch without opening SSH

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Immutable infrastructure fits cloud workloads: changes go into a tested image, and running instances are replaced, so every server matches a known build and login access can be removed. B is wrong because it widens privileged access and keeps the drift. C is wrong because it gives up elasticity to suit a manual process. D is wrong because it changes the access path but still patches in place, so drift continues.
</details>

---

### Question 25 - Domain 8: Cloud Workload Security
**Scenario:** A review of a Kubernetes cluster finds several pods running as privileged, as root, with the node's file system mounted. The team says the cluster is private, so it is fine.

A. Accept the risk, because a private cluster has no exposure an attacker could use
B. Enforce admission policies that block privileged pods, root users, and host mounts unless granted an exception
C. Move the pods to a separate namespace, since namespaces stop a container from reaching the node
D. Scan the container images again, because image scanning will catch privileged settings at runtime

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Privileged containers with host mounts make a container escape easy, and admission control is how the cluster refuses insecure pod settings before they run. A is wrong because a compromised app inside a private cluster is still a foothold. C is wrong because namespaces are a logical boundary and do not stop a privileged container reaching the host. D is wrong because image scanning checks the image contents, not the pod's runtime settings.
</details>

---

### Question 26 - Domain 9: Data Security
**Scenario:** A company is ending a contract with a SaaS provider. It needs confidence that its data on the provider's storage can no longer be read, but it cannot inspect the provider's disks.

A. Ask the provider to send the physical drives that held the data so they can be destroyed on site
B. Delete the records through the application, since application deletion wipes the underlying media
C. Rely on the provider's statement that data is removed within 90 days of contract end
D. Destroy the customer-managed keys that encrypted the data, making any remaining copies unreadable

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Crypto-shredding is the practical answer to deletion in multitenant storage. If the data was encrypted with keys the customer controls, destroying those keys renders every copy, including backups, unreadable. A is wrong because multitenant drives hold other customers' data and will not be handed over. B is wrong because logical deletion does not guarantee the media or backups are cleared. C is wrong because a statement gives no verifiable assurance, though it should still be in the contract.
</details>

---

### Question 27 - Domain 10: Application Security
**Scenario:** A developer committed a database password to a shared code repository. It was removed in the next commit an hour later. What should happen?

A. Nothing more, since the password was removed in the very next commit and the repository is internal
B. Rewrite the repository history to remove the commit and treat the matter as closed
C. Rotate the password, move secrets to a vault, and add secret scanning to the pipeline
D. Make the repository private to a smaller group so fewer people could have seen the password

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Once a secret is committed, assume it is exposed: history, clones, and forks keep copies. Rotation removes the risk, a secrets manager stops it recurring, and pipeline scanning catches the next one. A is wrong because the old commit still holds the password. B is wrong because existing clones keep the old history and the password still works. D is wrong because it narrows the audience but leaves the leaked password valid.
</details>

---

### Question 28 - Domain 10: Application Security
**Scenario:** A web app on a cloud VM fetches images from URLs that users supply. A tester shows the app can be made to request the instance metadata service and return the VM's role credentials.

A. Validate and restrict outbound URLs, require token-based metadata access, and keep the VM role least privileged
B. Remove the VM's role and store a long-lived access key in the app's configuration file instead
C. Add a web application firewall rule that blocks the word "metadata" in request parameters
D. Move the app to a larger instance type so the metadata service has more capacity

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** This is server-side request forgery against cloud metadata. Defense in depth fixes the input handling, hardens the metadata service so a simple forged request fails, and limits what stolen credentials could do. B is wrong because a static key in a file is easier to steal and never expires. C is wrong because a keyword filter is easy to bypass with an IP address or encoding. D is wrong because instance size has nothing to do with the flaw.
</details>

---

### Question 29 - Domain 11: Incident Response and Resilience
**Scenario:** Monitoring flags a cloud VM making outbound connections to a known command-and-control address. The on-call engineer wants to terminate the instance right away.

A. Terminate the instance at once, since a clean one will launch from the image and stop the activity
B. Isolate it with a restrictive security group, snapshot its disks and metadata, then investigate
C. Reboot the instance to clear the malware from memory and keep it running for users
D. Leave it running unchanged so the attacker does not notice and the team can watch longer

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Cloud makes containment and evidence capture fast: a network change isolates the VM, and snapshots preserve the disks for forensic work without the provider's help. A is wrong because termination destroys the volatile and often disk evidence needed to find the entry point. C is wrong because a reboot loses memory evidence and the compromise may persist. D is wrong because leaving an active compromise connected risks further damage without a deliberate, approved decision to monitor.
</details>

---

### Question 30 - Domain 12: Related Technologies and Strategies
**Scenario:** Staff are pasting customer records into a public generative AI chat service to draft replies. The business sees real value in the tool and does not want to ban it.

A. Allow any AI service staff prefer, since AI tools do not store or reuse the prompts they receive
B. Ban all AI tools on corporate devices and rely on staff not to use them on personal devices
C. Treat it as a SaaS adoption: approve an enterprise tenant with suitable data terms, set data rules, and add DLP
D. Tell staff to remove customer names from prompts and leave the rest of the records unchanged

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Generative AI services are cloud services, so the same governance applies: assess the provider, contract for how prompts are kept and used, decide which data classes may be sent, and enforce it. A is wrong because many consumer services keep prompts and may use them for training. B is wrong because a ban drives use to unmanaged devices with no visibility. D is wrong because removing names alone does not make the remaining records safe to share.
</details>

---

## Where to go deeper

- [CCSK cert page](../../exams/cloud-security-alliance/ccsk/) - notes, practice plan, strategy
- [CCSP practice questions](./isc2-ccsp.md) - the deeper cloud security professional exam
- [Shared responsibility model](../../learn/concepts/shared-responsibility-model.md) - plain-English foundation
- [Zero trust architecture](../architecture-patterns/zero-trust-architecture.md) - the design pattern behind identity-aware controls
- **[📖 CSA Security Guidance](https://cloudsecurityalliance.org/research/guidance/)** - the primary CCSK source document
