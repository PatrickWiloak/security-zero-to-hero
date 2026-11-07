---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
---

# 04 - Security operations

**Domain 4: Security Operations (22%)** - CAS-005. Sections follow CompTIA's published objectives summary.

Operations is where the design meets an adversary. The exam asks you to read data, decide what it means, and choose a proportionate response.

---

## Monitoring and data analysis

**SIEM** platforms collect, normalise, correlate and alert on events from many sources. At this level you are expected to tune and troubleshoot them:

- **Event parsing** turns raw logs into fields. Bad parsing makes good rules silently useless, so test every new source with sample events and watch for fields that come through empty.
- **Retention** must meet legal, regulatory and investigative needs: hot storage for recent searches, cheaper tiers for long retention, and integrity protection so logs can serve as evidence.
- **False positives** (alerts for benign activity) waste analyst time and teach people to ignore the console; **false negatives** (missed attacks) are the dangerous kind. Tune with allow-lists, context and severity weighting, and measure both rates.
- **Aggregate analysis** looks across sources and time rather than at single events: a failed login, a success from a new country, then a mailbox rule is a story that no single log shows.
- **Behavior baselines** describe normal activity per user, host or service so that deviations stand out. User and entity behaviour analytics builds on them. Baselines must be refreshed, or they become stale and noisy.

Example of a rule-based detection written as a Sigma rule, a vendor-neutral format that can be converted to a SIEM's query language:

```yaml
title: PowerShell with encoded command
status: experimental
logsource:
  product: windows
  category: process_creation
detection:
  selection:
    Image|endswith: '\powershell.exe'
    CommandLine|contains: '-EncodedCommand'
  condition: selection
level: medium
```

Encoded commands have legitimate uses, so a rule like this is a lead, not proof; it needs context such as the parent process and the user.

## Vulnerabilities and attack surface

Know the classic weaknesses and their fixes, because questions give a symptom and ask for the control:

| Weakness | What it is | Primary mitigation |
|---|---|---|
| Injection (SQL, command, LDAP) | Untrusted input interpreted as code | Input validation, parameterised queries, least-privilege accounts |
| Cross-site scripting (XSS) | Attacker script runs in a victim's browser | Output encoding, content security policy, input validation |
| Insecure configuration | Defaults, open services, verbose errors | Hardening baselines, configuration monitoring |
| Outdated software | Known flaws left unpatched | Patch management, software inventory, virtual patching |
| Weak ciphers | Obsolete algorithms or protocol versions | Disable them, enforce current TLS, test with scanners |

Layer the mitigations (**defense in depth**): validation at the edge, a WAF in front, secure code behind, encryption of data and monitoring across. Where you cannot patch, compensate: isolate, restrict access, add monitoring and apply a virtual patch at a gateway.

## Threat hunting and threat intelligence

**Threat hunting** is proactive: assume an adversary is already present, form a hypothesis (for example "an attacker uses scheduled tasks for persistence"), search the data for evidence, and convert findings into detections. It differs from alert triage, which reacts to something the tools flagged.

- **Internal intelligence** comes from your own environment: **honeypots** and honeytokens (decoys that should never be touched, so any access is a high-fidelity signal) and **user behaviour analytics**.
- **External intelligence** comes from outside: **OSINT**, dark web monitoring, vendor feeds and **ISACs** (information sharing and analysis centers, which share sector-specific threat information among members).
- **Threat intelligence platforms** ingest, deduplicate, score and distribute indicators. Sharing standards such as STIX (the format) and TAXII (the transport) let tools exchange indicators of compromise automatically. MITRE ATT&CK, a knowledge base of adversary tactics and techniques from real-world observations, is the common language for mapping hunts and detections.
- **Rule-based detection languages** let you write portable detections: Sigma for logs, YARA for files and memory, and Snort or Suricata rules for network traffic.

A small YARA rule, to read the syntax:

```
rule Example_Packed_Downloader
{
    meta:
        description = "Illustrative rule: MZ header plus a suspicious command string"
    strings:
        $mz  = { 4D 5A }
        $cmd = "cmd.exe /c" ascii nocase
    condition:
        $mz at 0 and $cmd
}
```

Indicators age quickly. Prefer detections on adversary behaviour (techniques) over brittle indicators such as IP addresses and file hashes, and record the confidence and source of each.

## Incident response

Follow the established life cycle: preparation, detection and analysis, containment, eradication, recovery and lessons learned. At this level the analysis techniques are the focus.

**Malware analysis** has static and dynamic approaches. Static analysis examines the file without running it (hashes, strings, headers, imports). Dynamic analysis runs it in a **sandbox** and observes behaviour: files, registry, processes, network. **Indicator of compromise (IoC) extraction** collects the observables (domains, hashes, mutexes, persistence locations) to hunt across the estate. **Code stylometry** compares coding style and structure to attribute samples to the same author or toolkit, with caution because styles can be copied. **Reverse engineering** disassembles or decompiles a binary to understand its logic, for example how it communicates and what it encrypts. Handle samples in an isolated lab, because malware may detect analysis environments or call home.

**Metadata analysis** extracts context from files and communications: document properties, email headers, image metadata, file system timestamps and network flow records. It can show origin, authorship, timeline and path without examining content. **Data recovery** restores deleted or damaged data from backups, snapshots or forensic carving, and must preserve evidence integrity: work on copies, hash the originals, document chain of custody.

**Root cause analysis** asks why, not only what: how the adversary got in, what control failed, and what change prevents recurrence. Techniques include timeline reconstruction, the five whys and attack path mapping to the ATT&CK matrix. The output is a corrected control, not a blame list; feed it back into architecture (notes 02) and engineering (notes 03).

Evidence rules still apply: order of volatility (memory first), forensic copies, hash verification, chain of custody and, where litigation is possible, legal hold and counsel.

---

## Key terms

- **Event parsing** - converting raw log lines into structured fields so rules can use them
- **Behavior baseline** - a record of normal activity per user, host or service used to detect deviations
- **User and entity behavior analytics** - analysis of behaviour against baselines to detect anomalies
- **Sigma** - a vendor-neutral rule format for describing log-based detections
- **YARA** - a rule language for identifying malware in files and memory by patterns
- **Honeypot** - a decoy system that no legitimate user should touch, so any access is a strong signal
- **ISAC** - an information sharing and analysis center that shares sector-specific threat information
- **Threat hunting** - proactive searching of data for adversary activity based on a hypothesis
- **Threat intelligence platform** - a system that ingests, scores and distributes threat indicators
- **STIX** - a standard format for describing cyber threat information
- **TAXII** - a transport protocol for sharing threat information between systems
- **Indicator of compromise** - an observable artefact, such as a domain or hash, that suggests a system has been compromised
- **Sandbox** - an isolated environment where suspicious files are run and observed
- **Code stylometry** - comparing coding style and structure to link malware samples to a common author or toolkit
- **Metadata analysis** - extracting context such as timestamps, headers and properties from files and communications
- **Root cause analysis** - determining why an incident was possible and which change prevents recurrence

---

## Related

- [Notes 03: security engineering](./03-security-engineering.md)
- [Detection and response topic](../../../../topics/detection-and-response.md)
- [Cloud incident response tabletop](../../../../resources/hands-on-projects/cloud-incident-response-tabletop.md)
- **[📖 MITRE ATT&CK](https://attack.mitre.org/)** - tactics and techniques for mapping hunts and detections
- **[📖 CompTIA SecurityX](https://www.comptia.org/en-us/certifications/securityx/)** - the objectives summary for this domain
- **[📖 NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final)** - incident response within CSF 2.0 (April 2025)
