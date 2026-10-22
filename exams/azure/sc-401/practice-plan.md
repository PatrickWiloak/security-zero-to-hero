---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 5 min
---

# SC-401 Study Plan

Six weeks at 6-8 hours per week, with a lab every week in a Microsoft 365 E5 trial tenant.

## Week 1: Classification foundations

- [ ] Read the [SC-401 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-401)
- [ ] Built-in sensitive information types and how confidence levels work
- [ ] Custom sensitive information types: patterns, supporting evidence, proximity
- [ ] Exact data match (EDM): schema, hashing, upload process, and when it beats a pattern
- [ ] Document fingerprinting for form-based content
- [ ] Trainable classifiers: pre-trained versus custom, and the training and testing cycle
- [ ] **Lab**: build a custom SIT with supporting keywords, test it against sample content
- [ ] Review Notes: `notes/01-information-protection.md`

## Week 2: Sensitivity labels

- [ ] Label scopes: items, groups and sites, schematized data assets
- [ ] Label settings: encryption, content marking, auto-labeling in client, site and group protection
- [ ] Encryption settings: permissions, user-defined permissions, offline access, expiry
- [ ] Label policies: publishing, default label, mandatory labeling, downgrade justification
- [ ] Label priority and inheritance, including attachments and derived content
- [ ] Co-authoring on encrypted documents and its prerequisites
- [ ] Double Key Encryption: what it protects against and what it costs
- [ ] **Lab**: create and publish a label with encryption; open the file as a user outside the permitted group

## Week 3: Auto-labeling and data discovery

- [ ] Client-side auto-labeling (in the label) versus service-side auto-labeling policies
- [ ] Simulation mode, reading results, and tuning before enforcement
- [ ] Purview Information Protection scanner for on-premises file shares
- [ ] Data map, scan rule sets, and classification across Azure and other clouds
- [ ] DSPM and DSPM for AI: what each reports
- [ ] **Lab**: run an auto-labeling policy in simulation and analyze the matches

## Week 4: Data loss prevention and retention (Domain 2)

- [ ] DLP policy anatomy: locations, rules, conditions, exceptions, actions
- [ ] Per-location behavior differences across Exchange, SharePoint, OneDrive, Teams
- [ ] Endpoint DLP: onboarding, restricted apps, unallowed browsers, removable storage, printing
- [ ] Policy tips, user overrides, business justification, incident reports
- [ ] DLP for AI applications and Microsoft 365 Copilot
- [ ] Adaptive Protection linking insider risk level to DLP strength
- [ ] Test mode, then test with policy tips, then enforce
- [ ] DLP roles and permissions; policy and rule precedence across policies
- [ ] Defender for Cloud Apps file policies that use a DLP policy
- [ ] Endpoint DLP device requirements and browser extension; just-in-time protection
- [ ] Retention policies versus retention labels; publish versus auto-apply label policies
- [ ] Adaptive scopes, retention precedence, Policy lookup, and recovering retained content
- [ ] Records management: declaring records, disposition review, file plan
- [ ] **Lab**: build a DLP policy in test mode, trigger it, and inspect the alert and incident report
- [ ] Review Notes: `notes/02-data-loss-prevention.md`

## Week 5: Insider risk and alert response (Domain 3)

- [ ] Insider Risk Management policy templates and what each detects
- [ ] Indicators, triggering events, sequence detection, and risk scoring
- [ ] Alert triage, cases, and actions including escalation to eDiscovery
- [ ] Privacy controls and username anonymization
- [ ] Insider Risk Management connectors, Defender for Endpoint integration, forensic evidence, notice templates
- [ ] Activity explorer; responding to alerts in the Purview portal, Defender XDR, and Defender for Cloud Apps
- [ ] Communication Compliance and Information Barriers, briefly (no longer named in the outline)
- [ ] **Lab**: create an insider risk policy from the data theft by departing users template and review its indicators
- [ ] Review Notes: `notes/03-risks-alerts-and-activities.md`

## Week 6: Audit, eDiscovery, AI services, and review (Domain 3)

- [ ] Review retention precedence from Week 4 until you can state it from memory
- [ ] Purview Audit standard versus premium, audit retention policies
- [ ] eDiscovery: cases, holds, search, export; premium features
- [ ] Protect data used by AI services: DSPM for AI prerequisites, roles, policies, and activity monitoring
- [ ] Work every scenario in [scenarios.md](./scenarios.md)
- [ ] Two full timed practice exams

## Readiness check

- [ ] Explain when a sensitivity label is required rather than a DLP policy, and vice versa
- [ ] State the retention precedence order from memory
- [ ] Describe the difference between client-side and service-side auto-labeling
- [ ] Name the prerequisite for endpoint DLP to enforce on a device
- [ ] Explain what Adaptive Protection does and which two products it links
- [ ] Describe when EDM beats a pattern-based sensitive information type
- [ ] Explain what DSPM for AI reports and why a Copilot rollout needs it
