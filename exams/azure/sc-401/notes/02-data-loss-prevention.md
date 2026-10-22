---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 11 min
---

# 02 - Data loss prevention and retention

**Domain 2: Implement data loss prevention and retention (30-35%)**

DLP inspects activity and intervenes at a boundary. It does not change the file. Retention decides how long content is kept and what happens at the end, and it is part of this domain in the current outline.

---

## Policy anatomy

A DLP policy is: **locations** plus one or more **rules**, each with **conditions**, optional **exceptions**, **actions**, **user notifications**, **user overrides**, and **incident reports**.

**Conditions** include content containing a sensitive information type, sensitivity label, or retention label; content shared with people inside or outside the organization; document properties; file extension; and sender or recipient attributes.

**Actions** include restricting access or encrypting, blocking the activity, blocking with override, auditing only, and running Power Automate flows.

**Rule priority** matters: rules are evaluated in order and the first matching rule's actions apply for a given policy.

**Precedence across policies.** When one item matches rules in several DLP policies, the most restrictive action wins. If one policy audits and another blocks, the block applies. Policy tips show the tip from the highest-priority, most restrictive rule. Questions that describe "a user was blocked although our policy only audits" are usually about a second policy in scope.

**Roles and permissions.** Creating and managing DLP policies needs a compliance role, such as membership in the Compliance Administrator or Compliance Data Administrator role group, or a custom role group with the DLP Compliance Management role. Seeing the actual matched content in alerts is a separate and more sensitive permission than managing policy, which is how you let an analyst triage alerts without letting the policy author read the data.

**Defender for Cloud Apps file policies using DLP.** For files in connected third-party cloud apps, a Defender for Cloud Apps file policy can use Purview's data classification service as its inspection method. The same sensitive information types then drive governance actions in the other app, such as removing external sharing, quarantining the file, or applying a sensitivity label.

---

## Locations and their differences

| Location | Notable behavior |
|---|---|
| **Exchange** | Mail flow inspection, transport-level blocking, notification to sender |
| **SharePoint / OneDrive** | Content at rest and on sharing; blocks external sharing of matched content |
| **Teams chat and channel messages** | Blocks messages and file shares in conversations |
| **Devices (endpoint DLP)** | Requires onboarded devices; controls copy, print, USB, network share, browser upload, clipboard |
| **On-premises repositories** | Through the Information Protection scanner |
| **Fabric and Power BI** | Applies to semantic models and datasets |
| **Defender for Cloud Apps** | Extends to third-party SaaS through the app connector |
| **AI applications** | Covers Microsoft 365 Copilot and other AI apps, restricting what content can be processed |

---

## Endpoint DLP

The location with the most prerequisites and the most exam detail.

- Devices must be **onboarded** (through Intune, Configuration Manager, or a script). An unonboarded device enforces nothing.
- **Restricted apps and app groups**: name applications that may not access protected content.
- **Unallowed browsers**: uploads through a browser that is not policy-aware are blocked rather than monitored, which is how personal cloud storage uploads are stopped.
- **Service domains**: allow or block lists governing where content may be uploaded.
- **Removable storage, network share, printing, clipboard, and Bluetooth** controls.
- **Advanced classification** sends content to the service for evaluation when local classification is insufficient.

**Device requirements.** Endpoint DLP runs on supported Windows and macOS versions, and the device must be onboarded to Purview. To cover uploads from Chrome and Firefox, the Microsoft Purview browser extension must be installed; Edge is DLP-aware without one.

**Just-in-time protection** closes a gap on onboarded devices: a file that has not been classified yet. With it on, egress actions on such a file (copy to USB, upload, print) are held to a configured action, such as block or audit, until classification finishes, so a freshly copied file is not a free pass.

**Monitoring** happens in Activity explorer and the DLP alerts page, where endpoint activities such as file copied to removable media or uploaded to a cloud domain appear with the device and user.

For unmanaged devices, endpoint DLP is not available and **Defender for Cloud Apps session policies** are the alternative control.

---

## Rollout discipline

The exam consistently rewards staged deployment:

1. **Test mode** (simulation) with no user impact, reviewing matches
2. **Test with policy tips**, so users see notifications and you learn about false positives
3. **Enforce**, usually with **override plus business justification** for a period
4. **Tighten** to hard block for the highest-severity rules

**Incident reports** and alerts feed the DLP alerts dashboard, and can raise severity based on volume and repetition.

---

## Adaptive Protection

Links Insider Risk Management to enforcement. A user whose insider risk level rises from minor to moderate to elevated automatically receives progressively stricter DLP actions, and can also be targeted by Conditional Access.

This is the recurring exam answer to "apply stricter controls only to users who are behaving riskily, without applying them to everyone".

---

## DLP for AI

- Prevents content carrying specified sensitivity labels from being processed or summarized by Microsoft 365 Copilot and other AI applications.
- Works alongside **DSPM for AI**, which reports what is happening, while DLP enforces.
- The important design point remains that AI honors existing permissions, so DLP and labels are layered on top of a permissions clean-up rather than substituting for it.

## Retention

Retention moved into this domain in the SC-401 outline (the domain title is now "Implement data loss prevention and retention"). The reason is sound: DLP and retention are both about what happens to data over time and at boundaries, and both act on the same classification.

**Policies versus labels.** A **retention policy** applies broadly at container scope, such as every mailbox or a set of SharePoint sites, and users never see it. A **retention label** applies to individual items. Users can apply it, it can be applied automatically, it supports **disposition review**, and it can declare content a record. The exam pattern is simple: if the requirement is "everything in this location", reach for a policy; if it is "these particular documents", or anything involving disposition review or records, reach for a label.

**Getting labels onto content.** A label does nothing until a **retention label policy** delivers it. There are two kinds. A **publishing** policy makes labels available for users to apply by hand in Outlook, SharePoint, and OneDrive. An **auto-apply** policy applies a label without the user, based on sensitive information types, keywords or a KQL query, trainable classifiers, or cloud attachments. Auto-apply policies take time to run and can be simulated first, the same rollout habit the exam rewards for DLP.

**Scopes.** A policy targets either a **static scope** (named locations, or all of them) or an **adaptive scope**. An adaptive scope is a query over attributes, for example every user whose department is Finance, or every site with a given property. Membership updates as attributes change, so a new Finance hire is covered without anyone editing the policy. Adaptive scopes are the answer when the requirement says the coverage must follow people or sites as they change.

**Precedence.** When several retention settings apply to the same item, the principles of retention decide, in order:

1. Retention wins over deletion
2. The longest retention period wins
3. An explicit label beats an inherited policy
4. The shortest deletion period applies only when nothing requires retention

**Policy lookup** in the Purview portal answers the practical question "which retention policies apply to this user, site, or group?" Use it before reasoning about precedence, because the most common real problem is a policy you did not know was in scope.

**Recovering retained content.** Retention keeps content that a user deletes. For mailboxes it is held in the Recoverable Items folder; for SharePoint and OneDrive it moves to the Preservation Hold library. Recovery goes through search tools such as eDiscovery content search rather than the user's own recycle bin, which is why "the user deleted it and the retention policy kept it, how do we get it back?" points to a search and export.

**Records management** builds on labels: a file plan, record declaration (locking content against edit or deletion), regulatory records (which cannot be unlocked, even by an administrator), event-based retention that starts the clock on an event such as an employee leaving, and disposition review with approver sign-off.

**[📖 Learn about retention](https://learn.microsoft.com/en-us/purview/retention)** - policies, labels, and the principles of retention
**[📖 Adaptive policy scopes](https://learn.microsoft.com/en-us/purview/purview-adaptive-scopes)** - attribute-based targeting for retention and other policies

---

## Key terms

- **DLP policy** - a rule set that inspects activity and blocks, warns, or audits when classified content crosses a boundary
- **Policy tip** - the in-product notification shown to a user when their action matches a DLP rule
- **User override** - a DLP setting allowing a user to proceed with a business justification, recorded in the incident report
- **Test mode** - a DLP state that evaluates policy and records matches without affecting users
- **Endpoint DLP** - the DLP location enforcing on onboarded devices, covering copy, print, USB, clipboard, and browser upload
- **Device onboarding** - the prerequisite process registering a device so endpoint DLP and Defender for Endpoint can enforce
- **Unallowed browser** - a browser that is not DLP-aware, whose uploads endpoint DLP blocks outright
- **Service domain list** - the endpoint DLP allow or block list of destinations content may be uploaded to
- **Adaptive Protection** - the capability that raises DLP or Conditional Access strictness automatically as a user's insider risk level increases
- **Incident report** - the record generated when a DLP rule matches, including the activity, content, and any justification
- **Advanced classification** - endpoint DLP capability sending content to the service for evaluation beyond local classification
- **DLP for AI applications** - DLP coverage preventing classified content being processed by Copilot and other AI applications
- **Just-in-time protection** - endpoint DLP setting that holds egress actions on not-yet-classified files to a configured action until classification completes
- **Retention policy** - broad container-scoped retention that is invisible to end users
- **Retention label** - per-item retention supporting user application, auto-application, record declaration, and disposition review
- **Disposition review** - the approval step before content reaches the end of its retention period and is deleted
- **Regulatory record** - a record declaration that cannot be unlocked or removed even by an administrator
- **Adaptive scope** - an attribute query that decides which users, sites, or groups a retention policy covers, updating as attributes change
- **Policy lookup** - the Purview tool listing which retention policies apply to a given user, site, or group
- **Preservation Hold library** - the SharePoint and OneDrive location where retained content is kept after a user deletes it

---

## Related

- [Notes 03: risks, alerts, and activities](./03-risks-alerts-and-activities.md)
- [Scenarios](../scenarios.md) - scenarios 4 and 6
- [Prompt injection defense](https://ai.noblerworks.com/safety/security/prompt-injection-defense/)
