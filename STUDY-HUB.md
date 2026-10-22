# 📚 Study Hub - Security Zero to Hero

> **Your navigation hub for every security certification on this site, plus the [Learn](./learn/) pillar for anyone learning security without an exam date.**

<!-- markdown="1" lets the documentation site render the markdown inside this
     centered block. GitHub ignores the attribute, so rendering there is unchanged. -->
<div align="center" markdown="1">

**Welcome. Whether you're new to security or chasing your CISSP, this is the entry point.**

**New to security? Start with [Security from Scratch](./learn/security-from-scratch.md)**, the plain-English path from zero to security engineer.

**[Browse it as a searchable site](README.md)** - full-text search across every page, which is faster than this index once you know what you are looking for.

</div>

---

## 🗺️ Table of Contents

- [Quick Navigation](#-quick-navigation)
- [Not chasing a certification?](#-not-chasing-a-certification)
- [Decision Tree: Find Your Cert](#-decision-tree-find-your-cert)
- [Study Tracks by Career Path](#-study-tracks-by-career-path)
- [Certifications by Provider](#-certifications-by-provider)
- [Most Popular Certifications](#-most-popular-certifications)
- [Study Timeline Estimates](#-study-timeline-estimates)
- [Resource Library](#-resource-library)
- [Cost Planning](#-cost-planning)

---

## 🎯 Quick Navigation

| I Want To... | Go To... |
|--------------|----------|
| 🚀 Learn security from zero, in order | [Security from Scratch](./learn/security-from-scratch.md) |
| 💡 Understand one idea (MFA, encryption, threat modeling) | [Concepts](./learn/concepts/) |
| 🗂️ Browse by topic across pillars | [Topic indexes](./topics/) |
| 🆕 Take my first security cert | [Entry level](#entry-level) |
| 🎯 Choose the right cert | [Decision Tree](#-decision-tree-find-your-cert) |
| 🚀 Follow a career path | [Study Tracks](#-study-tracks-by-career-path) |
| 📜 Prepare for an audit | [Compliance guides](./resources/compliance-guides/) |
| 📚 Browse all materials | [Resource Library](#-resource-library) |
| 📅 Per-cert last-verified dates | [Freshness ledger](./docs/freshness.md) |
| 🧪 Find the lab for my cert | [Labs by certification](./resources/hands-on-projects/labs-by-cert.md) |
| 🃏 Flashcards for a cert | `flashcards.csv` in each cert dir (Anki-importable) |
| 🤖 Secure AI apps and agents | [AI security on AI Zero to Hero](https://ai.noblerworks.com/safety/) |

---

## 🎓 Not chasing a certification?

The **[Learn](./learn/)** pillar is for everyone who wants to understand security without an exam date:

- **[Security from Scratch](./learn/security-from-scratch.md)** - seven phases from zero to security engineer, each ending with what you can now do.
- **[Concepts](./learn/concepts/)** - bite-size pages on identity and MFA, OAuth and OIDC, encryption and hashing, network, email and application security, cloud, container and Kubernetes security, DLP, threat modeling, risk management, vulnerability management, EDR, detection, incident response and ransomware resilience.
- **[Glossary](./learn/glossary.md)** - the vocabulary in plain English.
- **[Day One](https://cloud.noblerworks.com/learn/day-one/)** on Cloud Zero to Hero - terminal, git, HTTP, servers, if you are starting from absolute zero.

Come back when you decide to certify. Many do, after the Learn pillar shows them which direction they enjoy.

---

## 🌳 Decision Tree: Find Your Cert

```
What's your starting point?
│
├─ New to security
│  └─> ISC2 CC | CompTIA Security+ | Microsoft SC-900
│
├─ Some IT, dev or ops experience
│  ├─ Security operations (alerts, incidents) → CompTIA CySA+ | Microsoft SC-200
│  ├─ Identity and access                     → Microsoft SC-300
│  ├─ Data protection and compliance tooling  → Microsoft SC-401
│  ├─ Cloud security                          → CCSK v5 | GCP Cloud Security Engineer | IBM Cloud Security Engineer
│  └─ Secrets and access platforms            → HashiCorp Vault Associate | Boundary Associate
│
├─ Senior practitioner
│  ├─ Security leadership and architecture    → CISSP | Microsoft SC-100
│  ├─ Cloud security architecture             → CCSP
│  ├─ Audit and governance                    → ISACA CISA | CISM
│  └─ Offensive security                      → OSCP (PEN-200)
│
└─ Platform and product security
   ├─ Kubernetes                              → KCSA → CKS
   ├─ Code and supply chain                   → GitHub Advanced Security
   └─ Network security                        → Palo Alto PCNSA
```

AWS Security Specialty (SCS-C02) and Azure AZ-500 are retired; their guides stay as reference.

---

## 🚀 Study Tracks by Career Path

### Security Engineer (cloud) <a id="security-track"></a>
1. ISC2 CC *or* CompTIA Security+
2. CCSK v5 (vendor-neutral cloud security)
3. The security exam for your main cloud: GCP Cloud Security Engineer, or the Microsoft SC-series
4. CCSP, then CISSP as the capstone
5. Add: Kubernetes CKS, HashiCorp Vault Associate

### Security Operations (SOC) Analyst
1. CompTIA Security+
2. CompTIA CySA+ *or* Microsoft SC-200
3. Add: Palo Alto PCNSA for the network side

### Identity and Access
1. Microsoft SC-900
2. Microsoft SC-300
3. HashiCorp Boundary Associate *or* Vault Associate
4. Capstone: Microsoft SC-100

### Governance, Risk and Compliance (GRC)
1. ISC2 CC *or* CompTIA Security+
2. ISACA CISA (audit)
3. ISACA CISM (management)
4. Read alongside: the [compliance guides](./resources/compliance-guides/)

### Offensive Security
1. CompTIA Security+
2. OSCP (PEN-200)

### DevSecOps and Platform Security
1. CompTIA Security+ *or* KCSA
2. GitHub Advanced Security
3. Kubernetes CKS
4. HashiCorp Vault Associate

---

## 📋 Certifications by Provider

<!-- BEGIN GENERATED: provider-table - edit .github/scripts/build-provider-indexes.py, not this block -->

| Provider | Certs | Highlights | Browse |
|----------|------:|------------|--------|
| **CompTIA** | 2 | Security+ (SY0-701), CySA+ (CS0-004) | [exams/comptia/](./exams/comptia/) |
| **ISC2** | 3 | CC (entry level), CISSP, CCSP | [exams/isc2/](./exams/isc2/) |
| **ISACA** | 2 | CISA (audit), CISM (management) | [exams/isaca/](./exams/isaca/) |
| **Offensive Security** | 1 | OSCP (PEN-200), hands-on penetration testing | [exams/offensive-security/](./exams/offensive-security/) |
| **Cloud Security Alliance** | 1 | CCSK v5, vendor-neutral cloud security | [exams/cloud-security-alliance/](./exams/cloud-security-alliance/) |
| **AWS** | 1 | Security Specialty (SCS-C02, retired; kept as reference) | [exams/aws/](./exams/aws/) |
| **Azure** | 6 | SC-900, SC-200, SC-300, SC-401, SC-100, AZ-500 (retired; kept as reference) | [exams/azure/](./exams/azure/) |
| **GCP** | 1 | Professional Cloud Security Engineer | [exams/gcp/](./exams/gcp/) |
| **IBM Cloud** | 1 | Cloud Security Engineer | [exams/ibm/](./exams/ibm/) |
| **Kubernetes/CNCF** | 2 | KCSA, CKS | [exams/kubernetes/](./exams/kubernetes/) |
| **HashiCorp** | 2 | Vault Associate, Boundary Associate | [exams/hashicorp/](./exams/hashicorp/) |
| **GitHub** | 1 | Advanced Security (GHAS) | [exams/github/](./exams/github/) |
| **Palo Alto Networks** | 1 | PCNSA | [exams/palo-alto-networks/](./exams/palo-alto-networks/) |
| **CERTIFICATIONS TOTAL** | **24** | across 13 providers | |

The Certs column counts real exams.

<!-- END GENERATED: provider-table -->

---

## 🔥 Most Popular Certifications

Common picks in security job listings:

1. [CompTIA Security+ (SY0-701)](./exams/comptia/security-plus/) - the common first security cert
2. [CISSP](./exams/isc2/cissp/) - the senior security standard
3. [ISC2 CC](./exams/isc2/cc/) - entry level, no prerequisites
4. [CompTIA CySA+](./exams/comptia/cysa-plus/) - security operations
5. [CCSP](./exams/isc2/ccsp/) - cloud security professional
6. [CISM](./exams/isaca/cism/) - security management
7. [CISA](./exams/isaca/cisa/) - audit
8. [Microsoft SC-200](./exams/azure/sc-200/) - security operations on Microsoft
9. [CKS](./exams/kubernetes/cks/) - Kubernetes security
10. [OSCP](./exams/offensive-security/oscp-pen-200/) - penetration testing

---

## ⏱️ Study Timeline Estimates

| Cert Tier | Typical Prep Time | Daily Study | Examples |
|-----------|-------------------|-------------|----------|
| **Entry level** | 2-6 weeks | 1-2 hr | ISC2 CC, SC-900, Security+ |
| **Associate** | 6-10 weeks | 2-3 hr | CySA+, SC-200, SC-300, Vault Associate |
| **Professional** | 10-16 weeks | 2-4 hr | GCP Cloud Security Engineer, CCSK, CKS |
| **Security capstone** | 12-26 weeks | 2-4 hr | CISSP (16wk), CCSP (10wk), CISM |

### Entry level
First-cert path with no security background:
1. Work through [Security from Scratch](./learn/security-from-scratch.md), Phases 0 to 3
2. Take ISC2 CC, Security+ or SC-900
3. Build the [zero trust project](./resources/hands-on-projects/implement-zero-trust.md)
4. Pick a lane from Phase 7 of the path

---

## 📚 Resource Library

### Learn
[Security from Scratch](./learn/security-from-scratch.md) · [Concepts](./learn/concepts/) · [Glossary](./learn/glossary.md) · [Topic indexes](./topics/)

### Service Comparisons
[Security tools](./resources/service-comparison-security-tools.md) · [Identity and IAM](./resources/service-comparison-identity-iam.md)

### Architecture and Hands-on
[Zero trust architecture](./resources/architecture-patterns/zero-trust-architecture.md) · [Centralized logging and SIEM](./resources/architecture-patterns/centralized-security-logging-siem.md) · [Zero trust access for internal apps](./resources/architecture-patterns/zero-trust-access-internal-apps.md) · [Secrets and PKI platform](./resources/architecture-patterns/secrets-and-pki-platform.md) · [SOC detection and response](./resources/architecture-patterns/soc-detection-and-response-pipeline.md) · [Implement zero trust](./resources/hands-on-projects/implement-zero-trust.md) · [Centralized logging and alerting](./resources/hands-on-projects/centralized-logging-and-alerting.md) · [Harden a Linux server](./resources/hands-on-projects/harden-a-linux-server.md)

### Breach Case Studies
[Capital One 2019](./resources/case-study-capital-one-2019.md) · [SolarWinds 2020](./resources/case-study-solarwinds-2020.md) · [Log4Shell 2021](./resources/case-study-log4shell-2021.md) · [MOVEit 2023](./resources/case-study-moveit-2023.md)

### Career
[Security Engineer roadmap](./resources/certification-roadmap-security-engineer.md) · [Security engineer interview prep](./resources/interview-prep/security-engineer-interview.md) · [Cloud security in 1 hour](./resources/playlist-cloud-security-1hour.md)

### Compliance
SOC 2, ISO 27001, NIST CSF, HIPAA, PCI DSS, GDPR, FedRAMP, NIS2, DORA, CMMC - [resources/compliance-guides/](./resources/compliance-guides/). AI frameworks are on the AI site: [AI safety and governance](https://ai.noblerworks.com/safety/).

### Practice & Strategy
- [Practice Question Banks](./resources/practice-questions/) - scenario questions with explained answers, one bank per certification
- [Practice Resources Guide](./resources/practice-resources.md)
- [Study Strategies](./resources/study-strategies.md)
- [Exam Day Checklist](./resources/exam-day-checklist.md)
- [Budget Study Plan](./resources/budget-study-plan.md)
- [Community Resources](./resources/community-resources.md)

### On the sibling sites
Cloud fundamentals, CLI cheat sheets and architecture patterns: [Cloud Zero to Hero](https://cloud.noblerworks.com/) · Databases and pipelines: [Data Zero to Hero](https://data.noblerworks.com/) · LLMs, agents and AI security: [AI Zero to Hero](https://ai.noblerworks.com/)

---

## 💰 Cost Planning

| Item | Typical Cost |
|------|-------------:|
| **All study materials in this repo** | Free |
| **Official documentation** | Free |
| **Free tier sandbox accounts** | Free |
| **Video course (optional)** | $15-50 |
| **Third-party practice tests (optional)** | $15-30 |
| **Exam fee (per cert)** | $100-700 |
| **CISSP/CCSP exam fee** | $749/$599 |
| **Total per Security capstone** | $700-900 |

See the [budget study plan](./resources/budget-study-plan.md) for detailed cost-minimization strategies.

---

## 🤝 Community

- **Reddit:** r/cybersecurity, r/CompTIA, r/cissp, r/AzureCertification
- **Discord:** Security study servers (links in [community-resources.md](./resources/community-resources.md))
- **LinkedIn:** Search for "[Cert name] Study Group"
- **GitHub:** Star this repo and watch for updates

---

## 📝 How to Use This Hub

1. Start at [Decision Tree](#-decision-tree-find-your-cert) to identify your cert
2. Open that cert's directory: `exams/<provider>/<cert>/`
3. Read in order: `README.md` → `fact-sheet.md` → `practice-plan.md` → `notes/` → `scenarios.md` → `strategy.md`
4. Cross-reference with the [Resource Library](#-resource-library)
5. Take practice exams when consistently scoring 80%+ on practice questions
6. Schedule the real exam when you hit 85%+ twice in a row

---

<div align="center" markdown="1">

**Ready to start? [Security from Scratch](./learn/security-from-scratch.md) · [CompTIA](./exams/comptia/) · [ISC2](./exams/isc2/) · [ISACA](./exams/isaca/) · [Azure security](./exams/azure/)**

*Maintained by [Patrick Wiloak](https://patricklukewilson.com) - Star this repo if it helps you pass.*

</div>
