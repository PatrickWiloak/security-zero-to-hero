---
last-updated: 2026-10-22
difficulty: intermediate
---

# Microsoft Security Operations Analyst (SC-200) - Practice Questions

20 questions for SC-200 prep, weighted to the skills outline as of October 21, 2026: managing a security operations environment (40-45%), responding to security incidents (35-40%), and threat hunting (20-25%). Questions 16 to 20 cover the Sentinel platform and attack disruption.

> **Cert page:** [exams/azure/sc-200/](../../exams/azure/sc-200/)

---

### Question 1
**Scenario:** An analyst must find all sign-ins from a specific IP across the last 7 days in Microsoft Sentinel.

A. `SigninLogs | where IPAddress == "1.2.3.4" and TimeGenerated > ago(7d)`
B. `SigninLogs | search "1.2.3.4"`, relying on the portal time picker set to the last 7 days
C. Export the SigninLogs table to Excel through the portal and filter the IPAddress column there for 1.2.3.4
D. `search *` with the time picker set to 7 days, then filtering the results by IP in the grid

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Filtering the table with an explicit time range and an equality predicate is both correct and efficient, and putting the time filter early lets the engine prune partitions. A free-text `search` scans far more data for the same answer, and `search *` across all tables is the query you run once and never again.
</details>

---

### Question 2
**Scenario:** Which KQL operator joins alert data to enrichment data on a shared column?

A. `join` on the shared key column
B. `project`
C. `union`, which stacks the two result sets
D. `summarize`, which aggregates rows by group

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** `join` correlates two result sets on a key, with kinds such as `inner`, `leftouter`, and `leftanti`. `leftanti` is the one worth memorizing because it answers "which of these had no match," which is how you find first-time-seen behavior. `union` stacks rows, `summarize` aggregates, and `project` selects columns.
</details>

---

### Question 3
**Scenario:** A Defender for Endpoint alert shows a device with suspicious activity that must be cut off from the network but remain investigable.

A. Power it off remotely through the Defender portal so the attacker loses access immediately
B. Delete the device from the portal
C. Isolate the device, which blocks network traffic but keeps the Defender connection
D. Run a full antivirus scan only

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Isolation preserves the connection back to Defender so you can still run live response, collect an investigation package, and release it afterward. Powering off destroys volatile memory evidence and stops your telemetry. Deleting the device removes your visibility entirely.
</details>

---

### Question 4
**Scenario:** Sentinel should ingest AWS CloudTrail logs.

A. It is not possible
B. A syslog forwarder only
C. A data connector for AWS, configured with a role Sentinel can assume
D. Manual CSV upload

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Sentinel has first-party connectors for AWS, GCP, and many third-party sources; the AWS one uses a cross-account IAM role with an external ID. Being multicloud is a large part of why organizations pick Sentinel as the SIEM over a single-cloud tool.
</details>

---

### Question 5
**Scenario:** An analytics rule generates 400 alerts a day for the same benign administrative activity.

A. Tune it: add exclusions for the known-good identity or process, and consider grouping alerts
B. Increase the ingestion cap on the workspace so the repeated alerts no longer count against the daily quota and stop being dropped
C. Disable the rule
D. Ignore the alerts

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Alert fatigue is a real security failure, because analysts stop reading. Tuning keeps the detection while removing the known cause, and incident grouping collapses repeated alerts into one investigable unit. Disabling the rule outright loses coverage for the malicious version of the same behavior.
</details>

---

### Question 6
**Scenario:** A phishing email reached 50 mailboxes and must be removed from all of them.

A. A transport rule for future mail only, which quarantines any message matching the sender and subject from now on
B. Threat Explorer remediation in Defender for Office 365 (soft or hard delete)
C. Reset all 50 passwords and force each user to register MFA again on the next sign-in
D. Ask all 50 users to delete the message themselves and reply to confirm that they did

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Explorer finds the message across mailboxes and triggers remediation (zero-hour auto purge style removal) as a bulk action with an approval workflow. A transport rule stops the next one but does not touch mail already delivered. Password resets may still be warranted if credentials were entered, but they do not remove the message.
</details>

---

### Question 7
**Scenario:** Which Defender product protects against identity attacks such as Pass-the-Hash against on-premises Active Directory?

A. Defender for Cloud Apps, the CASB for SaaS
B. Defender for Identity
C. Defender for Office 365, the mail filter
D. Defender for Endpoint, the device agent

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Defender for Identity installs sensors on domain controllers and AD FS servers and detects reconnaissance, credential theft, and lateral movement techniques against AD DS. Defender for Endpoint covers devices, Cloud Apps covers SaaS usage, and Office 365 covers mail and collaboration.
</details>

---

### Question 8
**Scenario:** A user's session in a SaaS app should be blocked from downloading sensitive files on an unmanaged device.

A. An analytics rule that detects the download and automatically revokes the user's session once the alert fires
B. A retention label
C. Defender for Cloud Apps session policy with Conditional Access App Control
D. A NSG rule

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Conditional Access App Control proxies the session so Cloud Apps can inspect and block actions in real time, including download, upload, copy, and print. Conditional Access alone can allow or deny the sign-in but cannot control what happens inside an allowed session.
</details>

---

### Question 9
**Scenario:** An incident must trigger an automatic Teams message and ticket creation.

A. An automation rule invoking a Logic Apps playbook
B. A workbook
C. A watchlist
D. A hunting query

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Automation rules define when to act (incident created, updated, matching conditions) and playbooks are the Logic Apps that perform the actions. Workbooks visualize, hunting queries search proactively, and watchlists are reference data you join against.
</details>

---

### Question 10
**Scenario:** A hunting hypothesis is "an attacker used a rarely seen parent-child process pair." What is the right Sentinel feature?

A. A workbook
B. A hunting query, saved and promoted to an analytics rule once validated
C. A data connector that ingests process creation events from the endpoints into the workspace
D. An analytics rule scheduled every five minutes so the rare pair raises an incident as soon as it appears

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Hunting is hypothesis-driven searching that has not yet earned a detection, and the natural lifecycle is hunt, validate, then promote to a scheduled analytics rule. Creating an unvalidated analytics rule first usually produces the alert fatigue from question 5.
</details>

---

### Question 11
**Scenario:** Log ingestion costs are rising and much of the volume is verbose, low-value data needed only for occasional audit.

A. Reduce retention to one day on the whole workspace, so the verbose data is purged before it adds meaningfully to storage cost
B. Route it to a cheaper tier such as auxiliary or basic logs, or archive it
C. Sample the verbose data randomly at ingestion and keep only about one event in ten
D. Stop collecting it altogether and drop the connector that sends the verbose data

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Sentinel's tiering exists precisely for this: analytics tier for data your rules query, cheaper tiers plus search jobs and restore for data you need occasionally. Dropping the data or cutting retention to a day removes your ability to investigate a breach discovered weeks later, which is the common case.
</details>

---

### Question 12
**Scenario:** During triage you need to see the full attack story: which device, which user, which files, in sequence.

A. Compliance Manager
B. Secure Score
C. The incident graph and the unified incident timeline in the Defender portal
D. The raw table

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Incident correlation stitches related alerts across Defender workloads and Sentinel into one incident with entities and a timeline, which is the difference between a pile of alerts and an attack narrative. Raw tables are where you go for detail after you know what to look at.
</details>

---

### Question 13
**Scenario:** A device group should get a more aggressive attack surface reduction rule set than the rest of the estate.

A. Conditional Access
B. A single tenant-wide policy set to the most aggressive level, applied to every device in the estate
C. A firewall rule
D. Device groups in Defender for Endpoint with a targeted ASR policy

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Device groups let you scope policy and also scope analyst permissions by group. Rolling ASR rules out in audit mode to a pilot group first, then enforcing, is the standard approach because some rules break legitimate line-of-business software.
</details>

---

### Question 14
**Scenario:** After containment, what should close out the incident process?

A. Reboot the affected servers and restore the previous day's snapshot, then close the ticket once users confirm
B. Delete the incident
C. Nothing further, because containment has stopped the attack and the ticket can simply stay open
D. Eradication and recovery, then a post-incident review that turns gaps into new rules

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The standard lifecycle is preparation, detection and analysis, containment, eradication, recovery, and lessons learned. The last stage is where a SOC actually improves: each incident should leave behind a new detection, a tuned rule, or a closed gap. Deleting the incident destroys the record you need for that.
</details>

---

### Question 15
**Scenario:** A rule must detect five failed sign-ins followed by a success from the same account within 10 minutes.

A. A Microsoft incident creation rule that turns alerts from other Microsoft security products into Sentinel incidents
B. A watchlist
C. A workbook charting failed and successful sign-ins per account over the last ten minutes, refreshed hourly
D. A scheduled analytics rule with a KQL query that uses `summarize` and a `join` for the success

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Scheduled rules run KQL on an interval with a lookback window, which is where you express multi-event logic like this. A Microsoft incident creation rule (A) only turns alerts that other products already raised into incidents, so it cannot count sign-ins over a window. Workbooks and watchlists do not generate incidents.
</details>

---

### Question 16
**Scenario:** A company ingests 400 GB per day of firewall logs. Auditors require three years of retention. The SOC does not need real-time detection on raw firewall rows, but wants an alert when a host's outbound volume spikes. Cost must be minimized.

A. Keep the firewall table in the analytics tier with three years of analytics retention and a scheduled analytics rule on the raw table
B. Send the firewall table to the data lake tier with three years of total retention, and run a summary rule that aggregates outbound volume per host into an analytics table for the detection
C. Stop ingesting firewall logs into Sentinel and export them to a storage account, then restore them when auditors ask
D. Ingest the firewall logs into the XDR default tier, which keeps them for three years at no cost

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The data lake tier gives cheap long-term retention, and a summary rule turns the high-volume table into a small analytics table that a detection can run on. Three years in the analytics tier is the expensive option the tiers exist to avoid, exporting outside Sentinel loses the summary-based detection, and the XDR default tier holds Defender advanced hunting data for 30 days, not third-party logs for years.
</details>

---

### Question 17
**Scenario:** During an investigation, an analyst needs eight-month-old DNS records for one host, which now live only in the Sentinel data lake tier. The records must be available to existing hunting queries and analytics rules.

A. Run a KQL job that queries the data lake for that host's DNS records and writes the results to an analytics-tier table
B. Move the entire DNS table to the analytics tier permanently so that all of its data is hot
C. Create a scheduled analytics rule that runs directly against the data lake tier table
D. Open a livestream session in Sentinel hunting for the DNS table

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** KQL jobs promote a slice of lake data into the analytics tier, where hunting and analytics rules work. Real-time analytics rules do not run on lake-tier tables, moving the whole table to the analytics tier pays hot-tier prices for every future row when only one host's history was needed (and the documented way to bring lake data back is a KQL or notebook job), and livestream watches incoming events, not eight-month-old ones.
</details>

---

### Question 18
**Scenario:** Human-operated ransomware is moving laterally at 2 a.m. Defender XDR correlates high-confidence signals from endpoint and identity. The SOC wants containment to begin without waiting for an analyst, while one legacy production controller must never be isolated automatically.

A. Create a Sentinel playbook that emails the on-call analyst and waits for approval before any action
B. Lower all alert severities to informational so that no automated investigation starts on the controller
C. Turn off automated investigation and response for the whole tenant to protect the controller
D. Rely on automatic attack disruption, with the controller's device group excluded from automated containment

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Automatic attack disruption contains devices and users on its own when correlated signals show a high-confidence attack, and exclusions keep specific assets out of automated containment. Waiting for approval defeats the 2 a.m. requirement, and changing severities or disabling automation tenant-wide removes protection from everything else.
</details>

---

### Question 19
**Scenario:** An app registration was compromised and a client secret was added. Entra audit logs show the secret being added. The investigator now needs to know which Microsoft Graph API calls the app made afterward, from which IP addresses.

A. Defender for Identity alerts on the domain controllers
B. Microsoft Graph activity logs, enabled through Microsoft Entra diagnostic settings
C. The Microsoft Entra sign-in logs for interactive users
D. Content search in Microsoft Purview eDiscovery

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Graph activity logs record the requests made to Microsoft Graph, including the calling app, the request, and the source IP, which scopes what the stolen secret was used for. Defender for Identity watches on-premises Active Directory, interactive sign-in logs cover users rather than app API calls, and Content search finds content, not API activity.
</details>

---

### Question 20
**Scenario:** A SOC manager wants to find Sentinel tables the company pays to ingest that no analytics rule uses, and to see which detections are missing for adversary-in-the-middle phishing.

A. SOC optimization recommendations
B. The Sentinel threat intelligence blade
C. Microsoft Secure Score in the Defender portal
D. A workbook built on the Usage table only

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** SOC optimization produces data value recommendations for unused ingested tables and threat-based coverage recommendations for attack scenarios such as AiTM. Secure Score measures configuration posture, the threat intelligence blade manages indicators, and a Usage workbook shows volume but not detection coverage.
</details>

---

## Where to go deeper

- [SC-200 cert page](../../exams/azure/sc-200/) - notes, practice plan, strategy
- [SC-900 practice questions](./azure-security-compliance-identity-sc-900.md) - the fundamentals below this
- [SC-100 practice questions](./azure-cybersecurity-architect-sc-100.md) - the architecture exam above it
- [AZ-500 practice questions](./azure-security-az-500.md) - the platform security counterpart
- **[📖 SC-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-200)** - official skills outline
