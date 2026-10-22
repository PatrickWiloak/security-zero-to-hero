---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 10 min
---

# ISC2 Certified in Cybersecurity (CC) Fact Sheet

## Exam Overview

**Exam Code:** CC
**Exam Name:** Certified in Cybersecurity
**Level:** Foundational (entry level)
**Duration:** 120 minutes
**Format:** Computerized adaptive testing (CAT); multiple choice and advanced item types
**Questions:** 100-125
**Passing Score:** 700 out of 1000
**Cost:** Free exam and free self-paced training through the ISC2 One Million Certified in Cybersecurity initiative; an Annual Maintenance Fee applies once certified
**Valid For:** 3 years, maintained with continuing professional education credits and the AMF
**Delivery:** Pearson VUE test center, or online proctored where available
**Prerequisites:** **None.** No work experience required

> **Verify before booking.** The free exam and training offer, AMF amount, and CPE requirements are set by ISC2 and change. Confirm on the official page below.

**[📖 ISC2 Certified in Cybersecurity](https://www.isc2.org/certifications/cc)** - exam outline, registration, and the free training offer
**[📖 ISC2 CC exam outline](https://www.isc2.org/certifications/cc/cc-certification-exam-outline)** - the authoritative domain breakdown, effective September 1, 2026
**[📖 ISC2 One Million Certified in Cybersecurity](https://www.isc2.org/landing/1mcc)** - the free training and exam program

## Why this exam is in this repo

This repository is called "zero to hero", and until now its security path started at [Security+](../../comptia/security-plus/), which assumes some background and costs several hundred dollars. CC is the genuine zero: **no prerequisites, free training, free exam**, and it is the entry rung of the ISC2 ladder that continues to [CCSP](../ccsp/) and [CISSP](../cissp/).

It is also the best first certification for someone testing whether security interests them at all, because the only cost is time.

## Target Audience

- Complete beginners to cybersecurity
- Career changers evaluating the field
- IT staff moving toward a security role
- Students, and anyone who wants an entry credential without a work-experience requirement
- Non-security staff who need credible security literacy: developers, project managers, auditors

## Exam Domains

The outline effective **September 1, 2026** replaced all five domains of the 2022 outline. Weights are ISC2's average weights for the adaptive exam.

**[📖 ISC2: Inside the updated CC exam](https://www.isc2.org/insights/2026/08/inside-the-updated-isc2-cc-exam)** - ISC2's own summary of what changed

| 2022 outline | 2026 outline |
|---|---|
| Security Principles (26%) | Security Principles (24%) |
| Business Continuity, Disaster Recovery and Incident Response (10%) | Split: BC and DR to Security Governance, IR to Security Operations and Incident Response |
| Access Control Concepts (22%) | Identity and Access Management (IAM) Concepts (20%) |
| Network Security (24%) | Networking and Cloud Security Concepts (21.3%) |
| Security Operations (18%) | Security Operations and Incident Response (17.3%) |
| - | Security Governance (17.3%), new |

### Domain 1: Security Principles (24%)

The largest domain.

**Objectives:** 1.1 cybersecurity concepts; 1.2 risk management concepts; 1.3 governance concepts; 1.4 cybersecurity controls; 1.5 professional and ethical conduct.

**Key Concepts:**
- The CIA triad: confidentiality, integrity, availability
- Authentication, authorization, and accounting (AAA), and non-repudiation
- Privacy and personally identifiable information
- The risk management lifecycle: identify, assess, prioritize, treat (avoid, mitigate, transfer, accept), monitor
- Regulations and laws, frameworks and guidelines (NIST CSF, ISO/IEC 27001, CIS Controls), and policies, standards, and procedures
- Technical, administrative, and physical controls, and the control functions
- Professional code of conduct, due care and due diligence, and the ISC2 Code of Ethics canons

### Domain 2: Security Governance (17.3%)

New in 2026.

**Objectives:** 2.1 plan governance, risk, and compliance (GRC); 2.2 understand redundancy; 2.3 understand security awareness; 2.4 measure cybersecurity effectiveness.

**Key Concepts:**
- The purpose and importance of GRC, and GRC frameworks and tools
- Business continuity: business impact analysis, maximum tolerable downtime, the continuity plan
- Disaster recovery: RTO, RPO, backup types, recovery sites, plan testing
- Organizational culture and security leadership
- Awareness concepts: social engineering, password protection, phishing, and AI-generated lures such as deepfakes
- Key metrics, key performance indicators, key risk indicators (KRIs), dashboards, scorecards, and reports

### Domain 3: Identity and Access Management (IAM) Concepts (20%)

**Objectives:** 3.1 understand identity life cycle management; 3.2 understand logical access controls.

**Key Concepts:**
- The identity life cycle: roles definition, provisioning, review, deprovisioning
- Joiner, mover, leaver, and privilege creep
- Non-human identities, including service accounts and AI agents
- IAM frameworks and tools: IGA, identity providers, SSO, federation, SCIM, privileged access management
- Principle of least privilege and need to know
- Separation of duties
- Access control models: DAC, MAC, RBAC, ABAC, rule-based

### Domain 4: Networking and Cloud Security Concepts (21.3%)

The second largest domain, and the one most beginners find hardest.

**Objectives:** 4.1 understand network security; 4.2 understand network security architecture; 4.3 understand cloud security.

**Key Concepts:**
- The OSI and TCP/IP models, IPv4 and IPv6, and VPNs
- Firewalls: ports versus applications (packet filtering, stateful, next-generation)
- Wireless: Wi-Fi security and Bluetooth risks
- Embedded systems, industrial control systems, and the Internet of Things
- Network segmentation: firewall zones, VLANs, microsegmentation
- Defense in depth and zero trust
- Cloud characteristics, service models, deployment models, and the shared security model

### Domain 5: Security Operations and Incident Response (17.3%)

**Objectives:** 5.1 understand data security; 5.2 understand security operations; 5.3 understand incident response; 5.4 understand asset protection; 5.5 understand security testing.

**Key Concepts:**
- Data handling: classification, labeling, masking, and sanitization
- Encryption: symmetric, asymmetric, hashing, and quantum-resistant cryptography
- Logging and monitoring, and security event triage (use cases, prioritization, correlation)
- Threat actors, cyber threat intelligence, and threat frameworks such as MITRE ATT&CK
- The incident response plan, data handling during incidents, and IR exercises such as tabletops
- Asset life cycle management, including end-of-life software and devices
- Configuration and change management
- Security readiness testing (red, blue, and purple teams), application testing (vulnerability scanning, static and dynamic analysis, threat modeling), and physical penetration testing

## Where CC sits in the ISC2 ladder

| Certification | Experience required | Level |
|---|---|---|
| **CC** | None | Entry |
| **SSCP** | 1 year | Practitioner |
| **[CCSP](../ccsp/)** | 5 years, including cloud | Cloud specialist |
| **[CISSP](../cissp/)** | 5 years across 2 domains | Senior |

CC has no experience requirement, which is what makes it the true starting point. CISSP requires five years, so passing the exam earlier makes you an Associate of ISC2 until you accumulate it.

## Related repo material

- [Notes](./notes/) - five notes, one per 2026 domain
- [Practice plan](./practice-plan.md) - 4-week schedule
- [Scenarios](./scenarios.md)
- [Strategy](./strategy.md)
- [Security+](../../comptia/security-plus/) - the natural next step
- [CISSP](../cissp/) and [CCSP](../ccsp/) - the senior ISC2 certifications
- [Day One](https://cloud.noblerworks.com/learn/day-one/) - if the terminal and networking vocabulary is new
- [Security topic](../../../topics/security.md)
