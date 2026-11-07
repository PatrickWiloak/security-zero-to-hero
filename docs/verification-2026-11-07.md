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

## Cert guides pass

Scope: the eight cert guides added on 2026-11-07 (SSCP, SCS-C03, SecurityX, Google Security Operations Engineer, AIGP, AAISM, AAIA, TAISE), their practice banks and Key terms flashcard lines. Counts are claim clusters (V verified / W wrong / U unverifiable).

| Guide | Logistics V/W/U | Bank (checked / wrong keys / distractor or explanation fixes) | Notes claims V/W/U |
|---|---|---|---|
| ISC2 SSCP | 12/0/0 | 28 / 0 / 0 | ~40/0/0 |
| AWS SCS-C03 | 14/0/0 | 29 / 0 / 7 | ~70/1/2 |
| CompTIA SecurityX | 12/0/3 | 27 / 0 / 2 | ~60/0/3 |
| GCP Security Operations Engineer | 8/0/1 | 28 / 0 / 10 | ~40/0/2 |
| IAPP AIGP | 14/0/3 | 24 / 0 / 1 | 38/1/4 |
| ISACA AAISM | 16/1/3 | 26 / 0 / 0 | 38/0/3 |
| ISACA AAIA | 12/1/2 | 28 / 0 / 1 | ~41/0/4 |
| CSA TAISE | 10/0/2 | 30 / 0 / 0 | ~29/0/1 |

No keyed answer was wrong in any bank. Most bank fixes were distractors pasted from other questions or explanations that named options that no longer exist.

### Fixes

| Page | Old | New | Source |
|---|---|---|---|
| scs-c03/notes/04 | Cross-account access needs caller identity policy "except where the resource policy names the principal" | Both resource policy and caller identity policy must allow; shortcut is same-account only | https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic-cross-account.html |
| scs-c03/notes/04 | "unused-access findings do not vary by Region" | Removed (external access analyzer is Regional) | https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-create-external.html |
| scs-c03/notes/01 + flashcards | Security Hub only sees findings after enablement | Per-Region enablement; troubleshooting cause is "not enabled in that Region" | https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html |
| scs-c03/notes/02 + flashcards | Quarantine SG "denies all inbound and outbound" | SGs only allow: use one with no rules; tracked connections can persist | https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-connection-tracking.html |
| scs-c03 bank Q7, 12, 17, 18, 24, 25, 26 | Defensible tabletop distractor, stale option references, off-topic distractors | Rewritten; Q18 states 90-day unused-access default; Q25 notes `logs:Unmask` | AWS docs above |
| securityx bank Q15, Q17 | Off-topic distractors | On-topic wrong options | n/a |
| gcp-secops bank Q13, 17, 18, 20, 23-28 | Pasted distractors | Rewritten, lengths balanced | n/a |
| gcp-secops fact-sheet, README | Original-guide weights only | Callout: Exam Guide 2.0 (PDF dated 2026-11-06) weights 13/20/18/20/18/11 and new topics; which guide the live exam follows is not confirmed | https://services.google.com/fh/files/misc/professional_security_operations_engineer_exam_guide_2.0_english.pdf |
| gcp-secops notes/04 | Reference lists "being replaced" by data tables | Adds legacy retirement July 2027 | https://docs.cloud.google.com/chronicle/docs/reference/reference-lists |
| gcp-secops notes/03, 04, 05 | Citations that did not state the claim (retrohunt of curated detections, Pending Actions widget, toxic combinations) | Cite unified rules, playbook actions and toxic-combinations pages | docs.cloud.google.com/chronicle and /security-command-center |
| aigp/notes/02 | Timetable proposals "discussed" | Regulation (EU) 2026/1744 (Digital Omnibus on AI) in force 27 Jul 2026, moves Annex III to 2 Dec 2027, Annex I to 2 Aug 2028 | https://eur-lex.europa.eu/eli/reg/2026/1744/oj |
| aigp/notes/02 | Art 113 chapter list vague | Exact chapters, Art 78, Art 101 exception, 1 Aug 2024 entry into force | https://eur-lex.europa.eu/eli/reg/2024/1689/oj |
| aigp bank Q3 | Retailer "under its own brand name" (made it a provider) | "inside its app"; explanation covers Art 25 | EU AI Act Art 3, 25 |
| aaism + aaia (README, fact-sheet, notes, bank, practice-plan) | Outline "June 2025" | Undated current outline (date not shown by ISACA) | https://www.isaca.org/credentialing/aaism/aaism-exam-content-outline |
| aaism + aaia fact-sheet, flashcards | "10 CPE hours a year in AI" | "10 CPE a year (30 over 3 years)" | https://www.isaca.org/credentialing/aaia/maintain-aaia-certification |
| aaism fact-sheet | Active CISM/CISSP checked at maintenance | Marked not verified | same |
| aaia fact-sheet, flashcards | Remote proctoring barred in India, Mainland China, Hong Kong | Marked not verified | candidate guide (no such text) |
| aaia bank Q3 | Explanation named "floor area" (not an option) | Names the actual options | n/a |
| taise fact-sheet | Languages not stated | Self-paced English only; instructor-led may vary; "Associate" level label marked not verified | https://cloudsecurityalliance.org/education/taise |
| taise notes/01 | EO 14110 quoted as current | Adds "(since rescinded in January 2025)" - from general knowledge, not fetched | none fetched |

### Remaining unverifiable

- SecurityX price, validity/CEU and delivery (not on CompTIA's page; marked). SecurityX Sigma/YARA/STIX/TAXII/ISAC/CASB descriptions are standard practice, unsourced.
- Google SecOps: which exam guide the live exam follows (original vs 2.0), exam code, passing score and validity (not published); custom-detector IOC template; the YARA-L `options` section.
- AIGP: price, delivery, languages; South Korea AI Basic Law; ISO 22989 and 42005; OECD and ISO 42001 category summaries (not re-read). The Regulation (EU) 2026/1744 details come from the subagent's EUR-Lex fetch; spot-check.
- AAISM/AAIA: outline date; remote-proctoring country list; TAISE level label, certificate validity and prep-kit contents.
- NIST AI RMF subcategory wording in the AAISM notes is from recall.
