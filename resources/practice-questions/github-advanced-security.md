---
last-updated: 2026-08-09
difficulty: intermediate
---

# GitHub Advanced Security (GHAS) - Practice Questions

15 questions for the GHAS exam, weighted toward code scanning and CodeQL (25%), secret scanning and push protection (20%), and dependency review and Dependabot (20%).

> **Cert page:** [exams/github/advanced-security/](../../exams/github/advanced-security/)

---

### Question 1
**Scenario:** A developer tries to push a commit containing an API key.

A. With push protection on, the push is blocked and the developer must remove the secret or give a bypass reason
B. The key is encrypted automatically by GitHub before it is stored, so the secret cannot be read from the commit or the history afterwards, even by a repository admin
C. The push succeeds and an alert is raised later by a scheduled scan
D. Nothing happens, because secret scanning only checks the default branch weekly

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Push protection stops the secret before it enters history, which is the only outcome that avoids rotation. Once a secret is pushed, treat it as compromised and rotate it: removing the commit does not undo the exposure, especially in a public repository.
</details>

---

### Question 2
**Scenario:** CodeQL must find injection vulnerabilities in application code.

A. It runs the application in a sandbox and sends crafted requests at it to see which inputs cause a failure
B. It matches patterns of bad strings, such as concatenated SQL keywords, in the source files with regular expressions alone
C. It checks dependencies only, comparing declared package versions with the advisory database for known flaws
D. It builds a queryable database of the code and runs semantic queries with data flow analysis from sources to sinks

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Taint tracking is what distinguishes CodeQL from a regular-expression scanner: it follows untrusted input through the code to a dangerous sink, which finds real vulnerabilities and suppresses cases where the input is sanitized on the way.
</details>

---

### Question 3
**Scenario:** A code scanning alert is a false positive.

A. Disable code scanning for the repository until the rule has been fixed by the maintainers of the query pack
B. Delete the code that triggers the alert, then restore it from history once the alert has closed itself and the scan is green again
C. Dismiss the alert with a reason, which is recorded and auditable
D. Ignore it and leave the alert open, since open alerts do not block merges and will age out in time

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Dismissing with a reason keeps the alert list meaningful while preserving the decision and who made it. Disabling scanning to silence one finding removes coverage everywhere, and an unmanaged backlog quickly makes the whole tool ignored.
</details>

---

### Question 4
**Scenario:** Dependabot must open pull requests for vulnerable dependencies.

A. Dependabot alerts only, which tell the team about vulnerable dependencies and leave the upgrade to a person
B. Manual dependency review each sprint, where a developer reads the advisory list and edits the manifests
C. Enable Dependabot security updates, which open pull requests that upgrade to a patched version
D. Secret scanning, which checks pushed content for credentials and opens an alert for each exposed token

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Alerts tell you; security updates act. Version updates are the separate feature that keeps dependencies current regardless of vulnerabilities, configured in `dependabot.yml` with a schedule and grouping.
</details>

---

### Question 5
**Scenario:** A pull request adds a dependency with a known critical vulnerability.

A. Only after merge, when the dependency graph updates on the default branch and Dependabot raises an alert that someone must then triage
B. Dependency review on the pull request surfaces it, and can be a required check that blocks the merge
C. It merges normally, because checks look only at the changed code
D. Nothing detects it until a dependency review is run by hand

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Catching it at review time is far cheaper than after merge, and the dependency review action can fail the build on a severity threshold or a disallowed license. That turns policy into a gate rather than a report.
</details>

---

### Question 6
**Scenario:** Code scanning must run on a schedule as well as on pull requests.

A. Once at setup, since the result of the first scan stays valid for as long as the code in the repo is unchanged
B. Configure the workflow with `pull_request`, `push` to the default branch, and a `schedule` trigger
C. Manual runs only, started by a maintainer from the Actions tab whenever a scan is wanted
D. Pull requests only, because scanning code that has not changed cannot produce any new alert, whatever the query pack

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The CodeQL query pack is updated over time, so a scheduled scan finds newly discoverable issues in code that has not changed. Pull request scanning gives fast feedback on new code; the schedule covers the rest of the repository.
</details>

---

### Question 7
**Scenario:** A monorepo has code in several languages.

A. Only one language can be scanned per repository, so a monorepo needs a separate repository for each language
B. Configure a matrix with one analysis per supported language, since CodeQL databases are per-language
C. Use secret scanning instead, which reads every file in any language
D. CodeQL detects and scans all languages automatically in one run, using a single combined database for the repo

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Each language gets its own database and query suite, which is why the default workflow uses a matrix. Compiled languages may also need a build step, either autobuild or explicit build commands, for the database to be complete.
</details>

---

### Question 8
**Scenario:** Scanning results from a third-party tool must appear in the GitHub security tab.

A. Upload results in SARIF format, which the code scanning API accepts from any tool
B. It is not possible, because the security tab only displays alerts produced by CodeQL analysis on GitHub
C. Paste them into an issue in the repository and label it, so the security tab picks up the findings
D. Only CodeQL is supported, and results from other tools must be converted into CodeQL query packs

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** SARIF is the interoperability format, so linters, SAST tools, and container scanners can all feed the same alert experience with deduplication and pull request annotations. This is what makes code scanning a hub rather than a single tool.
</details>

---

### Question 9
**Scenario:** A secret was pushed and is now in git history.

A. Rotate the credential first, then optionally rewrite history
B. Add the file to `.gitignore` so that it is not committed again and the secret leaves the repository
C. Delete the commit and consider it resolved, since a removed commit can no longer be cloned or viewed
D. Make the repository private, which stops anyone who has not already cloned it from reading the history

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Automated scrapers find secrets in public repositories within minutes, so rotation is the only reliable remediation and it comes first. History rewriting is cleanup; it does not recall what was already cloned or indexed.
</details>

---

### Question 10
**Scenario:** GHAS must be rolled out across a large enterprise without overwhelming teams.

A. Leave it to individual teams to turn on whichever features they want and handle alerts as they see fit
B. Enable everything everywhere at once, so every repository has secret, dependency, and code scanning together
C. Phase it: secret scanning and push protection first, then dependency management, then code scanning per language, with a triage owner
D. Enable code scanning only, across all repositories, and add the other features after the first year

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Secret scanning has the highest signal-to-noise ratio and needs the least developer effort, which builds credibility. Turning on everything at once produces a backlog nobody triages, and an ignored alert list is worse than no scanning because it looks like coverage.
</details>

---

### Question 11
**Scenario:** Which explains secret scanning's partner program?

A. It applies only to private repositories, where GitHub checks each token against the issuing partner's own records
B. When a partner's token pattern is found in a public repository, GitHub tells the provider, who can revoke it
C. Partners write the scanner themselves, and GitHub runs their code against each repository on the partner's own servers, then reports back
D. Secrets are shared with partners, who store a copy of each leaked value

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Provider notification means many leaked tokens are revoked before an attacker uses them, which is a meaningful safety net. It applies to public repositories, so private repository scanning depends on your own alerting and response.
</details>

---

### Question 12
**Scenario:** A custom CodeQL query must encode an organization-specific rule.

A. Ask GitHub support to add the rule to the default query suite for your organization
B. Use a regular expression in CI that fails the build when the banned pattern appears in a changed file
C. Not supported, because the query suites are fixed by GitHub and cannot be extended by any users of GitHub
D. Write a custom query or query pack in QL and include it in the code scanning configuration

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Custom queries let you encode internal rules such as banned APIs or required wrappers, with the same data flow capability as the built-in suites. Query packs make them distributable across repositories.
</details>

---

### Question 13
**Scenario:** A vulnerability is found in a repository's own code and must be fixed privately.

A. Open a public issue describing the flaw and how to reproduce it, so that users can mitigate it while a fix is being prepared
B. Email everyone who contributes to the repository with the details, so the fix is reviewed at once
C. A private repository security advisory, with a temporary private fork, then publish a CVE when the fix ships
D. Fix it silently in a normal commit and a normal pull request, and describe it only in the release notes

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Advisories provide private collaboration space until a fix is available, and publishing adds the advisory to the GitHub Advisory Database so downstream consumers get Dependabot alerts. A public issue tells attackers before users can patch.
</details>

---

### Question 14
**Scenario:** Alert volume from code scanning is high on a legacy codebase.

A. Fix all alerts before merging anything, so the repository starts from a clean state and stays that way
B. Dismiss everything as won't fix, so the list is empty and new alerts stand out clearly from the old ones
C. Disable scanning on the legacy repositories, then turn it back on for new code once the backlog is gone
D. Focus on new alerts from pull requests, set a severity threshold for blocking, and burn down the backlog on a plan

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Blocking on pre-existing findings stops all delivery and gets the tool turned off. Preventing new issues while scheduling the backlog is what teams actually sustain, and it means the trend improves from day one.
</details>

---

### Question 15
**Scenario:** GHAS licensing is described.

A. Advanced Security features are free on public repositories; private repositories require licensing, historically committer-based and now also available as separate Code Security and Secret Protection products
B. It is per repository, with a fee for each repository that has any of the features switched on
C. It is free for all repositories, public or private, on every plan, including the free plan for organizations
D. It is included in all plans at no cost, since the features are part of the base GitHub Enterprise subscription

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The distinction between public and private licensing is examinable, and the packaging has changed, so verify current terms before planning a rollout budget. Active committer counting is what drives cost in the committer-based model.
</details>

---

## Where to go deeper

- [GHAS cert page](../../exams/github/advanced-security/) - notes, practice plan, strategy
- [GitHub Actions practice questions](https://cloud.noblerworks.com/resources/practice-questions/github-actions/) - where scanning runs
- [GitHub Administration practice questions](https://cloud.noblerworks.com/resources/practice-questions/github-administration/) - enterprise rollout
- [Model supply chain security](https://ai.noblerworks.com/safety/security/model-supply-chain/) - the same reasoning applied to AI artifacts
- **[📖 GitHub Certifications](https://learn.github.com/certifications)** - official exam pages
