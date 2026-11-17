# GitHub Advanced Security - Exam-Style Scenarios

## Scenario 1: Licensing and Active Committers

### Scenario
A company has 500 developers in its GitHub enterprise. Only 120 of them have pushed to any GHAS-enabled private repo in the last 90 days. Another 80 have pushed only to public repos where code scanning is enabled.

**Question:** How many GHAS seats are consumed?

**Options:**
A. 500
B. 200
C. 120
D. 0

**Correct Answer:** C

**Explanation:**
GHAS is licensed per active committer, defined as a user who has pushed a commit in the last 90 days to a GHAS-enabled private repository. Public repo committers do not consume a seat. The answer is 120.

**Why other options are wrong:**
- **A:** All 500 would only count if they were all active committers to GHAS private repos.
- **B:** Public repo activity does not count.
- **D:** Some committers exist; seats are being used.

---

## Scenario 2: Default vs Advanced Setup

### Scenario
A team wants to enable code scanning quickly on 40 repos without writing any workflow YAML. They want GitHub to handle language detection and scanning schedule automatically.

**Question:** Which setup should they use?

**Options:**
A. Advanced setup with a `codeql.yml` workflow in each repo
B. Default setup applied via a security configuration at the org level
C. A manual SARIF upload script per repo
D. Disable code scanning and use a third-party SAST only

**Correct Answer:** B

**Explanation:**
Default setup auto-detects languages, runs CodeQL on push/PR/weekly schedule, and requires no YAML. Combined with a security configuration at the org level, it can be applied to many repos quickly.

**Why other options are wrong:**
- **A:** Advanced setup requires writing and maintaining YAML.
- **C:** SARIF uploads require external tools and scripts.
- **D:** Disabling scanning does not meet the goal.

---

## Scenario 3: CodeQL Query Suite Selection

### Scenario
A security team wants stronger security checks than the default, but they do not want code quality (non-security) alerts cluttering their backlog.

**Question:** Which CodeQL query suite should they choose?

**Options:**
A. `code-scanning`
B. `security-extended`
C. `security-and-quality`
D. `code-quality-only`

**Correct Answer:** B

**Explanation:**
`security-extended` adds lower-precision security queries on top of the default `code-scanning` suite but does NOT add quality queries. `security-and-quality` would add both.

**Why other options are wrong:**
- **A:** Default set; they want more security coverage.
- **C:** Adds quality alerts they do not want.
- **D:** Not a valid suite name.

---

## Scenario 4: Secret Scanning Custom Pattern

### Scenario
An organization uses a proprietary API token format: `INTX-` followed by 32 hex characters. They want GitHub to detect these tokens in all repositories.

**Question:** How should they configure this?

**Options:**
A. Submit the token format to GitHub as a partner pattern
B. Define a custom secret scanning pattern at the organization level with the appropriate regex
C. Write a GitHub Action that greps for the token on every push
D. Wait for GitHub to auto-detect it as a non-provider pattern

**Correct Answer:** B

**Explanation:**
Custom patterns are for customer-defined token formats. They can be scoped at repo, org, or enterprise level. Partner patterns are for vendor-supplied tokens (AWS, Stripe, etc.) and require GitHub partner enrollment.

**Why other options are wrong:**
- **A:** Partner patterns are for service providers, not internal tokens.
- **C:** A grep action is not integrated with secret scanning alerts or push protection.
- **D:** Non-provider patterns cover generic credentials; they would not reliably match a specific proprietary format.

---

## Scenario 5: Push Protection Bypass

### Scenario
A developer attempts to push a commit containing an API key used only in test fixtures. Push protection blocks the commit.

**Question:** What is the correct next step, assuming the key is intended for tests and cannot be removed?

**Options:**
A. Force push with `--no-verify` to bypass
B. Disable secret scanning on the repo temporarily
C. Bypass push protection with the reason "used in tests" so the alert is recorded
D. Rename the variable holding the key

**Correct Answer:** C

**Explanation:**
Push protection supports bypass with a reason. "Used in tests" is one of the standard reasons. The bypass is audited and the alert is recorded. This preserves visibility without blocking legitimate workflows.

**Why other options are wrong:**
- **A:** `--no-verify` does not bypass server-side push protection.
- **B:** Disabling secret scanning is overly broad and risky.
- **D:** Renaming the variable does not change the detected secret content.

---

## Scenario 6: Dependabot Configuration

### Scenario
A repository with a Node.js frontend and a Python backend wants weekly updates for both ecosystems. They also want daily updates for GitHub Actions versions.

**Question:** Which `dependabot.yml` configuration is correct?

**Options:**

A.
```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    schedule:
      interval: "weekly"
  - package-ecosystem: "pip"
    schedule:
      interval: "weekly"
  - package-ecosystem: "github-actions"
    schedule:
      interval: "daily"
```
(with `directory` fields missing)

B.
```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/frontend"
    schedule:
      interval: "weekly"
  - package-ecosystem: "pip"
    directory: "/backend"
    schedule:
      interval: "weekly"
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "daily"
```

C.
```yaml
version: 1
ecosystems:
  npm: weekly
  pip: weekly
  actions: daily
```

D.
```yaml
version: 2
updates:
  - ecosystem: "all"
    schedule: "weekly"
```

**Correct Answer:** B

**Explanation:**
`dependabot.yml` requires `version: 2`, `package-ecosystem`, `directory`, and `schedule.interval` per update entry. Option B correctly configures three ecosystems with paths and schedules.

**Why other options are wrong:**
- **A:** Missing required `directory` field per entry.
- **C:** Uses invalid version and schema.
- **D:** Not a valid Dependabot schema.

---

## Scenario 7: Security vs Version Updates

### Scenario
A team wants Dependabot to open PRs when a known CVE is published for one of their dependencies, but they do NOT want scheduled version bumps otherwise.

**Question:** What should they enable?

**Options:**
A. Only Dependabot version updates (via `dependabot.yml`)
B. Only Dependabot security updates
C. Both version and security updates
D. Neither; use dependency review instead

**Correct Answer:** B

**Explanation:**
Dependabot security updates automatically open PRs to fix vulnerable dependencies when a CVE is published. Version updates (configured via `dependabot.yml`) are schedule-driven and unrelated to vulnerabilities.

**Why other options are wrong:**
- **A:** Version updates do not respond to CVEs; they run on schedule.
- **C:** Adds unwanted scheduled bumps.
- **D:** Dependency review is a PR-time check, not a mechanism for opening remediation PRs.

---

## Scenario 8: Dependency Review Action

### Scenario
A team wants to block PRs that introduce new dependencies with high or critical severity vulnerabilities, or that use GPL-3.0 license.

**Question:** Which workflow step accomplishes this?

**Options:**

A.
```yaml
- uses: actions/dependency-review-action@v4
  with:
    fail-on-severity: high
    deny-licenses: GPL-3.0
```

B.
```yaml
- uses: github/codeql-action/init@v3
  with:
    block-severity: high
```

C.
```yaml
- run: dependabot check --severity high
```

D.
```yaml
- uses: actions/cve-check@v1
  with:
    level: high
```

**Correct Answer:** A

**Explanation:**
`actions/dependency-review-action` is the official action for PR-time dependency gating. It supports `fail-on-severity` and `deny-licenses` inputs.

**Why other options are wrong:**
- **B:** CodeQL init is for code scanning, not dependency gating.
- **C:** Not a valid Dependabot CLI.
- **D:** Not a real action.

---

## Scenario 9: Repository Security Advisory Workflow

### Scenario
A maintainer receives a private report of a vulnerability in their library. They want to fix it privately, request a CVE, and publish the advisory once a fix is released.

**Question:** Which sequence of actions is correct?

**Options:**
A. Open a public issue immediately, fix in main, publish a blog post
B. Draft a repository security advisory, open a private fork for the fix, request a CVE, release the fix, publish the advisory
C. Email affected users directly and skip GitHub advisories entirely
D. Publish the advisory first, then work on a fix publicly

**Correct Answer:** B

**Explanation:**
This is the standard coordinated disclosure flow for GitHub repository security advisories: draft privately, use a private fork, request a CVE through GitHub, release the fix, then publish.

**Why other options are wrong:**
- **A:** Public disclosure before a fix exposes users to attack.
- **C:** Skipping advisories prevents Dependabot consumers from receiving alerts.
- **D:** Publishing first defeats the purpose of coordinated disclosure.

---

## Scenario 10: Validity Checks

### Scenario
Secret scanning detects a Stripe live API key in a repository. The team wants to know whether this key is still active so they can prioritize remediation.

**Question:** Which feature answers this?

**Options:**
A. CodeQL alert severity
B. Secret scanning validity checks
C. Dependabot alerts
D. Security configurations

**Correct Answer:** B

**Explanation:**
Validity checks verify detected tokens against supported partners' APIs to determine if the token is still active. The alert will show Active or Inactive where supported.

**Why other options are wrong:**
- **A:** CodeQL does not assess secret validity.
- **C:** Dependabot covers dependencies, not secrets.
- **D:** Security configurations enable features; they do not verify token validity.

---

## Scenario 11: Security Overview and Reporting

### Scenario
A CISO wants a consolidated view of all open code scanning, secret scanning, and Dependabot alerts across 200 repos in an org, filterable by severity.

**Question:** What should they use?

**Options:**
A. The Insights tab on every repo individually
B. The organization Security Overview dashboard
C. A custom Dependabot dashboard
D. The repo Issues tab filtered by label

**Correct Answer:** B

**Explanation:**
Security Overview is the org and enterprise dashboard consolidating alerts across repositories, with filters for severity, feature, and coverage.

**Why other options are wrong:**
- **A:** Per-repo Insights does not consolidate across repos.
- **C:** No such product.
- **D:** Issues are unrelated to security alerts.

---

## Scenario 12: SARIF Upload

### Scenario
A team uses Semgrep for JavaScript scanning alongside CodeQL. They want Semgrep results to appear in the Security tab alongside CodeQL alerts.

**Question:** What should they do?

**Options:**
A. Replace CodeQL with Semgrep; only one tool can feed the Security tab
B. Generate a SARIF file from Semgrep and upload it via `github/codeql-action/upload-sarif`
C. Write a custom GitHub App to ingest Semgrep results
D. Use the Semgrep web UI; the Security tab cannot accept external tools

**Correct Answer:** B

**Explanation:**
Code scanning supports SARIF uploads from any compatible tool using `github/codeql-action/upload-sarif`. Multiple tools can feed the Security tab simultaneously, each with distinct rule IDs.

**Why other options are wrong:**
- **A:** Multiple tools can coexist.
- **C:** Unnecessary; upload-sarif already exists.
- **D:** The Security tab does accept external SARIF uploads.

---

## Scenario 13: Copilot Autofix for Code Scanning

### Scenario
A team has CodeQL running on every pull request. Developers say they spend too long working out how to fix each new alert. The security lead turns on Copilot Autofix. A manager asks what will change.

**Question:** Which statement about Copilot Autofix is correct?

**Options:**
A. It commits fixes straight to the default branch with no review step
B. It suggests fixes for alerts from any SARIF-uploading tool, such as Semgrep
C. It suggests a fix for CodeQL alerts, and a developer must review and accept the change before it is applied
D. It only works if every developer in the repo has a paid GitHub Copilot seat

**Correct Answer:** C

**Explanation:**
Copilot Autofix generates fix suggestions for CodeQL alerts found on pull requests and on the default branch. On a pull request the suggestion shows as an inline suggested change. On the default branch it shows on the alert page. Every suggestion is a proposed code change that a developer must review and accept. Treat AI-written fixes like any other code: check that they are correct and do not add new problems.

**[📖 Application card: GitHub security and quality AI features](https://docs.github.com/en/code-security/code-scanning/managing-code-scanning-alerts/responsible-use-autofix-code-scanning)** - What Copilot Autofix does and its limits

**Why other options are wrong:**
- **A:** Nothing is applied without a developer accepting it.
- **B:** Autofix is available for CodeQL analysis, not third-party tools.
- **D:** GitHub's docs state that Autofix for CodeQL does not require a GitHub Copilot subscription.

---

## Scenario 14: Blocking Merges on Code Scanning Results

### Scenario
An org wants pull requests to `main` blocked when CodeQL finds a new security alert of high or critical severity. Lower-severity alerts should still show up but should not block the merge.

**Question:** What is the best way to enforce this?

**Options:**
A. Ask reviewers to check the Security tab before they approve
B. Add a `fail-on-severity: high` input to `github/codeql-action/analyze`
C. Turn on secret scanning push protection for the repo
D. Create a branch ruleset with "Require code scanning results", pick CodeQL as the tool, and set the security alerts threshold to "High or higher"

**Correct Answer:** D

**Explanation:**
Code scanning merge protection is set with a ruleset. The "Require code scanning results" rule lets you pick the required tools and set two thresholds. "Alerts" covers non-security results (None, Errors, Errors and Warnings, All). "Security alerts" covers security severity (None, Critical, High or higher, Medium or higher, All). The rule blocks a merge when a required tool finds an alert at or above the threshold, when its analysis is still running, or when the tool is not set up for the repo. Without a ruleset, a classic branch protection rule can still make the code scanning check a required status check. That check fails on `error`, `critical` or `high` results by default, and you can change that level in the repo settings.

**[📖 Set code scanning merge protection](https://docs.github.com/en/code-security/code-scanning/managing-your-code-scanning-configuration/set-code-scanning-merge-protection)** - The ruleset rule and its threshold options

**Why other options are wrong:**
- **A:** A manual check is not enforced and is easy to skip.
- **B:** No such input exists on the CodeQL action.
- **C:** Push protection blocks secrets in pushes. It does not gate merges on code scanning alerts.

---

## Scenario 15: Delegated Bypass for Push Protection

### Scenario
A bank has push protection on across its org. Audit logs show developers often bypass blocks themselves by picking "I'll fix it later". Compliance wants a security team to approve every bypass first.

**Question:** What should the org admin configure?

**Options:**
A. Delegated bypass for push protection, with the security team on the bypass list
B. A pre-commit hook that rejects any commit message containing "bypass"
C. Turn off push protection and rely on secret scanning alerts instead
D. Remove write access from all developers

**Correct Answer:** A

**Explanation:**
Delegated bypass stops contributors from bypassing push protection on their own. Roles and teams on the bypass list can still bypass and they review requests. Everyone else must submit a bypass request when a push is blocked. Requests expire after 7 days. Delegated bypass can be set at the repo, org or enterprise level. Secret teams can't be added to the bypass list. Requests and reviewer decisions are recorded in the audit log.

**[📖 Enabling delegated bypass for push protection](https://docs.github.com/en/code-security/secret-scanning/using-advanced-secret-scanning-and-push-protection-features/delegated-bypass-for-push-protection/enabling-delegated-bypass-for-push-protection)** - Setting up the bypass list and reviewers

**Why other options are wrong:**
- **B:** Push protection is server-side. A local hook does not control GitHub's bypass flow, and developers can skip it.
- **C:** This makes the problem worse. Secrets would reach the repo before anyone sees them.
- **D:** Developers could no longer push at all. The goal is to review bypasses, not stop all work.

---

## Scenario 16: Dismissing Code Scanning Alerts

### Scenario
A developer reviews three open CodeQL alerts:
1. A SQL injection alert on code where the input is already a fixed constant, so it can never be attacker-controlled.
2. A hard-coded password alert in a test fixture that only runs in CI.
3. An alert in a legacy module due to be deleted next quarter. The team accepts the risk until then.

**Question:** Which dismissal reasons fit alerts 1, 2 and 3?

**Options:**
A. Won't fix, False positive, Used in tests
B. False positive, Used in tests, Won't fix
C. Used in tests, Won't fix, False positive
D. False positive, False positive, False positive

**Correct Answer:** B

**Explanation:**
When you dismiss a code scanning alert you must give a reason. "False positive" means the alert is wrong: the code is not actually vulnerable. "Used in tests" means the code only exists for testing. "Won't fix" means the issue is real but the team has accepted it and will not fix it. The reason matters for reporting: "won't fix" records accepted risk, while "false positive" records that there was no risk. GitHub's docs also say the reason may affect whether a query stays in future analysis. Add a dismissal comment, which can be used as justification during auditing and reporting. A dismissed alert moves to the closed list, where it can be reopened.

**[📖 Triaging code scanning alerts in pull requests](https://docs.github.com/en/code-security/code-scanning/managing-code-scanning-alerts/triaging-code-scanning-alerts-in-pull-requests)** - Dismissing alerts and why the reason matters

**Why other options are wrong:**
- **A:** Alert 1 is not a real issue, so "won't fix" is wrong. Alert 2 is test code, not a false positive.
- **C:** The reasons are shifted. Alert 3 is a real, accepted risk, not a false positive.
- **D:** Only alert 1 is a false positive. Calling real issues false positives hides accepted risk from reporting.
