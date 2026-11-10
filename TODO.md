# TODO

Working task list for **security-zero-to-hero** (Security Zero to Hero, <https://security.noblerworks.com/>). Read this at the start of a work session and keep it current as work completes - check items off with a date, add follow-ups as they surface. Stale TODOs are worse than none. Open actions only; history lives in git and CHANGELOG.md.

---

## Split from cloud-data-ai-security-zero-to-hero

- [x] 2026-10-21 Split from cloud-data-ai-security-zero-to-hero on 2026-10-21: security-only README, Study Hub, home, learn/topic indexes, new `learn/security-from-scratch.md`, amber accent, new IndexNow key, social card, family cross-links.
- [x] 2026-10-27 live. Patrick: push, then confirm the Pages deploy serves <https://security.noblerworks.com/> (custom domain + DNS are outside this repo).
- [ ] After the first deploy: the "Notify IndexNow" step says `IndexNow accepted` (a first-run 403 `SiteVerificationNotCompleted` is normal; re-run `notify-indexnow.py --all`). Key file: `https://security.noblerworks.com/<key>.txt`.
- [x] 2026-11-09 submitted `https://security.noblerworks.com/sitemap.xml` to Search Console via API.
- [ ] Patrick: Bing Webmaster Tools -> submit `https://security.noblerworks.com/sitemap.xml`.
- [x] 2026-10-21 `check-repo-metadata.py --fix` run and topics set.
- [x] 2026-10-27 social preview uploaded (`assets/brand/social-preview-1280x640.png`; GitHub reports a custom image).
- [x] 2026-10-21 Primary button fill darkened to `#b45309` (5.02:1 white text); cloud done the same day.

## Tooling

- [x] 2026-11-10 Freshness workflow on main; dispatched run 42795039513 green: 94 pages, 8 over 120 days (all `last-updated: 2026-05-03`, 191 d), 15 undated READMEs, none near the 365-day fail.
- [ ] 2026-12-15 Re-verify the 8 fact-sheets (GCP PCSE, GHAS, Boundary, Vault, IBM, KCSA, OSCP, PCNSA) (2026-05-03) on vendor pages, bump `last-updated` (365-d fail: 2027-05-03); date or exempt the 15 undated READMEs. `python3 .github/scripts/check-freshness.py --days 120`.
- [x] 2026-11-07 Cross-site learning paths (7 routes, `learn/learning-paths.md`, byte-identical in all four repos, linked from which-site, learn hub and home). Not pushed or deployed: ships with the train.
- [ ] 2026-12-07 re-verify every link in `learn/learning-paths.md` against each repo's `git ls-files` (script: loop the URLs through the four trees) and the matching certs against current exam codes.
- [ ] 🟡 `.github/scripts/site_hooks.py` has drifted from ai-zero-to-hero's port - one canonical module all sites vendor (with a sync check), or record the fork. S-M, low.
- [ ] 🟡 `glossary-add-anchors.py`, `glossary-autolink.py`, `glossary-upgrade-existing-links.py` are the documented manual glossary pipeline; delete only if it is retired.
- [x] 2026-11-07 `check-code-fences.py` added and heading-anchor validation folded into `check-internal-links.py` (184 anchors, 0 broken; ids match the strict build on all 529 comparable pages); both blocking in `structure-validate.yml`.

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

- [x] 2026-11-07 AI governance + AI security guides (IAPP AIGP, ISACA AAISM and AAIA, CSA TAISE) built as 4 local commits, NOT pushed: ship at wrap-up via the train. All four link ai.noblerworks.com/safety/. ✅ 2026-11-08: pushed.
- [ ] AIGP unverified: exam price, delivery, languages, scored/unscored split (IAPP pages unreadable or silent); ISO 42001 abstract read from national-body mirrors (iso.org blocked); South Korea AI Basic Law and US state laws not fetched. Re-check on iapp.org.
- [ ] AAISM unverified: outline effective date beyond "June 2025" label; guide leans on NIST AI 100-1/100-2/600-1, OWASP LLM Top 10 pages (descriptions for LLM01-04, 09 read as titles only). Re-check against the live ISACA outline at the next 180-day pass.
- [ ] AAIA unverified: outline effective date beyond "June 2025" label (candidate guide is (c) 2026); qualifying-credential list may change. Re-check on isaca.org/credentialing/aaia.
- [ ] TAISE unverified: certificate validity/renewal, languages, module-level weights beyond the equal 6 questions per module (prep kit Knowledge Guide and curriculum are downloads, not read). Notes use CSA module titles plus NIST/OWASP/EU AI Act/AICM primary sources.

1. ~~Defensive labs~~ done 2026-11-07 (container scan with SBOM, least-privilege IAM review, IR tabletop; see Wave 3 below).
2. **Cert gaps**: CompTIA PenTest+, Cisco CyberOps Associate, GIAC GSEC and GCLD. EC-Council CEH is Patrick's to write (blocked by the safety check three times; drafts in `~/.cache/ceh-draft-2026-09-29/`). New providers need entries in `PROVIDER_HIGHLIGHTS` / `PROVIDER_EMOJI` (`build-provider-indexes.py`).
   ISC2 SSCP, AWS SCS-C03, CompTIA SecurityX (CAS-005) and Google Professional Security Operations Engineer written 2026-11-07 (vendor pages and outlines read; SSCP and SecurityX price and CPE/CE terms and the Google exam's base validity are not on the vendor pages, so left as not verified).
   - [x] 2026-11-07 Google SecOps Engineer reworked to exam guide 2.0 (weights 13/20/18/20/18/11 read from the PDF; new task 2.3, GTI as third platform). Decision: the cert page text still links the original guide and does not say which the live exam follows, so notes follow 2.0.
   - [ ] 2026-12-07 Google SecOps Engineer: recheck <https://cloud.google.com/learn/certification/security-operations-engineer> for the guide link and which version is live. Unverified in notes 2.0: GTI LiveHunt/DTM docs (no SecOps ingestion page found), Triage and Investigation Agent playbook action, MCP specifics.
   - [ ] 2026-12-15 SecurityX: CompTIA lists a draft V6 objectives PDF on its "exam objectives under development" page (no code or date). Recheck for the CAS-005 successor and its launch; fetch the CAS-005 objectives PDF (not linked on the SecurityX page) and add the numbered objectives.
3. ~~Topic indexes~~ done 2026-11-07 (detection and response, governance and compliance, application security).

## 2026-10-21 content expansion follow-ups

- [ ] 2026-11-08 Run `resources/hands-on-projects/centralized-logging-and-alerting.md` and `harden-a-linux-server.md` end to end in a sandbox; fix any command that fails.
- [x] 2026-11-08 Weekly lychee run: if fidoalliance.org or iso.org links (403 to bots) fail, add them to `.lycheeignore`. ✅ 2026-11-08: 0 failures in the 11-07 and 11-02 runs; 403 is accepted, no ignore needed.

## 2026-10-22 content round follow-ups

- [x] 2026-11-10 CMMC Phase 2 did not start: DoW suspended it 13 July 2026 (Phases 3-4 on hold, Reform Task Force). `cmmc.md` "as of" line, phase table and status updated.
- [ ] 2026-12-15 CMMC: check the DoW CIO page (bot-blocked, by hand) for the task force outcome or a Phase 2 restart/rulemaking; update the phase table in `resources/compliance-guides/cmmc.md`.
- [ ] 2026-12-01 NIS2: by hand (bot-blocked), check transposition status and the 2026-01-20 amendment proposal on the Commission page; update `nis2.md`.
- [ ] 2026-12-01 DORA: check the ESAs' CTPP list and TLPT RTS for updates; update `dora.md`.
- [ ] 2026-12-01 Snowflake case study: add Moucka's sentence (justice.gov) to the timeline in `resources/case-study-snowflake-customer-breaches-2024.md`. 11-06: set for 10-27, no sentence reported; DOJ case page last updated 08-07.
- [x] 2026-11-06 Snowflake case study updated: phase 3 window passed, but Snowflake does not say it is complete (per-account dates, may be extended).
- [x] 2026-11-08 Weekly lychee: if gao.gov (403 to bots) or community.progress.com (JS-only) links in `resources/case-study-*.md` fail, add them to `.lycheeignore`. ✅ 2026-11-08: 0 failures in the 11-07 and 11-02 runs; no ignore needed.

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
- [ ] 2026-11-29 Labs: run `cloud-incident-response-tabletop.md` once with a real person or team and fill its Results table (NOT RUN, design only); edit the playbooks with the gaps found.
- [ ] 2026-11-22 `container-image-scan-with-sbom.md` step 6 (rescan a current nginx tag and compare counts) NOT RUN; and `least-privilege-iam-review.md` rewritten `02` policy not linted. Run both, paste real output. A real-account IAM pass (last-accessed data, policy generation) needs Patrick's sandbox account.
- [ ] 2026-11-14 Built, not pushed: Wave 3 and Wave 5 flashcard commits are local; push goes through the train at wrap-up.
- [ ] 2026-11-29 Hand-check Wave 4 still open (second pass 2026-11-07 settled CRA Art 32, AL/OK dates): PCAOB AS 2201 wording (403), LA/VT laws, CCPA threshold (503), 192.7M Change figure (HHS 403), Colonial DOJ page. Log: docs/verification-2026-11-07.md.
- [ ] 2026-12-01 SEC cyber rule: checked 2026-11-07, no proposal to amend Item 1.05/106 (trade-group letters only); recheck sec.gov, update `sec-cyber-disclosure-rule.md` Status.
- [ ] 2027-01-01 CCPA ADMT rules start; re-read cppa.ca.gov and update `us-state-privacy-laws.md` (also state law effective dates, e.g. Connecticut 2026-07-01 amendments, Vermont 2028).
- [ ] 2026-12-01 EU CRA: check the Commission page for implementing acts, harmonised standards or amendments before 2027-12-11; update `eu-cyber-resilience-act.md`.
- [x] 2026-11-07 Flashcard decks for `gcp/cloud-security-engineer` and `hashicorp/vault-associate` (Key terms sections in their notes).
- [ ] Flashcard decks still missing: `azure/az-500` skipped on purpose (retired 2026-08-31, reference only); `hashicorp/boundary-associate` skipped (exam unverified, only 6 cards). Revisit if either guide is kept or verified.
- [x] 2026-11-07 "Check yourself" quiz (3-4 questions, collapsed `<details>` answers) at the end of all 34 concept pages; strict build verified.
- [ ] 2026-11-07 Built, not pushed: the two Check yourself commits are local; push goes through the train at wrap-up. Patrick or a fresh session: skim a few answers against their pages (written from the page text only; `owasp-api-security-top-10-explained.md` also has an older "Quick self-check").
