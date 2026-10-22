---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 12 min
---

# Microsoft Information Security Administrator (SC-401) Fact Sheet

## Exam Overview

**Exam Code:** SC-401
**Exam Name:** Administering Information Security in Microsoft 365
**Level:** Associate
**Duration:** 100 minutes
**Format:** Multiple choice, multiple select, drag-and-drop, case studies, yes/no series
**Questions:** Typically 40-60
**Passing Score:** 700 out of 1000
**Cost:** USD 165 (varies by country)
**Valid For:** 1 year, renewable free online through Microsoft Learn
**Delivery:** Pearson VUE, test center or online proctored
**Prerequisites:** None formally; working knowledge of Microsoft 365 and Purview expected

> **Replaces SC-400.** SC-401 (Information Security Administrator) superseded SC-400 (Information Protection and Compliance Administrator). The scope shifted toward data security operations and now includes Microsoft Purview DSPM for AI and protections for Copilot data access. If you find SC-400 study material, treat the Purview fundamentals as still valid and the domain structure and AI content as out of date.

<!-- -->

> **Verify before booking.** Confirm the current outline and price on the official pages below.

**[📖 SC-401 certification page](https://learn.microsoft.com/en-us/credentials/certifications/information-security-administrator/)** - registration and renewal
**[📖 SC-401 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-401)** - the authoritative skills-measured outline
**[📖 Microsoft Purview documentation](https://learn.microsoft.com/en-us/purview/)** - the product this exam is about

## Why this exam is in this repo

The repo's [compliance guides](../../../resources/compliance-guides/) cover SOC 2, ISO 27001, NIST CSF, HIPAA, PCI DSS, GDPR, FedRAMP, NIS2, DORA, CMMC; AI governance guides live on the [AI site](https://ai.noblerworks.com/safety/). SC-401 is the certification that turns those obligations into configured controls: classification, labeling, DLP, insider risk, and data governance for AI.

It is also the data-protection counterpart to [SC-300](../sc-300/) on identity, and both feed [SC-100](../sc-100/).

## Target Audience

- Information protection and compliance administrators
- Microsoft 365 administrators owning data security
- Security engineers implementing DLP and insider risk controls
- Anyone preparing a Copilot or AI assistant rollout that touches sensitive data

## Exam Domains

Domains and skills follow the SC-401 study guide "skills measured as of October 28, 2026" (checked 2026-10-22; Microsoft lists only a minor change to the sensitivity labels section against the previous version). Domain 2 is titled "Implement data loss prevention and retention", so retention is studied with DLP, not with audit and eDiscovery. Domain 3 adds a section, "Protect data used by AI services".

### Domain 1: Implement information protection (30-35%)

Three sections: implement and manage data classification; implement and manage sensitivity labels in Microsoft Purview; implement information protection for Windows, file shares, and Exchange.

**Key Concepts:**
- Sensitive information types: built-in, custom, exact data match (EDM), document fingerprinting
- Trainable classifiers: pre-trained and custom, and when each is appropriate
- Sensitivity labels: scopes (items, groups and sites, schematized data assets), label settings, encryption, content marking
- Label policies: publishing, default labels, mandatory labeling, downgrade justification
- Auto-labeling: client-side (in policy) versus service-side (auto-labeling policies), and simulation mode
- Label priority, inheritance, and co-authoring on encrypted documents
- Double Key Encryption and when its trade-offs are acceptable
- Encryption with Rights Management, usage rights, and offline access
- Purview Information Protection scanner for on-premises file shares
- Optical character recognition (OCR) so sensitive information types match text in images
- Data explorer and Content explorer for monitoring classification and label usage
- Labels for containers (Teams, Microsoft 365 Groups, SharePoint sites) and Power BI items, and labeling through Defender for Cloud Apps
- Microsoft Purview Information Protection client for files on Windows, and bulk classification with the scanner
- Microsoft Purview Message Encryption and Advanced Message Encryption for Exchange

**[📖 Sensitivity labels](https://learn.microsoft.com/en-us/purview/sensitivity-labels)** - label design and behavior
**[📖 Trainable classifiers](https://learn.microsoft.com/en-us/purview/classifier-learn-about)** - classification at scale

### Domain 2: Implement data loss prevention and retention (30-35%)

Three sections: create and configure DLP policies; implement and monitor Microsoft Purview Endpoint DLP; implement and manage retention.

**Key Concepts:**
- DLP policy anatomy: locations, conditions, exceptions, actions, user notifications, overrides, incident reports
- Locations: Exchange, SharePoint, OneDrive, Teams chat and channel messages, devices (endpoint DLP), on-premises repositories, Fabric and Power BI, Defender for Cloud Apps, and AI applications
- Endpoint DLP: onboarding devices, restricted apps, unallowed browsers, network exceptions, printer and removable storage controls
- Policy tips, user overrides with justification, and false positive handling
- DLP for Microsoft 365 Copilot and other AI applications
- Adaptive Protection: dynamically strengthening DLP based on insider risk level
- Alerts, incident management, and DLP reporting
- Testing with simulation mode before enforcement
- Endpoint DLP versus Defender for Cloud Apps session policies
- Roles and permissions for DLP, and policy and rule precedence when several policies match
- Defender for Cloud Apps file policies that use a Purview DLP policy
- Endpoint DLP device requirements (including the browser extension), advanced device rules, and just-in-time protection
- Retention labels and retention label policies (publish or auto-apply), retention policies, and adaptive policy scopes
- Policy precedence and Policy lookup; recovering retained content in Microsoft 365
- Records management and disposition review

**[📖 Data loss prevention](https://learn.microsoft.com/en-us/purview/dlp-learn-about-dlp)** - policy design across workloads
**[📖 Endpoint DLP](https://learn.microsoft.com/en-us/purview/endpoint-dlp-learn-about)** - device-level enforcement
**[📖 Data lifecycle management](https://learn.microsoft.com/en-us/purview/data-lifecycle-management)** - retention and disposition

### Domain 3: Manage risks, alerts, and activities (30-35%)

Three sections: implement and manage Microsoft Purview Insider Risk Management; manage information security alerts and activities; protect data used by AI services.

**Key Concepts:**
- Insider Risk Management: policy templates, indicators, triggering events, sequence detection, and risk scoring
- Insider risk policy lifecycle: alerts, triage, cases, and actions including escalation
- Adaptive Protection integration between insider risk and DLP or Conditional Access
- Privacy controls: anonymization of usernames in insider risk
- Insider Risk Management connectors, Defender for Endpoint integration, forensic evidence, and notice templates
- Purview Audit: standard versus premium, search, retention policies for audit logs, high-value events
- eDiscovery: cases, holds, search, export, and premium features
- Content Search and its limits
- Activity explorer, and responding to Purview alerts in the Purview portal, Defender XDR, and Defender for Cloud Apps
- DSPM for AI: prerequisites, roles and permissions, policies, and activity monitoring
- Purview and Microsoft 365 controls protecting content used by Copilot and other AI services

Communication Compliance and Information Barriers are no longer named in the skills measured; they are covered briefly in the notes as context.

**[📖 Insider Risk Management](https://learn.microsoft.com/en-us/purview/insider-risk-management)** - policies, indicators, and triage
**[📖 Purview Audit](https://learn.microsoft.com/en-us/purview/audit-solutions-overview)** - audit search and retention
**[📖 DSPM for AI](https://learn.microsoft.com/en-us/purview/dspm-for-ai)** - AI data security reports and policies

## Decision quick reference

| Requirement | Feature |
|---|---|
| Protection that travels with the file, including outside the tenant | Sensitivity label with encryption |
| Prevent an action at a boundary (send, copy, print, upload) | DLP policy |
| Classify at scale without user action | Auto-labeling policy with trainable classifiers |
| Keep content for a fixed period regardless of user deletion | Retention policy or retention label |
| Formal records declaration with disposition review | Records management |
| Detect a departing employee exfiltrating data | Insider Risk Management |
| Prevent two groups from communicating | Information Barriers |
| Review messages for policy violations | Communication Compliance |
| Prove who accessed what | Purview Audit |
| Preserve content for litigation | eDiscovery hold |
| See what sensitive data AI is touching | DSPM for AI |

## Related repo material

- [Notes](./notes/) - three notes, one per domain
- [Practice plan](./practice-plan.md) - 6-week schedule
- [Scenarios](./scenarios.md)
- [Strategy](./strategy.md)
- [SC-300](../sc-300/) - the identity counterpart
- [SC-100](../sc-100/) - the design exam this feeds
- [Compliance guides](../../../resources/compliance-guides/) - the obligations behind the controls
- [AI security](https://ai.noblerworks.com/safety/) - the engineering view of the AI risks Purview governs
