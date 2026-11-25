---
last-updated: 2026-11-25
difficulty: n/a
---

# Content gaps and improvement plan (2026-11-25)

**Scope:** security.noblerworks.com, the whole tree at `main` on 2026-11-25 (`2a2d8da`), plus the two pages
waiting in `drafts/`.

**Method:** a Gemini (Antigravity CLI) audit was the starting list, treated as leads only. Every figure was
re-measured with `git ls-files` and `git grep` (never a filesystem walk), and every exam date and code was
checked on the vendor page on 2026-11-25. A topic is called a gap only when the search found nothing, or
found it only as a passing mention, and the evidence is given beside it. Anything a page already covers is
listed as not a gap, so the content-gaps loop does not queue it.

The earlier plan is [content-gaps-2026-11-07.md](content-gaps-2026-11-07.md). Open items are tracked in
`TODO.md` under "Content gaps". Dated freshness work (fact-sheet re-verification, exam outline changes) lives
in [freshness.md](freshness.md) and the "Exam changes" part of `TODO.md`, and is not repeated here.

## Gemini claims checked

24 claims: **14 confirmed, 5 overstated, 5 false.**

| # | Claim | Verdict | Measured figure (2026-11-25) |
|---|---|---|---|
| 1 | No `learn/day-one/` on-ramp; cloud has 15, ai 7, data 7 | confirmed | 0 here. Cloud 15 pages + README, ai 7, data 6 pages + README |
| 2 | The six suggested day-one topics are not covered | overstated | The ideas are covered by concept pages (TLS, CVSS, MFA and passkeys, SPF/DKIM/DMARC). Only the hands-on walk-throughs are missing; see Wave 2 |
| 3 | Two drafts unpublished | confirmed | `drafts/learn/concepts/red-team-vs-penetration-test-vs-purple-team.md`, `drafts/resources/playbooks/business-email-compromise.md`; verdicts below |
| 4 | Logging and Linux hardening labs not run end to end | confirmed | Neither has a "How this was run" section; the other three run labs do. TODO line dated 2026-11-08 is overdue |
| 5 | 8 fact-sheets stamped 2026-05-03 | confirmed | Exactly GCP PCSE, GHAS, Boundary, Vault, IBM, KCSA, OSCP, PCNSA. Already a TODO (2026-12-15) |
| 6 | Boundary unverified; only active cert with no `flashcards.csv` | confirmed | HashiCorp's certification list shows 3 Terraform and 2 Vault exams, no Boundary. AZ-500 also has no deck, but it is retired |
| 7 | PCNSA possibly retired or renamed | confirmed | Not on Palo Alto's certification page; "Network Security Analyst" is listed. Retirement on 2025-01-31 is reported only in community sources |
| 8 | IBM Cloud Security Engineer metadata unverified | confirmed | IBM's C1000-173 page renders no exam text to a fetch; code still unconfirmed |
| 9 | AIGP, AAISM, AAIA, TAISE metadata unverified | confirmed | Matches the four open TODO lines; not re-fetched in this pass |
| 10 | Thin notes under 5,000 words (az-500 2.3k, pcnsa 3.9k, sc-401 4.0k, aaism 4.1k, aaia 4.1k, taise 4.3k, kcsa 4.8k) | overstated | Figures exact (2,341 / 3,907 / 4,068 / 4,097 / 4,132 / 4,342 / 4,844). Word count alone is not a gap: no outline objective was shown to be missing, and az-500 is retired |
| 11 | 21 of 32 certs have no lab | confirmed | 11 of 32 in `labs-by-cert.md`. Also: labs are tagged to the retired SCS-C02, so the live SCS-C03 has none (Wave 3) |
| 12 | CISM 2026 outline transition | confirmed | Effective 2026-11-03; repo already has 18/20/33/29. ISACA's outline page now lists 42 supporting tasks, which unblocks the TODO reconcile item |
| 13 | CySA+ CS0-003 retires December 2026 | confirmed | V3 English retires 2026-12-22, translations 2027-03-23 (comptia.org). Repo already says this |
| 14 | Security+ SY0-801 in January 2027 | **false** | V8 is already the recommended version (the repo records launch 2026-11-17); V7 English retires 2027-06-11, translations 2027-08-13. January 2027 is only the repo's own rebuild target |
| 15 | CISSP new outline April 2027 | confirmed | Effective 2027-04-15 (isc2.org) |
| 16 | AZ-500 to SC-500 | confirmed | AZ-500 retired 2026-08-31. SC-500 (Cloud and AI Security Engineer Associate) has a live Microsoft Learn page with Pearson VUE scheduling. Microsoft does not call it the replacement on that page |
| 17 | Only 2 service comparisons | confirmed | `service-comparison-identity-iam.md`, `service-comparison-security-tools.md` |
| 18 | No SIEM/XDR comparison | overstated | No SIEM section in the comparison, but `architecture-patterns/centralized-security-logging-siem.md` has a per-cloud SIEM table and `endpoint-security-edr-xdr.md` covers XDR |
| 19 | No CNAPP/CSPM comparison | **false** | `service-comparison-security-tools.md` "Security Posture Management" table (Security Hub, Defender CSPM, SCC Premium); concept page `cspm-and-cnapp-explained.md` |
| 20 | No secrets management comparison | **false** | `service-comparison-security-tools.md` "AWS Secrets Manager vs Azure Key Vault vs Secret Manager", plus KMS and certificate tables |
| 21 | No workload identity page (SPIFFE/SPIRE, OIDC federation) | **false** | `secrets-management.md` "Workload identity: the level worth reaching"; `oauth-and-oidc-explained.md` covers GitHub OIDC federation; `secrets-and-pki-platform.md` covers SPIFFE and SPIRE |
| 22 | No post-quantum crypto page | overstated | `encryption-explained.md` has "A note on post-quantum cryptography" (ML-KEM, ML-DSA, SLH-DSA, crypto-agility). The migration how-to is missing; see Wave 4 |
| 23 | No network segmentation or WAF/DDoS page | **false** | `network-security-basics.md` has Segmentation, Microsegmentation, WAF and DDoS sections; the comparison has WAF and DDoS tables |
| 24 | No AI security cross-link hub to ai.noblerworks.com/safety | overstated | `security-from-scratch.md` "AI security is now part of the job" links 4 safety pages; 10 learn/resources pages link /safety. What is missing is a topic index that also gathers the 4 AI cert guides (Wave 4) |

Also found, not in the Gemini audit: `docs/freshness.md` had not been rebuilt since 2026-10-22 and was missing
the 8 cert guides added on 2026-11-07. Rebuilt in the same commit as this review.

## Plan, in order

### Wave 1 - the live exam with no guide

1. **SC-500 guide** at `exams/azure/sc-500/` (README, fact-sheet, notes, practice-plan, scenarios, strategy,
   flashcards). Microsoft Certified: Cloud and AI Security Engineer Associate. The Learn page lists 120 minutes
   and four assessed areas (identity, access and governance; storage, databases and networking; compute;
   security posture), and its responsibilities add securing AI solutions. Read the study guide
   (`https://aka.ms/SC500-StudyGuide`) for weights before writing. Add a pointer from the retired
   `exams/azure/az-500/README.md` to the new guide.
   Evidence: `git grep -i sc-500` finds only the TODO line; AZ-500, the guide it follows, retired 2026-08-31.

### Wave 2 - a hands-on day-one on-ramp (`learn/day-one/`)

The concept pages explain the ideas; none walks a beginner through doing the thing. Each page below is a
short, defensive, do-it-on-your-own-stuff exercise in the format of `cloud-zero-to-hero/learn/day-one/`
(10-minute read, one task, real output). Each links the concept page instead of repeating it, and the
Linux and networking basics stay on the cloud site (Phase 0 of `security-from-scratch.md` already links
them). Add a `learn/day-one/README.md` and link it from `learn/README.md` and Phase 0.

| Target | What is missing | Evidence |
|---|---|---|
| `learn/day-one/read-a-login-log.md` | Reading your own Linux auth log (`journalctl -u ssh`, `last`, failed vs accepted logins) and one CloudTrail `ConsoleLogin` event | `git grep -iE 'auth\.log\|journalctl\|lastb\|/var/log/secure' -- learn resources`: 0 hits |
| `learn/day-one/inspect-a-tls-certificate.md` | Inspecting a site's certificate chain, dates and SANs with `openssl s_client` and the browser, and searching crt.sh for your domain | `openssl s_client`: 0 hits; crt.sh is one sentence in `tls-and-https.md`. Headers are already shown with `curl -I` in `security-headers-and-csp.md`, so link it |
| `learn/day-one/read-a-cve-record.md` | Reading one real CVE on cve.org and NVD: description, CWE, a CVSS vector string decoded field by field, then checking KEV and EPSS | `vulnerability-management.md` explains base metrics, but `CVSS:3`/`CVSS:4`/`AV:N`: 0 hits; cve.org or NVD named on 1 learn page |
| `learn/day-one/check-an-email-header.md` | Opening "show original" on a message you received and reading `Received`, `Return-Path`, `Reply-To` and `Authentication-Results` | `Received:`: 0 hits; `Authentication-Results` appears once, in an exam-mapping line of `email-security-spf-dkim-dmarc.md` |
| `learn/day-one/secure-your-own-accounts.md` | Setting up a password manager and registering a passkey or hardware key, with two keys and a recovery plan | `mfa-and-passkeys.md` explains FIDO2 and recovery but has no set-up steps; "password manager" appears only in passing |
| `learn/day-one/lock-down-a-personal-cloud-account.md` | First hour on a new AWS account: MFA on the root user, no root access keys, a daily-use admin via IAM Identity Center, a budget alert, CloudTrail on | `root user` in learn/: 0 hits (labs and practice questions only). The cloud site does not cover it either (`git -C ../cloud-zero-to-hero grep -il 'root user' -- learn`: only a Docker page and cloud-from-scratch) |

### Wave 3 - small fixes with clear evidence

- **Tag the labs for SCS-C03.** Add `aws/specialty/security-scs-c03` to the `certs:` frontmatter of
  `centralized-logging-and-alerting.md`, `cloud-incident-response-tabletop.md`, `implement-zero-trust.md` and
  `least-privilege-iam-review.md`, then run `build-lab-map.py`. Evidence: all four list only the retired
  `security-scs-c02`; `labs-by-cert.md` has no SCS-C03 row.
- **Mark PCNSA retired** in `docs/certs.json` and the guide's README and fact sheet, once a Palo Alto page
  confirms the date (community sources say 2025-01-31). Evidence: not on
  `paloaltonetworks.com/services/education/certification` on 2026-11-25. Network Security Analyst is the
  nearest listed specialist cert, but Palo Alto says there is no direct equivalence. Needs a hand check
  (LIVEcommunity returns 403 to fetches).
- **Decide on Boundary.** HashiCorp's list has no Boundary exam on 2026-11-25. Either mark the guide
  retired or unverified in `certs.json` and its README, or prune it. Patrick's call; no flashcards until then.
- **CISM reconcile is unblocked.** The ISACA outline page now lists 42 supporting tasks under the four
  2026 domains. The existing TODO line (2026-11-14) can be done: reconcile notes 01-05 and drop
  `exam-retires`.

### Wave 4 - pages that are actually missing

- **`topics/ai-security.md`** topic index: the four AI cert guides (AIGP, AAISM, AAIA, TAISE), SC-100 notes
  05 (AI and agent security design), the AI section of `security-from-scratch.md`, and the
  ai.noblerworks.com/safety/ pages. Evidence: `git grep -iE 'aigp|aaism|aaia|taise' -- topics learn` finds
  only `learning-paths.md`; no topic index links any of the four guides.
- **`learn/concepts/post-quantum-migration.md`**: crypto inventory, hybrid key exchange in TLS, FIPS 203/204/205,
  and NIST's deprecation timeline (NIST IR 8547). Link the existing section in `encryption-explained.md`
  rather than repeat it. Evidence: `git grep -iE '8547|FIPS 20[345]' -- learn resources`: 0 hits; the topic
  is one section of three paragraphs.
- **SIEM section in `resources/service-comparison-security-tools.md`**: Microsoft Sentinel vs Amazon Security
  Lake plus a query layer vs Google Security Operations (ingestion, schema, pricing model, SOAR). Extend the
  existing page; do not start a third comparison file. Evidence: the comparison names Sentinel once, in its
  exam-focus list; the only per-cloud SIEM table is 4 rows in the architecture pattern.
- **`learn/concepts/non-human-identity.md`** (lowest priority here): owning, inventorying and expiring service
  accounts, CI tokens and API keys as a governance job. It must link, not repeat, the workload identity
  section of `secrets-management.md`. Evidence: "non-human" appears once, as a mistakes bullet in
  `least-privilege-explained.md`.

### Wave 5 - labs (session or Patrick, not the loop)

- Run `centralized-logging-and-alerting.md` and `harden-a-linux-server.md` end to end and add a "How this was
  run" section, as the SBOM and IAM labs have. The logging lab needs a sandbox AWS account; the Linux lab can
  run on a throwaway VM. Already a TODO line (2026-11-08, overdue).
- New labs for the largest unmapped groups, defensive only: a Vault dev-server secrets and dynamic-credentials
  lab (Vault Associate, SC-300 has nothing either), and a Kubernetes RBAC and NetworkPolicy lab on kind
  (KCSA; CKS already has three). Evidence: none of `hashicorp/vault-associate`, `kubernetes/kcsa`,
  `azure/sc-300` appears in `labs-by-cert.md`.

## Not gaps (do not queue)

Secrets management comparison, CSPM/CNAPP comparison, workload identity and SPIFFE/SPIRE, network
segmentation, WAF and DDoS: all covered (claims 19 to 23). Thin notes by word count: measure each against its
outline first; no missing objective was shown. Security+, CySA+ and CISSP transitions: already dated in
`TODO.md`.

## Draft verdicts

Both drafts were read in full, their relative links resolve from the published location, and both stay
defensive (no attack steps). Neither duplicates a published page: `red team`/`purple team` has 0 hits in
`learn/concepts` and `resources/playbooks`, and BEC is mentioned in 4 learn pages but has no playbook.
Not published here; that is Patrick's TODO line.

### `drafts/learn/concepts/red-team-vs-penetration-test-vs-purple-team.md`: publish after listed fixes

Checked: NIST SP 800-115 is current and final (2008, no withdrawal on CSRC). TIBER-EU is the ECB's
threat-intelligence-based red-teaming framework, updated in 2024 to align with the DORA TLPT standards. The
MITRE CTID Adversary Emulation Library exists, is maintained, and says it is for authorised defensive testing.
TLPT every three years for designated entities matches the repo's own `dora.md` (Articles 24-27, applies
from 17 January 2025). Security+ terms (known, partially known, unknown environment; purple team) match the
repo's SY0-701 and SY0-801 notes. Fixes:

1. "following the ECB's TIBER-EU approach in practice" should say TLPT follows the RTS on TLPT, which
   TIBER-EU was updated in 2024 to align with (the ECB page's wording).
2. PCI DSS 11.4 (at least every 12 months and after significant changes) has no citation, and the repo's
   `pci-dss.md` does not state the frequency. Add a link to the PCI SSC document library, or soften to
   "requires regular penetration testing".
3. CBEST is named without a source. Add the Bank of England CBEST page or drop the sentence.

### `drafts/resources/playbooks/business-email-compromise.md`: publish after listed fixes

Checked: the Microsoft Learn page "Respond to a compromised email account in Microsoft 365" exists (updated
2026-08-19) and the draft's contain steps (reset, revoke sessions, remove MFA methods, rules, forwarding,
app grants) match it. IC3 is the FBI's intake for cyber-enabled fraud and lists BEC. Fixes:

1. Microsoft's first step is to **disable the account** during the investigation, with a password reset as
   the next best option. Add it to Contain step 4.
2. Add the Microsoft points the draft misses: app passwords are not revoked by a password reset; check
   **hidden** inbox rules; review admin roles given to the user; for AD-synced accounts reset on premises.
3. "A prompt report can help banks act on frozen funds" reads oddly. IC3 says only that reports let the FBI
   investigate and "in some cases, even freeze stolen funds". Use that wording.
4. On publish, add a row to `resources/playbooks/README.md` (the draft does not do it).
