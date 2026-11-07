---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 18 min
---

# 03 - Security engineering

**Domain 3: Security Engineering (31%)** - CAS-005. The largest domain, covering automation, vulnerability management and cryptography. Sections follow CompTIA's published objectives summary.

Engineering is turning the architecture into working, repeatable control. The exam expects you to read short scripts and rules and to know which cryptographic tool fits which job.

---

## Automation

Anything done by hand more than twice should be a script, an event trigger or a workflow. Reasons: speed (response in seconds), consistency (the same step every time) and auditability (the script is the record).

**Scripting.** Know what each language is for. **PowerShell** administers Windows and Microsoft cloud services with object pipelines. **Bash** glues Unix tools. **Python** handles APIs, parsing and analysis. Typical tasks: pulling logs, checking certificate expiry, rotating keys and enriching alerts. A certificate expiry check in Python:

```python
import socket
import ssl
from datetime import datetime, timezone

def days_until_expiry(host: str, port: int = 443) -> int:
    context = ssl.create_default_context()
    with socket.create_connection((host, port), timeout=5) as sock:
        with context.wrap_socket(sock, server_hostname=host) as tls:
            cert = tls.getpeercert()
    expires = datetime.fromtimestamp(ssl.cert_time_to_seconds(cert["notAfter"]), tz=timezone.utc)
    return (expires - datetime.now(timezone.utc)).days

print(days_until_expiry("example.com"))
```

The same task in PowerShell, for certificates in the local machine store:

```powershell
Get-ChildItem Cert:\LocalMachine\My |
  Where-Object { $_.NotAfter -lt (Get-Date).AddDays(30) } |
  Select-Object Subject, NotAfter
```

**Event triggers and cloud APIs.** Run code in response to events (a new storage object, a security finding) with serverless functions or event buses, and call cloud APIs to change state. **Infrastructure as code** keeps environments declarative; scan it before deploy. **Containerization** packages tools so they run identically anywhere. **Automated patching** applies updates by ring (test, pilot, broad) with rollback.

**SOAR (security orchestration, automation and response)** connects tools and runs playbooks: enrich an alert, check reputation, isolate a host, open a ticket. Automate high-volume, low-risk, high-confidence actions first and keep a human approval step for disruptive ones, since a wrong automated action can cause the outage the attacker wanted. **Generative AI** can summarise alerts, draft detection rules and explain scripts, but its output is untrusted input: verify it, never give it unreviewed write access, and guard against prompt injection when it reads attacker-controlled text.

## Vulnerability management

The cycle is: discover assets, scan, prioritise, remediate or mitigate, verify, report. Scans may be **credentialed** (log in, accurate) or **uncredentialed** (the attacker's view), network-based, agent-based or application-focused (static, dynamic, software composition analysis).

**SCAP** (Security Content Automation Protocol) is a suite of interoperable NIST specifications for expressing, exchanging and processing security configuration and vulnerability information; the current version is SCAP 1.4. Its components include:

- **XCCDF** (Extensible Configuration Checklist Description Format): checklists and benchmarks.
- **OVAL** (Open Vulnerability and Assessment Language): machine-readable tests for vulnerabilities and configuration state.
- **CPE** (Common Platform Enumeration): names for products and platforms.
- **CCE** (Common Configuration Enumeration): identifiers for configuration items.
- **CVE** (Common Vulnerabilities and Exposures) identifies a specific vulnerability; **CVSS** scores it.

**CVSS** is a published standard that captures a vulnerability's main characteristics and produces a numerical severity score, translated into low, medium, high and critical levels; the current version is CVSS v4.0. Severity is not risk. Prioritise by exploitability (is it being exploited?), exposure (internet facing?), asset criticality and available compensating controls. Report by risk to the business, track time to remediate against agreed service levels, and record accepted risk with an owner and review date.

## Advanced cryptography

**Post-quantum cryptography (PQC).** A large quantum computer would break public key algorithms based on factoring and discrete logarithms (RSA, Diffie-Hellman, elliptic curves). NIST published its principal PQC standards in August 2024: FIPS 203 (ML-KEM, a module-lattice-based key-encapsulation mechanism), FIPS 204 (ML-DSA, a module-lattice-based signature standard) and FIPS 205 (SLH-DSA, a stateless hash-based signature standard). NIST says these can and should be put into use now, and has selected HQC as a further key-encapsulation mechanism for standardization. The threat is "harvest now, decrypt later": adversaries store encrypted traffic today. Plan with an inventory of where public key cryptography is used, **crypto-agility** so algorithms can be swapped, and hybrid deployments that combine classical and post-quantum algorithms during transition.

**Key stretching** makes password guessing slow by applying a deliberately expensive function (PBKDF2, bcrypt, scrypt, Argon2) many times with a unique salt. **Homomorphic encryption** allows computation on encrypted data without decrypting it, for privacy-preserving analytics, at a large performance cost. **Forward secrecy** uses ephemeral key exchange so that compromising a long-term key later does not expose past sessions. **Hardware acceleration** (AES instructions in CPUs, HSMs, TPMs, secure enclaves) provides speed and keeps keys out of general memory.

## Cryptographic use cases

Cover data in all three states: **at rest** (disk, database, object and field-level encryption), **in transit** (TLS, IPsec, SSH, mutual TLS) and **in use** (confidential computing, trusted execution environments). Further cases: **secure email** (S/MIME, PGP), **blockchain** (hashing and signatures for tamper-evident ledgers), **privacy** (pseudonymisation, differential privacy), **compliance** (algorithms and key lengths dictated by regulation) and **certificate-based authentication** (mutual TLS, smart cards, device certificates in place of passwords).

## Cryptographic techniques

- **Tokenization** replaces sensitive data with a surrogate token, with the real value stored in a protected vault. It removes systems from compliance scope (for example payment card data) because tokens are useless if stolen.
- **Code signing** proves who published code and that it was not altered; protect signing keys in HSMs and timestamp signatures.
- **Cryptographic erase** destroys the key to render encrypted data unrecoverable, essential where physical sanitisation is impossible.
- **Digital signatures** give integrity, authentication and non-repudiation using a private key.
- **Hashing** gives integrity; **symmetric** cryptography is fast for bulk data; **asymmetric** cryptography handles key exchange and signatures. Real protocols combine them.

---

## Key terms

- **SOAR** - security orchestration, automation and response: connecting tools and automating playbooks
- **Playbook** - a defined sequence of automated and manual steps for responding to a type of event
- **SCAP** - the Security Content Automation Protocol, NIST specifications for exchanging security configuration and vulnerability information
- **XCCDF** - the Extensible Configuration Checklist Description Format used for security checklists and benchmarks
- **OVAL** - the Open Vulnerability and Assessment Language for machine-readable system state tests
- **CPE** - Common Platform Enumeration, a naming scheme for products and platforms
- **CVE** - Common Vulnerabilities and Exposures, identifiers for specific publicly known vulnerabilities
- **CVSS** - the Common Vulnerability Scoring System, a standard for rating vulnerability severity numerically
- **Credentialed scan** - a vulnerability scan that authenticates to the target and sees configuration and patch state directly
- **ML-KEM** - the NIST module-lattice-based key-encapsulation mechanism standardised in FIPS 203
- **ML-DSA** - the NIST module-lattice-based digital signature standard in FIPS 204
- **SLH-DSA** - the NIST stateless hash-based digital signature standard in FIPS 205
- **Harvest now, decrypt later** - collecting encrypted data today to decrypt it when quantum computers are available
- **Crypto-agility** - the ability to replace cryptographic algorithms without redesigning the system
- **Key stretching** - using a deliberately slow, salted function to make password guessing expensive
- **Homomorphic encryption** - encryption that permits computation on data without decrypting it
- **Forward secrecy** - a property of ephemeral key exchange in which later key compromise does not expose past sessions
- **Tokenization** - replacing sensitive data with a surrogate token while the real value is held in a secure vault
- **Code signing** - signing software with a private key so users can verify its publisher and integrity

---

## Related

- [Notes 02: security architecture](./02-security-architecture.md)
- [Notes 04: security operations](./04-security-operations.md)
- [TLS and HTTPS](../../../../learn/concepts/tls-and-https.md)
- **[📖 NIST Security Content Automation Protocol](https://csrc.nist.gov/projects/security-content-automation-protocol)** - SCAP 1.4 and its component specifications
- **[📖 FIRST CVSS](https://www.first.org/cvss/)** - the CVSS standard, currently v4.0
- **[📖 NIST post-quantum cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography)** - FIPS 203, 204 and 205 and HQC
- **[📖 NIST FIPS 203: ML-KEM](https://csrc.nist.gov/pubs/fips/203/final)** - the key-encapsulation standard (August 2024)
