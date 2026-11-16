# Queue

Content work the **queue loop** builds for this site (nobler-os `scripts/loops/queue-loop.mjs`, loop `queue-z2h-security`, docs/LOOPS.md "queue"). Items are written by the **content-gaps loop** (`content-gaps-z2h-security`, since 2026-11-13) from the gap docs, TODO.md content lines, Search Console and the vendors' cert pages, already `approved` (Patrick, 2026-11-13: "auto-build, I land"). Patrick may add, edit or delete items by hand too. The loop reads this file at `origin/main` only.

**A push to this repo publishes the site**, so nothing here lands on its own: each built item waits on a local branch for Patrick.

## Format

Each item is a `## Q-NNN: title` section with these fields, then `### Spec` and `### Done when`:

- `status`: `proposed` | `approved` (the loop may build it) | `in-progress` | `done` | `failed`. The loop builds `approved` items, oldest `added` first. It writes `done` + a `result` line on its branch; `failed` (with the reason) lives in its state file (`~/.cache/loops/queue/state-security-zero-to-hero.json`). To retry, change the spec or run `node ~/coding/nobler-os/scripts/loops/queue-loop.mjs --repo security-zero-to-hero --retry Q-NNN`.
- `added`: YYYY-MM-DD. `source`: where the item came from (gap doc, TODO line, search data, vendor page). `after` (optional): items that must be landed first.
- `allow`: the backticked paths the change may touch (`*` within a folder, `**` any depth), including generated files its generators rewrite. Anything else changed fails the item. Never QUEUE.md or gate configuration.
- `### Done when`: one backticked command per line, run by the loop in the worktree; every one must exit 0. Allowed commands start with `python3 .github/scripts/check-internal-links.py`, `python3 .github/scripts/check-readme-counts.py --check`, `python3 .github/scripts/build-certs-index.py --check`, `python3 .github/scripts/build-provider-indexes.py --check`, `python3 .github/scripts/build-flashcards.py --check`, `python3 .github/scripts/build-lab-map.py --check`, `python3 .github/scripts/check-code-fences.py`, `python3 .github/scripts/check-cert-freshness.py`, `python3 .github/scripts/balance-answer-positions.py --check`, `bash .github/scripts/validate-cert-structure.sh`, `bash .github/scripts/validate-frontmatter.sh`, `grep`, `test -f`, `test ! -f` - no `;`, `&`, `|`, `<`, `>`, `$`, backticks or backslashes. The repo's full local gate (`scripts/check-ci-local.mjs`) always runs after them, and an independent reviewer must approve the diff.

The builder may read vendor docs sites (WebFetch, vendor domains only) to check exam codes and facts.

## Landing a built item

The loop commits to a local `loop/queue-<id>` branch and never pushes; the branch expires after 14 days. Read it, then land it:

```bash
git -C ~/coding/security-zero-to-hero log -p main..loop/queue-q-001
git -C ~/coding/security-zero-to-hero merge --ff-only loop/queue-q-001
ship security-zero-to-hero --no-deploy        # the push deploys the site
```

## Q-001: GHAS exam scenarios 13-16 (autofix, merge protection, delegated bypass, dismissal reasons)
- status: approved
- added: 2026-11-16
- source: Search Console 28 days: /exams/github/advanced-security/scenarios, 1081 impressions, position 5.7, 0 clicks
- allow: `exams/github/advanced-security/scenarios.md`

### Spec
Edit `exams/github/advanced-security/scenarios.md`. The page has 12 scenarios; readers who land on it find none on Copilot Autofix, branch/ruleset enforcement of code scanning, delegated bypass for push protection, or alert dismissal reasons. Append four scenarios after Scenario 12, in exactly the existing shape (`## Scenario N: Title`, `### Scenario`, `**Question:**`, `**Options:**` A-D, `**Correct Answer:**`, `**Explanation:**`, `**Why other options are wrong:**`, `---` between them):
- `## Scenario 13: Copilot Autofix for Code Scanning` (what it suggests, that a human reviews and commits the fix, which alerts it applies to).
- `## Scenario 14: Blocking Merges on Code Scanning Results` (required code scanning results via a branch protection rule or ruleset, and the alert-severity threshold setting).
- `## Scenario 15: Delegated Bypass for Push Protection` (org setting that sends bypass requests to designated reviewers instead of letting contributors self-bypass).
- `## Scenario 16: Dismissing Code Scanning Alerts` (the dismissal reasons: false positive, used in tests, won't fix, and what each means for reporting).
Check every fact against the current GitHub Docs (docs.github.com, code security section: "About Copilot Autofix for code scanning", "About code scanning alerts" / "Triaging code scanning alerts in pull requests", "Enabling delegated bypass for push protection") and keep facts consistent with `notes/02-code-scanning-and-codeql.md` and `notes/03-secret-scanning-and-push-protection.md`. Spread the correct answers across A-D (no letter used for more than two of the four). Do not edit existing scenarios.

### Done when
- `grep -qF '## Scenario 13: Copilot Autofix for Code Scanning' exams/github/advanced-security/scenarios.md`
- `grep -qF '## Scenario 14: Blocking Merges on Code Scanning Results' exams/github/advanced-security/scenarios.md`
- `grep -qF '## Scenario 15: Delegated Bypass for Push Protection' exams/github/advanced-security/scenarios.md`
- `grep -qF '## Scenario 16: Dismissing Code Scanning Alerts' exams/github/advanced-security/scenarios.md`
- `python3 .github/scripts/check-internal-links.py`
- `bash .github/scripts/validate-frontmatter.sh`

## Q-002: GHAS strategy page - which-feature decision table and where-configured table
- status: approved
- added: 2026-11-16
- source: Search Console 28 days: /exams/github/advanced-security/strategy, 784 impressions, position 6.5, 0 clicks
- allow: `exams/github/advanced-security/strategy.md`

### Spec
Edit `exams/github/advanced-security/strategy.md`. Under `## Exam Tactics`, after the `### Key Differentiators to Study` table and before `## Common Pitfalls`, add two sections:
- `### Which Feature Answers This Risk?`: a table with columns Risk | Feature | Where to look, at least 8 rows (vulnerable first-party code, committed credential, vulnerable dependency in a manifest, risky dependency introduced by a pull request, private vulnerability disclosure, org-wide alert view, enforcing features across many repos, preventing a push containing a secret). Use only feature names already used in `notes/01` to `notes/06` of this guide.
- `### Where Is It Configured?`: a table with columns Setting | Repo | Org | Enterprise, covering at least: enabling GHAS, security configurations, push protection, custom secret patterns, CodeQL default setup, Dependabot alerts, delegated bypass. Mark each cell with the level where it can be set, consistent with `notes/06-ghas-administration-and-enterprise-rollout.md` and `fact-sheet.md`; confirm against docs.github.com (code security section) and do not guess any cell you cannot confirm (write "see docs" instead).
Add one sentence to `### Alert Triage` under `## Common Pitfalls` linking to `scenarios.md`. Do not change other text.

### Done when
- `grep -qF '### Which Feature Answers This Risk?' exams/github/advanced-security/strategy.md`
- `grep -qF '### Where Is It Configured?' exams/github/advanced-security/strategy.md`
- `python3 .github/scripts/check-internal-links.py`
- `bash .github/scripts/validate-frontmatter.sh`
