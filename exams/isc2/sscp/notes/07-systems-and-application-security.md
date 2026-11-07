---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 14 min
---

# 07 - Systems and application security

**Domain 7: Systems and Application Security (15%)** - objectives 7.1 to 7.5.

The endpoint and the workload: what attacks it, how to harden it, and how mobile, cloud and virtual environments change the rules.

---

## 7.1 Malicious code and activity

Classify malware by how it spreads and what it does.

| Type | Defining behaviour |
|---|---|
| Virus | Attaches to a file and needs a user to run it |
| Worm | Spreads on its own across networks |
| Trojan | Looks legitimate and hides a payload |
| Ransomware | Encrypts data and demands payment, often after stealing it first |
| Rootkit | Hides itself and other malware deep in the system |
| Spyware, keylogger | Collects activity and credentials |
| Botnet agent | Takes remote orders from a command-and-control server |
| Logic bomb | Fires on a condition such as a date or a missing employee record |
| Fileless malware | Runs in memory using legitimate tools such as scripting engines |

Attack types worth recognising: **zero-day** exploitation of unknown flaws, **privilege escalation**, **buffer overflow**, **injection** (SQL, command), **cross-site scripting**, **cross-site request forgery**, **credential stuffing** (reusing leaked passwords) and **password spraying** (one common password against many accounts). **Social engineering** targets people: phishing, spear phishing, whaling (executives), vishing (voice), smishing (text), pretexting, baiting and tailgating. AI-generated lures and deepfakes make convincing messages cheap, so verify requests for money or credentials through a separate channel.

Defences combine layers: patching, least privilege, application allow-listing, email filtering, user awareness and backups. **Behavior analytics** compares activity with normal patterns to catch what signatures miss, such as an account suddenly downloading gigabytes at night.

## 7.2 Endpoint device security

Harden the endpoint as if the network will fail.

- **Host-based IDS/IPS** and **host firewalls** add local detection and filtering. **Endpoint detection and response (EDR)** records endpoint behaviour, detects suspicious chains of activity and lets responders isolate a host remotely; it replaced signature-only antivirus as the core tool.
- **Full-disk encryption** protects data when a device is lost. A **Trusted Platform Module (TPM)** stores keys in hardware and supports secure and measured boot, so the machine can prove it booted unmodified.
- **Hardening** removes unneeded software and services, applies a **secure baseline** (CIS Benchmarks and vendor guides are common), disables autorun and local admin rights, and patches promptly.
- **Application control** allows only approved software, which stops most commodity malware.
- **Removable media** controls and **DLP** limit leakage; **logging** from the endpoint feeds the SIEM from [notes 03](./03-risk-identification-monitoring-and-analysis.md).

## 7.3 Mobile devices

NIST SP 800-124 Rev. 2 (May 2023) describes mobile devices as permanent fixtures in enterprises and covers risks, mitigations and the full device life cycle for both organisation-provided and personally owned devices. Know the ownership models: **COPE** (corporate-owned, personally enabled), **BYOD** (bring your own device) and **COBO** (corporate-owned, business only). BYOD maximises convenience and minimises control, so it needs clear policy, consent to management and a way to wipe business data without wiping personal data.

**Mobile device management (MDM)** and its broader cousins enforce policy: passcode and encryption requirements, remote lock and wipe, app allow-lists, OS version minimums and compliance checks that block non-compliant devices from corporate resources. **Containerisation** separates corporate apps and data from personal ones on the same device. **Application management** vets apps and controls distribution. Threats include loss and theft, malicious apps, unpatched operating systems, insecure Wi-Fi and jailbroken or rooted devices, which should be refused.

## 7.4 Cloud security

Cloud changes who runs what, not who is accountable. **Service models**: IaaS gives virtual infrastructure, PaaS adds a managed platform, SaaS delivers the whole application. **Deployment models**: public, private, community and hybrid. The **shared responsibility model** divides duties: the provider secures the facilities and underlying platform; the customer secures their data, identities, configuration and, depending on the model, the operating system and application. The further toward SaaS, the more the provider does, but you always keep responsibility for your data and who can access it.

Practitioner concerns: misconfiguration is the leading cause of cloud exposure (public storage, over-broad roles), so use policy guardrails and configuration monitoring; protect identities with MFA and least privilege; encrypt data and manage keys; turn on audit logging; and understand **legal concerns** such as where data resides and which jurisdiction can compel access. **Third-party requirements** include contracts, service level agreements, right to audit, assurance reports (such as SOC 2 and ISO/IEC 27001 certificates), breach notification terms and exit plans. For depth see the cloud material at [cloud.noblerworks.com](https://cloud.noblerworks.com/).

## 7.5 Secure virtual environments

A **hypervisor** runs virtual machines: **type 1** runs on bare metal and is standard for servers, **type 2** runs on top of an operating system and suits desktops. NIST SP 800-125 examines the security risks of full virtualization and recommends mitigations. The principal threats are **VM escape** (breaking out of a guest to the host), **VM sprawl** (forgotten machines that are never patched), snapshots that retain sensitive memory, and management-plane compromise, which hands over every guest. Defend by patching the hypervisor, isolating the management network, restricting administrators, and segmenting guests.

**Containers** share the host kernel, so isolation is weaker than a VM's: use minimal images, scan them, run as non-root, drop capabilities, and never mount the container runtime socket into a container. Treat images as software supply chain components. **Resilience** comes from clustering, live migration, redundant storage and tested backups; **storage** security covers encrypted volumes, access zoning and secure deletion of virtual disks.

---

## Key terms

- **Worm** - malware that spreads across networks on its own without user action
- **Ransomware** - malware that encrypts data and demands payment, often after stealing it
- **Rootkit** - malware that hides itself and other malicious code deep in a system
- **Credential stuffing** - reusing username and password pairs leaked from other breaches to log in
- **Password spraying** - trying one common password against many accounts to avoid lockouts
- **Endpoint detection and response** - tooling that records endpoint behaviour, detects suspicious activity and lets responders isolate hosts
- **Trusted Platform Module** - a hardware component that stores keys and supports measured and secure boot
- **COPE** - corporate-owned, personally enabled: a company device that staff may also use personally
- **Mobile device management** - tooling that enforces policy on mobile devices, including lock, wipe and compliance checks
- **Shared responsibility model** - the division of security duties between a cloud provider and its customer
- **Type 1 hypervisor** - a hypervisor that runs directly on hardware
- **VM escape** - an attack that breaks out of a guest virtual machine to reach the host
- **VM sprawl** - uncontrolled growth of forgotten virtual machines that are never patched

---

## Related

- [Notes 06: network and communications security](./06-network-and-communications-security.md)
- [Security topic](../../../../topics/security.md)
- **[📖 NIST SP 800-124 Rev. 2: Managing the Security of Mobile Devices in the Enterprise](https://csrc.nist.gov/pubs/sp/800/124/r2/final)** - mobile risks, mitigations and device life cycle (May 2023)
- **[📖 NIST SP 800-125: Guide to Security for Full Virtualization Technologies](https://csrc.nist.gov/pubs/sp/800/125/final)** - virtualization risks and recommendations (January 2011)
