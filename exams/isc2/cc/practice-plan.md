---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 4 min
---

# ISC2 CC Study Plan

Four weeks at 5-6 hours per week, assuming you are starting from little or no security background. The plan follows the outline effective September 1, 2026. The free ISC2 self-paced course is the best primary source; check that the version you are given matches the 2026 domains, and use these notes for anything it does not cover yet.

## Week 1: Security principles (Domain 1, 24%)

- [ ] Register for the free ISC2 training and download the 2026 exam outline
- [ ] The CIA triad, with an example of a breach of each
- [ ] Authentication, authorization, accounting, non-repudiation
- [ ] Privacy and personally identifiable information
- [ ] Risk vocabulary: asset, threat, vulnerability, likelihood, impact, risk
- [ ] The risk management lifecycle in order, and the four treatments with an example of each
- [ ] Regulations and laws, frameworks (NIST CSF, ISO/IEC 27001, CIS Controls), and policies, standards, procedures, guidelines
- [ ] Control types (technical, administrative, physical) and functions (preventive, detective, corrective, deterrent, compensating)
- [ ] Physical controls: badges, mantraps, guards, CCTV, and the tailgating problem
- [ ] Due care versus due diligence; the ISC2 Code of Ethics canons, in order
- [ ] Review Notes: `notes/01-security-principles.md`

## Week 2: Networking and cloud security (Domain 4, 21.3%)

- [ ] OSI model layers and what each does; TCP/IP model mapping
- [ ] IPv4 and IPv6, private ranges and NAT, common ports, TCP versus UDP
- [ ] VPNs: remote access and site-to-site
- [ ] Firewalls: packet filtering, stateful, next-generation (application-aware), WAF
- [ ] IDS versus IPS
- [ ] Wireless: WPA3 and WPA2, evil twins, rogue access points, Bluetooth risks
- [ ] Embedded systems, IoT, and industrial control systems, and why they are segmented
- [ ] Segmentation: firewall zones and the DMZ, VLANs, microsegmentation
- [ ] Defense in depth and the three zero trust principles
- [ ] The five cloud characteristics, service models, deployment models
- [ ] The shared security model, SLAs, and managed service providers
- [ ] Review Notes: `notes/04-networking-and-cloud-security.md`

## Week 3: Identity and governance (Domains 3 and 2)

- [ ] The identity life cycle: roles definition, provisioning, review, deprovisioning
- [ ] Joiner, mover, leaver; privilege creep; non-human identities and AI agents
- [ ] IAM tools: IGA, identity providers, SSO, federation, SCIM, PAM and just-in-time access
- [ ] Least privilege, need to know, separation of duties, job rotation
- [ ] Access control models: DAC, MAC, RBAC, ABAC, rule-based
- [ ] GRC: what it is for, why leadership owns risk, frameworks and GRC tools
- [ ] Business continuity: BIA, maximum tolerable downtime, the continuity plan
- [ ] Disaster recovery: RTO, RPO, backup types, recovery sites, plan testing
- [ ] Security culture, leadership, social engineering, phishing variants, deepfakes, password protection
- [ ] Metrics, KPIs versus KRIs, dashboards, scorecards, and reports
- [ ] Review Notes: `notes/03-identity-and-access-management.md` and `notes/02-security-governance.md`

## Week 4: Operations, incident response, and review (Domain 5, 17.3%)

- [ ] Data handling: classification, labeling, masking, sanitization
- [ ] Encryption: symmetric, asymmetric, hashing, and what each is for
- [ ] Quantum-resistant cryptography and harvest now, decrypt later
- [ ] Logging, monitoring, SIEM, and triage (use cases, prioritization, correlation)
- [ ] Threat actor types and motivations; threat intelligence and IOCs; MITRE ATT&CK and the Cyber Kill Chain
- [ ] Incident response phases in order; the incident response plan; evidence and chain of custody; tabletop exercises
- [ ] Asset life cycle and end-of-life risk; configuration and change management
- [ ] Red, blue, and purple teams; vulnerability scanning, static and dynamic analysis, threat modeling; physical penetration testing
- [ ] Review Notes: `notes/05-security-operations-and-incident-response.md`
- [ ] Work every scenario in [scenarios.md](./scenarios.md)
- [ ] Write out every definition pair listed in the readiness check below
- [ ] Two full timed practice exams; review every wrong answer
- [ ] Light review the day before; do not learn new material

## Readiness check

Define each pair cleanly, with an example, without notes:

- [ ] Threat versus vulnerability versus risk
- [ ] Authentication versus authorization versus accounting
- [ ] Preventive versus detective versus corrective versus deterrent versus compensating
- [ ] Technical versus administrative versus physical control
- [ ] Least privilege versus need to know
- [ ] DAC versus MAC versus RBAC versus ABAC
- [ ] Symmetric versus asymmetric encryption versus hashing
- [ ] IDS versus IPS
- [ ] RTO versus RPO
- [ ] Business continuity versus disaster recovery versus incident response
- [ ] Policy versus standard versus procedure versus guideline
- [ ] Due care versus due diligence
- [ ] KPI versus KRI
- [ ] Red team versus blue team versus purple team
- [ ] Static analysis versus dynamic analysis versus vulnerability scanning
