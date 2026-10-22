# Microsoft Cybersecurity Architect (SC-100) - Practice Questions

19 design questions for SC-100 prep, aligned to the skills outline as of October 21, 2026 (questions 16 to 19 cover its AI and agent objectives). SC-100 is a **design** exam: more than one option usually works, and the constraint in the question decides which is correct. Read the qualifier before the options.

> **Cert page:** [exams/azure/sc-100/](../../exams/azure/sc-100/)

---

### Question 1
**Scenario:** A company must ensure backups survive an attack in which an administrator account is fully compromised. Cost is a secondary concern. What should the design include?

A. More frequent backup schedules, with hourly recovery points in the same vault
B. Immutable vault with soft delete and multi-user authorization using a Resource Guard
C. Geo-redundant storage on the Recovery Services vault, with cross-region restore enabled for the protected workloads
D. A second vendor's backup product, writing to a separate subscription

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The threat is an authorized identity performing destructive operations. Immutability prevents deletion or retention reduction within the retention period, and multi-user authorization requires a second approver held in a separate subscription. Geo-redundancy protects against regional failure, not against authorized deletion. More frequent backups create more recovery points that the same compromised identity could delete. A second product duplicates cost without addressing identity compromise.
</details>

---

### Question 2
**Scenario:** An organization must prevent engineers from holding standing subscription Owner rights while allowing them to perform occasional administrative work. The tenant has Microsoft Entra ID P2. Least administrative effort is required.

A. Conditional Access requiring MFA and a compliant device for every administrator sign-in to the Azure portal
B. An entitlement management access package that grants the Owner role for a set period after a manager approves
C. Privileged Identity Management with eligible assignments, approval, and time limits
D. A scheduled script in an Automation runbook that adds and removes the Owner role assignments when engineers ask

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** PIM is the feature for just-in-time privileged role activation with approval, justification, and time bounds. Conditional Access governs the conditions of a sign-in, not standing role assignment. Entitlement management covers resource entitlement, not directory or Azure role activation. A script is custom effort to build and maintain, which fails the least-effort constraint.
</details>

---

### Question 3
**Scenario:** A retailer has 12 subscriptions across three regions and two Entra tenants after an acquisition. A single central SOC operates it. EU log data must remain in EU regions, and the logging bill is unsustainable. What Sentinel design fits?

A. Migrate the acquired tenant into the main tenant first, then use a single workspace for all twelve subscriptions
B. One workspace per subscription, each in the region of its resources, with analytics rules copied to all twelve
C. One workspace per data residency boundary, cross-workspace queries, and Azure Lighthouse
D. One global US workspace, with table-level RBAC for the EU data

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Workspace count is driven by data residency and tenancy, not subscription count. Two workspaces satisfy the EU boundary, cross-workspace queries keep a single SOC investigation surface, and Lighthouse provides cross-tenant access without a tenant migration project. A global workspace violates residency. Twelve workspaces are costly and fragment investigation. Tenant migration is a large project when Lighthouse achieves the operational goal now.
</details>

---

### Question 4
**Scenario:** An insurer requires that application VMs reach Azure Storage without traffic traversing the public internet, that the storage account is unreachable from any other network, and that on-premises systems over ExpressRoute reach it privately.

A. Service endpoints on the VM subnet, with the storage firewall limited to that subnet so only its VMs connect
B. Storage firewall rules allowlisting the on-premises public IP range of the ExpressRoute Microsoft peering circuit
C. Private endpoint with public network access disabled, plus a linked private DNS zone and on-premises conditional forwarders
D. A service endpoint for the VM subnet and a private endpoint for the on-premises systems

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Only a private endpoint gives the resource a private IP and allows disabling public access entirely, and only it extends to on-premises over ExpressRoute. Service endpoints keep a public IP on the resource and do not work from on-premises. IP allowlisting still traverses the public internet. Configuring both is redundant and makes DNS resolution ambiguous. The private DNS component is part of the correct answer, not an optional extra.
</details>

---

### Question 5
**Scenario:** An organization runs Azure, AWS, GCP, and VMware on-premises. It wants one posture view, one ISO 27001 compliance report across all environments, and runtime threat detection on servers, with minimal agent sprawl.

A. Separate compliance reporting per cloud, with each platform's native tool and the results merged by hand for the audit
B. Defender for Cloud with AWS and GCP connectors, Azure Arc for VMware, and Defender for Servers Plan 2
C. Deploy Defender for Endpoint independently on every server, and onboard each one to the Defender portal by script
D. A third-party CSPM product with agentless scanning of the three clouds

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Defender for Cloud is the single posture plane; native connectors bring AWS and GCP in agentlessly; Arc projects the VMware servers into Azure Resource Manager; and Defender for Servers Plan 2 deploys Defender for Endpoint through Arc rather than as a separate agent stack, satisfying the agent-sprawl constraint. A third-party tool adds a product the native connectors make unnecessary. Separate reports fail the single-report requirement.
</details>

---

### Question 6
**Scenario:** A hospital group must keep on-premises Active Directory authoritative and has a compliance requirement that password hashes must not be stored in the cloud in any form. Which hybrid identity method fits, and what is the consequence?

A. Password hash sync, which stores a hash of the password hash in Entra ID; there is no consequence
B. Cloud-only identities, which remove the sync client; on-premises authority is lost
C. AD FS federation, which is the simplest option to operate because Microsoft hosts the whole farm and all of the proxies for you
D. Pass-through authentication with redundant connectors; cloud sign-in depends on on-premises connector availability

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** PTA validates credentials against on-premises AD without storing any hash in Entra ID, satisfying the constraint. The consequence is that sign-in depends on connector availability, so a datacenter outage breaks cloud authentication. Password hash sync is Microsoft's default recommendation but is excluded by the constraint. Cloud-only loses on-premises authority. AD FS meets the constraint but adds substantial infrastructure and is the option Microsoft guidance steers away from.
</details>

---

### Question 7
**Scenario:** A payments company must isolate its cardholder data environment, inspect all traffic between it and the rest of the estate including TLS-encrypted flows, prevent direct internet egress, and produce PCI DSS assessment evidence.

A. Azure Firewall Premium in the hub with TLS inspection and IDPS, forced tunneling, a dedicated CDE subscription, and the PCI DSS initiative
B. A single subscription with resource groups as the compliance boundary, using RBAC and tags to scope the audit evidence
C. Azure Firewall Standard in a hub, with NSGs in the spoke, and its threat intelligence filtering set to alert and deny
D. NSGs and application security groups only, with flow logs enabled and sent to a Log Analytics workspace for the auditors

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Premium is the tier that provides TLS inspection and IDPS, which Standard lacks. Forced tunneling removes direct internet routes. Aligning the compliance boundary with a subscription and management group gives clean policy, RBAC, and audit scoping. The regulatory compliance dashboard supplies assessment evidence. NSGs alone offer no layer 7 inspection.
</details>

---

### Question 8
**Scenario:** A company is deploying an internal AI assistant over SharePoint and OneDrive. Legal is concerned employees will surface documents they should not see. Reclassifying the entire document estate by hand is not acceptable.

A. Rely on the assistant's built-in filtering, which hides sensitive documents from users whatever the permissions say
B. Block the assistant from all sites containing sensitive data, using a restricted search setting for those sites
C. Manually classify the highest-risk document libraries first, then extend
D. Fix oversharing at the source, then apply Purview auto-labeling, DLP for AI applications, and DSPM for AI

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** An AI assistant honors existing permissions, so oversharing in SharePoint becomes exposure in the assistant. The correct sequence is fix permissions, then classify at scale with auto-labeling, then enforce with DLP, then monitor with DSPM for AI. Blocking sites defeats the deployment. Built-in filtering enforces permissions, it does not fix them. Manual classification fails the stated constraint.
</details>

---

### Question 9
**Scenario:** A design must ensure that a recommendation about misconfigured storage accounts appears in a compliance report, and that exploitation attempts against those accounts raise alerts. Which Defender for Cloud capabilities are needed?

A. CSPM for the recommendation and Defender for Storage for runtime alerting
B. CSPM only, since it also raises alerts when it sees an exploitation attempt against a misconfigured account
C. Azure Policy only, with an audit effect for the compliance report and an alert rule on the activity log
D. Defender for Storage only, which reports the misconfiguration and also raises the exploitation alerts

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Posture and compliance recommendations come from CSPM, which is largely free. Runtime threat detection, including malware scanning and anomalous access alerts, requires the paid Defender for Storage workload plan. The two halves answer different requirements, and questions frequently include both in one scenario.
</details>

---

### Question 10
**Scenario:** Which Zero Trust principle does requiring a compliant device through Conditional Access primarily implement?

A. Assume breach, which means designing as if an attacker is already inside
B. Segment everything, which means splitting the network into small zones
C. Verify explicitly, which means authorizing on every available signal, such as device state
D. Use least privilege access, giving each identity only the access it needs

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Verify explicitly means authenticating and authorizing on all available signals, including device state. Least privilege concerns the scope of granted access, addressed by PIM and RBAC. Assume breach drives segmentation, encryption, and detection. "Segment everything" is not one of the three principles.
</details>

---

### Question 11
**Scenario:** A regulated customer requires that Microsoft cannot access the keys protecting their data, and that the key store is single-tenant and FIPS 140-2 Level 3 validated. What should the design specify?

A. Platform-managed keys, which Microsoft rotates and protects
B. Double encryption with platform-managed keys
C. Azure Key Vault Managed HSM, a single-tenant FIPS 140-2 Level 3 module
D. Customer-managed keys in the standard Key Vault tier, which gives key control but uses a multi-tenant service

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Managed HSM provides a single-tenant, FIPS 140-2 Level 3 validated HSM under customer control. Standard Key Vault is multi-tenant and validated at a lower level. Platform-managed keys give the customer no key control at all. Double encryption adds layers but does not satisfy the single-tenancy and validation requirements.
</details>

---

### Question 12
**Scenario:** A design must give a central SOC visibility into on-premises Windows servers, including vulnerability assessment and file integrity monitoring, with the least agent management.

A. Defender for Servers Plan 2 through Azure Arc
B. Forward Windows event logs to Sentinel only, using the Azure Monitor agent and the security events connector
C. Defender for Servers Plan 2 enabled on the Azure subscription only, with the on-premises servers left unconnected
D. Install Defender for Endpoint manually on each server and run vulnerability scans from the Defender portal

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Vulnerability assessment, file integrity monitoring, just-in-time VM access, and agentless scanning are Plan 2 capabilities. Plan 1 covers Defender for Endpoint integration but not those, and enabling a plan on a subscription (C) does nothing for on-premises servers that are not connected through Arc. Arc is the mechanism that brings non-Azure servers into scope and carries the agent, minimizing separate agent management. Log forwarding alone gives no endpoint protection.
</details>

---

### Question 13
**Scenario:** Which control should a design use to ensure that no resource in a management group can be created with a public IP address?

A. A Conditional Access policy that blocks the creation of any resource by an identity that is not on a compliant device
B. An Azure Policy assignment with a deny effect at the management group scope
C. An NSG rule on each subnet that denies inbound traffic from the internet to any address in the range
D. A Defender for Cloud recommendation to remove public IP addresses, with an owner and a due date assigned

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** "Ensure" and "prevent" call for prevention rather than detection. Azure Policy deny stops the resource being created. A Defender for Cloud recommendation reports non-compliance after the fact. NSGs filter traffic, they do not prevent resource creation. Conditional Access governs sign-in conditions.
</details>

---

### Question 14
**Scenario:** An organization has Microsoft-only workloads, standard detection needs, no third-party log sources, and a strict cost constraint. What should the security operations design recommend?

A. Microsoft Defender XDR alone, deferring Sentinel until a third-party source or long retention is needed
B. Microsoft Sentinel with every connector enabled, so that each Microsoft signal is ingested and kept in the workspace
C. A third-party SIEM, deployed on virtual machines in the tenant, with connectors for each of the Microsoft services
D. Sentinel with Basic logs for every table, to cut the ingestion charge

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Defender XDR provides correlated detection and response across the Microsoft estate with per-user or per-workload licensing rather than per-GB ingestion. Sentinel earns its cost when you need third-party sources, custom analytics, or long retention. Enabling all connectors is the classic cost mistake. Basic logs reduce cost but also reduce query capability and do not change the underlying question of whether a SIEM is needed.
</details>

---

### Question 15
**Scenario:** A design must let a single SOC team investigate incidents across two Entra tenants after an acquisition, without migrating identities. What should it use?

A. Merging the tenants immediately, with a cross-tenant migration
B. A second SOC team in its own workspace, handing off by ticket
C. B2B guest accounts for every analyst in the other tenant, with roles assigned to each guest on the workspaces
D. Azure Lighthouse delegated resource management across the two tenants

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Lighthouse provides cross-tenant delegated management so one team operates across both without identity migration or duplicated accounts. Guest accounts scale poorly and complicate privileged access. A second team duplicates cost. Tenant merger is a long project that does not answer the immediate operational need.
</details>

---

### Question 16
**Scenario:** A company runs a dozen autonomous agents that read SharePoint and Microsoft Graph with their own agent identities and no signed-in user. Only agents that passed security review may reach those resources, new agents must be blocked by default, and the design must scale as teams add agents.

A. Require multifactor authentication in a Conditional Access policy that targets all agent identities
B. Tag reviewed agents with a custom security attribute and use a Conditional Access policy on agent identities that blocks access unless the attribute marks the agent as approved
C. Create a Conditional Access policy for All users that requires a compliant device, which covers agents as well as people
D. Give each agent an API key for SharePoint and rotate the keys quarterly through Key Vault

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Application-only agent access is evaluated against the agent identity, and attribute-driven policies apply automatically to agents added later. MFA cannot be satisfied by an autonomous agent, the All users assignment does not cover agent identities, and API keys bypass Entra ID token issuance, so Conditional Access never sees them.
</details>

---

### Question 17
**Scenario:** An agent summarizes a user's mailbox while the user is signed in, using the on-behalf-of flow. Security wants that access blocked when the user signs in from an unmanaged device.

A. A Conditional Access policy that targets the agent identity and requires a compliant device
B. A Conditional Access policy that targets the agent identity blueprint and blocks unmanaged devices
C. A Conditional Access policy that targets the user and requires a compliant device for the resource
D. A Conditional Access policy that targets the agent's user account and requires a compliant device

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** In the on-behalf-of flow the user is the token subject, so Conditional Access evaluates the user's policies. Policies that target the agent identity or its blueprint apply only to application-only access, and a policy on an agent's user account applies only when the agent acts as that account.
</details>

---

### Question 18
**Scenario:** Before rolling out Microsoft 365 Copilot to 5,000 users, the CISO wants assurance that Copilot will not surface board papers and merger documents to staff who should not see them. The rollout must not wait for a new permissions model across the tenant.

A. Run an oversharing assessment, apply sensitivity labels with encryption to board and merger content, and restrict the affected sites before broad rollout
B. Add a system instruction to Copilot telling it never to reveal confidential documents
C. Delay Copilot until every SharePoint site has been migrated to a new site structure
D. Block Copilot for all users in Defender for Cloud Apps and allow only the security team

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Copilot respects the user's existing permissions and label-based encryption, so fixing oversharing on the most sensitive content is the targeted control. Instructions are not access control. A full site migration fails the timing constraint, and blocking Copilot defeats the rollout rather than securing it.
</details>

---

### Question 19
**Scenario:** The board's stated priority is to reduce the damage a ransomware breach could do. The security architect is asked to plan Zero Trust work using Microsoft's current adoption guidance.

A. Start with the technology pillar that has the lowest secure score and work through pillars in score order
B. Start from the business scenario for preventing or reducing business damage from a breach, then map its security disciplines to the technology pillars that implement them
C. Follow RaMP's initiative list in order, because the adoption framework only applies to new tenants
D. Deploy Microsoft Sentinel first, because detection must exist before any other Zero Trust work

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The Zero Trust adoption framework starts from business scenarios (why), then security disciplines (what), then technology pillars (where), so work stays tied to the outcome leadership asked for. Ordering by secure score or by one product ignores the stated business priority, and the outline replaced RaMP with the adoption framework.
</details>

---

## Scoring guide

- **16-19 correct (85%+):** Ready. Focus remaining time on case study technique and reading for the constraint.
- **12-15 correct (65-80%):** Re-read the domain notes for your weak areas, especially Domains 2 and 3, which are 25-30% of the exam each.
- **Below 12:** Work the [scenarios](../../exams/azure/sc-100/scenarios.md) and the Microsoft Cybersecurity Reference Architectures before retesting.

Remember that on SC-100 more than one option is usually technically valid. The qualifier in the question, such as "least administrative effort" or "without additional licensing", is what selects the answer.
