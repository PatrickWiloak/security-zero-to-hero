---
last-updated: 2026-11-07
---

# Fact verification pass, 2026-11-07

Scope: the 36 content pages added on 2026-11-07 plus the Key terms of the GCP Cloud Security Engineer and Vault Associate flashcard decks. Claims were checked against fetched primary sources. WRONG claims were fixed; UNVERIFIABLE claims were left where already marked or are mild general practice. Counts are claim clusters, approximate.

## Per-page counts (verified / wrong / unverifiable)

| Page | V | W | U |
|---|---|---|---|
| compliance-guides/sox-itgc | 8 | 0 | 2 |
| compliance-guides/us-state-privacy-laws | 24 | 2 | 4 |
| compliance-guides/eu-cyber-resilience-act | 17 | 2 | 1 |
| compliance-guides/sec-cyber-disclosure-rule | 16 | 0 | 1 |
| compliance-guides/nist-sp-800-53 | 6 | 0 | 1 |
| compliance-guides/cis-controls-v8 | 8 | 0 | 0 |
| case-study-change-healthcare-2024 | 22 | 1 | 1 |
| case-study-colonial-pipeline-2021 | 17 | 0 | 0 |
| case-study-mgm-resorts-2023 | 20 | 1 | 1 |
| playbooks/README | 5 | 0 | 0 |
| playbooks/leaked-cloud-access-key | 11 | 1 | 1 |
| playbooks/phishing-report-triage | 9 | 0 | 0 |
| playbooks/suspicious-oauth-app-grant | 8 | 1 | 0 |
| playbooks/ransomware-first-hour | 10 | 1 | 1 |
| playbooks/lost-or-stolen-laptop | 8 | 0 | 0 |
| playbooks/publicly-exposed-storage-bucket | 9 | 0 | 0 |
| interview-prep/appsec-interview | 9 | 1 | 0 |
| interview-prep/cloud-security-interview | 12 | 0 | 0 |
| interview-prep/grc-audit-interview | 12 | 0 | 0 |
| interview-prep/soc-analyst-interview | 10 | 1 | 0 |
| topics/application-security | 3 | 0 | 0 |
| topics/detection-and-response | 3 | 0 | 0 |
| topics/governance-and-compliance | 2 | 0 | 0 |
| concepts/digital-forensics-basics | 12 | 0 | 1 |
| concepts/mitre-attack-for-defenders | 8 | 0 | 0 |
| concepts/owasp-api-security-top-10-explained | 11 | 1 | 0 |
| concepts/privacy-engineering-basics | 8 | 0 | 0 |
| concepts/secure-sdlc-and-devsecops | 6 | 2 | 0 |
| concepts/security-headers-and-csp | 17 | 1 | 0 |
| concepts/threat-intelligence-basics | 8 | 1 | 0 |
| 4 certification roadmaps | 7+ | 0 | 0 |
| hands-on: container-image-scan-with-sbom | 12 | 0 | 0 (flags from Syft/Grype README knowledge, not re-fetched) |
| hands-on: least-privilege-iam-review | 14 | 0 | 0 |
| hands-on: cloud-incident-response-tabletop | 3 | 0 | 0 |
| Flashcard Key terms: GCP Cloud Security Engineer | 13 | 2 | 0 |
| Flashcard Key terms: Vault Associate | 28 | 3 | 0 |

## Fixes

Paths under `resources/` unless noted.

| Page | Old | New | Source |
|---|---|---|---|
| compliance-guides/eu-cyber-resilience-act | Class II route "Third-party assessment" | Modules B+C, module H, or certification scheme at least "substantial" (Art. 32(3)) | https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:L_202402847 |
| compliance-guides/eu-cyber-resilience-act | Critical route "Third-party assessment, and possibly a certification" | European certification scheme where Art. 8(1) applies, else Class II routes (Art. 32(4)) | same |
| compliance-guides/eu-cyber-resilience-act | Caveat: summarized from Article 32 headings | Routes read from Art. 32(2) to (4) | same |
| compliance-guides/us-state-privacy-laws | Breach damages "up to $750 per consumer per incident" | "Up to $750 per incident", check Civil Code 1798.150 | https://oag.ca.gov/privacy/ccpa |
| compliance-guides/us-state-privacy-laws | DROP "launch announced January 2026" | DROP shown live on CPPA site; 26 Jan 2026 move to privacy.ca.gov kept | https://cppa.ca.gov/announcements/ |
| compliance-guides/us-state-privacy-laws | Connecticut amendments 1 July 2026 only | Also a 2026 amendment effective 1 Oct 2026 (marked unverified) | https://privacyworld.blog/2026/08/adding-to-the-count-the-latest-in-state-consumer-privacy-laws/ |
| compliance-guides/nist-sp-800-53 | FISMA basis "unverified here" | Developed under FISMA, 44 U.S.C. 3551 et seq., voluntary for nongovernmental organizations | https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf |
| compliance-guides/nist-sp-800-53 | "17 of 20 families" unflagged | Flagged as not re-checked | same |
| case-study-change-healthcare-2024 | Restore order pharmacy, claims, payments | Pharmacy first; testimony lists pharmacy, provider payments, claims | Witty testimony 1 May 2024 (House Energy and Commerce) |
| case-study-mgm-resorts-2023 | "first public filings used Regulation FD items" | MGM Items 7.01 and 2.02/7.01; Caesars Item 8.01 | https://www.sec.gov (EDGAR 0001193125-23-233855, 0001193125-23-251667) |
| interview-prep/appsec-interview | 2021 top-five order | 2025 top five (access control, misconfiguration, supply chain failures, cryptographic failures, injection) | https://owasp.org/Top10/2025/ |
| playbooks/suspicious-oauth-app-grant | "its tokens stop working" | "no new tokens are issued" | https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/disable-user-sign-in-portal |
| interview-prep/soc-analyst-interview | Lifecycle stated as NIST's | Attributed to SP 800-61 Rev. 2; Rev. 3 (2025) uses CSF 2.0 functions | https://csrc.nist.gov/pubs/sp/800/61/r3/final |
| playbooks/leaked-cloud-access-key | "scraped within minutes" | "found quickly" (no source for minutes) | none found |
| playbooks/ransomware-first-hour | "memory holds evidence, such as keys" | "memory holds evidence" | https://www.cisa.gov/stopransomware/ransomware-guide |
| concepts/owasp-api-security-top-10-explained | Four authorization risks | Three (API1, API3, API5) | https://api-security.owasp.org/editions/2023/en/0x11-t10 |
| concepts/secure-sdlc-and-devsecops | OWASP guideline "secret scanning" under pre-commit (2 places) | "secrets management" | https://owasp.github.io/www-project-devsecops-guideline/latest |
| concepts/threat-intelligence-basics | NIST definition paraphrase | SP 800-150 wording | https://csrc.nist.gov/pubs/sp/800/150/final |
| concepts/security-headers-and-csp | MDN "replaces X-Frame-Options" | "'none' is similar to X-Frame-Options: deny" | https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy/frame-ancestors |
| exams/gcp/cloud-security-engineer/notes/identity-and-access-management.md | Google-managed SA example App Engine default | Service agents (App Engine default is user-managed) | https://cloud.google.com/iam/docs/service-account-types |
| same | Org policy "inherit and merge down" | Inherited; child can override or merge | https://cloud.google.com/resource-manager/docs/organization-policy/understanding-hierarchy |
| exams/hashicorp/vault-associate/notes/01-vault-architecture.md | Shamir splits "master key" (2 places) | "unseal key" | https://developer.hashicorp.com/vault/docs/concepts/seal |
| same | Root key reconstructed from unseal keys, never stored | Stored encrypted by the unseal key alongside data | same |
| same | Sealed: "only a health check is available" | Only unseal and status operations | same |

## Remaining unverifiable

- PCAOB AS 2201 wording (pcaobus.org blocks bots); claim that inspections repeatedly flag ITGC testing.
- State laws: Alabama HB 351, Louisiana SB 386, Oklahoma SB 546 (law-firm or tracker sources only); Oregon opt-out/cure dates; Colorado 2025 amendments; Sidley and RadarFirst counts; CCPA threshold inflation adjustment.
- Whether any SEC proposal amends Item 1.05/106; CRA single reporting platform status; "17 of 20 NIST families".
- Change Healthcare 192.7M (HHS page 403); MGM page note on two DOJ Scattered Spider releases.
- Forensics: sealed-evidence and two-copies practice (generic, unsourced); SSDF PO/PS/PW/RV groups not on the csrc page; FIRST TLP 2.0 labels not fetched (CISA matches).
- Roadmaps: SY0-701/SY0-801 and CS0-004 codes and dates, SCS-C02 retirement date 1 Dec 2025, CISM outline date 2026-11-03 rest on repo guides only.
- Playbooks: AWS compromised-access page description; "many groups steal data first".
- GCP flashcard fixes and Syft/Grype flags were checked from documentation knowledge, not fetched this session; spot-check.
- Capital One case study (outside scope) says SSRF is its own 2021 category; 2025 list folds it into access control.
