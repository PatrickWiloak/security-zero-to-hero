# Microsoft Information Security Administrator (SC-401) - Practice Questions

30 questions for SC-401 prep. SC-401 replaced SC-400. The recurring decision is whether a requirement needs protection that travels with the file (a sensitivity label) or prevention of an action at a boundary (a DLP policy).

> **Cert page:** [exams/azure/sc-401/](../../exams/azure/sc-401/)

---

### Question 1
**Scenario:** Contracts must remain unreadable to anyone outside the matter team even if emailed to a personal address or copied to a USB drive. Partners must be able to open them offline while traveling.

A. A retention label applied to the contracts library, set to keep the files for seven years and then delete them
B. A DLP policy blocking egress of documents from the contracts library, with a notification to the lead
C. SharePoint permissions restricted to the matter team, with external sharing turned off and site access reviewed every quarter
D. A sensitivity label with encryption for the matter team, offline access configured, published through a label policy

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Only label-applied encryption travels with the file and continues to apply once the document has left the tenant. DLP prevents actions at a boundary but does not protect a file that legitimately left. SharePoint permissions do not follow a downloaded copy. Retention governs lifetime, not access.
</details>

---

### Question 2
**Scenario:** Patient IDs are eight digits. A pattern-based custom sensitive information type produces hundreds of false positives because invoice numbers share the format. The compliance team holds an authoritative CSV of 400,000 real patient IDs.

A. Use exact data match with the authoritative table, adding supporting elements in a proximity window
B. Train a custom classifier on patient records so that it learns which eight-digit numbers are real patient IDs
C. Increase the instance count threshold so only documents with many matches trigger, which removes the invoice noise
D. Raise the confidence level on the existing SIT to high, so that only strongly corroborated matches are reported

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** EDM matches hashed values from a real list, so ambiguity with other eight-digit numbers disappears. Raising confidence reduces recall without resolving the ambiguity. Increasing instance count misses single-record leaks. Trainable classifiers identify categories of content, not known values.
</details>

---

### Question 3
**Scenario:** Ten million existing documents in SharePoint and OneDrive must be classified without asking users to do it and without breaking access unexpectedly.

A. Manual classification of the highest-risk libraries, with site owners labeling files in batches each quarter
B. A service-side auto-labeling policy run in simulation first, initially without encryption, and widened only after the results are reviewed
C. Client-side auto-labeling in the sensitivity label, so documents are classified as the first users open them
D. Mandatory labeling in the label policy, so every user must pick a label the next time a file is saved

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Service-side auto-labeling applies to content at rest without user involvement and supports simulation. Mandatory labeling forces users to act, contradicting the requirement. Client-side auto-labeling only applies as users open and edit documents, leaving untouched content unlabeled. Applying encryption on the first automated pass is what causes unexpected access breakage.
</details>

---

### Question 4
**Scenario:** Users copy customer data to personal OneDrive and Dropbox through the browser and onto USB drives. Windows endpoints are managed by Intune.

A. Group Policy blocking all USB devices on the Intune-managed endpoints and a banner reminding users about the policy
B. A sensitivity label applied to the affected documents, with a watermark and a header marking them customer data
C. An Exchange-scoped DLP policy that inspects customer data in outbound email and blocks external recipients
D. Endpoint DLP with onboarded devices, unallowed browsers configured, and removable storage restrictions applied through a DLP rule

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Browser uploads and USB copies are device-level actions, which only endpoint DLP sees, and only on onboarded devices. Configuring unallowed browsers is what turns a monitored upload into a blocked one. Exchange DLP does not see either action. A label classifies but does not stop the copy. Blanket USB blocking has no content awareness.
</details>

---

### Question 5
**Scenario:** A company repeatedly discovers weeks later that departing salespeople downloaded the customer list. It wants detection at the time, an investigation trail, and privacy controls on investigator access.

A. Insider Risk Management using the data theft by departing users template, an HR connector trigger, and username anonymization
B. Communication Compliance policies on outbound email, with reviewers sampling messages from departing users and flagging attachments that contain customer names
C. A DLP policy blocking downloads from the CRM for every user, with an override requiring a business justification
D. Audit log search after each departure, filtered on the user's file download events during the last month

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Insider risk scores behavior over time anchored on a triggering event from HR data, which is what produces detection before the departure rather than after. Anonymization satisfies the privacy requirement. DLP blocks specific actions but builds no behavioral case. Audit search is the reactive approach they already have. Communication Compliance reviews message content, not file exfiltration.
</details>

---

### Question 6
**Scenario:** Finance records are covered by a seven-year retention policy on the site. A document also carries a retention label set to delete after three years. A user deletes the document after one year. What happens?

A. The document is retained for three years, because the label is more specific
B. The document is retained for seven years; retention wins over deletion and the longest period applies
C. The deletion succeeds but the file is recoverable from the recycle bin for 93 days and then removed permanently
D. The document is deleted immediately, because the user's delete action overrides the retention rules in force

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Retention precedence is: retention beats deletion, the longest retention wins, an explicit label beats an inherited policy, and the shortest deletion applies only when nothing requires retention. Specificity does not override the retain-longest rule. The user's deletion moves the item to preservation rather than removing it.
</details>

---

### Question 7
**Scenario:** After an acquisition, the investment banking team and the trading team must not be able to communicate in Teams or discover each other in the directory, for regulatory reasons.

A. Information Barriers with segments defined by department and block-mode policies, applied to Teams, SharePoint, and OneDrive
B. Conditional Access policies scoped to each group, blocking sign-in to Teams from the other team's devices
C. Communication Compliance policies reviewing messages between the two groups, with keyword alerts to compliance
D. Separate Entra tenants for each team, with cross-tenant access settings blocking all collaboration

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Information Barriers is the only feature that prevents communication and discovery between defined segments, and enforcement extends across Teams, SharePoint, and OneDrive. Communication Compliance reviews content after the fact rather than preventing contact. Conditional Access governs sign-in conditions. Separate tenants achieve it at enormous operational cost the scenario does not require.
</details>

---

### Question 8
**Scenario:** Before deploying Microsoft 365 Copilot, what is the correct first step to prevent employees surfacing documents they should not see?

A. Auto-label all sensitive content, so Copilot excludes it from every user's responses
B. Enable DSPM for AI reporting, so the oversharing is detected and blocked before any prompt runs against the tenant's data
C. Fix oversharing at the source, using site access reviews and removing organization-wide sharing links
D. Apply DLP policies for AI applications, which stop Copilot returning any file the user should not see, whatever the sharing

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Copilot honors existing permissions, so pre-existing oversharing becomes immediate exposure. Labeling, DLP, and DSPM for AI are all part of the design, but they layer on top of a permissions clean-up rather than substituting for it. The exam tests the ordering.
</details>

---

### Question 9
**Scenario:** Which feature automatically applies stricter DLP enforcement only to users whose risky behavior has increased?

A. Insider Risk Management alerts
B. A DLP policy scoped to a dynamic group
C. Conditional Access with sign-in risk
D. Adaptive Protection

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Adaptive Protection links a user's insider risk level to enforcement strength, tightening DLP actions as risk rises without applying the strictest policy to everyone. Sign-in risk is an identity signal, not a data one. A dynamic group is static membership by attribute, not by behavior. Insider risk alerts inform investigators but do not themselves change enforcement.
</details>

---

### Question 10
**Scenario:** An organization needs protection applied to documents that are not yet classified, must not rely on users, and wants to see what would be affected before anything changes.

A. A DLP policy in test mode, which reports what content would be blocked or encrypted
B. A service-side auto-labeling policy in simulation mode
C. The Purview Information Protection scanner running a discovery scan on the file shares
D. Mandatory labeling with a default label, so every unlabeled item receives a label at next edit

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Simulation mode is the auto-labeling feature that reports what would be labeled without applying anything. DLP test mode simulates a DLP policy, not labeling. A default label applies to new content and relies on the label policy reaching users. The scanner addresses on-premises file shares, which the scenario does not mention.
</details>

---

### Question 11
**Scenario:** What does Double Key Encryption give you, and what does it cost?

A. Two encryption layers, each with its own key, with no functional cost to search, eDiscovery, or collaboration features
B. FIPS 140-2 Level 3 validation for the key store, at the cost of slower sign-in for each user
C. A customer-held key alongside the Microsoft key, at the cost of service-side search, eDiscovery, and co-authoring
D. Automatic key rotation every 90 days, at the cost of having to re-encrypt every document by hand

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** DKE means Microsoft cannot decrypt the content, which is exactly why service-side processing stops working. That trade-off is why DKE is reserved for the smallest set of genuinely most sensitive content rather than applied broadly.
</details>

---

### Question 12
**Scenario:** Which audit capability is required to see which mailbox items a compromised account accessed?

A. A Sentinel connector for Microsoft 365, which generates item-access events when the account is compromised
B. Purview Audit, searching the MailItemsAccessed event
C. Exchange message trace, which lists each mailbox item opened by the account during the incident window
D. Purview Audit Standard, searched for FileAccessed events across the SharePoint workloads

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** MailItemsAccessed is the mailbox auditing event that records which mail items an account accessed, and it is the specific record used in mailbox compromise investigations. It is available in Audit Standard as well as Audit Premium, and Premium keeps it for longer. File access events (D) do not cover mailbox items. Message trace shows mail flow, not item access. A Sentinel connector transports events but cannot create ones that were never generated.

**Key Concept:** [Use MailItemsAccessed to investigate compromised accounts](https://learn.microsoft.com/en-us/purview/audit-log-investigate-accounts)
</details>

---

### Question 13
**Scenario:** A retention requirement demands that records cannot be removed even by a global administrator, and that disposal requires reviewer approval.

A. An eDiscovery hold on the custodians, with a case manager approving releases
B. A sensitivity label with encryption, with the global administrator excluded from the label's permissions
C. A retention label declaring content a regulatory record, with disposition review enabled
D. A retention policy with a seven-year period, with the global administrator removed from the retention role group

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Regulatory record declaration is what prevents removal even by administrators, and disposition review is what inserts the approval step. A retention policy prevents user deletion but does not declare a record. An eDiscovery hold preserves for legal process without a disposition workflow. A sensitivity label governs access, not lifetime.
</details>

---

### Question 14
**Scenario:** An organization wants to know which sensitive data types employees' AI interactions are actually touching.

A. Insider Risk Management
B. Communication Compliance
C. Purview DSPM for AI (Data Security Posture Management)
D. DLP for AI applications, such as Copilot and other enterprise AI apps

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** DSPM for AI is the reporting and visibility capability for sensitive data flowing through AI interactions, including Copilot. DLP for AI is the enforcement side of the same problem. Communication Compliance reviews messages. Insider risk scores user behavior.
</details>

---

### Question 15
**Scenario:** Which combination is required so that endpoint DLP can block a file upload through a non-Edge browser?

A. A DLP policy scoped to the Devices location, the device onboarded, and the browser set as unallowed
B. A sensitivity label with encryption, applied to every file so uploads elsewhere fail
C. A DLP policy with the Devices location selected and an upload restriction rule, without onboarding the device
D. Intune compliance policies marking non-Edge browsers as noncompliant so the endpoint blocks the upload automatically

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** All three are needed. Selecting the Devices location without onboarding enforces nothing. Onboarding without the unallowed-browser setting means uploads through a non-policy-aware browser are monitored rather than blocked. Compliance policies and labels address different problems.
</details>

---

### Question 16 - Domain 1: Implement information protection
**Scenario:** HR uses a standard blank employment-offer form. Completed offers vary in names, salaries, and dates, so no keyword or pattern reliably finds them. HR wants DLP to detect any document created from that form.

A. A trainable classifier built from a few hundred completed offers, published and then used as the DLP condition
B. A custom sensitive info type with a regular expression that matches the salary field on the completed form
C. Document fingerprinting created from the blank form, then used as a sensitive info type in a DLP rule
D. An exact data match type loaded with HR's list of every employee name, matched against the offer documents

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Document fingerprinting turns a standard form into a sensitive info type that matches documents derived from it, which is exactly the "same form, different values" case. A trainable classifier identifies a broad category of content and needs a large training set, which is far more effort for a single known form. A salary regex will match salaries in many unrelated documents. EDM matches known values, and a list of employee names would flag almost every HR file, not only offers.
</details>

---

### Question 17 - Domain 1: Implement information protection
**Scenario:** A legal team wants every new Teams team marked "Restricted" to be private, to block guest members, and to stop the connected SharePoint site from being shared externally. Labeling the individual files is a separate project.

A. A sensitivity label scoped to groups and sites, with privacy and external sharing settings, published to team owners
B. A sensitivity label scoped to files and emails, with encryption limited to the legal team, published to team owners
C. A DLP policy on the Teams and SharePoint locations that blocks sharing whenever the team name contains "Restricted"
D. A retention label on the team's SharePoint site, configured to mark the site as a record and lock its settings

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Container labels (the groups and sites scope) control the privacy, guest access, and external sharing settings of a team, group, or site. They do not label the files inside, which matches the scenario. A file-scoped label protects items, not the container's settings. DLP inspects content for sensitive data and does not set team privacy or guest membership. A retention label governs lifetime, not who can join or share.
</details>

---

### Question 18 - Domain 1: Implement information protection
**Scenario:** A bank sends encrypted statements to external customers. Regulators now require that these messages stop opening after 30 days and that the bank can revoke a message sent in error. Each business unit wants its own branded portal.

A. Office Message Encryption with the default template, plus a mail flow rule that deletes sent items after 30 days
B. A sensitivity label with encryption for the external customers, with offline access set to 30 days in label settings
C. S/MIME certificates issued to each customer, with the certificate validity set to expire 30 days after sending
D. Purview Advanced Message Encryption, with branding templates per unit and an expiration set by a mail flow rule

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Advanced Message Encryption adds message expiration, revocation, and multiple custom branding templates on top of standard Purview Message Encryption. Standard message encryption alone does not give expiration, and deleting the sender's copy does nothing to the recipient's copy. Offline access duration controls cached use licenses, not a hard expiry for external recipients, and labels give no branded portal. S/MIME needs certificates on both sides and gives neither revocation nor branded portals.
</details>

---

### Question 19 - Domain 1: Implement information protection
**Scenario:** Field staff photograph signed customer forms with their phones and upload the images to SharePoint and Exchange. A DLP policy for national ID numbers never matches these images, even though the numbers are clearly visible.

A. Convert the DLP rules to use a trainable classifier, which reads text inside photographs by default
B. Turn on optical character recognition in Purview settings, link billing, and select the locations to scan
C. Raise the DLP policy's instance count so that images with a single visible ID number are still reported
D. Apply a default sensitivity label to the upload libraries so every image is labeled and then encrypted

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Sensitive info types only see text, so images need OCR. Purview OCR is turned on in settings, uses pay-as-you-go billing, and is scoped to chosen locations, after which existing SIT-based policies can match text in images. Trainable classifiers do not read images by default. Raising the instance count makes matching stricter, not possible. A default label would label every image without detecting which ones hold ID numbers.
</details>

---

### Question 20 - Domain 1: Implement information protection
**Scenario:** The CISO asks how many files in SharePoint and OneDrive currently contain credit card numbers, and which sites hold the most. A compliance analyst needs to answer and drill into examples.

A. Activity explorer, filtered on the credit card sensitive info type for the last 30 days of label and DLP activity
B. Purview Audit, searching for FileAccessed events on documents that contain the credit card info type
C. Data explorer and Content explorer, with the analyst holding the Content explorer list and content viewer roles
D. A DLP policy in simulation mode, then counting the matches in the policy's simulation report per site

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Content explorer shows content at rest by sensitive info type and location and, with the content viewer role, lets the analyst open examples. Activity explorer shows events over time, such as labels applied or DLP matches, not an inventory of what is stored. Audit records actions and does not classify content. A DLP simulation would give a rough count but is a policy test, not the reporting tool, and needs a policy built just to answer a question.
</details>

---

### Question 21 - Domain 2: Implement data loss prevention and retention
**Scenario:** One DLP policy has two rules. The low-volume rule (1-9 card numbers) shows a policy tip. The high-volume rule (10 or more) blocks sharing with no override. A user shares a file with 15 card numbers externally. What happens?

A. The policy tip shows and sharing is allowed, because the rule that appears first in the list is the one applied
B. Sharing is blocked, because when content matches several rules the most restrictive action is enforced
C. Both rules apply in turn, so the user sees the tip and can then override the block with a justification
D. Neither rule applies, because the content matches more than one rule and the policy reports a conflict

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Fifteen card numbers satisfy both rules, and DLP enforces the most restrictive action across the matched rules, so the block applies. Rule order does not let a weaker action win over a stronger one for the same content. The block rule has no override, so the user cannot justify past it. Multiple matches are normal and do not produce a conflict that disables the policy.
</details>

---

### Question 22 - Domain 2: Implement data loss prevention and retention
**Scenario:** Every mailbox and OneDrive belonging to someone with "Director" or above in their job title must be retained for ten years. People are promoted and leave every week, and HR keeps titles accurate in Entra ID.

A. A static retention policy listing today's directors, with a monthly task to add and remove users by hand
B. A retention policy applied to all mailboxes, with the directors' items tagged by a manual retention label
C. A litigation hold placed on each director's mailbox when HR notifies compliance of a promotion
D. An adaptive policy scope querying the job title attribute, used by a retention policy for mailboxes and OneDrive

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Adaptive scopes use an attribute query that is re-evaluated, so membership follows promotions and departures without manual edits. A static list goes stale between updates and depends on someone remembering. A policy on every mailbox over-retains everyone else, and relying on users to apply manual labels misses content. Litigation hold is a legal preservation tool, not a records policy, and relies on a manual notice for each change.
</details>

---

### Question 23 - Domain 2: Implement data loss prevention and retention
**Scenario:** A project site owner says files are not being deleted after two years as expected. The admin suspects another retention policy also covers the site but does not know which of the 60 policies it is.

A. Use Policy lookup in data lifecycle management, entering the site URL to list every retention policy that applies
B. Open each retention policy in turn and compare its locations against the site, starting with the newest one
C. Search Purview Audit for retention events on the site, then infer which policies are applied from the results
D. Run Content explorer filtered on retention labels, which lists the retention policies applied to each site

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Policy lookup shows all retention policies that apply to a given user, site, or Microsoft 365 group, which is exactly the question, and then the precedence rules explain the outcome. Opening 60 policies by hand works but is slow and error-prone. Audit records changes, not the current set of applied policies. Content explorer shows retention labels on items, not retention policies on locations.
</details>

---

### Question 24 - Domain 2: Implement data loss prevention and retention
**Scenario:** A user deleted a contract from a SharePoint site and then emptied both recycle bins. The site is covered by a five-year retention policy. The contract is needed back today.

A. Open a support case so Microsoft restores the site from backup to the point before the deletion
B. Temporarily remove the site from the retention policy, which moves retained items back into the library
C. Have a site collection admin copy the retained version from the site's Preservation Hold Library
D. Restore the file from the first-stage recycle bin, where retained items reappear for another 93 days

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** When content under retention is deleted, a copy is kept in the Preservation Hold Library, where an admin can find it and copy it back. A full site restore from backup is slow and rolls back other changes too. Removing the site from the policy does not move items back and puts the retained copies at risk of cleanup. The recycle bins were already emptied, and retained copies do not reappear there.
</details>

---

### Question 25 - Domain 2: Implement data loss prevention and retention
**Scenario:** A firm is onboarding 5,000 laptops to endpoint DLP. Many existing files have never been scanned, and the firm is worried users could copy them to USB in the window before DLP evaluates them.

A. Delay all device onboarding until the Purview Information Protection scanner has labeled every laptop's files
B. Turn on just-in-time protection in endpoint DLP settings so egress of unevaluated files is controlled until scanned
C. Add a device-scoped DLP rule that blocks USB copies of every file, whatever its content or label
D. Configure network share exceptions so file activity on the laptops is only evaluated when on the corporate VPN

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Just-in-time protection applies a configured action to egress of files that endpoint DLP has not yet evaluated, closing the gap while scanning catches up. The scanner targets on-premises file shares, not laptop disks, and delaying onboarding leaves the gap open longer. Blocking every USB copy has no content awareness and stops legitimate work. Network exceptions change where policies apply, they do not protect unscanned files.
</details>

---

### Question 26 - Domain 3: Manage risks, alerts, and activities
**Scenario:** The security team wants Insider Risk Management to flag users who install unwanted software or try to disable security tools, and to combine those signals with data exfiltration activity.

A. Enable the Communication Compliance connector so Insider Risk can read the users' chat messages about security tools
B. Use the data theft by departing users template, with the HR connector providing the triggering resignation date
C. Turn on Adaptive Protection so that DLP policies supply the security tool tampering signals to Insider Risk
D. Integrate Microsoft Defender for Endpoint and use a security policy violations template with device indicators

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The security policy violations templates use Defender for Endpoint alerts, such as installing unwanted software or evading security controls, as indicators and triggers, so the integration is a prerequisite. The departing users template is triggered by resignation and does not score tampering. Adaptive Protection sends insider risk levels to DLP, not device alerts the other way. Communication Compliance reviews messages and is not a source of device security signals.
</details>

---

### Question 27 - Domain 3: Manage risks, alerts, and activities
**Scenario:** A regulator requires three years of audit records for SharePoint file activity by the finance team. Today the tenant keeps audit records for only 180 days.

A. Assign Audit (Premium) licenses to the finance users and create an audit retention policy for SharePoint with a three-year duration
B. Change the default retention in Audit (Standard) to three years for every workload in the audit settings page
C. Place the finance users' mailboxes and OneDrive accounts on litigation hold so their audit history is preserved
D. Create a five-year retention policy on the finance SharePoint sites so their activity records are kept alongside the files

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Custom audit log retention policies, scoped by record type and users, require Audit (Premium) licensing for the users involved. The Audit (Standard) default period is not a setting you can extend. Litigation hold preserves mailbox and OneDrive content, not the audit log. A retention policy on sites keeps files, not the audit records about activity on them.
</details>

---

### Question 28 - Domain 3: Manage risks, alerts, and activities
**Scenario:** The SOC triages everything in the Microsoft Defender portal. They want DLP alerts to appear in the same incident as related endpoint and identity alerts, rather than in a separate queue.

A. Export DLP alerts daily to a CSV file and attach it to the matching Defender incidents by hand
B. Forward DLP alert emails to a shared SOC mailbox, which the analysts check alongside the Defender queue
C. Use the Purview DLP alert integration with Defender XDR, so DLP alerts are correlated into its incidents
D. Recreate the DLP rules as Defender for Endpoint custom detections, so the alerts originate inside Defender

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Purview DLP alerts flow into Microsoft Defender XDR, where they are correlated with other alerts into incidents and can be triaged in one queue. CSV exports and shared mailboxes keep the queues separate and add manual work. Custom detections run on device telemetry and cannot replace content-aware DLP across email, SharePoint, and Teams.
</details>

---

### Question 29 - Domain 3: Manage risks, alerts, and activities
**Scenario:** Legal says a lawsuit is likely involving a sales director. Her mailbox, OneDrive, and Teams chats must be preserved now, searched for named customers, and the results handed to outside counsel.

A. Run a Content search for the customer names and export the results, which also preserves the content in place
B. Create an eDiscovery case, add her as a data source with a hold, then search the held data and export
C. Apply a ten-year retention policy to her mailbox and OneDrive, then ask IT to copy the files to a share
D. Turn on Communication Compliance for her account so reviewers can collect any messages naming the customers

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** An eDiscovery case provides the hold, the search, and the export in one place with access controlled to the case members. A search alone does not preserve anything, so content could be deleted before export. A retention policy is a lifecycle control, not a legal hold scoped to a matter, and copying files by hand breaks the chain of custody. Communication Compliance reviews policy violations and is not a legal preservation tool.
</details>

---

### Question 30 - Domain 3: Manage risks, alerts, and activities
**Scenario:** DSPM for AI shows Copilot interactions but nothing from employees pasting data into third-party AI websites in Chrome. Microsoft Purview Audit is already turned on.

A. Onboard the devices to Purview and deploy the Purview browser extension for Chrome, then turn on the related collection policies
B. Add the AI websites to a Defender for Cloud Apps block list, which feeds their prompt activity into DSPM for AI
C. Assign Copilot licenses to the employees, which extends DSPM for AI reporting to every AI website they visit
D. Create an Insider Risk Management policy for risky AI usage, which is the only source of third-party AI prompts

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Visibility into third-party AI sites depends on device onboarding and, for Chrome, the Purview browser extension, with policies that collect the browsing and paste activity. Blocking the sites in Defender for Cloud Apps stops use but does not create the prompt activity DSPM for AI reports. Copilot licensing covers Copilot, not other AI websites. Insider risk can use these signals, but it relies on the same device and browser collection, so it does not replace the prerequisites.
</details>

---

## Scoring guide

- **26-30 correct (85%+):** Ready. Confirm you can state the retention precedence order from memory.
- **20-25 correct (65-83%):** Re-read the label versus DLP distinction and the insider risk material, which candidates commonly under-study.
- **Below 20:** Work the [scenarios](../../exams/azure/sc-401/scenarios.md) and build the labs in the [practice plan](../../exams/azure/sc-401/practice-plan.md).

All three SC-401 domains are 30-35%, so there is no domain you can afford to skip.
