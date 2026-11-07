---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 7 min
---

# Google Cloud Professional Security Operations Engineer Scenarios

Worked operations situations. Each targets a distinction the exam leans on.

---

## Scenario 1: Missing fields after a vendor update

**Scenario**: Detections for a firewall product stopped firing after the vendor updated its log format. Health Hub shows parser errors rising for that source.

**Solution Pattern**:
- Compare failing raw logs with the parser mapping to find the changed field
- Add a parser extension to map the new field to the UDM field the rules use, and test on samples
- Re-check the affected rules and run a retrohunt (alerting disabled) over the gap
- Add a parser error rate alert

**Key Takeaway**: Fix normalisation first; rules cannot match fields that were never mapped.

---

## Scenario 2: A noisy rule

**Scenario**: A rule alerts several thousand times a week, mostly for one backup server's service account.

**Solution Pattern**:
- Measure alert frequency by entity to confirm the pattern
- Exclude the known-good entity with a precise condition or a reference list that has an owner
- Keep the rule for everyone else and record the exception
- Track false positive rate on a dashboard

**Key Takeaway**: Tune with precise exclusions; never delete a rule to quiet it.

---

## Scenario 3: A new indicator arrives

**Scenario**: Threat intelligence publishes a domain used in a campaign against your sector. The campaign started three weeks ago.

**Solution Pattern**:
- Search retained telemetry for the domain over the last three weeks (historical IOC search)
- Add the indicator to a detection so future connections alert, scored by confidence
- If a hit appears, open an incident, scope with entity data and hand to response

**Key Takeaway**: New intelligence has to be applied backwards (retrohunt) as well as forwards.

---

## Scenario 4: A source goes quiet

**Scenario**: No authentication logs have arrived from the identity provider for six hours, and no alert fired.

**Solution Pattern**:
- Treat it as possible tampering until proven otherwise; check the provider, the collector or feed, credentials and quotas
- Configure silent source detection with a short interval for this critical source
- Backfill the gap if the source retains logs, and review what could have happened unseen

**Key Takeaway**: Silent source detection protects against blind spots, including attacker-caused ones.

---

## Scenario 5: Automate or ask?

**Scenario**: A phishing playbook can look up URL reputation, search for other recipients and disable the user's account.

**Solution Pattern**:
- Automate reputation lookups, recipient search and ticket creation (high frequency, low risk)
- Put a manual action in front of disabling the account, or require high confidence plus approval
- Notify the user's manager and the security channel with a summary

**Key Takeaway**: Automate enrichment freely; gate disruptive actions.

---

## Scenario 6: Choosing the right log tool

**Scenario**: An analyst must find which service accounts called an unusual number of different APIs over 30 days, across a large organization.

**Solution Pattern**:
- Aggregate audit logs by principal with a distinct count of methods per day using Log Analytics or BigQuery
- Investigate the outliers in SecOps with entity context
- Convert the finding into a rule if it proves useful

**Key Takeaway**: SQL over large volumes suits Log Analytics or BigQuery; Logs Explorer suits quick checks on known resources.

---

## Scenario 7: A slow attack no single rule sees

**Scenario**: Over ten days the same user trips a low-severity impossible-travel rule, then a rare-process rule, then a storage-listing rule. Each alert was closed alone as benign. Coverage review shows the storage technique has no rule with technique metadata.

**Solution Pattern**:
- Write a composite detection that takes those rules' detections as input and matches on the user inside a window (the longest allowed is 14 days)
- Add technique IDs to the custom rules' metadata so the ATT&CK matrix counts them, then use the empty cards as the backlog
- Test the chain by running a retrohunt on each base rule in order, then on the composite rule
- Record closure reasons on future cases so tuning is driven by data

**Key Takeaway**: Individually benign detections can be a campaign; correlate them over time and measure coverage against ATT&CK.
