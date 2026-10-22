# CompTIA CySA+ (CS0-004)

## Important Notice

**This guide follows CySA+ V4, exam code CS0-004, launched June 23, 2026.** The previous exam, CS0-003, retires in English on December 22, 2026 (Japanese, Portuguese, and Spanish on March 23, 2027). If you are booked on CS0-003 before then, notes 01 to 04 still apply and [notes 05](notes/05-whats-new-in-cs0-004.md) is optional; objective 1.6 (AI in security operations) has no CS0-003 counterpart at all.

What changed from CS0-003: a new objective on AI in security operations (1.6), new named tools (OpenCTI, YARA, Nuclei, Prowler, Trivy, Checkov, Atomic Red Team, Caldera and others), EPSS in prioritization, a rewritten objective 2.4 on control types, risk, application security, and third-party risk, attack methodology frameworks moved into incident response, and new SOC metrics. Weights shifted toward incident response. All of it is taught in [notes 05](notes/05-whats-new-in-cs0-004.md).

Sources: **[📖 CompTIA CySA+ V4](https://www.comptia.org/en/certifications/cybersecurity-analyst/v4/)** (exam details) and **[📖 CompTIA CySA+](https://www.comptia.org/en/certifications/cybersecurity-analyst/)** (V3 retirement dates)

---

## Exam Overview

The CompTIA Cybersecurity Analyst (CySA+) CS0-004 certification validates the ability to perform incident response and vulnerability management, detect and analyze indicators of malicious activity, and use tools, methods, and frameworks to prioritize vulnerabilities and respond to incidents. It bridges Security+ and SecurityX/PenTest+, focusing on the analyst-level "blue team" defensive role inside a security operations center (SOC).

**Exam Details:**
- **Exam Code:** CS0-004 (V4)
- **Launch Date:** June 23, 2026
- **Duration:** 165 minutes
- **Number of Questions:** Maximum of 85
- **Question Types:** Multiple choice and performance-based questions (PBQs)
- **Passing Score:** 750 on a scale of 100-900
- **Cost:** $404 USD
- **Delivery:** Pearson VUE testing center or online proctoring
- **Validity:** 3 years (renewable via CE program)
- **Prerequisites:** None required (Network+ and Security+ recommended; CompTIA recommends about 4 years as a SOC or vulnerability analyst)

## Exam Domains

### Domain 1: Security Operations (34%)
- 1.1 Explain concepts related to system and network architecture in security operations
- 1.2 Given a scenario, analyze indicators of potential malicious activity
- 1.3 Given a scenario, use tools to determine malicious activity
- 1.4 Explain threat intelligence and threat-hunting concepts
- 1.5 Explain the importance of efficiency and process improvement in security operations
- 1.6 Summarize concepts related to the use of AI in security operations (new in V4)

**Key Topics:**
- Logging concepts, OS and infrastructure architecture, ZTNA, SASE, PAM, secrets management, OT/ICS/SCADA
- Network, host, application, cloud, and identity indicators: beaconing, LOLBins, impossible travel, BEC, typosquatting
- Tools - CyberChef, Wireshark, tcpdump, Snort, Suricata, Zeek, SIEM, OTX, MISP, OpenCTI, EDR/XDR, WHOIS, AbuseIPDB, YARA, VirusTotal, sandboxes, MXToolbox, UEBA
- Threat intelligence - TTPs, heat maps, Pyramid of Pain, attribution, confidence, atomic vs behavioral IoCs, STRIDE, cyber deception
- SOAR, infrastructure as code, rule tuning, APIs, webhooks
- AI risks (hallucinations, data exposure, model poisoning, malicious prompts), AI governance, AI use cases

### Domain 2: Vulnerability Management (26%)
- 2.1 Given a scenario, implement the appropriate vulnerability scanning method
- 2.2 Given a scenario, analyze output from vulnerability assessment tools
- 2.3 Given a scenario, analyze data to prioritize and mitigate vulnerabilities
- 2.4 Explain concepts related to control types, risks, and vulnerability management

**Key Topics:**
- Asset inventory, scan planning, internal/external, agent/agentless, credentialed, passive/active, discovery, baseline scanning (PCI DSS, CIS, ISO 27000)
- Tools - Angry IP Scanner, Masscan, Nmap, Metasploit, Maltego, Recon-ng, Burp Suite, ZAP, Nikto, Nessus, Nuclei, OpenVAS, ScoutSuite, Prowler, Trivy, Checkov, Atomic Red Team, Caldera
- CVSS, EPSS, active exploitation, asset value, context, true/false positives and negatives
- Mitigation - attack surface management, secure coding, patching, exceptions, compensating controls, validation of remediation
- Control types and functions, inherent and residual risk, risk appetite, SLOs, SAST, DAST, SAMM, SCA, SBOM

### Domain 3: Incident Response and Management (24%)
- 3.1 Summarize concepts related to attack methodology frameworks
- 3.2 Summarize the incident response process
- 3.3 Given a scenario, implement incident response techniques

**Key Topics:**
- Cyber Kill Chain, Diamond Model, MITRE ATT&CK
- Preparation, detection, analysis, containment, eradication, recovery, post-incident
- Plans, playbooks, roles, tabletop and simulation exercises
- Log collection, correlation, enrichment, triage, timelines, severity and impact
- Evidence, chain of custody, integrity validation, legal hold, isolation and release, restoration, root cause analysis, corrective actions

### Domain 4: Reporting and Communication (16%)
- 4.1 Explain the importance of vulnerability management reporting and communication
- 4.2 Explain the importance of security operations and incident response reporting and communication

**Key Topics:**
- Vulnerability scan reports, compliance findings, risk scorecards, action plans, escalation
- Inhibitors to remediation - dependencies, contracts, governance, business interruption, legacy and proprietary systems, patch availability
- Incident declaration, executive summary, stakeholders (legal, PR, regulators, law enforcement, customers)
- After action reports, lessons learned, shift handover, internal threat intelligence reports
- Metrics - alert volume, false-positive and true-positive rates, mean time to close, detect, respond, and remediate, phishing click rate

## Study Materials

### Notes
- [01 - Security Operations](notes/01-security-operations.md) - Logs, IoCs, threat intel, MITRE ATT&CK, hunting
- [02 - Vulnerability Management](notes/02-vulnerability-management.md) - Scanning, CVSS, prioritization, remediation
- [03 - Incident Response](notes/03-incident-response.md) - NIST 800-61, evidence handling, forensics
- [04 - Reporting and Communication](notes/04-reporting-communication.md) - Reports, metrics, stakeholders
- [05 - What changed in CS0-004](notes/05-whats-new-in-cs0-004.md) - AI in security operations, new tools, EPSS, control types and risk, IR techniques, SOC metrics

### Study Resources
- [Fact Sheet](fact-sheet.md) - SIEM queries, Sigma rules, Snort/Suricata, MITRE ATT&CK, log cheatsheets
- [Practice Plan](practice-plan.md) - 8-week structured study schedule
- [Scenarios](scenarios.md) - 12+ incident response and threat hunting scenarios
- [Strategy](strategy.md) - Exam day strategy, PBQ tips, keyword decoding

## Official Resources

- **[CompTIA CySA+ V4 page](https://www.comptia.org/en/certifications/cybersecurity-analyst/v4/)** - Official certification details for CS0-004
- **[CS0-004 Exam Objectives](https://lecbyo.files.cmp.optimizely.com/download/68b1eae88e5011f08868a275d699e612)** - Complete exam objectives PDF
- **[CompTIA CertMaster Learn CySA+](https://www.comptia.org/en-us/certifications/cybersecurity-analyst/)** - Official interactive learning
- **[CompTIA CertMaster Practice CySA+](https://www.comptia.org/en-us/resources/certmaster-training/)** - Official practice questions
- **[CompTIA CertMaster Labs CySA+](https://www.comptia.org/en-us/resources/certmaster-training/)** - Official hands-on labs

## Recommended Training

### Video Courses
1. **Jason Dion CySA+** (Udemy, check the course covers CS0-004) - Most popular, full video course plus practice
2. **CompTIA CertMaster Learn** - Official self-paced training with labs
3. **ITProTV/ACI Learning CySA+** - Video course with hands-on labs
4. **Pluralsight CySA+ Path** - Multi-instructor structured path

### Practice Exams
1. **CompTIA CertMaster Practice** - Official practice questions
2. **Jason Dion Practice Exams** (Udemy) - Six full-length practice exams
3. **Kaplan IT Training** - Practice exams with explanations
4. **CyberVista** - Adaptive practice platform

### Books
1. **CompTIA CySA+ Study Guide (CS0-004)** by Mike Chapple and David Seidl - Sybex
2. **CompTIA CySA+ Cert Guide** by Troy McMillan - Pearson (CS0-003 edition; check for a CS0-004 edition)
3. **CompTIA CySA+ All-in-One Exam Guide** by Brent Chapman - McGraw Hill (CS0-003 edition; check for a CS0-004 edition)

### Hands-On Labs
- **TryHackMe SOC Level 1** path - SIEM, log analysis, threat intel
- **Blue Team Labs Online** - Investigation challenges
- **LetsDefend.io** - Live SOC simulation with real alerts
- **CyberDefenders.org** - DFIR and blue team challenges
- **Splunk Boss of the SOC (BOTS)** - Splunk dataset challenges

## Companion Materials

| Cert | Why It Pairs |
|------|--------------|
| **CompTIA Security+ (SY0-701)** | Foundational layer; CySA+ assumes Security+ knowledge |
| **AWS Security Specialty (SCS-C02)** | Cloud-native detection, GuardDuty, Security Hub, CloudTrail |
| **Microsoft SC-200** | Sentinel KQL, Defender XDR, mirrors CySA+ analyst role for Azure |
| **(ISC)2 CISSP** | Strategic and managerial layer above CySA+ tactical work |
| **GIAC GCIH** | Deep dive on incident handling, complements Domain 3 |
| **GIAC GCIA** | Network intrusion analysis, complements packet/log work |
| **GIAC GCFA** | Forensic analysis, complements evidence handling |

## Next Steps After Certification

### Career Paths
- SOC Analyst (Tier 1, Tier 2, Tier 3)
- Incident Responder / DFIR Analyst
- Threat Hunter
- Vulnerability Management Analyst
- Cyber Threat Intelligence Analyst
- Detection Engineer
- Security Operations Engineer

### Advanced Certifications
- **CompTIA CASP+ (SecurityX)** - Senior security engineer/architect role
- **CompTIA PenTest+** - Offensive complement to CySA+
- **GIAC GCIH** - GIAC Certified Incident Handler
- **GIAC GCIA** - GIAC Certified Intrusion Analyst
- **GIAC GCFA** - GIAC Certified Forensic Analyst
- **(ISC)2 CISSP** - Senior leadership track
- **AWS Security Specialty / Microsoft SC-200** - Cloud-native blue team

---

**Good luck with your CompTIA CySA+ certification!** This is the gateway certification for SOC analyst and incident responder roles. Focus on log reading, tool output interpretation, and matching IoCs to MITRE ATT&CK techniques.
