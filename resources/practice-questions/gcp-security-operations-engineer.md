---
last-updated: 2026-11-07
---

# Google Cloud Professional Security Operations Engineer - Practice Questions

28 original scenario questions weighted to the six sections of the exam guide: Platform operations (~14%) 4 questions, Data management (~14%) 4, Threat hunting (~19%) 5, Detection engineering (~22%) 6, Incident response (~21%) 6 and Observability (~10%) 3. These are original questions, not vendor exam content.

> **Cert page:** [exams/gcp/security-operations-engineer/](../../exams/gcp/security-operations-engineer/)

---

### Question 1 - Section 1: Platform operations
**Scenario:** A security team needs staff at partner companies to reach Google Cloud security tools through single sign-on using each partner's own identity provider, without copying those users into Google-managed accounts. What should they configure?

A. Workforce Identity Federation with OIDC or SAML 2.0
B. Google Cloud Directory Sync from each partner directory
C. A shared service account key given to every partner analyst
D. Cloud Identity accounts created manually for each partner user

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Workforce Identity Federation lets an external identity provider authenticate workforce users via OIDC or SAML 2.0 and avoids synchronising identities. Directory sync copies accounts, and shared keys destroy accountability.
</details>

---

### Question 2 - Section 1: Platform operations
**Scenario:** An investigation needs to show who read records in a Cloud Storage bucket last month, but no read events appear in Cloud Audit Logs. What is the most likely reason?

A. Data Access audit logs were not enabled for the service, since they are off by default except for BigQuery
B. System Event logs replace Data Access logs automatically in newer Google Cloud projects
C. Policy Denied logs overwrite read events whenever they are turned on for the same project
D. Admin Activity logs expire after one week and can never be exported for analysis

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Data Access logs record reads of user data and are off by default for all services except BigQuery, so they must be enabled in advance. Admin Activity logs record configuration changes, not data reads.
</details>

---

### Question 3 - Section 1: Platform operations
**Scenario:** A team runs two tools that both detect threats on virtual machines. A manager asks whether to keep both. What is the best way to justify keeping an overlapping tool?

A. Remove the tool with fewer alerts, on the grounds that fewer alerts must mean less noise for analysts
B. Show a requirement that each tool uniquely satisfies and the coverage gap if one is removed
C. Keep whichever tool is cheaper without comparing what each one detects or where they differ
D. Argue that more tools always produce better security outcomes, so every overlapping tool should stay

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Overlap is justified by requirements: what each tool covers that the other does not and what gap its removal creates. Counting tools or alerts says nothing about coverage.
</details>

---

### Question 4 - Section 1: Platform operations
**Scenario:** Which Google service writes findings about misconfigurations, vulnerabilities and threats in Google Cloud resources and supports posture management?

A. Security Command Center
B. Looker Studio
C. Cloud Monitoring uptime checks
D. Google Cloud Directory Sync

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Security Command Center produces findings from built-in services such as Security Health Analytics and Event Threat Detection and supports posture management. The others report, monitor availability or synchronise directories.
</details>

---

### Question 5 - Section 2: Data management
**Scenario:** Detections that rely on the target user field have stopped working for one log source after a vendor update. Health Hub shows parser errors rising. What should the engineer do first?

A. Rewrite every rule that uses the target user field so that it matches against raw log text instead
B. Lower the severity of the affected rules so that fewer analysts are paged for the missing field
C. Disable the log source until the vendor releases an official fix for the changed log format
D. Create a parser extension that maps the new field to the UDM field and test it with samples

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The problem is normalisation, so fix the mapping with a parser extension and test it. Rewriting rules to use raw text is brittle, and disabling the source or lowering severity hides the failure.
</details>

---

### Question 6 - Section 2: Data management
**Scenario:** An analyst wants to know whether a logged-in account belongs to a privileged finance user. Which kind of data supplies this?

A. The firewall log of the connection that followed
B. The audit log that lists which API methods were called
C. Event data from a single login log entry
D. Entity data, such as organisational context for the user

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Entity data describes users and assets and their attributes (role, department, privilege). Event data records that something happened but not what the user is.
</details>

---

### Question 7 - Section 2: Data management
**Scenario:** Two sources identify the same laptop, one by hostname and one by IP address. How can the platform combine their activity into one picture?

A. Aliasing fields so event and entity data match across identifiers
B. Renaming the hostname in the source logs by hand every day
C. Deleting the IP-based source because it is less precise
D. Running a retrohunt with alerting enabled on both sources

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Aliasing links different identifiers for the same entity so events and context can be matched. Renaming by hand or deleting a source does not scale or loses data.
</details>

---

### Question 8 - Section 2: Data management
**Scenario:** The finance team complains about logging costs after Data Access audit logs and flow logs were enabled everywhere. What is the most appropriate approach?

A. Keep ingesting everything from every source because storage in the cloud is described as cheap
B. Cut the number of log sources down to a smaller set chosen at random by the platform team
C. Ingest what supports detections, investigations or compliance, filter low-value events and keep verbose logs in cheaper storage
D. Turn off all audit logging across the organization so that the logging cost disappears entirely

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Manage cost by justifying each source, filtering noise and tiering storage, while keeping what detections need. Turning off logging or ingesting everything are both poor trade-offs.
</details>

---

### Question 9 - Section 3: Threat hunting
**Scenario:** A hunter needs to run SQL aggregations over a large volume of audit logs to find service accounts calling an unusual number of distinct APIs over 30 days. Which tools suit this?

A. Cloud Monitoring uptime checks configured against each service account in the organization
B. A manual review of console screenshots collected by each project owner over the month
C. Log Analytics or BigQuery
D. A single quick filter in the Logs Explorer for one resource

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Log Analytics and BigQuery provide SQL over large datasets for aggregation and trend analysis. Logs Explorer is suited to quick searches on known resources.
</details>

---

### Question 10 - Section 3: Threat hunting
**Scenario:** Intelligence reports a malicious domain used by a campaign that began three weeks ago. What should the team do first with the indicator?

A. Delete DNS logs older than a week to limit the exposure of the organization to disclosure
B. Search retained telemetry for the domain across the last three weeks
C. Wait for the vendor to release a curated detection that happens to cover the domain
D. Add it to a rule that only evaluates events arriving from tomorrow onwards and stop there

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** New indicators must be applied to historical data to find activity that predated them. Forward-only rules miss the earlier period, and deleting logs destroys evidence.
</details>

---

### Question 11 - Section 3: Threat hunting
**Scenario:** A team wants to run an existing YARA-L rule's logic over the last two weeks of data. What should they do to avoid flooding the case queue?

A. Run a retrohunt with the rule's alerting status disabled
B. Run the retrohunt with alerting enabled so that every old match opens a case immediately
C. Copy the rule to a new rule and enable alerting on both of the rules at the same time
D. Run the retrohunt over a time range that is smaller than the rule's match window

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A retrohunt with alerting enabled creates an alert for every historical detection, so the documentation recommends disabling alerting for the run. For multi-event rules, the range must be at least the match window.
</details>

---

### Question 12 - Section 3: Threat hunting
**Scenario:** A hunter notices a user with a steadily rising risk score from many small detections. How should the score be used?

A. As a replacement for reading the underlying detections
B. As proof that the user is malicious and the account should be deleted
C. As a prioritisation signal for whom to hunt first, verified against evidence
D. As a number that can be ignored because scores are always wrong

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Entity risk score highlights anomalous behaviour and helps prioritise, but it accumulates from rules that may be noisy, so verify. It is not proof or a replacement for analysis.
</details>

---

### Question 13 - Section 3: Threat hunting
**Scenario:** Which hunting hypothesis is specific and testable?

A. As a full replacement for reading the underlying detections that produced the number
B. As proof that the user is malicious, so the account should be deleted straight away
C. A stolen service account key will be used from an unusual network to list storage buckets
D. As a number that can safely be ignored because risk scores are always unreliable

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A testable hypothesis names a behaviour and data that can confirm or refute it. The others are too vague to turn into a search.
</details>

---

### Question 14 - Section 4: Detection engineering
**Scenario:** Which YARA-L section calculates additional values, such as a risk score, for each detection?

A. options
B. meta
C. events
D. outcome

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The outcome section calculates extra values for each detection, such as risk scores. Meta holds descriptive details, events selects UDM events and options sets rule settings.
</details>

---

### Question 15 - Section 4: Detection engineering
**Scenario:** A rule must alert when at least five blocked logins are followed by an allowed login for the same user within ten minutes. Which rule type is needed?

A. A rule with only a meta section and an author
B. A reference list of usernames with no rule logic
C. A multi-event rule with a match window grouped by user
D. A single-event rule with no match section

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Counting events across a time window grouped by a variable needs a multi-event rule with a match section. A single-event rule evaluates one event at a time.
</details>

---

### Question 16 - Section 4: Detection engineering
**Scenario:** The security team wants a rule to flag connections from a set of high-risk IPv4 ranges that is updated weekly without editing the rule. Which feature fits?

A. Hard-coded address ranges in the events section
B. A CIDR reference list referenced with the in operator
C. A regex list of hostnames for the ranges
D. A string reference list of individual addresses written as exact text

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A CIDR reference list tests whether an IP falls within listed ranges and can be updated without editing the rule. Hard-coded values require rule changes, and string lists require exact matches.
</details>

---

### Question 17 - Section 4: Detection engineering
**Scenario:** Security Health Analytics findings show a firewall rule opened a sensitive port to the internet. Which detection design addresses posture changes like this?

A. A rule containing only a meta section with an author and a description of the goal
B. A single-event rule with no match section that evaluates each login event on its own
C. A reference list of usernames with no rule logic attached to it at all
D. A detection or posture control that alerts on the change from the baseline and routes it to the owner

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Posture changes are best detected as drift from a baseline using SCC Security Health Analytics, posture management and SecOps rules, with routing to the owner. Quarterly reviews are too slow and blocking all changes is impractical.
</details>

---

### Question 18 - Section 4: Detection engineering
**Scenario:** A rule fires thousands of times a week, mostly for one backup server's service account. What is the best tuning action?

A. Hard-coded address ranges typed into the events section of every rule that needs them
B. A string reference list of individual addresses written as exact, case-sensitive text values
C. A regex list of hostnames that are believed to belong to the same address ranges
D. Exclude that known-good entity precisely and keep the rule for everyone else

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Tune with a precise exclusion and a recorded exception, keeping coverage for others. Deleting the rule or disabling classes of accounts creates blind spots.
</details>

---

### Question 19 - Section 4: Detection engineering
**Scenario:** Which SCC capability lets you raise a finding when specific bad IP addresses or domains appear in the logs it reads?

A. Event Threat Detection custom detectors for IOCs
B. Workforce Identity Federation attribute mapping
C. Looker Studio scheduled reports
D. Cloud Audit Logs Data Access logging

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Event Threat Detection supports custom detectors, using module templates, to detect specific IOCs and write findings. The other options report, record or authenticate.
</details>

---

### Question 20 - Section 5: Incident response
**Scenario:** Analysts confirm a compromised service account is exfiltrating data from a production project. Which action best contains it while preserving evidence?

A. A rule that blocks every firewall change made by every engineer in the organization
B. Restrict or disable the service account's access and keys, snapshot affected disks, and keep the logs
C. A detection that ignores configuration changes and reads only endpoint logs from the hosts
D. A manual quarterly review of every firewall rule by the networking team and an auditor

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Containment should stop the harm reversibly while preserving evidence: restrict the credential, snapshot disks and retain logs. Deleting the project or rebooting destroys evidence, and waiting extends exposure.
</details>

---

### Question 21 - Section 5: Incident response
**Scenario:** Which playbook steps are the best candidates for full automation?

A. Shutting down all virtual machines in a folder
B. Reputation lookups, enrichment and ticket creation
C. Deleting user mailboxes after a phishing alert
D. Disabling a production database service account on any single alert

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Frequent, well understood, low-risk steps such as enrichment and ticket creation suit automation. Disruptive actions should have manual approval or high-confidence triggers.
</details>

---

### Question 22 - Section 5: Incident response
**Scenario:** In Google SecOps SOAR, what is the relationship between a case and an alert?

A. An alert is the top-level container holding one or more cases
B. They are the same object with two names
C. A case is the top-level container holding one or more alerts
D. A case is a single event inside an alert

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A case is the top-level container composed of one or more alerts ingested from various sources, and an alert is a notification containing one or more security events.
</details>

---

### Question 23 - Section 5: Incident response
**Scenario:** A playbook needs an analyst to approve disabling an account before it continues. Which feature provides this?

A. Change nothing at all until the root cause analysis report has been finished and approved
B. A manual action that pauses the playbook until completed or skipped
C. Reboot every instance in the project to clear memory and remove anything the attacker started
D. Delete the project immediately so that all activity in it stops at once and nothing remains

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A manual action pauses the playbook until an analyst completes or skips it and appears in the Pending Actions widget.
</details>

---

### Question 24 - Section 5: Incident response
**Scenario:** Cases are often delayed when they pass between shifts. What improves the case management life cycle?

A. A handoff template with summary, evidence, actions taken, open tasks and next owner
B. Shutting down every virtual machine in a folder as soon as one alert is raised
C. Deleting the mailboxes of users who received a phishing message before anyone reviews them
D. Disabling a production database service account whenever any single alert mentions it

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A structured handoff lets the receiving analyst continue without rework. Hiding history, auto-closing and funnelling to one person create delays or lost information.
</details>

---

### Question 25 - Section 5: Incident response
**Scenario:** After an incident, the cause is an over-permissioned account that SCC had flagged for weeks. What is the proper outcome of root cause analysis?

A. Corrective changes to permissions and a process that routes such findings to owners with deadlines
B. A case is a single event inside an alert, such as one log line from one source
C. They are the same object, and the two names are used interchangeably in the interface
D. An alert is the top-level container holding one or more cases that were opened by analysts

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Root cause analysis should lead to a fix and a process change, not blame. Disabling the tool removes the signal.
</details>

---

### Question 26 - Section 6: Observability
**Scenario:** Which dashboard metric best indicates that a detection programme is producing too much noise?

A. A dashboard widget that shows the total number of cases that were closed this quarter
B. A longer playbook trigger window so the playbook waits before it runs the next action
C. A second playbook that has the same name as the first one and runs at the same time
D. False positive rate and alert volume by rule, with a trend

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** False positive rate and alert volume per rule show noise and where to tune. The other numbers do not measure alert quality.
</details>

---

### Question 27 - Section 6: Observability
**Scenario:** An authentication log source stops sending events for six hours and nobody notices. Which feature would have raised an alert?

A. Assigning every case to the most senior analyst regardless of the shift schedule or workload
B. Hiding the case history from the receiving analyst so they form their own view of events
C. Closing cases automatically at every shift change and asking the next shift to reopen them
D. Silent source detection configured with an interval suited to that source

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Silent source detection alerts when a source sends no events within its expected interval, catching failures and possible tampering. Case or detection summaries do not reveal missing data.
</details>

---

### Question 28 - Section 6: Observability
**Scenario:** Which set of metrics best shows the health of the log ingestion pipeline?

A. Ingestion rate and newest event age per source, plus parser error rate
B. Disabling Security Command Center so that it creates fewer findings for the team to ignore
C. Waiting for the next incident to see whether the same weakness is exploited a second time
D. A report that names the analyst who missed the finding, with a recommendation for retraining

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Pipeline health is shown by per-source ingestion rate, event freshness and parser errors. The other options do not measure data flow.
</details>

---
