---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 16 min
---

# 06 - Network and communications security

**Domain 6: Network and Communications Security (16%)** - objectives 6.1 to 6.7.

The broadest technical domain. A practitioner is expected to read a network diagram, know what each device does and where it belongs, and recognise the common attacks.

---

## 6.1 Fundamental networking concepts

The **OSI model** has seven layers: physical (1), data link (2), network (3), transport (4), session (5), presentation (6) and application (7). The **TCP/IP model** compresses them to link, internet, transport and application. Know which devices and attacks live at which layer: switches and MAC addresses at layer 2, routers and IP at layer 3, firewalls (stateful at 3 and 4, application-aware at 7), TCP and UDP at layer 4.

Know common ports and what runs on them: 20/21 FTP, 22 SSH, 23 Telnet, 25 SMTP, 53 DNS, 80 HTTP, 110 POP3, 143 IMAP, 443 HTTPS, 3389 RDP, 389 and 636 LDAP and LDAPS. The insecure partners to retire: Telnet, FTP, HTTP and plain LDAP.

**TCP** is connection-oriented, with a three-way handshake and reliability; **UDP** is connectionless and fast. **IPv4** has 32-bit addresses, with private ranges 10.0.0.0/8, 172.16.0.0/12 and 192.168.0.0/16 translated at the edge by **NAT**; **IPv6** has 128-bit addresses and brings its own attack surface (often unmonitored on dual-stack networks). **Topologies** (star, mesh, bus, ring) differ in resilience and cost; modern LANs are stars around switches. **Transmission media** run from copper (susceptible to interference and tapping) to fibre (immune to electromagnetic interference and harder to tap). **Software-defined networking (SDN)** separates the control plane from the data plane; centralising control makes policy easy to apply and makes the controller a high-value target.

## 6.2 Network attacks and countermeasures

| Attack | What it does | Countermeasure |
|---|---|---|
| Denial of service, DDoS | Exhausts bandwidth or resources | Rate limiting, upstream scrubbing, redundancy |
| Man-in-the-middle | Sits between two parties to read or alter traffic | TLS with certificate validation, mutual authentication |
| ARP spoofing | Poisons the layer 2 address map | Dynamic ARP inspection, port security |
| DNS cache poisoning | Plants false DNS answers | DNSSEC, source port randomisation, patched resolvers |
| VLAN hopping | Jumps between VLANs | Disable unused trunking, explicit native VLAN |
| Spoofing | Forges source addresses | Ingress and egress filtering |
| Eavesdropping, sniffing | Captures traffic | Encryption, switched networks |
| Replay | Resends captured valid messages | Nonces, timestamps, session tokens |

The pattern: identify the layer, then choose the control that removes the trust the attack relies on. Network-wide, **egress filtering** (controlling what leaves) catches malware calling home and stops your network being used to attack others.

## 6.3 Network access controls

Controlling who may join and how they reach resources.

- **802.1X** is port-based network access control. The device (supplicant) authenticates through a switch or access point (authenticator) to an authentication server before the port passes traffic. It uses **EAP** methods, with certificate-based EAP-TLS the strongest.
- **RADIUS** centralises authentication, authorisation and accounting for network access such as Wi-Fi and VPN. **TACACS+** does the same for device administration; RFC 8907 describes it as widely used to centralise administration of routers, network access servers and other devices. TACACS+ separates authentication, authorisation and accounting and encrypts the whole payload, which is why it is preferred for administrator command authorisation, while RADIUS is typical for end-user network access.
- **Network access control (NAC)** checks a device's posture (patched, antivirus running) before admitting it, and quarantines failures.
- **Remote access**: VPNs (IPsec or TLS based), bastion hosts and privileged access gateways. Require MFA, log sessions, and prefer a **split tunnel** only when you accept that the client's other traffic is outside your inspection; **full tunnel** sends everything through the corporate path.

## 6.4 Network security management

Good design limits blast radius. **Segmentation** places systems in separate zones with enforced rules between them, using VLANs, subnets and firewalls. Put public servers in a DMZ, databases in an internal tier, management interfaces on an isolated **out-of-band** network, and guests apart from staff. **Microsegmentation** applies the same idea per workload.

Place devices deliberately: a firewall at each trust boundary, an IDS where traffic is visible but not inline, a proxy near egress, a VPN gateway at the edge. Secure **device management**: change default credentials, disable unused services, use SSH not Telnet, restrict management to a dedicated network, back up configurations, patch firmware, and record changes.

## 6.5 Network security appliances and services

- **Firewalls** control traffic by policy. NIST SP 800-41 Rev. 1 reviews firewall technologies and how to establish policy, and recommends selecting, configuring, testing, deploying and managing them deliberately. Types: **packet filtering** (addresses, ports), **stateful inspection** (tracks connections), **proxy or application gateway** (terminates and inspects), and **next-generation** (adds application identity, user identity and intrusion prevention). Rule hygiene: default deny, least privilege, ordered rules, documented reasons and regular review.
- **IDS** detects and alerts; **IPS** sits inline and blocks. Detection can be **signature-based** (known patterns, few false positives, blind to new attacks) or **anomaly-based** (finds new behaviour, more false positives). **Network-based** sensors see traffic; **host-based** see what happens on the machine.
- **Web application firewall (WAF)** filters HTTP for application attacks. **Proxies** and **secure web gateways** filter and log outbound web use. **Load balancers** distribute traffic and terminate TLS.
- **Data loss prevention (DLP)** inspects data in motion, at rest and at the endpoint for sensitive patterns and blocks or alerts.
- **Unified threat management (UTM)** bundles several functions in one box, convenient but a single point of failure.

## 6.6 Securing wireless communications

Wi-Fi security moved from WEP (broken) through WPA and WPA2 to **WPA3**; use WPA3 or WPA2 with AES (CCMP), never WEP or open networks for business use. **WPA-Personal** shares one passphrase; **WPA-Enterprise** authenticates each user through 802.1X and EAP, so leavers can be cut off individually. Also disable WPS, use strong passphrases, separate guest and corporate SSIDs, and scan for **rogue access points** and **evil twins** (a fake access point with a legitimate name). Hiding the SSID is not a security control.

**Bluetooth** risks include pairing weaknesses and unwanted discoverability; turn it off when unused. **NFC** works over centimetres, which limits eavesdropping but not relay attacks. **Cellular** networks add the risk of rogue base stations. All short-range wireless should be treated as untrusted transport and protected with application-level encryption.

## 6.7 Secure and monitor IoT devices

IoT devices are often unpatchable, ship with default credentials and are never inventoried. The practitioner response: inventory them, change defaults, **isolate** them on their own segment with default-deny rules to the internet, apply firmware updates when they exist, monitor their traffic for change, and plan **end-of-life**, because a device no longer receiving updates is a permanent vulnerability to replace or wall off.

---

## Key terms

- **802.1X** - port-based network access control in which a device authenticates before the port passes traffic
- **RADIUS** - a protocol centralising authentication, authorisation and accounting for network access
- **TACACS+** - a protocol centralising device administration, separating authentication, authorisation and accounting
- **Network access control** - checking a device's posture before admitting it to the network and quarantining failures
- **Screened subnet** - a network segment between external and internal firewalls hosting public-facing servers
- **Microsegmentation** - applying segmentation rules per workload rather than per network
- **Stateful inspection** - a firewall technique that tracks the state of connections to judge packets
- **Intrusion prevention system** - an inline device that detects and blocks malicious traffic
- **Data loss prevention** - tooling that inspects data for sensitive patterns and blocks or alerts on leakage
- **Evil twin** - a rogue wireless access point impersonating a legitimate network name
- **DNS cache poisoning** - planting false DNS answers in a resolver's cache
- **Egress filtering** - controlling what traffic is allowed to leave a network
- **Software-defined networking** - separating the network control plane from the data plane for central policy

---

## Related

- [Notes 05: cryptography](./05-cryptography.md)
- [Notes 07: systems and application security](./07-systems-and-application-security.md)
- [DNS explained](https://cloud.noblerworks.com/learn/concepts/dns-explained/)
- **[📖 NIST SP 800-41 Rev. 1: Guidelines on Firewalls and Firewall Policy](https://csrc.nist.gov/pubs/sp/800/41/r1/final)** - firewall technologies and policy (September 2009)
- **[📖 RFC 8907: TACACS+ Protocol](https://www.rfc-editor.org/rfc/rfc8907)** - centralised device administration
