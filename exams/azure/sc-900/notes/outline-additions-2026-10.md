---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 20 min
---

# SC-900 Outline Additions: What the Other Notes Miss

The other three SC-900 notes were written against an older skills outline. Microsoft's study guide (skills measured as of October 21, 2026) names several topics they cover thinly or not at all, and the October update renamed two of them. This page fills those gaps. Read it after the three domain notes, not instead of them.

What changed on October 21, 2026, according to the study guide's change log:

- **Identity types:** "Describe types of identities, including agent ID" became "Describe types of identities, including workload identities".
- **Threat protection:** "Describe Microsoft Defender Threat Intelligence (Defender TI)" became "Describe Microsoft Threat Intelligence".

Microsoft classed both as minor. The weights did not change with this update, but they differ from what older SC-900 courses teach: security solutions is now 35-40% and compliance 20-25%.

**[📖 SC-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-900)** - the official skills outline and change log

---

## Workload identities

### What a workload identity is

Most identity talk is about people: a user signs in, proves who they are, and gets access. But a large share of the sign-ins in any tenant are not people at all. A nightly job copies files into a storage account. A web app reads a secret from Key Vault. A deployment pipeline creates resources. Each of those is software acting on its own behalf, and each needs an identity so that Microsoft Entra ID can authenticate it and Azure can decide what it may touch.

Microsoft calls these **workload identities**: identities assigned to software (applications, services, scripts, containers) rather than to a person. In Microsoft Entra there are three kinds:

- **Applications and service principals.** When you register an application in Entra ID, you create an *application object*, the global definition of the app. Each tenant that uses the app gets a *service principal*, the local instance that permissions are actually granted to. A service principal authenticates with a client secret or, better, a certificate.
- **Managed identities.** A special kind of service principal that Azure creates and manages for you. You never see or rotate a credential, because Azure handles it behind the scenes. A **system-assigned** managed identity is tied to one resource (a VM, a function app) and is deleted with it. A **user-assigned** managed identity is a standalone Azure resource that you can attach to several resources and that outlives any one of them.
- **Agent identities.** As AI agents started acting in tenants, Microsoft introduced identities for them as well (Microsoft Entra Agent ID). The July 2026 outline named these explicitly; the October wording folds them back under the broader "workload identities" heading. For SC-900, know that an AI agent acting on its own is another non-human identity that needs the same controls.

### Why it matters

A workload identity is a credential that never takes a holiday, never notices a phishing page, and often has broad permissions because someone granted "Contributor" to get a deployment working. That makes it attractive to attackers. A leaked client secret in a public repository is a direct path into a subscription.

The design lesson the exam wants is simple: **prefer managed identities wherever Azure supports them**, because there is no secret for anyone to leak. Use a service principal with a certificate when the workload runs outside Azure or across tenants. Use a client secret only when nothing else works, and rotate it.

### Worked scenario

A team runs a web app on Azure App Service that reads a database connection string from Key Vault. Today the app authenticates to Key Vault with a client secret stored in the app's configuration. The security lead wants to remove that stored secret.

The fit is a system-assigned managed identity on the App Service, granted read access to that one Key Vault. The app asks Azure for a token, Azure vouches for it, and no secret exists anywhere in the configuration. If the app is deleted, its identity goes with it, so there is no orphaned credential left behind.

### How the exam tests this

SC-900 asks you to *describe*, not configure. Expect questions such as "which identity type lets an Azure resource authenticate without storing credentials?" (managed identity) or "what is created in each tenant when an application is used there?" (service principal). Watch for the trap of picking "user account" for a background job; a shared user account for automation is exactly what workload identities exist to replace.

- **[📖 What are workload identities?](https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-overview)** - application, service principal, and managed identity explained
- **[📖 Managed identities for Azure resources](https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/overview)** - system-assigned versus user-assigned

---

## Microsoft Threat Intelligence

### What it is

Threat intelligence is knowledge about adversaries: who they are, what infrastructure they use, which techniques they favor, and which indicators (IP addresses, domains, file hashes) mark their activity. Microsoft sees an enormous volume of signals across Windows, Microsoft 365, Azure, and Entra, and it employs analysts who track named threat actors. **Microsoft Threat Intelligence** is the name for that capability and the way it reaches customers.

The older outline named a specific product, Microsoft Defender Threat Intelligence (Defender TI), which began as a standalone portal for researching indicators and infrastructure. Microsoft has since brought threat intelligence into the Microsoft Defender portal, where analysts meet it as **threat analytics** reports (what a campaign does, which of your devices are exposed, which mitigations you have in place), **intel profiles** on threat actors and tools, and indicator research. The renamed bullet reflects that shift: the exam now asks what Microsoft's threat intelligence does for you, not about one portal's feature list.

### Why it matters

Raw alerts tell you *what* happened on your devices. Threat intelligence tells you *why it matters*: that a suspicious domain belongs to a ransomware affiliate, or that the vulnerability you have not patched yet is being used by an active campaign. That context lets a small team prioritize. It also works in the other direction: Microsoft uses the same intelligence to tune detections across Defender XDR and Sentinel, so customers benefit even if they never open an intel report.

### Worked scenario

A news story reports a new phishing campaign aimed at your industry. Your manager asks, "Are we exposed?" In the Defender portal, the threat analytics report for that campaign lists the techniques it uses, shows which of your devices or mailboxes saw related activity, and checks which recommended mitigations are already in place. You answer the question in minutes instead of reading vendor blogs and searching logs by hand.

### How the exam tests this

Expect "which capability provides context on threat actors and campaigns?" style questions. The distractors are usually other Defender products: Defender for Endpoint protects devices, Defender Vulnerability Management finds weaknesses, but intelligence about the adversary is Microsoft Threat Intelligence. If a question still uses the Defender TI name, treat it as the same capability.

- **[📖 Threat analytics in Microsoft Defender XDR](https://learn.microsoft.com/en-us/defender-xdr/threat-analytics)** - campaign reports, exposure, and mitigations
- **[📖 What is Microsoft Defender Threat Intelligence?](https://learn.microsoft.com/en-us/defender/threat-intelligence/what-is-microsoft-defender-threat-intelligence-defender-ti)** - the indicator and infrastructure research capability

---

## Microsoft Defender Vulnerability Management and the Defender portal

**Defender Vulnerability Management** finds weaknesses before an attacker does. It inventories the software and configuration on devices onboarded to Defender for Endpoint, matches them against known vulnerabilities, and ranks what to fix using exposure and active-exploitation data rather than severity alone. It then hands remediation requests to IT and tracks them. The difference from a classic scheduled scanner is continuity: the sensor already on the device reports changes as they happen, so there is no weekly blind spot.

The **Microsoft Defender portal** is where the XDR products meet. Incidents from Defender for Endpoint, Office 365, Identity, and Cloud Apps are correlated into single incidents there, so an analyst investigates one phishing-to-compromise story instead of four alerts in four consoles. Microsoft Sentinel can also be used in the same portal, which is why the outline treats the portal as a capability in its own right.

**How the exam tests this:** match the requirement to the product. "Prioritize software weaknesses on endpoints" is Vulnerability Management. "See one incident that spans email, identity, and endpoint" is Defender XDR in the Defender portal.

- **[📖 Microsoft Defender Vulnerability Management](https://learn.microsoft.com/en-us/defender-vulnerability-management/defender-vulnerability-management)** - risk-based vulnerability management

---

## Cloud security posture management and Azure Bastion

### CSPM in Defender for Cloud

**Cloud security posture management (CSPM)** is the practice of continuously checking cloud configuration against a standard and telling you what is wrong. Defender for Cloud does this with three linked ideas the outline names directly:

- **Security policies** define what "good" looks like, expressed as Azure Policy definitions.
- **Standards** group policies into a benchmark. The default is the Microsoft Cloud Security Benchmark; regulatory standards such as PCI DSS or ISO 27001 can be added.
- **Recommendations** are the result: each resource that fails a policy produces a recommendation with remediation steps. Fixing recommendations raises the **secure score**, a single number leadership can track.

Foundational CSPM is free; deeper capabilities, such as attack path analysis, come with the paid Defender CSPM plan. Separately, **cloud workload protection** plans (Defender for Servers, Storage, Databases, Containers, and others) add threat detection for running workloads. Posture is about configuration; workload protection is about attacks in progress. The exam likes that distinction.

### Azure Bastion

Exposing a virtual machine's RDP or SSH port to the internet invites brute-force attempts within minutes. **Azure Bastion** is a managed service deployed into your virtual network that lets administrators connect to VMs over TLS from the Azure portal (or a native client), so the VMs need no public IP address at all. The trade-off is cost and a dedicated subnet, against removing an entire class of exposure.

**How the exam tests this:** "Administrators need RDP access to VMs without public IP addresses" is Bastion. "Show which resources are misconfigured against a benchmark" is CSPM in Defender for Cloud. "Detect an attack on a running SQL server" is a workload protection plan.

- **[📖 Secure score in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/secure-score-security-controls)** - how recommendations roll up into a score
- **[📖 What is Azure Bastion?](https://learn.microsoft.com/en-us/azure/bastion/bastion-overview)** - RDP and SSH without public IPs

---

## Governance, risk, and compliance (GRC) concepts

The outline added GRC to the concepts domain. The three words mean different things, and questions test whether you can tell them apart.

- **Governance** is the system of rules, roles, and decision rights by which an organization directs its activities. Policies and accountability live here.
- **Risk** management is identifying what could go wrong, how likely and harmful it would be, and deciding what to do about it: reduce it, transfer it, avoid it, or accept it.
- **Compliance** is meeting obligations imposed from outside (laws, regulations, contracts, industry standards) and being able to prove it.

A few related terms appear in SC-900 questions. **Data residency** is where data is physically stored. **Data sovereignty** is the idea that data is subject to the laws of the country where it is located. **Data privacy** is about how personal data is collected, used, and shared, and the rights people have over it.

**Worked example:** a company decides that only the finance team may approve payments over a threshold (governance), assesses the chance that a compromised account approves a fraudulent payment (risk), and keeps records that satisfy its auditors under a financial regulation (compliance). One process, three lenses.

---

## Service Trust Portal and Microsoft's privacy principles

When a customer moves data to Microsoft's cloud, their auditors will ask how Microsoft protects it. The **Service Trust Portal** answers that: it publishes Microsoft's independent audit reports (SOC, ISO, FedRAMP and others), compliance guides, and white papers about how Microsoft cloud services handle data. Some documents require signing in with a work account. The portal is about **Microsoft's** compliance; your own compliance posture is measured in Compliance Manager.

Microsoft also states a set of **privacy principles** that govern how it handles customer data: **control** (you decide what happens to your data), **transparency** (Microsoft explains how it collects and uses data), **security** (data is protected with strong security and encryption), **strong legal protections** (respecting local privacy laws and defending customer data in court), **no content-based targeting** (customer email, chat, and files are not used for advertising), and **benefits to you** (data Microsoft does collect is used to improve your experience).

**How the exam tests this:** "Where can an auditor download Microsoft's ISO 27001 report?" is the Service Trust Portal. "Where do you track your own progress against a regulation?" is Compliance Manager. Mixing those two up is the most common mistake.

- **[📖 Get started with the Service Trust Portal](https://learn.microsoft.com/en-us/purview/get-started-with-service-trust-portal)** - audit reports and compliance documents
- **[📖 Microsoft Trust Center: privacy](https://www.microsoft.com/en-us/trust-center/privacy)** - Microsoft's privacy commitments

---

## Content explorer and Activity explorer

Both live in Microsoft Purview's data classification area, and the outline names them together because they answer two halves of one question.

- **Content explorer** shows *what sensitive data you have and where it is*: which items carry a sensitivity label or contain a sensitive information type (a credit card number, a passport number) across SharePoint, OneDrive, and Exchange. Because it can display the actual content, access to it is tightly role-restricted.
- **Activity explorer** shows *what people are doing with labeled and sensitive data*: labels applied, changed, or removed, files copied to USB, DLP rule matches, over time.

**Worked scenario:** before rolling out a DLP policy, a compliance team uses Content explorer to learn that thousands of spreadsheets contain card numbers in one SharePoint site. After rollout, they use Activity explorer to see whether users are downgrading labels to get around the policy.

**How the exam tests this:** "where is it" is Content explorer; "what happened to it" is Activity explorer.

- **[📖 Learn about Content explorer](https://learn.microsoft.com/en-us/purview/data-classification-content-explorer)** - finding labeled and sensitive items
- **[📖 Learn about Activity explorer](https://learn.microsoft.com/en-us/purview/data-classification-activity-explorer)** - tracking actions on labeled content
