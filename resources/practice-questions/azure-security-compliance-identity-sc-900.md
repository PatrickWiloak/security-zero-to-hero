---
last-updated: 2026-10-22
difficulty: beginner
---

# Microsoft Security, Compliance, and Identity Fundamentals (SC-900) - Practice Questions

19 questions for SC-900 prep, weighted toward Microsoft security solutions (35-40%), Microsoft Entra (25-30%), and compliance solutions (20-25%), per the skills outline as of October 21, 2026. Questions 16 to 19 cover topics that outline added or renamed.

SC-900 tests whether you can name the right capability for a requirement, not whether you can configure it.

> **Cert page:** [exams/azure/sc-900/](../../exams/azure/sc-900/)

---

### Question 1
**Scenario:** Which principle states that no request is trusted based on network location alone?

A. Least privilege
B. Zero trust, verify explicitly
C. Defense in depth, using layered controls
D. Separation of duties across teams and roles

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Zero trust's guiding principles are verify explicitly, use least privilege access, and assume breach. The consequence is that being inside the corporate network grants nothing by itself. Defense in depth and least privilege are complementary ideas, not the same one.
</details>

---

### Question 2
**Scenario:** A user proves identity with a password plus a code from an authenticator app.

A. Single sign-on, where one authentication lets the user reach several applications without signing in to each again
B. Conditional Access, the policy engine that evaluates sign-in signals and decides whether to grant, block, or challenge
C. Multi-factor authentication
D. Federation

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** MFA combines factors from different categories: something you know, something you have, and something you are. SSO means authenticating once for multiple applications. Federation is trust between identity systems. Conditional Access is the policy engine that can require MFA under given conditions.
</details>

---

### Question 3
**Scenario:** Access to a finance app should require MFA only when the sign-in comes from outside the corporate network.

A. A Conditional Access policy targeting the finance app, with a location condition for sign-ins outside the corporate network and an MFA grant control
B. Privileged Identity Management, which can require MFA at role activation but does not evaluate the network location of a sign-in
C. A sensitivity label on the finance documents, which classifies and protects content but does not control how users sign in
D. Turning on per-user MFA for every account, which prompts every user at each sign-in whatever the network location

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Conditional Access evaluates signals (user, device, location, application, risk) and applies controls, which is what makes the requirement conditional. Per-user MFA is unconditional. PIM handles just-in-time elevation of privileged roles, and labels classify data.
</details>

---

### Question 4
**Scenario:** An administrator should hold the Global Administrator role only for approved windows, with justification and approval.

A. Entitlement management, which bundles resources into access packages that users request, but does not time-limit a single admin role
B. Conditional Access, which applies controls at sign-in but does not make a role assignment eligible or time-limited
C. Microsoft Entra PIM with just-in-time activation
D. Access reviews, which let owners periodically confirm whether existing access is still needed but do not grant timed elevation

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** PIM makes a role assignment eligible rather than active, so it must be activated with justification, optional approval, and a time limit. Access reviews periodically confirm whether existing access is still needed, which is a different and complementary control.
</details>

---

### Question 5
**Scenario:** Which service is Microsoft's cloud identity provider?

A. Active Directory Domain Services
B. Microsoft Entra ID service
C. Microsoft Defender for Identity
D. Microsoft Purview

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Entra ID (formerly Azure AD) is the cloud identity and access management service. AD DS is the on-premises directory using Kerberos and LDAP. Defender for Identity monitors AD DS for attacks, and Purview handles data governance and compliance.
</details>

---

### Question 6
**Scenario:** Which capability lets an external partner sign in to your resources using their own organization's credentials?

A. Managed identities, which let Azure resources authenticate to other Azure services without credentials in code
B. Entra External ID (B2B collaboration)
C. Passwordless sign-in with FIDO2 keys or the authenticator app, which removes passwords for your own users but does not federate partners
D. Service principals, which represent applications in a tenant and let them authenticate to resources with a secret or certificate

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** B2B collaboration invites guests who authenticate at their home tenant, so you never manage their credentials or their offboarding. Managed identities are for Azure resources authenticating to services, and service principals represent applications.
</details>

---

### Question 7
**Scenario:** A workload in Azure must call Azure Storage without any stored credential.

A. A managed identity granted an RBAC role on the storage account, with the app requesting short-lived tokens from Microsoft Entra ID at run time
B. A user account with a password, created for the application and kept in a key vault that the app reads at start-up
C. The storage account key, kept in the application's configuration and rotated by the team on a regular schedule
D. A shared access signature stored in the app configuration, with an expiry set to limit the time a leaked token stays usable

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Managed identities are created and rotated by the platform, so there is no secret in code or configuration to leak. Both the account key and a long-lived SAS are secrets you must store, rotate, and hope nobody commits to git.
</details>

---

### Question 8
**Scenario:** Which service provides cloud security posture management and workload protection across Azure, AWS, and GCP?

A. Microsoft Sentinel, the SIEM and SOAR that correlates logs and runs response playbooks
B. Microsoft Purview, which governs data and compliance across Microsoft 365 and Azure but does not assess workload security posture
C. Azure Monitor, which collects metrics and logs for performance and availability monitoring
D. Defender for Cloud, which combines posture management with workload protection across Azure, AWS and GCP

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Defender for Cloud combines CSPM (secure score, recommendations, regulatory compliance) with CWPP (Defender plans for servers, containers, storage, databases) and is multicloud. Sentinel is the SIEM and SOAR. Purview is data governance. Azure Monitor is telemetry.
</details>

---

### Question 9
**Scenario:** A security team needs to collect logs from many sources, correlate them, and run automated response playbooks.

A. Microsoft Sentinel, a cloud-native SIEM
B. Entra ID Protection
C. Defender for Cloud
D. Compliance Manager, which tracks regulatory improvement actions

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Sentinel is the cloud-native SIEM and SOAR: data connectors, analytics rules, incidents, hunting, and Logic Apps playbooks for automation. Defender for Cloud protects workloads and feeds Sentinel rather than replacing it.
</details>

---

### Question 10
**Scenario:** Which Microsoft 365 capability classifies a document as Confidential and encrypts it so protection travels with the file?

A. Data loss prevention policies that block sharing
B. eDiscovery
C. Sensitivity labels with encryption
D. Retention policies

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A sensitivity label can apply encryption and rights so the protection persists even when the file leaves the tenant. DLP prevents actions at a boundary such as sending or copying. Retention governs how long content is kept, and eDiscovery finds and preserves content for legal matters.
</details>

---

### Question 11
**Scenario:** An organization must stop credit card numbers from being emailed externally.

A. Insider Risk Management, which spots patterns of risky user behavior over time but does not block an email as it is sent
B. A retention label, which keeps or deletes content for a set period but does not inspect messages for card numbers
C. A DLP policy with the credit card sensitive information type that detects card numbers in outgoing mail and blocks external sharing
D. A sensitivity label applied to every message, which classifies the content and can encrypt it but does not block a send itself

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** DLP detects sensitive information types in content and enforces an action at the moment of sharing, with policy tips and optional user override. Labels classify but do not by themselves block a send. Insider risk detects patterns of risky user behavior over time.
</details>

---

### Question 12
**Scenario:** Which tool gives a score and improvement actions mapped to regulations such as GDPR and ISO 27001?

A. Compliance Manager
B. Secure Score
C. Azure Advisor recommendations
D. Service Trust Portal documents

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Compliance Manager tracks improvement actions against regulatory templates and produces a compliance score. Secure Score measures security posture rather than regulatory alignment. The Service Trust Portal publishes Microsoft's own audit reports and certifications.
</details>

---

### Question 13
**Scenario:** Under the shared responsibility model in SaaS, who is responsible for the data and for identity management?

A. Microsoft entirely, because in a SaaS service the provider runs everything, including data
B. The customer, always, for data and for identities and accounts, in every service model including SaaS
C. Responsibility passes to the identity provider that signs users in, so the customer has no duties once single sign-on is turned on
D. It varies by month, depending on which updates Microsoft has applied to the service

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Data, devices, accounts, and identities remain the customer's responsibility in every service model. What shifts between IaaS, PaaS, and SaaS is the infrastructure and application layers. This is the single most repeated concept across all Microsoft fundamentals exams.
</details>

---

### Question 14
**Scenario:** Sign-ins from an anonymous IP address should be flagged as risky and challenged automatically.

A. A retention policy, which controls how long content is kept or when it is deleted but does not evaluate sign-in risk
B. A firewall rule that blocks known anonymous proxy ranges at the network edge, which cannot challenge users as they sign in
C. Purview auditing, which records sign-in and activity events for later investigation but does not act on them
D. Entra ID Protection risk policies, combined with Conditional Access

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** ID Protection calculates sign-in risk and user risk from signals such as impossible travel, anonymous IPs, and leaked credentials, and Conditional Access consumes that risk level as a condition to require MFA or a password change. Auditing records events but takes no action.
</details>

---

### Question 15
**Scenario:** Which describes the difference between authentication and authorization?

A. They are the same thing, since proving who you are always includes checking what you are allowed to do
B. Authentication proves who you are; authorization decides what you may do
C. Authentication applies only to administrator accounts, while ordinary users are authorized by their group membership alone
D. Authorization happens first, because a system must know what a user may do before it can check who the user is

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** AuthN establishes identity, AuthZ evaluates permissions for that identity, and it happens after. Keeping the two distinct is what makes it obvious that MFA (an authentication strength control) does nothing about over-permissioned accounts, which is an authorization problem.
</details>

---

### Question 16
**Scenario:** A function app needs to read secrets from Azure Key Vault. The security team wants no credential stored in the app's configuration or code.

A. Create a dedicated user account for the app and store its password in an app setting
B. Register an application and give the function app a client secret that is rotated every 90 days
C. Share the Key Vault access keys with the developers so they can embed them in the build
D. Enable a managed identity on the function app and grant it access to the vault

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A managed identity is a workload identity whose credential Azure creates and rotates, so nothing is stored for anyone to leak. A registered application with a secret works but still leaves a secret in configuration. A user account for automation is the pattern workload identities exist to replace, and Key Vault has no shared access keys to embed.
</details>

---

### Question 17
**Scenario:** After a news report on a ransomware campaign, a manager asks which of the company's devices are exposed and which recommended mitigations are already in place.

A. Microsoft Threat Intelligence, through the campaign's threat analytics report in the Defender portal
B. Microsoft Purview Compliance Manager, through its improvement actions for ransomware
C. Microsoft Entra ID Protection, through its risky sign-ins report for the affected users
D. Azure DDoS Protection, through its attack analytics for the public endpoints

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Threat analytics reports combine Microsoft's intelligence on a campaign with your own exposure and mitigation status. Compliance Manager tracks regulatory controls, ID Protection scores sign-in risk, and DDoS Protection covers volumetric network attacks, none of which describe an adversary campaign.
</details>

---

### Question 18
**Scenario:** An external auditor asks for Microsoft's latest ISO 27001 audit report for Microsoft 365.

A. Compliance Manager in the Microsoft Purview portal
B. The Service Trust Portal
C. Microsoft Defender for Cloud regulatory compliance dashboard
D. The Microsoft Entra admin center audit logs

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The Service Trust Portal publishes Microsoft's own audit reports and compliance documents. Compliance Manager measures your organization's progress against a regulation, and Defender for Cloud measures your Azure resources against standards; neither holds Microsoft's audit reports. Entra audit logs record directory changes.
</details>

---

### Question 19
**Scenario:** After a DLP rollout, the compliance team wants to see whether users are removing or downgrading sensitivity labels on files.

A. Content explorer, because it lists every item that carries a sensitivity label
B. eDiscovery, because it can place the affected files on legal hold
C. Activity explorer, because it records actions taken on labeled content over time
D. Compliance score, because it drops when labels are removed from files

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Activity explorer answers "what happened to the data": labels applied, changed, or removed, and DLP matches. Content explorer answers "where is the sensitive data" at a point in time. eDiscovery serves legal investigations, and compliance score measures control implementation, not user actions on files.
</details>

---

## Where to go deeper

- [SC-900 cert page](../../exams/azure/sc-900/) - notes, practice plan, strategy
- [SC-300 practice questions](./azure-identity-access-sc-300.md) - identity at administrator depth
- [SC-200 practice questions](./azure-security-operations-sc-200.md) - the SOC analyst path
- [Shared responsibility model](../../learn/concepts/shared-responsibility-model.md) - the concept behind question 13
- [SC-900 outline additions](../../exams/azure/sc-900/notes/outline-additions-2026-10.md) - the notes behind questions 16 to 19
- **[📖 SC-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-900)** - official skills outline
