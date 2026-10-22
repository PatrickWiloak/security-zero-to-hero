---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 16 min
---

# 04 - Networking and cloud security concepts

**Domain 4: Networking and Cloud Security Concepts (21.3%)** - the second largest domain in the outline effective September 1, 2026, and usually the hardest for beginners.

The outline has three objectives: network security (4.1), network security architecture (4.2), and cloud security (4.3). Cloud used to be a few lines inside the network domain; it now has its own objective and appears in the domain's name.

---

## 4.1 Network security

### Models: OSI and TCP/IP

Network models split communication into layers so each problem can be handled on its own. You do not need to configure anything, but you do need to know what happens at each layer, because questions describe a device or attack and ask where it operates.

| Layer | Name | Handles | Examples |
|---:|---|---|---|
| 7 | Application | The application protocol itself | HTTP, SMTP, DNS, FTP |
| 6 | Presentation | Formatting, encoding, encryption | TLS, JPEG, ASCII |
| 5 | Session | Establishing and managing sessions | Session setup and teardown |
| 4 | Transport | End-to-end delivery, ports | TCP, UDP |
| 3 | Network | Logical addressing and routing | IP, ICMP, routers |
| 2 | Data link | Local delivery, MAC addressing | Ethernet, switches |
| 1 | Physical | Bits on the medium | Cables, radio, hubs |

The **TCP/IP model** condenses this into four layers: Application (OSI 5 to 7), Transport (4), Internet (3), and Network Access (1 and 2).

### Addressing and protocols

**IPv4** addresses are 32 bits, written as four numbers such as `192.168.1.10`. There are only about 4.3 billion of them, which is why the **private ranges** (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`) exist: they are reused inside organizations and reach the internet through **network address translation (NAT)**. **IPv6** addresses are 128 bits, written in hexadecimal such as `2001:db8::1`, and there are enough that NAT is not needed. IPv6 also builds in IPsec support. A security point worth knowing: many networks run IPv6 without monitoring it, so attackers can use it as an unwatched path.

**TCP** is connection-oriented and reliable, starting with a three-way handshake (SYN, SYN-ACK, ACK). **UDP** is connectionless and faster, with no delivery guarantee, and is used for DNS lookups, streaming, and voice.

**Ports** identify the service on a host. Learn the common ones, because they appear as answer options:

| Port | Service | Secure alternative |
|---:|---|---|
| 21 | FTP | SFTP (22) or FTPS |
| 22 | SSH, SFTP | - |
| 23 | Telnet | SSH (22) |
| 25 | SMTP | SMTP with STARTTLS (587) |
| 53 | DNS | DNS over HTTPS or TLS |
| 80 | HTTP | HTTPS (443) |
| 443 | HTTPS | - |
| 3389 | RDP | RDP behind a VPN or gateway |

### VPN

A **virtual private network (VPN)** builds an encrypted tunnel across an untrusted network such as the internet. **Remote access VPNs** connect individual users to the organization; **site-to-site VPNs** connect whole offices. Common protocols are IPsec and TLS-based VPNs. A VPN protects data in transit, but once connected, a traditional VPN often gives broad network access, which zero trust (4.2) aims to replace with per-application access.

### Firewalls

A **firewall** permits or denies traffic according to rules. The outline mentions **ports** and **applications**, which are two generations of firewall:

- A **packet-filtering** firewall decides from addresses, protocols, and ports. It can allow port 443 but cannot tell whether the traffic on it is a web page or a tunnel for something else.
- A **stateful** firewall also tracks connections, so it lets replies back in only for conversations that started inside.
- A **next-generation firewall (NGFW)** is **application-aware**: it identifies the application regardless of port, and can apply rules such as "allow the CRM, block file-sharing apps", often with intrusion prevention built in.
- A **web application firewall (WAF)** protects a web application specifically, inspecting HTTP requests for attacks such as SQL injection.

Firewall rules should end with an implicit **deny all**, so anything not explicitly allowed is blocked.

### Other network devices

| Device | Layer | Does |
|---|---|---|
| **Switch** | 2 | Forwards frames to the right port by MAC address |
| **Router** | 3 | Forwards packets between networks by IP address |
| **Proxy** | 7 | Makes requests on behalf of clients; can filter and cache |
| **Load balancer** | 4 or 7 | Spreads traffic across servers |
| **IDS** | - | **Detects** suspicious traffic and alerts |
| **IPS** | - | Sits **inline** and **detects and blocks** |

IDS versus IPS is one of the most reliable questions in this domain: detection versus inline prevention.

### Wireless

**Wi-Fi** should use **WPA3**, or WPA2 where WPA3 is not available. WEP and WPA are broken and should never be used. Enterprise Wi-Fi authenticates each user individually (802.1X) rather than with one shared password. Threats to know are the **evil twin** (a fake access point with a trusted name), **rogue access points** (unauthorized ones plugged into the network), and eavesdropping on open networks.

**Bluetooth** is short range but not safe by default. **Bluejacking** sends unsolicited messages, **bluesnarfing** steals data from a device, and unpatched Bluetooth stacks have allowed remote code execution. The basic controls are turning Bluetooth off or making devices non-discoverable when not in use, pairing only with known devices, and patching.

### Embedded systems, IoT, and ICS

An **embedded system** is a computer built into another device to do one job: a printer, a medical pump, a car's braking system. The **Internet of Things (IoT)** is the large, growing set of such devices that connect to networks: cameras, smart TVs, thermostats, sensors. **Industrial control systems (ICS)**, including **SCADA** systems, run physical processes such as power grids, water treatment, and factory lines.

These devices share security problems: default or hard-coded passwords, little or no patching, long lifespans (an industrial controller may run for 20 years), and limited ability to run security software. In ICS, availability and safety come before confidentiality, because stopping a process can be dangerous. The standard answers are to **inventory** them, change default credentials, and **segment** them onto their own networks so a compromised camera cannot reach the finance servers.

### Common network threats

| Threat | What it is |
|---|---|
| **DoS / DDoS** | Overwhelming a service so legitimate users cannot reach it; DDoS uses many sources at once, often a botnet of compromised IoT devices |
| **On-path (man-in-the-middle)** | Intercepting traffic between two parties to read or alter it |
| **Spoofing** | Faking an identity: an IP address, MAC address, or email sender |
| **DNS poisoning** | Corrupting DNS answers to send users to a malicious site |
| **Malware** | Virus (attaches to a file), worm (spreads itself), trojan (disguised as something useful), ransomware (encrypts for payment), spyware, rootkit |
| **Zero-day** | Exploiting a vulnerability that has no patch yet |

Social engineering and phishing are covered with security awareness in [notes 02](./02-security-governance.md#23-security-awareness), and threat actors in [notes 05](./05-security-operations-and-incident-response.md#52-security-operations).

---

## 4.2 Network security architecture

### Network segmentation

**Segmentation** divides a network into zones so that a compromise in one does not spread freely to the others. The outline names three ways to do it.

**Firewall zones** group systems by trust level and put a firewall between them. The classic layout has an internet zone, a **DMZ** (screened subnet) holding public-facing servers such as a web server, and an internal zone. If the web server is compromised, the attacker is still outside the internal network.

**VLANs** (virtual local area networks) split one physical switch into several logical networks. Finance, guest Wi-Fi, and IoT devices can share cabling while staying on separate networks, with traffic between them forced through a router or firewall where rules apply.

**Microsegmentation** takes the idea down to individual workloads: each server or application gets its own policy, so even two servers in the same zone cannot talk unless they need to. It is common in data centers and cloud, and it is how zero trust is applied inside the network.

### Defense in depth

**Defense in depth** layers different controls so no single failure exposes the asset. On a network, that means perimeter firewalls, segmentation, intrusion prevention, hardened hosts, application controls, and encrypted data, each assuming the layer in front of it might fail.

### Zero trust

**Zero trust (ZT)** drops the old assumption that anything inside the network is trustworthy. Every request is checked on its merits, wherever it comes from. Its core principles are to **verify explicitly** (check identity, device health, and context on every request), use **least privilege** access (grant only what the request needs, for as short a time as possible), and **assume breach** (design as if an attacker is already inside, so segment and monitor everything).

In practice zero trust replaces "connect to the VPN and reach everything" with per-application access decided by a policy engine. It is a strategy, not a product: no single tool makes a network zero trust.

---

## 4.3 Cloud security

### Characteristics

The outline uses the five essential characteristics from the NIST definition of cloud computing. **On-demand self-service** means customers provision resources themselves without asking a person. **Broad network access** means services are reached over the network from many kinds of device. **Resource pooling** means the provider serves many customers from shared hardware (multi-tenancy). **Rapid elasticity** means capacity grows and shrinks quickly, often automatically. **Measured service** means usage is metered and billed.

Each has a security side. Self-service means anyone with credentials can create resources, including insecure ones. Broad network access means a stolen password works from anywhere. Resource pooling means isolation between tenants is the provider's job. Measured service means a compromised account can run up enormous bills, for example by mining cryptocurrency.

### Service models

| Model | You manage | Provider manages | Example |
|---|---|---|---|
| **IaaS** | Operating system, runtime, applications, data | Hardware, virtualization, physical network | Virtual machines |
| **PaaS** | Applications and data | Everything below | App hosting platforms, managed databases |
| **SaaS** | Data and access configuration | Everything else | Email, CRM |

### Deployment models

**Public** cloud is shared infrastructure owned by a provider. **Private** cloud serves one organization, on its premises or hosted. **Hybrid** cloud connects public and private. **Community** cloud is shared by organizations with common requirements, such as government agencies. **Multi-cloud** means using more than one public provider.

### Shared security model

The **shared responsibility model** (the outline calls it the shared security model) divides security duties between provider and customer, and the line moves with the service model. Responsibility shifts toward the provider as you go from IaaS to PaaS to SaaS. Two things never move: **physical security is always the provider's**, and **your data and who can access it are always yours**.

Most cloud breaches happen on the customer's side of the line: a storage bucket left public, an access key committed to a code repository, an over-privileged account. The provider secured its part; the customer did not.

A **service level agreement (SLA)** defines the level of service a provider commits to and what happens if it misses. A **managed service provider (MSP)** operates services on your behalf; you can hand it tasks, but not accountability.

AI services follow the same model. With an AI service from a cloud provider, the provider secures the model platform, while the customer owns the data sent to it, who can call it, and how its output is used.

---

## Key terms

- **OSI model** - the seven-layer conceptual model of network communication
- **TCP** - the connection-oriented transport protocol providing reliable, ordered delivery
- **UDP** - the connectionless transport protocol offering speed without delivery guarantees
- **IPv6** - the 128-bit successor to IPv4 addressing, with enough addresses that NAT is unnecessary
- **NAT** - network address translation, mapping private addresses to public ones at the network edge
- **Port** - the number identifying a particular service on a host
- **VPN** - an encrypted tunnel carrying traffic across an untrusted network
- **Firewall** - a device or software permitting or denying traffic according to rules
- **Next-generation firewall** - an application-aware firewall that identifies applications regardless of port
- **Web application firewall** - a firewall inspecting HTTP traffic to protect a specific web application
- **IDS** - an intrusion detection system that alerts on suspicious traffic without blocking it
- **IPS** - an intrusion prevention system that detects and blocks suspicious traffic inline
- **WPA3** - the current Wi-Fi security standard, replacing WPA2
- **Evil twin** - a malicious wireless access point impersonating a legitimate network name
- **Bluesnarfing** - stealing data from a device over Bluetooth
- **Embedded system** - a computer built into another device to perform a dedicated function
- **IoT** - the Internet of Things, network-connected everyday and industrial devices
- **ICS** - industrial control systems that run physical processes, including SCADA
- **DDoS** - a distributed denial of service attack using many sources to exhaust a target
- **On-path attack** - interception of communication between two parties, formerly called man-in-the-middle
- **Zero-day** - an exploit against a vulnerability for which no patch exists
- **Network segmentation** - dividing a network into zones so a compromise in one does not spread to others
- **DMZ** - a screened subnet hosting internet-facing services, isolated from the internal network
- **VLAN** - a logical segmentation of a physical network
- **Microsegmentation** - applying separate access policy to individual workloads rather than whole zones
- **Zero trust** - a model that verifies explicitly, grants least privilege, and assumes breach rather than trusting network location
- **Rapid elasticity** - the cloud characteristic of scaling capacity up and down quickly, often automatically
- **Resource pooling** - the cloud characteristic of serving many customers from shared infrastructure
- **IaaS** - a cloud model providing infrastructure, with the customer managing the operating system upward
- **PaaS** - a cloud model providing a managed platform, with the customer managing applications and data
- **SaaS** - a cloud model providing complete applications, with the customer managing data and access only
- **Shared responsibility model** - the division of security duties between cloud provider and customer
- **SLA** - a service level agreement defining committed service levels and remedies

---

## Related

- [Notes 05: security operations and incident response](./05-security-operations-and-incident-response.md)
- [Scenarios](../scenarios.md) - scenario 8
- [DNS explained](https://cloud.noblerworks.com/learn/concepts/dns-explained/)
- [TLS and HTTPS](../../../../learn/concepts/tls-and-https.md)
- [Shared responsibility model](../../../../learn/concepts/shared-responsibility-model.md)
- **[📖 NIST SP 800-145](https://csrc.nist.gov/pubs/sp/800/145/final)** - the NIST definition of cloud computing and its five characteristics
- **[📖 NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final)** - zero trust architecture
