# TODO

Working task list for **security-zero-to-hero** (Security Zero to Hero, <https://security.noblerworks.com/>). Read this at the start of a work session and keep it current as work completes - check items off with a date, add follow-ups as they surface. Stale TODOs are worse than none. Open actions only; history lives in git and CHANGELOG.md.

---

## Split from cloud-data-ai-security-zero-to-hero

- [x] 2026-10-21 Split from cloud-data-ai-security-zero-to-hero on 2026-10-21: security-only README, Study Hub, home, learn/topic indexes, new `learn/security-from-scratch.md`, amber accent, new IndexNow key, social card, family cross-links.
- [ ] Patrick: push, then confirm the Pages deploy serves <https://security.noblerworks.com/> (custom domain + DNS are outside this repo).
- [ ] After the first deploy: the "Notify IndexNow" step says `IndexNow accepted` (a first-run 403 `SiteVerificationNotCompleted` is normal; re-run `notify-indexnow.py --all`). Key file: `https://security.noblerworks.com/<key>.txt`.
- [ ] Patrick: Search Console `sc-domain:noblerworks.com` -> submit `https://security.noblerworks.com/sitemap.xml`; Bing Webmaster Tools the same.
- [x] 2026-10-21 `check-repo-metadata.py --fix` run and topics set.
- [ ] 2026-10-28 Patrick: upload `assets/brand/social-preview-1280x640.png` at GitHub Settings > General > Social preview (no API). Card is the shared Zero to Hero template (`assets/brand/social-preview.html`, 2026-10-21).
- [x] 2026-10-21 Primary button fill darkened to `#b45309` (5.02:1 white text); cloud done the same day.

## Tooling

- [ ] 🟡 `.github/scripts/site_hooks.py` has drifted from ai-zero-to-hero's port - one canonical module all sites vendor (with a sync check), or record the fork. S-M, low.
- [ ] 🟡 `glossary-add-anchors.py`, `glossary-autolink.py`, `glossary-upgrade-existing-links.py` are the documented manual glossary pipeline; delete only if it is retired.
- [ ] No CI check for unbalanced code fences; fold heading-anchor validation into `check-internal-links.py`.

## Author bio counts

- [ ] **Patrick: decide** whether the home-page bio should carry a cert count again (would need a `{{personal_certs}}` token fed from one checked-in value).
- [ ] 2026-11-05: Database Specialty lapses - `README.md` (top bio line and About the Author) goes from 19x multi-cloud / 14x AWS / 64 to **18x / 13x / 63** (source `go-to-market/claims.md`).

## Exam changes (from the 2026-10-16 retired-exam sweep)

- [ ] Successors: AZ-500 -> SC-500 (third-party only; confirm on learn.microsoft.com before writing); AWS SCS-C03 is open now [H]. Decide whether the retired SCS-C02 and AZ-500 guides stay as reference or are pruned.
- [ ] 2026-11-03 CISM: when ISACA's outline page shows the 2026 task and knowledge statements, reconcile notes 01-05 and drop the 2022 weights and `exam-retires` (exams/isaca/cism).
- [ ] 2026-11-18 Security+: confirm SY0-801 launched; rebuild the guide on SY0-801 in place by 2027-01-31 (notes 06 covers it until then), keep a SY0-701 note until 2027-06-11.
- [ ] 2026-12-23 CySA+: CS0-003 retired in English; trim the CS0-003 notices in README and fact sheet (translations retire 2027-03-23).
- [ ] 2027-04-15 CISSP: 2027 outline live; move weights and Domain 1 name into README/fact sheet, fold notes 09 into notes 01-08, drop `exam-retires`.
- [ ] GitHub Advanced Security: confirm the 2-year validity stated in the guide [H].
- [ ] PCNSA: Palo Alto's page no longer lists PCNSA and promotes Network Security Analyst; check retired vs renamed [M].
- [ ] Unverified exams: HashiCorp `boundary-associate` is on no HashiCorp exam list [M]; the IBM Cloud Security Engineer code/title pairing is suspect [L]; OSCP content vs the current exam. Patrick or a fresh session: check the vendor pages by hand before editing.
- [ ] New-guide candidate: HashiCorp Vault Operations Advanced (verify the code first) [L].

## Content backlog (ranked)

- [ ] AI governance + AI security certs (the niche, almost no free guides): IAPP AIGP, ISACA AAISM and AAIA, CSA TAISE - verify names/codes; cross-link ai.noblerworks.com/safety/.

1. **Breach postmortems**: Capital One 2019, Snowflake customer breaches 2024, SolarWinds, MOVEit.
2. **Defensive labs**: least-privilege IAM, cloud incident response, container scan with SBOM (logging/alerting and Linux hardening shipped 2026-10-21).
3. **Cert gaps**: CompTIA PenTest+, SecurityX (CASP+), ISC2 SSCP, Cisco CyberOps Associate, GIAC GSEC and GCLD, Google Professional Security Operations Engineer. EC-Council CEH is Patrick's to write (blocked by the safety check three times; drafts in `~/.cache/ceh-draft-2026-09-29/`). New providers need entries in `PROVIDER_HIGHLIGHTS` / `PROVIDER_EMOJI` (`build-provider-indexes.py`).
4. **Concept pages**: security awareness and culture (DLP, CSPM, containers, Kubernetes, email, EDR, backup and risk management shipped 2026-10-22).
5. **Topic indexes**: detection and response; governance and compliance.

## 2026-10-21 content expansion follow-ups

- [ ] 2026-11-08 Run `resources/hands-on-projects/centralized-logging-and-alerting.md` and `harden-a-linux-server.md` end to end in a sandbox; fix any command that fails.
- [ ] 2026-11-08 Weekly lychee run: if fidoalliance.org or iso.org links (403 to bots) fail, add them to `.lycheeignore`.

## 2026-10-22 content round follow-ups

- [ ] 2026-11-10 CMMC Phase 2 (Level 2 C3PAO) starts: confirm on dodcio.defense.gov and update the "as of" line in `resources/compliance-guides/cmmc.md`.
- [ ] 2026-12-01 NIS2: by hand (bot-blocked), check transposition status and the 2026-01-20 amendment proposal on the Commission page; update `nis2.md`.
- [ ] 2026-12-01 DORA: check the ESAs' CTPP list and TLPT RTS for updates; update `dora.md`.

## Distribution

- [ ] Patrick: submit to awesome lists (awesome-security, awesome-cybersecurity, awesome-certifications) and post one useful page each to r/CompTIA, r/cybersecurity, r/cissp, linking back.
