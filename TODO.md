# TODO

Working task list for **security-zero-to-hero** (Security Zero to Hero, <https://security.noblerworks.com/>). Read this at the start of a work session and keep it current as work completes - check items off with a date, add follow-ups as they surface. Stale TODOs are worse than none. Open actions only; history lives in git and CHANGELOG.md.

---

## Split from cloud-data-ai-security-zero-to-hero

- [x] 2026-10-21 Split from cloud-data-ai-security-zero-to-hero on 2026-10-21: security-only README, Study Hub, home, learn/topic indexes, new `learn/security-from-scratch.md`, amber accent, new IndexNow key, social card, family cross-links.
- [x] 2026-10-27 live. Patrick: push, then confirm the Pages deploy serves <https://security.noblerworks.com/> (custom domain + DNS are outside this repo).
- [ ] After the first deploy: the "Notify IndexNow" step says `IndexNow accepted` (a first-run 403 `SiteVerificationNotCompleted` is normal; re-run `notify-indexnow.py --all`). Key file: `https://security.noblerworks.com/<key>.txt`.
- [ ] Patrick: Search Console `sc-domain:noblerworks.com` -> submit `https://security.noblerworks.com/sitemap.xml`; Bing Webmaster Tools the same.
- [x] 2026-10-21 `check-repo-metadata.py --fix` run and topics set.
- [x] 2026-10-27 social preview uploaded (`assets/brand/social-preview-1280x640.png`; GitHub reports a custom image).
- [x] 2026-10-21 Primary button fill darkened to `#b45309` (5.02:1 white text); cloud done the same day.

## Tooling

- [ ] 🟡 `.github/scripts/site_hooks.py` has drifted from ai-zero-to-hero's port - one canonical module all sites vendor (with a sync check), or record the fork. S-M, low.
- [ ] 🟡 `glossary-add-anchors.py`, `glossary-autolink.py`, `glossary-upgrade-existing-links.py` are the documented manual glossary pipeline; delete only if it is retired.
- [ ] No CI check for unbalanced code fences; fold heading-anchor validation into `check-internal-links.py`.

## Author bio counts

- [ ] **Patrick: decide** whether the home-page bio should carry a cert count again (would need a `{{personal_certs}}` token fed from one checked-in value).
- [x] ✅ 2026-11-06: 2026-11-05: Database Specialty lapses - `README.md` (top bio line and About the Author) goes from 19x multi-cloud / 14x AWS / 64 to **18x / 13x / 63** (source `go-to-market/claims.md`).

## Exam changes (from the 2026-10-16 retired-exam sweep)

- [ ] Successors: AZ-500 -> SC-500 (third-party only; confirm on learn.microsoft.com before writing); AWS SCS-C03 guide written 2026-11-07 (SCS-C02 kept as reference, marked superseded). Decide whether the retired SCS-C02 and AZ-500 guides stay as reference or are pruned.
- [ ] 2026-11-14 CISM: when ISACA's outline page shows the 2026 task and knowledge statements, reconcile notes 01-05 and drop the 2022 weights and `exam-retires` (exams/isaca/cism). ✏️ 2026-11-07 re-dated 2026-11-14: ISACA outline page fetched 11-07 but no 2026 task/knowledge statements confirmed read-only; recheck
- [ ] 2026-11-18 Security+: confirm SY0-801 launched; rebuild the guide on SY0-801 in place by 2027-01-31 (notes 06 covers it until then), keep a SY0-701 note until 2027-06-11.
- [ ] 2026-12-23 CySA+: CS0-003 retired in English; trim the CS0-003 notices in README and fact sheet (translations retire 2027-03-23).
- [ ] 2027-04-15 CISSP: 2027 outline live; move weights and Domain 1 name into README/fact sheet, fold notes 09 into notes 01-08, drop `exam-retires`.
- [x] 2026-11-06 GitHub Advanced Security guide says 2 years, matching GitHub certs (vendor page read, cloud TODO [H]).
- [ ] PCNSA: Palo Alto's page no longer lists PCNSA and promotes Network Security Analyst; check retired vs renamed [M].
- [ ] Unverified exams: HashiCorp `boundary-associate` is on no HashiCorp exam list [M]; the IBM Cloud Security Engineer code/title pairing is suspect [L]; OSCP content vs the current exam. Patrick or a fresh session: check the vendor pages by hand before editing.
- [ ] New-guide candidate: HashiCorp Vault Operations Advanced (verify the code first) [L].
- [x] 2026-10-22 CC, CCSP, CISA, CKS, SC-401, CCSK pages updated to the current official outlines (CHANGELOG 2026-10-22 (5)).

## Content backlog (ranked)

- [ ] 2026-11-07 AI governance + AI security guides (IAPP AIGP, ISACA AAISM and AAIA, CSA TAISE) built as 4 local commits, NOT pushed: ship at wrap-up via the train. All four link ai.noblerworks.com/safety/.
- [ ] 2026-11-07 AIGP unverified: exam price, delivery, languages, scored/unscored split (IAPP pages unreadable or silent); ISO 42001 abstract read from national-body mirrors (iso.org blocked); South Korea AI Basic Law and US state laws not fetched. Re-check on iapp.org.
- [ ] 2026-11-07 AAISM unverified: outline effective date beyond "June 2025" label; guide leans on NIST AI 100-1/100-2/600-1, OWASP LLM Top 10 pages (descriptions for LLM01-04, 09 read as titles only). Re-check against the live ISACA outline at the next 180-day pass.
- [ ] 2026-11-07 AAIA unverified: outline effective date beyond "June 2025" label (candidate guide is (c) 2026); qualifying-credential list may change. Re-check on isaca.org/credentialing/aaia.
- [ ] 2026-11-07 TAISE unverified: certificate validity/renewal, languages, module-level weights beyond the equal 6 questions per module (prep kit Knowledge Guide and curriculum are downloads, not read). Notes use CSA module titles plus NIST/OWASP/EU AI Act/AICM primary sources.

1. ~~Defensive labs~~ done 2026-11-07 (container scan with SBOM, least-privilege IAM review, IR tabletop; see Wave 3 below).
2. **Cert gaps**: CompTIA PenTest+, Cisco CyberOps Associate, GIAC GSEC and GCLD. EC-Council CEH is Patrick's to write (blocked by the safety check three times; drafts in `~/.cache/ceh-draft-2026-09-29/`). New providers need entries in `PROVIDER_HIGHLIGHTS` / `PROVIDER_EMOJI` (`build-provider-indexes.py`).
   ISC2 SSCP, AWS SCS-C03, CompTIA SecurityX (CAS-005) and Google Professional Security Operations Engineer written 2026-11-07 (vendor pages and outlines read; SSCP and SecurityX price and CPE/CE terms and the Google exam's base validity are not on the vendor pages, so left as not verified).
   - [ ] 2026-12-15 SecurityX: CompTIA lists a draft V6 objectives PDF on its "exam objectives under development" page (no code or date). Recheck for the CAS-005 successor and its launch; fetch the CAS-005 objectives PDF (not linked on the SecurityX page) and add the numbered objectives.
3. ~~Topic indexes~~ done 2026-11-07 (detection and response, governance and compliance, application security).

## 2026-10-21 content expansion follow-ups

- [ ] 2026-11-08 Run `resources/hands-on-projects/centralized-logging-and-alerting.md` and `harden-a-linux-server.md` end to end in a sandbox; fix any command that fails.
- [ ] 2026-11-08 Weekly lychee run: if fidoalliance.org or iso.org links (403 to bots) fail, add them to `.lycheeignore`.

## 2026-10-22 content round follow-ups

- [ ] 2026-11-10 CMMC Phase 2 (Level 2 C3PAO) starts: confirm on dodcio.defense.gov and update the "as of" line in `resources/compliance-guides/cmmc.md`.
- [ ] 2026-12-01 NIS2: by hand (bot-blocked), check transposition status and the 2026-01-20 amendment proposal on the Commission page; update `nis2.md`.
- [ ] 2026-12-01 DORA: check the ESAs' CTPP list and TLPT RTS for updates; update `dora.md`.
- [ ] 2026-12-01 Snowflake case study: add Moucka's sentence (justice.gov) to the timeline in `resources/case-study-snowflake-customer-breaches-2024.md`. 11-06: set for 10-27, no sentence reported; DOJ case page last updated 08-07.
- [x] 2026-11-06 Snowflake case study updated: phase 3 window passed, but Snowflake does not say it is complete (per-account dates, may be extended).
- [ ] 2026-11-08 Weekly lychee: if gao.gov (403 to bots) or community.progress.com (JS-only) links in `resources/case-study-*.md` fail, add them to `.lycheeignore`.

## Distribution

- [ ] Patrick: submit to awesome lists (awesome-security, awesome-cybersecurity, awesome-certifications) and post one useful page each to r/CompTIA, r/cybersecurity, r/cissp, linking back.

## Content gaps (2026-11-07 review)

Plan: [docs/content-gaps-2026-11-07.md](docs/content-gaps-2026-11-07.md). Waves 3 and 5 are already listed above.

- [x] 2026-11-07 Wave 1: incident response playbooks (`resources/playbooks/`: leaked key, phishing triage, OAuth grant, ransomware first hour, lost laptop, public bucket).
- [x] 2026-11-07 Wave 1: roadmaps + interview guides for SOC analyst, GRC, AppSec, cloud security.
- [ ] 2026-11-07 Built, not pushed: Wave 1 commit is local; push goes through the train at wrap-up. Patrick or a fresh session: hand-check the new pages' vendor links read as described (reachability was tested, wording was not).
- [x] 2026-11-07 Wave 2: concept pages - OWASP API Top 10, secure SDLC/DevSecOps, security headers + CSP, ATT&CK for defenders, forensics, threat intel, privacy engineering.
- [x] 2026-11-07 Wave 4: six compliance guides (`sox-itgc`, `us-state-privacy-laws`, `cis-controls-v8`, `nist-sp-800-53`, `eu-cyber-resilience-act`, `sec-cyber-disclosure-rule`) and case studies Change Healthcare, MGM, Colonial Pipeline. Local commits, not pushed; the train pushes at wrap-up.
- [x] 2026-11-07 Wave 3: topic indexes (`topics/detection-and-response.md`, `governance-and-compliance.md`, `application-security.md`) and labs (`container-image-scan-with-sbom`, `least-privilege-iam-review`, `cloud-incident-response-tabletop`).
- [ ] 2026-11-14 Labs: run `cloud-incident-response-tabletop.md` once with a real person or team and fill its Results table (NOT RUN, design only); edit the playbooks with the gaps found.
- [ ] 2026-11-14 `container-image-scan-with-sbom.md` step 6 (rescan a current nginx tag and compare counts) NOT RUN; and `least-privilege-iam-review.md` rewritten `02` policy not linted. Run both, paste real output. A real-account IAM pass (last-accessed data, policy generation) needs Patrick's sandbox account.
- [ ] 2026-11-14 Built, not pushed: Wave 3 and Wave 5 flashcard commits are local; push goes through the train at wrap-up.
- [ ] 2026-11-14 Hand-check Wave 4 items marked unverified: PCAOB AS 2201 wording (site blocked bots), the other-states table in `us-state-privacy-laws.md` (law-firm and vendor sources, 2026-enacted AL/LA/OK/VT single-sourced), CRA Article 32 class routes, the 192.7M Change figure (HHS page 403), Colonial/DOJ seizure page (DOJ blocked bots; figures come from the Senate hearing record).
- [ ] 2026-12-01 SEC cyber disclosure rule: check sec.gov for any proposal to amend or rescind Item 1.05 / Item 106 (Reg S-K review); update `sec-cyber-disclosure-rule.md` Status.
- [ ] 2027-01-01 CCPA ADMT rules start; re-read cppa.ca.gov and update `us-state-privacy-laws.md` (also state law effective dates, e.g. Connecticut 2026-07-01 amendments, Vermont 2028).
- [ ] 2026-12-01 EU CRA: check the Commission page for implementing acts, harmonised standards or amendments before 2027-12-11; update `eu-cyber-resilience-act.md`.
- [x] 2026-11-07 Flashcard decks for `gcp/cloud-security-engineer` and `hashicorp/vault-associate` (Key terms sections in their notes).
- [ ] Flashcard decks still missing: `azure/az-500` skipped on purpose (retired 2026-08-31, reference only); `hashicorp/boundary-associate` skipped (exam unverified, only 6 cards). Revisit if either guide is kept or verified.
