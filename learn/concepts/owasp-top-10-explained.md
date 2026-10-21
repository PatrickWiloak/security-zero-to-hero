---
last-updated: 2026-10-21
difficulty: intermediate
reading-time: 15 min
---

# OWASP Top 10 explained

> **15-minute read. Written for builders and defenders: what each risk is, why it happens, and how to prevent it. Helps to know basic HTTP.**

## The one-line answer

The OWASP Top 10 is a community-built list of the ten most important categories of web application security risk, refreshed every few years from real vulnerability data and practitioner surveys. It is not a standard or a checklist you can "pass". It is a shared vocabulary and a priority list: if your team prevents these ten categories well, you have removed most of the ways web applications actually get breached.

**[📖 OWASP Top 10](https://owasp.org/projects/top-ten)** - the project page, with the current edition and each category's full write-up

## Why it matters

OWASP (the Open Worldwide Application Security Project) is a non-profit. Its Top 10 is referenced by PCI DSS, by procurement questionnaires, by most application security tools and by nearly every security certification. When a pen test report, a scanner or an auditor says "A01", this is the list they mean.

This page follows the **2025 edition**. The 2021 edition is still widely referenced, and exams may use either, so the table below maps between them. Names and ordering can change between editions; always check the project page for the current list.

| 2025 | Category | Closest 2021 category |
|---|---|---|
| A01 | Broken Access Control | A01 (now also includes SSRF, 2021's A10) |
| A02 | Security Misconfiguration | A05 |
| A03 | Software Supply Chain Failures | Expanded from A06 Vulnerable and Outdated Components |
| A04 | Cryptographic Failures | A02 |
| A05 | Injection | A03 (includes cross-site scripting) |
| A06 | Insecure Design | A04 |
| A07 | Authentication Failures | A07 Identification and Authentication Failures |
| A08 | Software or Data Integrity Failures | A08 |
| A09 | Security Logging and Alerting Failures | A09 Security Logging and Monitoring Failures |
| A10 | Mishandling of Exceptional Conditions | New |

## The ten, from a defender's point of view

### A01 Broken Access Control

**What it is:** a user can do something they should not: see another customer's invoice by changing an ID in the URL, call an admin API without being an admin, or make the server fetch an internal URL on their behalf (server-side request forgery, SSRF).

**Why it happens:** authorization is business logic. Frameworks handle authentication for you, but only your code knows that invoice 1042 belongs to customer 77. Checks get missed on one endpoint out of a hundred.

**How to prevent it:**

- Deny by default; every endpoint requires an explicit authorization decision.
- Check ownership on the server for every object access, not just "is logged in".
- Centralise authorization in one module or policy engine instead of scattering `if` statements.
- For SSRF, allowlist the destinations the server may fetch, and block access to cloud metadata endpoints (use IMDSv2 on AWS).
- Write tests that try to access another user's resources and expect a 403 or 404.

### A02 Security Misconfiguration

**What it is:** the code is fine but the setup is not. Default credentials, debug mode in production, verbose error pages, directory listing, overly permissive CORS, a public storage bucket, missing security headers.

**How to prevent it:** build environments from code (infrastructure as code) so production is reviewed and repeatable; harden images against a baseline; turn off what you do not use; scan configuration continuously with posture management tools; keep development and production settings clearly separated.

### A03 Software Supply Chain Failures

**What it is:** your application is mostly other people's code. Risk comes from known-vulnerable dependencies, malicious or hijacked packages, compromised build systems and untrusted update channels.

**How to prevent it:** keep an inventory (SBOM), scan dependencies continuously, pin and verify versions, protect the CI pipeline like production, and verify signatures on what you deploy. The full story is in [Software supply chain security](./software-supply-chain-security.md).

### A04 Cryptographic Failures

**What it is:** sensitive data exposed because it was not encrypted, was encrypted badly, or keys were mishandled. Plain HTTP, weak TLS settings, MD5 for passwords, hardcoded keys, sensitive data in URLs or logs.

**How to prevent it:** classify data so you know what is sensitive; TLS everywhere with HSTS; encrypt sensitive data at rest with managed keys; hash passwords with Argon2id or bcrypt; use vetted libraries only. See [Encryption explained](./encryption-explained.md) and [Hashing and password storage](./hashing-and-password-storage.md).

### A05 Injection

**What it is:** untrusted input is interpreted as code or commands. SQL injection, OS command injection, LDAP injection, template injection, and cross-site scripting (XSS), where input ends up as script in another user's browser.

**Why it happens:** the application builds a query, command or page by concatenating strings that include user input, so the input can change the structure, not just the data.

**How to prevent it:**

- Use **parameterised queries** (prepared statements) or a safe ORM. The query structure is fixed and input is only ever data.
- Avoid shelling out; if you must, pass arguments as a list, never through a shell string.
- For XSS, use a framework that **escapes output by default** (React, Angular, modern templating engines), avoid raw HTML insertion, and add a Content Security Policy as a second layer.
- Validate input against an allowlist of expected formats, as defence in depth rather than the primary control.

```python
# Vulnerable: input becomes part of the SQL text
cursor.execute(f"SELECT * FROM orders WHERE id = '{order_id}'")

# Safe: the driver sends the value separately from the query
cursor.execute("SELECT * FROM orders WHERE id = %s", (order_id,))
```

**[📖 OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)** - parameterisation and the other defences in order of preference

### A06 Insecure Design

**What it is:** flaws in the design itself, which perfect code cannot fix. A password reset flow that trusts a guessable question; a checkout that lets you change the price in the request; no rate limit on a gift-card balance check.

**How to prevent it:** [threat model](./threat-modeling-explained.md) features before building them, write abuse cases alongside user stories, use secure design patterns and reference architectures, and limit resource consumption per user.

### A07 Authentication Failures

**What it is:** weaknesses in proving identity. Allowing credential stuffing and brute force, weak passwords, no MFA, session IDs in URLs, sessions that never expire or survive logout.

**How to prevent it:** use a proven identity provider or framework rather than custom login code; MFA, ideally [passkeys](./mfa-and-passkeys.md); rate limiting and breached-password checks; secure, `HttpOnly`, `SameSite` session cookies rotated at login and invalidated at logout.

### A08 Software or Data Integrity Failures

**What it is:** trusting code or data without checking it has not been tampered with. Auto-updates without signature checks, deserialising untrusted data into objects, CI pipelines that pull unverified plugins, or trusting client-side data for decisions.

**How to prevent it:** verify signatures on updates and artifacts; avoid native deserialisation of untrusted input (use simple formats like JSON with schema validation); review and restrict CI/CD permissions; keep integrity checks on critical data.

### A09 Security Logging and Alerting Failures

**What it is:** attacks happen and nobody notices. Logins, access-control failures and high-value transactions are not logged, logs are not monitored, or alerts go nowhere. Breach studies consistently show detection times measured in months.

**How to prevent it:** log security-relevant events with enough context (who, what, when, from where), protect logs from tampering, send them somewhere central, and alert on the events that matter. See [Logging and detection](./logging-and-detection.md).

### A10 Mishandling of Exceptional Conditions

**What it is:** the application behaves unsafely when something goes wrong: errors that reveal stack traces and internals, failures that "fail open" (an authorization service times out and the request is allowed), partially completed transactions that leave data inconsistent.

**How to prevent it:** fail closed on security decisions; catch errors and return generic messages while logging the detail internally; make multi-step operations transactional; test error paths, timeouts and resource exhaustion, not just the happy path.

## How teams use the list well

- **As training material.** Every developer on a web team should be able to explain these ten in their own words.
- **As a review prompt.** During design and code review, walk the list: "where could access control be missed here?"
- **Alongside the ASVS.** The OWASP Application Security Verification Standard turns the categories into testable requirements at three levels. Use it when you need a real checklist.
- **With automated tooling in CI.** Static analysis (SAST), dependency scanning (SCA), dynamic scanning (DAST) and secret scanning catch a share of these early, though access control and design flaws mostly need humans.

**[📖 OWASP Application Security Verification Standard](https://owasp.org/projects/asvs)** - testable security requirements for web apps

## Common mistakes

- **Treating the Top 10 as complete.** It is the top ten categories, not the only ten. Business logic flaws, race conditions and API-specific issues need attention too (OWASP also maintains an API Security Top 10).
- **Relying on a WAF to cover it.** A [WAF](./network-security-basics.md#web-application-firewalls) filters some injection patterns but cannot see broken access control or insecure design.
- **Scanning instead of designing.** Tools find a share of injection and misconfiguration. They rarely find authorization bugs.
- **Fixing instances, not classes.** Patching one injection point instead of moving the whole codebase to parameterised queries.

## How exams test this

- **Security+ and CySA+**: recognise each vulnerability type from a description or a log snippet (for example, a URL containing `' OR 1=1`), and pick the right mitigation: parameterised queries for SQL injection, output encoding for XSS, server-side authorization for IDOR.
- **CISSP and CSSLP-style questions**: secure development lifecycle, where in the lifecycle each defence belongs, and why design flaws cost the most to fix late.
- **Cloud security exams**: which managed service mitigates which category, such as a WAF with managed rules for injection, posture management for misconfiguration, and IMDSv2 for SSRF against instance metadata.
- **GitHub Advanced Security**: code scanning, dependency review and secret scanning mapped to these categories.

## Beyond web apps

LLM applications have their own list, the OWASP Top 10 for LLM Applications, covering prompt injection, insecure output handling, excessive agency and more. It lives on the AI Zero to Hero site: **[OWASP Top 10 for LLM applications](https://ai.noblerworks.com/safety/security/owasp-llm-top-10/)**.

## What to look at next

- **[Threat modeling explained](./threat-modeling-explained.md)** - find design flaws before they are code
- **[Software supply chain security](./software-supply-chain-security.md)** - the A03 category in depth
- **[Vulnerability management](./vulnerability-management.md)** - what to do when a scanner finds one of these
- **[GitHub Advanced Security](../../exams/github/advanced-security/)** - the certification for code, secret and dependency scanning
