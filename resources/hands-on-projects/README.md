---
last-updated: 2026-10-21
---

# Hands-on projects

Security is learned by doing. These guided builds are all defensive: each one leaves you with a system that is harder to break into and easier to watch, with inline commands you can run in a free-tier account or a throwaway VM. If you are new, start with **[Harden a Linux server](./harden-a-linux-server.md)**.

| Build | Time | What you'll have at the end |
|---|---|---|
| [Harden a Linux server](./harden-a-linux-server.md) | 2-3 hours | An Ubuntu server with key-only SSH, default-deny firewall, automatic patching and audit logging, measured with Lynis |
| [Centralized logging and alerting](./centralized-logging-and-alerting.md) | 3-4 hours | Cloud audit logs in a locked archive, managed threat detection and five tested email alerts (AWS, with Azure and GCP equivalents) |
| [Implement zero-trust security](./implement-zero-trust.md) | 4-5 hours | Identity-aware access, phishing-resistant MFA, no-implicit-trust networking on AWS, Azure and GCP |

Each phase of [Security from Scratch](../../learn/security-from-scratch.md) also ends with a small "Try it" exercise you can do in under an hour.

## Builds on the sibling sites

Most security work happens on top of a real system, so these builds from the other Zero to Hero sites make good practice targets. Build one, then harden it:

- [Deploy a 3-tier app](https://cloud.noblerworks.com/resources/hands-on-projects/deploy-3-tier-app/) (Cloud Zero to Hero) - then lock down its network paths and IAM roles
- [Build a CI/CD pipeline](https://cloud.noblerworks.com/resources/hands-on-projects/build-ci-cd-pipeline/) (Cloud Zero to Hero) - then add secret scanning and dependency checks
- [Set up a monitoring stack](https://cloud.noblerworks.com/resources/hands-on-projects/setup-monitoring-stack/) (Cloud Zero to Hero) - then alert on suspicious logins
- [Build a RAG pipeline](https://ai.noblerworks.com/build/projects/build-rag-pipeline/) (AI Zero to Hero) - then try to break it with [prompt injection](https://ai.noblerworks.com/safety/security/prompt-injection-explained/)

## Related

- [Concepts](../../learn/concepts/) - the "why" behind each pattern
- [Architecture patterns](../architecture-patterns/) - reference designs each build follows
- [Topic indexes](../../topics/) - all four pillars per subject
- [Labs by certification](./labs-by-cert.md) - which build backs which exam

## Which lab for which cert

Each lab maps to the certs it exercises. The reverse index lives in [labs-by-cert.md](./labs-by-cert.md).

<!-- BEGIN GENERATED: lab-cert-map - run .github/scripts/build-lab-map.py -->

| Lab | Certs it supports |
|------|-------------------|
| [Hands-On Project: Centralized Logging and Alerting](./centralized-logging-and-alerting.md) | [CS0-004](../../exams/comptia/cysa-plus/), [SC-200](../../exams/azure/sc-200/), [SCS-C02](../../exams/aws/specialty/security-scs-c02/), [Google Cloud Professional Cloud Security Engineer Certification](../../exams/gcp/cloud-security-engineer/) |
| [Hands-On Project: Harden a Linux Server](./harden-a-linux-server.md) | [SY0-701](../../exams/comptia/security-plus/), [CS0-004](../../exams/comptia/cysa-plus/), [CKS](../../exams/kubernetes/cks/) |
| [Hands-On Project: Implement Zero Trust Security](./implement-zero-trust.md) | [CCSK v5 - Certificate of Cloud Security Knowledge](../../exams/cloud-security-alliance/ccsk/), [AZ-500](../../exams/azure/az-500/), [SCS-C02](../../exams/aws/specialty/security-scs-c02/), [Google Cloud Professional Cloud Security Engineer Certification](../../exams/gcp/cloud-security-engineer/), [CKS](../../exams/kubernetes/cks/) |

<!-- END GENERATED: lab-cert-map -->
