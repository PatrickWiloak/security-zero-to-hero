---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 25 min
---

# 05 - Global Secure Access, emergency access, and other outline gaps

Notes 01 to 04 follow the four SC-300 domains. This page covers what the October 28, 2026 skills outline changed, plus outline bullets the other notes only mention in passing: Global Secure Access in depth, emergency access accounts, Microsoft Entra Kerberos, cross-tenant synchronization, custom security attributes, protected actions, and Identity Secure Score.

**[📖 SC-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-300)** - skills measured as of October 28, 2026, with the change log

## What changed on October 28, 2026

The change log marks three skill groups as minor changes. Comparing the April 27 and October 28 outlines line by line:

| Skill group | Before | From October 28, 2026 |
|-------------|--------|------------------------|
| User authentication | Authentication methods "including certificate-based authentication, Temporary Access Pass, OAuth 2.0 tokens, Microsoft Authenticator, and passkeys (FIDO2)" | The same list without "OAuth 2.0 tokens" |
| Global Secure Access | "Deploy and manage Private Access", "Internet Access", "Internet Access for Microsoft 365" | "Deploy and manage Microsoft Entra Private Access", "Microsoft Entra Internet Access", "the Microsoft traffic profile for Microsoft 365" |
| Privileged access | "Create and manage break-glass accounts" | "Create and manage emergency access accounts" |

None of these add a new technology. The OAuth removal is a correction: an OAuth 2.0 token is the *result* of authentication, not a method a user authenticates with, and the methods policy never listed it. The other two are naming that now matches Microsoft's product documentation. If a practice question uses the old names, treat them as the same thing.

Two oddities in the published outline are worth knowing so they do not confuse you. The "Skills at a glance" list shows *Implement authentication and access management* at 25-30%, while that domain's own heading shows 20-25%; the at-a-glance figure is the one that has been stable across versions, so this guide uses 25-30%. And the fourth domain is now titled *Plan and automate identity governance*, which signals the weight Microsoft puts on lifecycle workflows and automation.

---

## Global Secure Access

### The problem it solves

The classic remote-access model is a VPN: a user connects, lands on the corporate network, and can then reach whatever that network routes to. That model has two weaknesses. Access is network-wide rather than per application, so a compromised laptop on the VPN can scan and move laterally. And the decision to let someone in happens once, at connection time, with little knowledge of who the user is or what state their device is in.

**Global Secure Access** is Microsoft's Security Service Edge (SSE): a cloud service that sits between users and the resources they reach, and applies identity-aware policy to each connection. Because it is built into Microsoft Entra, the same Conditional Access engine that guards sign-ins can now guard network traffic.

### The pieces

- **Global Secure Access client.** Installed on Windows, macOS, iOS, and Android devices, it captures the traffic selected by the forwarding profiles and tunnels it to Microsoft's edge. Deploying the client (usually through Intune) is an outline bullet in its own right; without it, nothing is forwarded.
- **Traffic forwarding profiles.** These decide which traffic goes through the service. There are three: the **Microsoft traffic profile** (Microsoft 365 services such as Exchange Online and SharePoint Online), the **Private Access profile** (your private applications), and the **Internet Access profile** (general internet and SaaS traffic).
- **Microsoft Entra Private Access.** Zero Trust network access (ZTNA) to private applications, on-premises or in another cloud. A lightweight **connector** inside the private network makes an outbound connection to the service, so no inbound firewall ports open. You publish applications by FQDN or IP range and port, and you assign users to each application, so a user reaches exactly the apps they are assigned and nothing else on the network. Conditional Access can then require MFA or a compliant device per application. Quick Access is the simplest starting point: a broad VPN-replacement definition that you narrow into per-app definitions over time.
- **Microsoft Entra Internet Access.** A secure web gateway: web content filtering by category or FQDN, applied through security profiles that are linked to Conditional Access policies. Because the policy knows the user, a finance user and a contractor can get different web rules on the same network.
- **The Microsoft traffic profile.** Forwarding Microsoft 365 traffic through Global Secure Access gives two security wins that Microsoft emphasizes: **universal tenant restrictions**, which stop users from signing into *other* tenants with corporate devices (a data exfiltration path), and **compliant network checks** in Conditional Access, which can require that access to Microsoft 365 came through your Global Secure Access tunnel. Because the tunnel carries the user's original source IP, sign-in logs and location-based policies stay accurate.

### Worked scenario

A company runs an internal HR application on a server in its datacenter. Today, staff reach it over a VPN that gives every connected device access to the whole server subnet. After a ransomware scare, leadership wants HR staff to reach only the HR app, only from compliant devices, with MFA.

The design: install a Private Access connector in the datacenter, create an enterprise application for the HR app's FQDN and port, assign the HR group to it, and create a Conditional Access policy targeting that application that requires MFA and a compliant device. Deploy the Global Secure Access client with the Private Access profile enabled to HR staff. Every other server on the subnet is now unreachable from those laptops, and the access decision is re-evaluated per application rather than once at VPN connect.

### Trade-offs

Global Secure Access ties network access to Entra licensing and the client. Devices without the client (unmanaged personal devices, some servers) need another path. Some older protocols and applications need testing before you move them off a VPN. And Internet Access overlaps with an existing third-party secure web gateway if you have one, so many organizations start with Private Access and the Microsoft traffic profile.

### How the exam tests this

- "Users must reach only specific on-premises apps without a VPN, with Conditional Access per app" is **Private Access**.
- "Block a category of websites for contractors only" is **Internet Access** with a security profile linked to a Conditional Access policy.
- "Prevent users from signing into a personal or another company's tenant from corporate devices" is **universal tenant restrictions** through the **Microsoft traffic profile**.
- Questions often hinge on a missing prerequisite: the client is not deployed, the forwarding profile is not enabled, or no connector is installed.

- **[📖 What is Global Secure Access?](https://learn.microsoft.com/en-us/entra/global-secure-access/overview-what-is-global-secure-access)** - the SSE overview and components
- **[📖 Traffic forwarding profiles](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-traffic-forwarding)** - Microsoft, Private Access, and Internet Access profiles
- **[📖 Microsoft Entra Private Access](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-private-access)** - connectors, Quick Access, and per-app access

---

## Emergency access accounts

### Why you need them

Every strong control can lock you out. A Conditional Access policy that requires a compliant device, applied to all users by mistake. An MFA outage. A federation provider that is down. The only global administrators are the people who just lost access. **Emergency access accounts** (the outline's new name for break-glass accounts) are the insurance: a small number of highly privileged accounts that can still sign in when normal administration fails.

### How to build them well

Microsoft's guidance, which the exam follows:

- Create **at least two** cloud-only accounts on the tenant's `*.onmicrosoft.com` domain, not synchronized from on-premises and not federated, so an on-premises or federation outage cannot block them.
- Assign them the **Global Administrator** role *permanently* (not eligible through PIM), because an emergency is not the moment for an activation workflow that may itself depend on something broken.
- Protect them with a **phishing-resistant, passwordless method**: a passkey (FIDO2) security key is Microsoft's recommendation, certificate-based authentication if you already run a PKI. These satisfy Azure's mandatory MFA requirement, and they should differ from the method your everyday admin accounts use, so one method failing cannot take out both.
- **Exclude them from every Conditional Access policy that blocks or restricts sign-in**, ideally through a dedicated group such as *EmergencyAccess*. The strong credential protects the account; an enforced policy that requires a compliant device could make it unusable in exactly the emergency it exists for. Report-only policies do not need the exclusion.
- **Monitor every sign-in.** Send Entra sign-in logs to a Log Analytics workspace and create an Azure Monitor alert (Microsoft's example is a `SigninLogs` query on the accounts' object IDs, threshold greater than zero, severity critical). They should almost never be used, so every use gets a post-mortem.
- Keep the credentials in separate, secure locations, not tied to any individual's phone or device, and use the accounts only from a privileged access workstation.
- **Validate them at least every 90 days** and after staff changes: confirm they can sign in, that alerts fire, and that the list of authorized people is current.

### Worked scenario

An administrator enables a Conditional Access policy requiring a compliant device for all users and all apps, intending to scope it to a pilot group. Within minutes, no administrator can sign in from their unmanaged admin workstations. Because the emergency access accounts were excluded from that policy, an administrator retrieves one account's FIDO2 key from the safe, signs in, fixes the scope, and the alert on that sign-in opens a ticket that records why the account was used.

### How the exam tests this

Expect questions that ask what to configure *alongside* a new Conditional Access policy (exclude the emergency accounts), how to detect misuse (alert on sign-ins via Log Analytics), and which assignment type to use in PIM (permanent active, not eligible). A distractor that makes the emergency account a synchronized on-premises account is wrong, because it fails in exactly the outage it exists for.

- **[📖 Manage emergency access accounts in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/security-emergency-access)** - Microsoft's guidance

---

## Microsoft Entra Kerberos for hybrid identities

Many hybrid organizations keep on-premises resources that speak Kerberos, the ticket-based protocol Active Directory uses. **Microsoft Entra Kerberos** lets Entra ID issue Kerberos tickets, which closes gaps that appear when users sign in with cloud credentials:

- A user signs into Windows with **Windows Hello for Business** or a **FIDO2 security key** (both passwordless) and still needs single sign-on to on-premises file shares. Entra ID issues a partial ticket-granting ticket that the on-premises domain controller exchanges, so the passwordless sign-in still reaches Kerberos resources.
- **Azure Files** shares can be accessed by hybrid identities with Kerberos tickets issued by Entra ID, without line-of-sight to a domain controller.

The setup step the exam names is creating a Kerberos server object in the on-premises domain so Entra ID and AD can trust each other's tickets. The test is usually framed as "passwordless users cannot reach on-premises resources; what enables SSO?"

- **[📖 Passwordless security key sign-in to on-premises resources](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-passwordless-security-key-on-premises)** - Microsoft Entra Kerberos setup

---

## Cross-tenant synchronization and custom security attributes

**Cross-tenant synchronization** automates creating, updating, and removing B2B collaboration users across tenants in the same organization, typically after a merger or for a multi-tenant enterprise. The *source* tenant pushes users; the *target* tenant must allow inbound synchronization in its **cross-tenant access settings**, and usually enables automatic redemption so users skip the consent prompt. Compare it with B2B invitations, which are one user at a time and manual, and with B2B direct connect, which is for Teams shared channels without creating guest objects.

**Custom security attributes** are business-specific key-value attributes (for example `Project=Falcon` or `Clearance=Restricted`) that you define and assign to users, service principals, and other objects. They differ from directory extension attributes in one crucial way: only holders of the dedicated attribute roles (Attribute Definition Administrator, Attribute Assignment Administrator, and the reader roles) can see or set them, and even Global Administrators do not get access by default. That makes them safe for sensitive values and for attribute-based access control in Azure role assignment conditions and Conditional Access app filters.

**How the exam tests these:** "Users in a newly acquired company's tenant should appear automatically in ours and be removed when they leave" is cross-tenant synchronization. "Store a sensitive attribute that most admins must not read" is custom security attributes.

- **[📖 What is cross-tenant synchronization?](https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview)** - source and target configuration
- **[📖 What are custom security attributes?](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview)** - definition, roles, and uses

---

## Protected actions and Identity Secure Score

**Protected actions** let you require extra Conditional Access conditions for specific high-impact *administrative operations*, independent of the role that performs them. You assign an **authentication context** to a permission such as updating Conditional Access policies or deleting cross-tenant access settings, then write a Conditional Access policy for that authentication context (for example, requiring phishing-resistant MFA from a compliant device). An administrator can browse freely but is stepped up at the moment they try to change a policy. The value is defense against a stolen admin session: the token may be valid, but it cannot change the most sensitive settings without fresh, strong proof.

**Identity Secure Score** is a percentage that measures how closely your tenant follows Microsoft's identity recommendations, such as requiring MFA for administrative roles, blocking legacy authentication, and enabling self-service password reset. Each recommendation shows its score impact and how to fix it. It is a posture metric, not an incident tool: use it to prioritize hardening and to report progress over time.

**How the exam tests these:** "Require phishing-resistant MFA only when an admin modifies Conditional Access policies" is a protected action with authentication context. "Show leadership a measure of identity configuration hygiene" is Identity Secure Score.

- **[📖 What are protected actions in Microsoft Entra ID?](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/protected-actions-overview)** - authentication context on admin permissions
- **[📖 What is the identity secure score?](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-identity-secure-score)** - how the score is calculated

---

## Related

- [Notes 02: authentication and Conditional Access](./02-authentication-and-conditional-access.md) - the policy engine this page builds on
- [Notes 04: identity governance](./04-identity-governance.md) - PIM, where emergency accounts are exempt from activation
- [Zero trust explained](../../../../learn/concepts/zero-trust-explained.md) - why per-app access replaces network access
