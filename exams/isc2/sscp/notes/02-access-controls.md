---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 14 min
---

# 02 - Access controls

**Domain 2: Access Controls (15%)** - objectives 2.1 to 2.4.

Access control answers three questions in order: who are you (authentication), what may you do (authorisation) and what did you do (accounting). This domain covers how each is implemented and run.

---

## 2.1 Authentication methods

Authentication proves an identity using one or more **factors**: something you know (password, PIN), something you have (hardware token, phone, smart card) and something you are (fingerprint, face). **Multi-factor authentication** requires factors from at least two different categories; two passwords are still one factor.

NIST's digital identity guidance, SP 800-63B-4 (July 2025), covers authentication and authenticator management at three assurance levels, and is the reference for what a strong authenticator is. In practice the strongest everyday choices are phishing-resistant: hardware security keys and passkeys bind the login to the real site, so a fake login page cannot relay the credential. SMS codes and push approvals are better than passwords alone but can be phished or fatigued.

**Single sign-on** lets one authentication cover many applications. It reduces password sprawl and gives a single place to enforce MFA, but it concentrates risk: the identity provider becomes the most important system you run. **Federation** extends that across organisations using standards such as SAML and OpenID Connect, where an identity provider asserts who the user is and a relying party trusts the assertion. **Device authentication** (certificates, device compliance checks) proves the machine as well as the person.

Biometrics add two error rates to know: the **false acceptance rate** (an impostor gets in) and the **false rejection rate** (a legitimate user is refused). The point where they are equal is the **crossover error rate**, used to compare systems.

## 2.2 Internetwork trust architectures

A trust architecture decides which networks and parties are trusted to what degree.

- **Internet** is untrusted. **Intranet** is the organisation's own trusted network. **Extranet** is a controlled shared segment for partners. A **DMZ** (screened subnet) holds public-facing servers between two firewalls so a compromise there does not land directly on the internal network.
- **Trust relationships** between domains can be one-way or two-way and transitive or not. Transitive trust is convenient and dangerous, because A trusting B and B trusting C means A silently trusts C.
- **Third-party connections** (vendor VPNs, API integrations, managed service providers) are an extension of your attack surface. Give them the narrowest access, time limit it, log it and require the same MFA you require internally.

The modern direction is **zero trust**: no network location is trusted by default, and each request is evaluated on identity, device and context. For this exam, the safe reading is that location alone never grants trust.

## 2.3 Identity management life cycle

Every account has a life: proofing, provisioning, monitoring and entitlement management, review and deprovisioning.

- **Identity proofing** establishes that a person is who they claim before an account is created. The rigor should match the sensitivity of what the account can reach.
- **Provisioning** creates the account and grants entitlements. The best practice is role-based and automated from an authoritative source such as HR, so joiners get correct access and leavers lose it the same day.
- **Entitlement management** tracks what each identity can do. **Privilege creep** happens when people move roles and keep old access; **periodic access reviews** (recertification) by the data or system owner remove it.
- **Deprovisioning** disables accounts promptly on departure and handles the dormant and orphaned accounts that outlive their owners. Disable first, delete after a retention period, and rotate any shared secret the person knew.
- **Privileged accounts** need extra care: separate admin accounts, just-in-time elevation, session recording and vaulting of shared secrets. **Service accounts** have no human to notice a leak, so give them narrow rights, strong secrets and owners.

**Identity and access management systems** automate this, including directories, identity governance tools and privileged access management.

## 2.4 Access control models

| Model | Who decides | Typical use |
|---|---|---|
| **Discretionary (DAC)** | The resource owner | File shares where owners grant access |
| **Mandatory (MAC)** | The system, from labels and clearances | Military and high-assurance systems |
| **Role-based (RBAC)** | Permissions attach to roles, users get roles | Most enterprise applications |
| **Rule-based** | Global rules apply to everyone | Firewall rules, time-of-day restrictions |
| **Attribute-based (ABAC)** | A policy evaluates attributes at request time | Context-aware access in cloud and zero trust |

DAC is flexible and weak, because owners make mistakes. MAC is rigid and strong. RBAC scales well but suffers from **role explosion** if roles are too fine. ABAC is the most expressive and the hardest to audit. A common exam trap: a rule-based control is not the same as role-based; "rule" refers to rules applied to all subjects, "role" to a job function.

Also know the **reference monitor** idea: every access request passes through a component that checks it, and that component cannot be bypassed. And **access control lists** (a list on the object of who may do what) versus **capabilities** (a token held by the subject).

---

## Key terms

- **Multi-factor authentication** - requiring factors from at least two categories: something you know, have or are
- **Federation** - trust between organisations so an identity provider's assertion is accepted by a relying party
- **Single sign-on** - one authentication event granting access to many applications
- **DMZ** - a screened subnet holding public-facing servers between external and internal firewalls
- **Transitive trust** - trust that extends automatically from A to C when A trusts B and B trusts C
- **Identity proofing** - verifying a person is who they claim before an account is created
- **Privilege creep** - accumulation of unnecessary access as a person changes roles
- **Access recertification** - periodic review by an owner confirming access is still required
- **DAC** - discretionary access control, where the resource owner decides access
- **MAC** - mandatory access control, where the system enforces access from labels and clearances
- **RBAC** - role-based access control, where permissions attach to roles
- **ABAC** - attribute-based access control, where a policy evaluates attributes at request time
- **Crossover error rate** - the point where a biometric system's false acceptance and false rejection rates are equal

---

## Related

- [Notes 01: security concepts and practices](./01-security-concepts-and-practices.md)
- [Notes 06: network and communications security](./06-network-and-communications-security.md) for 802.1X, RADIUS and TACACS+
- [IAM explained](../../../../learn/concepts/iam-explained.md)
- **[📖 NIST SP 800-63B-4: Authentication and Authenticator Management](https://csrc.nist.gov/pubs/sp/800/63/b/4/final)** - authenticator requirements at three assurance levels (July 2025)
