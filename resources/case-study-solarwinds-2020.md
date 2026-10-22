---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 15 min
---

# Case Study: SolarWinds Orion, 2020

> A state intelligence service broke into SolarWinds' build environment and planted a backdoor in signed updates of the Orion network management product. Up to about 18,000 customers installed the tainted updates, and the intruders then chose a much smaller set of high-value targets, including US federal agencies, for follow-on intrusions. This page covers the public record, the root causes, and the controls that reduce the risk of a build-system compromise. It is written for defenders; it contains no attack instructions.

---

## Why this case matters

Most security advice assumes the software you install from a trusted vendor, signed with the vendor's real key, is safe. SolarWinds broke that assumption. The malicious code was not in the vendor's source repository; it was inserted during the build, so it shipped inside a legitimately signed product through the vendor's normal update channel. Customers who did everything right (installed vendor updates promptly, verified signatures) were the ones who received it.

The case changed policy as much as practice. It fed directly into US Executive Order 14028 (May 2021), the NIST Secure Software Development Framework's adoption for federal suppliers, the push for software bills of materials, and supply chain frameworks such as SLSA.

---

## What happened (public record)

- **The intrusion at SolarWinds.** SolarWinds later reported that the earliest suspicious activity in its environment was in **September 2019**, and that the intruders injected test code into an Orion release in **October 2019** to check that their method worked. The US Government Accountability Office (GAO) reported that the threat actor had breached SolarWinds' networks as early as **January 2019**.
- **The build implant.** CrowdStrike, working with SolarWinds, described a tool it named **SUNSPOT** that ran on the build server, watched for the Orion product being compiled, and swapped in a modified source file only for the duration of the build. The source code in version control stayed clean, and the build completed normally, so neither code review nor build failures would reveal it.
- **The backdoor.** The resulting backdoor, named **SUNBURST** by FireEye, shipped in Orion Platform releases distributed from **March to June 2020** (versions 2019.4 HF 5, 2020.2 with no hotfix, and 2020.2 HF 1). It was signed with SolarWinds' legitimate code-signing certificate. SolarWinds' SEC filing said fewer than **18,000** customers may have installed an affected version.
- **Selective follow-on.** SUNBURST stayed dormant for up to two weeks after installation, then contacted infrastructure that let the operators decide which victims were worth pursuing. Only a small fraction of installs received second-stage tools. In the targets they chose, the intruders moved into identity systems, including on-premises federation servers and cloud tenants, to read email and documents.
- **Discovery.** FireEye (now part of Google as Mandiant) found that it had been breached and on **8 December 2020** disclosed the theft of its red team tools. Its investigation traced the intrusion to the Orion update, and on **13 December 2020** FireEye and SolarWinds disclosed the supply chain compromise. FireEye's CEO later told Congress the first clue was an alert that an employee's account had registered a second device for multi-factor authentication, which the employee had not done.
- **Government response.** On **13 December 2020** CISA issued **Emergency Directive 21-01**, ordering federal civilian agencies to disconnect or power down affected Orion products immediately. CISA's alert **AA20-352A** on 17 December noted that the same actor had used other initial access vectors as well, so removing Orion was not enough on its own.
- **Attribution.** On **15 April 2021** the US government formally attributed the campaign to Russia's Foreign Intelligence Service (SVR), also tracked as APT29.
- **Aftermath.** The SEC sued SolarWinds and its CISO in October 2023 over security disclosures. A federal court dismissed most of the claims in July 2024, and in November 2025 the SEC and the defendants filed a joint stipulation to dismiss the remaining case.

**[📖 CISA Emergency Directive 21-01](https://www.cisa.gov/emergency-directive-21-01)** - the federal order to disconnect Orion and its supplemental guidance.
**[📖 CISA alert AA20-352A](https://www.cisa.gov/news-events/cybersecurity-advisories/aa20-352a)** - technical details, other access vectors and mitigations.
**[📖 GAO-22-104746, Federal Response to SolarWinds and Microsoft Exchange Incidents](https://www.gao.gov/products/gao-22-104746)** - the GAO review of the incident and the federal response.
**[📖 SolarWinds Form 8-K, 17 December 2020](https://www.sec.gov/Archives/edgar/data/1739942/000162828020017620/swi-20201217.htm)** - the company's filing on affected versions and customer counts.

---

## Root causes

### 1. The build system was a trusted, long-lived, internet-reachable environment

The build server held everything an attacker needed: the source tree at compile time and a pipeline that fed straight into code signing and distribution. It was a persistent machine on the corporate network, so an intruder who reached it could stay for months. A build environment is as sensitive as a production database of customer secrets, but it is often run like a developer workstation.

### 2. Nothing compared what was built against what was written

Code review protected the source repository. Code signing protected the artifact after the build. The gap between them, the compilation itself, was trusted implicitly. No independent build was checking that the same source produced the same binary.

### 3. Signing proved origin, not integrity of the process

The Orion updates were signed by SolarWinds. Signature verification at customers confirmed the updates came from SolarWinds, which was true. A signature tells you who released something, not that the process that produced it was clean.

### 4. Network management tools had wide reach and broad egress

Orion, like most network monitoring tools, needs credentials and network reach across much of an estate. Many customers also let the Orion server talk to the internet freely. A management tool with domain-wide credentials and open outbound internet is an ideal beachhead.

### 5. Identity infrastructure was the real target

In chosen victims, the intruders went after identity: federation servers' token-signing keys, privileged cloud accounts, and application credentials that could read mail. Once an attacker can mint authentication tokens, network controls stop mattering. Detection of identity-plane abuse was weak across much of the industry at the time.

### 6. Long dwell time

The intruders were inside SolarWinds for most of a year and inside some customers for months. Many organizations did not have logs going back far enough to scope their own exposure.

---

## What would have stopped or detected it

No single control prevents a well-resourced state actor. The aim is to make each step harder and more visible.

### At the software producer (if you build and ship software)

| Weakness | Control |
|---|---|
| Persistent build server | **Ephemeral, isolated build environments**: each build runs on a fresh, short-lived worker with no interactive access, destroyed afterwards. This is a core SLSA build requirement. |
| Build process trusted implicitly | **Reproducible or parallel builds**: build the same source in independent environments and compare outputs before signing. SolarWinds' own post-incident Next-Generation Build System uses parallel builds in three separate environments. |
| No record of how an artifact was made | **Signed build provenance**: the build platform, not the build script, generates a signed attestation of which source, which builder and which inputs produced the artifact (SLSA provenance, in-toto attestations, Sigstore). |
| Signing key reachable from the build | **Signing in a separate, hardened service** with HSM-held keys, releasing a signature only for artifacts with valid provenance. |
| Weak access to build systems | Phishing-resistant MFA, least privilege and just-in-time access for anyone who can change build definitions or runners. |
| No assurance framework | Follow the **NIST Secure Software Development Framework (SP 800-218)**, which became the basis for US federal supplier attestations. |

**[📖 SLSA framework](https://slsa.dev/)** - supply chain levels for software artifacts, including build isolation and provenance.
**[📖 NIST SP 800-218, Secure Software Development Framework](https://csrc.nist.gov/pubs/sp/800/218/final)** - the practices federal software suppliers attest to.

### At the software consumer (everyone)

| Weakness | Control |
|---|---|
| Management tools with open egress | **Restrict outbound traffic** from management and monitoring servers to the specific vendor endpoints they need. Unexpected outbound DNS and HTTPS from these servers is a strong signal. |
| Management tools with domain-wide rights | **Least privilege for service accounts** used by monitoring tools; separate credentials per segment; no domain admin. |
| Identity was the real target | Protect token-signing keys (move federation to a cloud identity provider or protect AD FS keys in HSMs), require phishing-resistant MFA for admins, monitor for new credentials added to applications and service principals, and alert on new MFA device registrations. |
| Third-party risk invisible | Inventory third-party software with privileged access, ask suppliers for SSDF attestations and SBOMs, and include supplier compromise in incident response plans. |
| Short log retention | Keep identity, DNS and network logs for at least a year, as covered in the [centralized logging pattern](./architecture-patterns/centralized-security-logging-siem.md). |

The detection that worked at FireEye is worth dwelling on. An alert for "user registered a new MFA device" is low-severity on its own and fires often. FireEye followed it up, confirmed with the employee, and found an intruder. Identity events like this are cheap to collect and easy to verify with the user.

---

## Lessons for detection engineering

The SOC lessons from SolarWinds are about baselines and identity:

- **Baseline your management servers.** Monitoring and IT management tools have very regular behaviour. A new outbound destination from the Orion server was an anomaly against a stable baseline.
- **Watch the identity plane.** New credentials on service principals, new federation trusts, token-signing certificate changes and new MFA devices should all be alerts routed to someone who will verify them.
- **Assume the vendor channel can be hostile.** Treat updates to privileged third-party tools as changes that warrant monitoring, especially in the days after installation.
- **Hunt with intel quickly.** When CISA and vendors published indicators, organizations with searchable historical logs could answer "were we affected?" in hours. Those without could not answer at all.

See the [SOC detection and response pipeline pattern](./architecture-patterns/soc-detection-and-response-pipeline.md) for how to turn these into tested detections.

---

## Defender's checklist

**If you produce software:**

- [ ] Builds run on ephemeral, isolated workers with no standing interactive access
- [ ] Build definitions and runner configuration changes require review and are logged
- [ ] Build provenance generated and signed by the build platform for every release artifact
- [ ] Critical artifacts reproduced or built in parallel and compared before signing
- [ ] Signing keys held in an HSM-backed service separate from the build environment
- [ ] SSDF practices mapped and attestation ready for customers who ask
- [ ] SBOM published with each release

**If you consume software (everyone):**

- [ ] Inventory of third-party tools with privileged access to your network or identity systems
- [ ] Outbound traffic from management servers limited to required vendor endpoints
- [ ] Monitoring tool service accounts scoped to least privilege
- [ ] Phishing-resistant MFA for all administrators
- [ ] Alerts on new MFA devices, new credentials on applications and service principals, and federation configuration changes
- [ ] Token-signing keys protected and monitored
- [ ] At least one year of searchable identity, DNS and network logs
- [ ] A playbook for "a trusted vendor's update was malicious": isolate, scope, rotate credentials the tool held

---

## Cert mapping

| Cert | What this case tests |
|---|---|
| [CISSP](../exams/isc2/cissp/) | Supply chain risk management, secure software development, security operations |
| [CCSP](../exams/isc2/ccsp/) | Cloud application security, identity federation risk |
| [CySA+](../exams/comptia/cysa-plus/) | Threat intelligence, indicators of compromise, anomaly detection |
| [GitHub Advanced Security](../exams/github/advanced-security/) | Supply chain security features, dependency and artifact integrity |
| [CISM](../exams/isaca/cism/) | Third-party risk, incident management, board reporting |

---

## Discussion questions

1. Your code is reviewed and your releases are signed. Write down every step between the merge and the signature. Which of those steps could change the output without anyone seeing it?
2. What would it take for your organization to detect a trusted management tool contacting a new external domain?
3. If a vendor told you tomorrow that its last three updates were malicious, which credentials would you need to rotate, and how long would that take?
4. Why did attribution and the Emergency Directive focus on identity systems as much as on the Orion software itself?
5. Which SLSA build level could you realistically reach in the next six months, and what is the first change?

---

## Related

- [Software supply chain security](../learn/concepts/software-supply-chain-security.md) - the concept page
- [Threat modeling explained](../learn/concepts/threat-modeling-explained.md) - modelling your build pipeline as a system
- [Incident response basics](../learn/concepts/incident-response-basics.md)
- [Secrets and PKI platform](./architecture-patterns/secrets-and-pki-platform.md) - protecting signing keys
- [SOC detection and response pipeline](./architecture-patterns/soc-detection-and-response-pipeline.md)
- Other case studies: [Capital One 2019](./case-study-capital-one-2019.md), [Log4Shell 2021](./case-study-log4shell-2021.md), [MOVEit 2023](./case-study-moveit-2023.md), [Snowflake customers 2024](./case-study-snowflake-customer-breaches-2024.md)
