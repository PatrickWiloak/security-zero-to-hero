---
last-updated: 2026-11-07
difficulty: n/a
---

# Content gaps and improvement plan (2026-11-07)

A gap review of security.noblerworks.com, done by listing the tree with `git ls-files` and searching it with
`git grep`. A topic is called missing only when the search found nothing (or one passing mention).
The open items are tracked in `TODO.md` under "Content gaps (2026-11-07 review)".

## Where the site stands

| Area | Has | Compared with the cloud site |
|---|---|---|
| Concept pages | 27 | Good breadth on fundamentals |
| Topic indexes | 2 (security, IAM) | Cloud has 7 |
| Hands-on projects | 3 + lab map | Least-privilege, IR and SBOM labs still open |
| Interview guides | 1 | Cloud has 4, data has 5 |
| Roadmaps | 1 (security engineer) | Cloud has 7 |
| Troubleshooting / incident playbooks | 0 | Cloud has 4, data has 3 |
| Compliance guides | 10 | The site's strength |
| Case studies | 5 | Good |
| Cert guides | 24, all over 9,000 words | 4 have no flashcard deck |

The thinnest part of the site is the **job-ready layer**. A reader can learn the concepts and pass an exam,
but the site does not yet help them with the job itself: running a phishing triage, answering a SOC
interview, or picking between a GRC and an AppSec career.

## Plan, in order

### Wave 1 - the job-ready layer (largest gap)

1. **Incident response playbooks** (new `resources/playbooks/`, defensive runbooks only): leaked cloud
   access key, phishing report triage, suspicious OAuth app grant, ransomware first hour, lost or stolen
   laptop, exposed S3 bucket or public storage. Each one has detect, contain, eradicate, recover and
   lessons-learned steps, with links to the concept pages.
2. **Career roadmaps** beside the security engineer one: SOC analyst, GRC analyst, AppSec engineer,
   cloud security engineer. Each maps to the certs already on the site.
3. **Interview guides** beside the security engineer one: SOC analyst, GRC / audit, AppSec, cloud security.

### Wave 2 - concept pages with no coverage

- **OWASP API Security Top 10** (no hits; the web Top 10 has a page).
- **Secure SDLC and DevSecOps** (one passing mention): SAST, DAST, SCA, where each runs in CI.
- **Security headers and CSP** (no hits).
- **MITRE ATT&CK for defenders**: it is mentioned in 6 pages but has no page of its own explaining how to
  read and use the matrix for detection coverage.
- **Digital forensics basics** and **threat intelligence basics** (both mentioned, neither explained).
- **Privacy engineering basics** (data minimisation, PII inventory, DSARs), which links to the GDPR guide.

### Wave 3 - topic indexes and labs (already in TODO, kept here so the plan is complete)

- Topic indexes: detection and response, governance and compliance, application security.
- Defensive labs: least-privilege IAM, cloud incident response, container scan with SBOM.

### Wave 4 - compliance and case studies

- Compliance guides: SOX ITGCs (no hits), US state privacy (CCPA/CPRA, one passing mention), CIS Controls v8,
  NIST SP 800-53, EU Cyber Resilience Act (one mention, obligations start 2026-2027), SEC cyber
  disclosure rule.
- Case studies: Change Healthcare 2024, MGM Resorts 2023 (help-desk social engineering), Colonial Pipeline
  2021. None is covered. Write each from primary sources (company filings, CISA, DOJ, congressional testimony)
  as the existing five are.

### Wave 5 - certs (already in TODO)

- PenTest+, SecurityX, SSCP, CyberOps Associate, GSEC, GCLD, Google Security Operations Engineer, and the AI
  governance certs (AIGP, AAISM, AAIA, TAISE). Verify each code on the vendor page first.
- Flashcard decks for az-500, gcp/cloud-security-engineer, hashicorp/boundary-associate, hashicorp/vault-associate.
- **CEH stays out of scope for Claude**: the safety check stopped it three times. Patrick's drafts are in
  `~/.cache/ceh-draft-2026-09-29/`.

## How to do each item

Every new page uses the house style in `CLAUDE.md`: vendor or primary-source citations, the frontmatter
convention, Mermaid diagrams, and `check-readme-counts.py --fix` in the same commit. Playbooks stay
defensive: what to check, contain and report, with no attack steps.
