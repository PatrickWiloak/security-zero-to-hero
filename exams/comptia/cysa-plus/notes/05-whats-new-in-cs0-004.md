---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 35 min
---

# CySA+ CS0-004 - What Changed and the New Objectives

CompTIA launched CySA+ V4 (exam code **CS0-004**) on June 23, 2026. The English CS0-003 exam retires on December 22, 2026 (Japanese, Portuguese, and Spanish on March 23, 2027). Notes 01 to 04 cover the four domains, which keep their names in V4; this page teaches what V4 added or moved, so read it alongside them.

**[📖 CompTIA CySA+ V4](https://www.comptia.org/en/certifications/cybersecurity-analyst/v4/)** - exam details for CS0-004
**[📖 CS0-004 exam objectives (PDF)](https://lecbyo.files.cmp.optimizely.com/download/68b1eae88e5011f08868a275d699e612)** - the full objectives document

## The shape of the change

| Domain | CS0-003 | CS0-004 | What moved |
|--------|--------:|--------:|------------|
| 1. Security Operations | 33% | 34% | New objective 1.6 on AI in security operations; attack methodology frameworks moved out to domain 3 |
| 2. Vulnerability Management | 30% | 26% | Five objectives became four; the list of named attacks to mitigate (old 2.4) was folded away; a new 2.4 covers control types, risk, application security, and third-party risk |
| 3. Incident Response and Management | 20% | 24% | Now owns attack methodology frameworks (3.1); the process is a single seven-phase list (3.2) plus hands-on techniques (3.3) |
| 4. Reporting and Communication | 17% | 16% | Adds shift handover, internal threat intelligence reports, and SOC metrics such as true-positive rate and phishing click rate |

The test format is unchanged: a maximum of 85 questions, 165 minutes, and a passing score of 750 on a 100-900 scale. CompTIA recommends about four years of hands-on experience as a SOC or vulnerability analyst.

The practical reading of the weights: incident response gained four points and vulnerability management lost four. If your study plan was built on CS0-003, move time from scanner trivia to running an incident.

---

## 1.6 - AI in security operations

This is the only entirely new objective, and the one existing CySA+ material does not cover at all.

### Why it is on the exam

Security teams now use AI assistants to read logs, summarize incidents, explain obfuscated scripts, and draft reports. Used well, that saves hours per incident. Used carelessly, it leaks sensitive data to a third party, invents facts, or acts on instructions an attacker planted in the data. CS0-004 expects an analyst to use these tools and to know where they fail.

### The risks CompTIA names

- **Hallucinations.** A model produces plausible but false output: a MITRE technique ID that does not match the behavior, a CVE that does not exist, a confident conclusion the logs do not support. The control is verification: every AI-produced claim that drives a decision is checked against the evidence.
- **Data exposure.** Pasting logs, incident details, or customer data into an external AI service may send regulated or confidential data outside the organization, and may let the provider retain it. The control is an approved tool with contractual data protections, and data minimization before prompting.
- **Model poisoning.** If an attacker can influence the data a model learns from or retrieves, they can bias its output, for example teaching a detection model that their tool's behavior is normal. The control is protecting training and retrieval data like any other critical asset.
- **Malicious prompts.** Prompt injection hides instructions in content the model processes. An analyst asks an assistant to summarize a phishing email, and the email contains text telling the assistant to declare it safe. The control is to treat AI output on attacker-controlled input as untrusted, and never give an assistant authority to act on such content without review.

### Governance

AI use in the SOC falls under the same **legal and regulatory compliance** obligations as everything else (privacy law, sector rules, contractual data handling), and the organization needs an **AI usage policy** that says which tools are approved, what data may be entered, and who is accountable for AI-assisted decisions.

### Use cases CompTIA lists

Comparing artifacts (two versions of a script, two configuration files), analyzing log files, document creation (reports, playbooks), incident investigation, event correlation, and automation and orchestration.

### Worked scenario

At 3 a.m. an analyst finds a 400-line obfuscated PowerShell script on a server. Using the organization's approved AI assistant, she asks it to deobfuscate and explain the script. The assistant reports that it downloads a payload from a domain and creates a scheduled task. She verifies both claims: the domain appears in proxy logs, and the scheduled task exists in the host's event log. She then asks the assistant to draft the incident summary, edits it, and files it. What she did not do is paste the customer database extract the script touched into the assistant, or accept its statement that "no data was exfiltrated" without checking egress logs.

### How the exam tests this

Expect scenarios where the right answer uses AI to accelerate a task and keeps a human verification step, or where the risk to identify is data exposure (sensitive data sent to an unapproved tool) or prompt injection (attacker-controlled content steering the model). Answers that let AI output trigger containment or close incidents with no review are usually wrong.

---

## Security operations additions (1.1 to 1.5)

### Architecture concepts (1.1)

V4 widens the architecture list. Three groups deserve attention:

- **Critical infrastructure: operational technology (OT), industrial control systems (ICS), and SCADA.** These systems run physical processes. Availability and safety outrank confidentiality, devices often cannot be patched or run agents, and scanning can crash them. Monitoring is therefore passive (network sensors watching industrial protocols) and segmentation from IT networks is the primary control.
- **Identity infrastructure: IAM, privileged access management (PAM), authentication and authorization methods, and secrets management.** Secrets management means API keys, tokens, and passwords live in a vault and are fetched at runtime rather than stored in code or configuration. For an analyst, the indicator is a secret in the wrong place: a key in a public repository, or a vault access pattern that does not match the workload.
- **Logging concepts: ingestion, configuration, integrity and security, time synchronization, retention.** Log integrity (append-only storage, hashing, forwarding off the host) matters because attackers clear logs, which is itself an indicator.

### Indicators (1.2)

New or newly explicit indicators:

- **Identity-based:** IAM account compromise, unauthorized access, and **impossible travel** (sign-ins from two locations too far apart for the time between them). Impossible travel has false positives, such as VPN egress points and cloud proxies, so the analyst confirms with device, user agent, and MFA details.
- **Email-related:** **business email compromise (BEC)**, where an attacker uses a compromised or look-alike mailbox to redirect payments. The indicators are inbox rules that hide replies, changes to payment details, and sign-ins from new locations before the fraudulent request.
- **Social engineering:** **typosquatting** (look-alike domains) and **URL shorteners** that hide the real destination.
- **Host-related:** **Living Off the Land Binaries and Scripts (LOLBins)**, legitimate tools such as `certutil`, `mshta`, `rundll32`, or `wmic` used for malicious ends. They evade allow-listing because they are signed system binaries; the indicator is the parent process, command line, and network activity, not the binary's presence.
- **Cloud-related:** anomalous activity and **resource compromise**, such as unexpected compute instances mining cryptocurrency.

### Tools (1.3)

V4 names specific tools. You will not be asked to drive them, but you should know what each is for and recognize its output.

| Purpose | Tools named in CS0-004 |
|---------|------------------------|
| Decoding and parsing | CyberChef |
| Packet analysis | Wireshark, tcpdump, Snort, Suricata, Zeek |
| Threat intelligence platforms | Open Threat Exchange (OTX), MISP, OpenCTI |
| Endpoint | EDR and XDR, mobile device management (MDM) |
| Domain and IP reputation | WHOIS, AbuseIPDB, GEO-IP |
| File analysis | Strings, VirusTotal, YARA |
| Sandboxing | Joe Sandbox, Cuckoo Sandbox |
| Pattern recognition | Regular expressions, interpreting suspicious commands |
| Email analysis | MXToolbox |
| Behavior analytics | UEBA, OpenUBA |

V4 also lists **file formats** (JSON, XML, YAML, and Windows **EVTX** event logs) and **scripting languages** (Python, PowerShell, shell). Expect performance-based questions that show a JSON log record or a PowerShell command line and ask what it does. YARA deserves a minute: it is a rule language that matches files by strings and byte patterns, so a YARA rule written from one malware sample can find its siblings across a file share.

### Threat intelligence and hunting (1.4)

- **Heat maps** show where activity or detection coverage concentrates, for example ATT&CK techniques colored by how often you see them or how well you detect them.
- **The Pyramid of Pain** ranks indicators by how much it hurts the attacker when you block them: hash values (trivial to change) at the bottom, then IP addresses, domains, network and host artifacts, tools, and **TTPs** at the top. Detections built on behavior last longer than detections built on hashes.
- **Attribution** and **confidence-level impacts**: intelligence is weighed by **timeliness, relevance, and accuracy**. Stale, irrelevant, or unverified intelligence wastes analyst time.
- **IoC types:** **atomic** indicators stand alone (an IP, a hash); **behavioral** indicators describe activity patterns (a process spawning `cmd.exe` then making outbound connections).
- **Threat modeling with STRIDE**: spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege. Walk each category against a system's data flows to find what could go wrong.
- **Cyber deception**: honeypots, honey tokens, and canary credentials that no legitimate user touches, so any interaction is a high-fidelity alert.

### Efficiency and process improvement (1.5)

Mostly carried over, with **infrastructure as code (IaC)** named under automation, and **APIs, webhooks, and plug-ins** under tool integration. The exam point: automation that enriches and routes alerts frees analysts for judgment, and tuning rules (a data-enrichment item) reduces fatigue.

---

## Vulnerability management changes (2.1 to 2.4)

### Scanning (2.1)

Scan types are familiar (internal or external, agent or agentless, credentialed or not, passive or active), and V4 adds **discovery** (mapping scans, device fingerprinting) and **security baseline scanning** against PCI DSS, CIS Benchmarks, and the ISO 27000 series. A baseline scan answers "is this configured the way our standard says?", not "is this vulnerable to a CVE?". Planning considerations now explicitly include sensitivity levels, segmentation, and regulatory requirements.

### Tools (2.2)

New names to recognize:

- **Masscan** and **Angry IP Scanner**: fast network discovery; Masscan trades accuracy for speed across very large ranges.
- **Nuclei**: a template-driven scanner, good for checking many hosts for specific known issues quickly.
- **Cloud infrastructure assessment**: **ScoutSuite** and **Prowler** audit cloud account configuration; **Trivy** scans container images and infrastructure as code; **Checkov** scans IaC templates (Terraform, CloudFormation) before deployment.
- **Breach and attack simulation (BAS)**: **Atomic Red Team** (small tests mapped to ATT&CK techniques) and **MITRE Caldera** (automated adversary emulation). They test whether your *detections* fire, which a vulnerability scanner cannot.

### Prioritization (2.3)

Two additions matter. **EPSS** (Exploit Prediction Scoring System, from FIRST) estimates the probability that a vulnerability will be exploited in the next 30 days. CVSS says how bad exploitation would be; EPSS says how likely it is; known-exploited catalogs say it is already happening. Combine them with **asset value** and **context** (internal, external, isolated). V4 also lists **validation of remediation**: rescan or retest before you close the ticket.

### Control types, risk, and application security (2.4, new)

The CS0-003 objective that listed attacks to mitigate (XSS, overflows, injection, SSRF and so on) is no longer its own objective. You still need to recognize those vulnerabilities because scanner output in 2.2 reports them, but V4's 2.4 is about the management layer instead:

- **Control types** (administrative, technical, physical) and **control functions** (preventive, detective, responsive, corrective). A WAF rule is technical and preventive; a log review is administrative and detective.
- **Risk concepts:** **inherent risk** is risk before controls, **residual risk** is what remains after them, and **risk appetite** is how much the organization is willing to carry. Strategies are accept, transfer, avoid, and mitigate.
- **Policies, governance, and service-level objectives (SLOs)** such as "critical vulnerabilities on internet-facing systems remediated within 7 days".
- **Application security:** **SAST** reads source code without running it, **DAST** tests the running application from outside, and **OWASP SAMM** (Software Assurance Maturity Model) measures how mature a software security program is.
- **Third-party risk:** **supply chain**, **software composition analysis (SCA)**, which finds vulnerable open-source dependencies, and the **software bill of materials (SBOM)**, the ingredient list that lets you answer "are we using the vulnerable library?" in minutes when the next Log4Shell lands.

**Worked scenario:** a critical vulnerability is announced in a logging library. With SBOMs for every application, the team queries which builds include the affected version, finds three, and opens tickets within an hour. The SLO for critical issues on external systems is seven days; one application cannot be patched in time because the vendor has not released a fix, so the team applies a compensating WAF rule, records the residual risk, and gets the risk owner to accept it until the vendor patch arrives.

---

## Incident response changes (3.1 to 3.3)

- **3.1 moves attack methodology frameworks here:** the Cyber Kill Chain, the Diamond Model of Intrusion Analysis, and MITRE ATT&CK. Same content as before, now framed as incident analysis tools.
- **3.2 is a single process list:** preparation, detection, analysis, containment, eradication, recovery, post-incident. Note that detection and analysis are separate phases in CompTIA's list. NIST revised its incident response guidance in 2025 (SP 800-61 Revision 3) to align with the Cybersecurity Framework 2.0; CompTIA's phase names are the ones to use on the exam.
- **3.3 is the hands-on work**, and the list is long: developing the incident response and communication plans, creating playbooks, defining roles, training through **tabletop exercises and simulations**, log collection, correlation, **augmentation and enrichment**, triage, **establishing a timeline**, determining severity and impact, prioritization, evidence gathering with **chain of custody**, **data integrity validation** (hashing evidence), preservation and **legal hold**, isolating targets, escalation, remediation and verification, **release from isolation**, restoration, root cause analysis, and **corrective action development**.

Two items are easy to overlook. **Release from isolation** is a decision with criteria: the host is rebuilt or cleaned, the root cause is closed, and monitoring is in place; releasing early invites reinfection. **Corrective action development** turns root cause analysis into owned, dated changes; a lessons-learned meeting with no corrective actions has not finished the incident.

---

## Reporting and communication changes (4.1 and 4.2)

Vulnerability reporting (4.1) adds **risk scorecards** and **dependencies** among the inhibitors to remediation, alongside the familiar ones (business process interruption, degrading functionality, legacy and proprietary systems, contractual agreements, organizational governance, patch availability).

Security operations and incident reporting (4.2) adds:

- **Shift and incident handover**: a written state of each open incident (what is known, what is running, what is next) so the next shift does not restart from zero.
- **Internal threat intelligence reports** tailored to the organization: what attackers are doing to *you*, drawn from your own incidents and telemetry.
- **Metrics and KPIs**: alert volume, **false-positive rate**, **true-positive rate**, mean time to close, detect, respond, and remediate, and **phishing campaign click rate**. A falling false-positive rate means tuning is working; a falling click rate means awareness training is.

**How the exam tests reporting:** match the audience to the content. Executives get impact, risk, and trend in plain language; technical teams get indicators and remediation steps; regulators get what the law requires, on the law's timeline.

---

## Related

- [Notes 01: security operations](./01-security-operations.md)
- [Notes 02: vulnerability management](./02-vulnerability-management.md)
- [Notes 03: incident response](./03-incident-response.md)
- [Notes 04: reporting and communication](./04-reporting-communication.md)
- [Vulnerability management](../../../../learn/concepts/vulnerability-management.md) and [software supply chain security](../../../../learn/concepts/software-supply-chain-security.md) - concept pages behind 2.3 and 2.4
- [AI safety and security](https://ai.noblerworks.com/safety/) - the AI Zero to Hero pages on prompt injection and data exposure
