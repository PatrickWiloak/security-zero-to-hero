# Microsoft Identity and Access Administrator (SC-300) - Practice Questions

19 questions for SC-300 prep, aligned to the skills outline as of October 28, 2026 (questions 16 to 19 cover Global Secure Access and emergency access). Watch for the license tier stated in each scenario: it decides several of these outright.

> **Cert page:** [exams/azure/sc-300/](../../exams/azure/sc-300/)

---

### Question 1
**Scenario:** A consultancy onboards 200 contractors per quarter. Each needs specific applications, a SharePoint site, and a group. Access must be self-requested, approved by the engaging partner, and expire after 90 days. The tenant has Entra ID Governance licensing.

A. An entitlement management access package with an approval policy and 90-day expiry
B. PIM eligible assignments of Entra roles for each contractor, activated on request with approval and an expiry of 90 days
C. Manual assignment by the helpdesk each quarter, with calendar reminders to remove each contractor after 90 days
D. A dynamic group with a contractor attribute rule, so that membership and application access follow the user's department and job title

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Access packages are the only feature bundling heterogeneous resources behind a request, approval, and expiry workflow. Dynamic groups have no request or approval and no expiry. PIM governs privileged role activation, not resource entitlement. Manual assignment does not scale to 200 per quarter.
</details>

---

### Question 2
**Scenario:** Administrators must use phishing-resistant MFA for the Azure portal. Standard users continue with Microsoft Authenticator. What should be configured?

A. Per-user MFA settings enforced for each administrator account, so that they must complete a second factor on every sign-in
B. A custom authentication strength of FIDO2 and Windows Hello for Business, required by Conditional Access for administrators on Azure Management, scoped to the administrator roles
C. A Conditional Access policy requiring MFA for the administrator roles on all cloud apps, with Microsoft Authenticator as an accepted method
D. Removal of SMS and voice call from the tenant authentication methods policy, so that only app-based methods remain for all users

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** "Phishing-resistant" maps to authentication strengths, which name the specific permitted methods. A generic MFA requirement does not distinguish method strength. Removing SMS tenant-wide affects all users, not just administrators. Per-user MFA is legacy and cannot express method strength.
</details>

---

### Question 3
**Scenario:** Users synchronized from on-premises AD report that self-service password reset appears to succeed but their on-premises password is unchanged. What is missing?

A. They have not completed combined registration, so the service has no verified method on file and cannot change the on-premises password
B. SSPR is not enabled for their group, so the reset flow completes in the cloud but is never applied to the on-premises directory
C. Password writeback is not enabled in Entra Connect
D. The authentication methods policy blocks their registered method, so the reset is only partly processed by the service

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Without password writeback, SSPR changes only the cloud password for a synced user. The symptom is exactly this: the portal reports success and the on-premises directory is untouched. The other options would prevent the reset from appearing to succeed at all.
</details>

---

### Question 4
**Scenario:** A nightly job must read all users' calendars with no signed-in user. `Calendars.Read` was granted as a delegated permission and the job returns 403.

A. Grant a higher delegated permission such as `Calendars.ReadWrite`, so that the app has enough rights to read every user's calendar
B. Assign the Global Reader role to the service principal, so that it can read all directory, mailbox and calendar data in the tenant
C. Grant `Calendars.Read` as an application permission with admin consent, and use client credentials or a managed identity
D. Create a service account with a password and a license, and have the job sign in as that account

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Delegated permissions require a signed-in user and grant the intersection of app and user rights. A daemon has no user, so application permissions with admin consent are required. Entra roles are not Graph permissions. A service account with a password is the pattern managed identities exist to replace.
</details>

---

### Question 5
**Scenario:** An audit finds guests can enumerate the whole directory. B2B collaboration must continue. What fixes it?

A. Block all B2B collaboration in the external collaboration settings, which stops guests from enumerating the directory by removing them
B. Convert guests to member accounts so that they are governed by the same policies as employees and are easier to review
C. A Conditional Access policy targeting guest users and requiring MFA, which controls how guests sign in
D. Restrict external user permissions to the most limited option, limit who can invite, and review guests regularly

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Directory enumeration by guests is governed by external collaboration settings, not Conditional Access, which controls sign-in conditions rather than directory read permissions. Converting guests to members grants more directory access, not less. Blocking B2B fails the requirement.
</details>

---

### Question 6
**Scenario:** A GitHub Actions workflow deploys to Azure using a service principal client secret that expired over a weekend. Security also objects to a long-lived credential with subscription Contributor rights.

A. Configure workload identity federation scoped to the repository and environment, remove the secret, and narrow the RBAC scope
B. Automate secret rotation with a pipeline job that creates a new client secret before the old one expires and updates GitHub each month
C. Store the secret in Azure Key Vault and have the workflow retrieve it at run time, so it is no longer kept in GitHub
D. Use a user-assigned managed identity on the GitHub-hosted runner, which then signs in to Azure without any stored secret, leaving the Contributor assignment as it is

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Federation removes the stored credential entirely by trusting GitHub's OIDC issuer. Scoping the federated credential subject to a branch or environment is what makes it safer than the secret it replaces. Rotation still leaves a long-lived credential. Key Vault still requires a credential to reach Key Vault. GitHub-hosted runners are not Azure resources, so a managed identity alone does not apply.
</details>

---

### Question 7
**Scenario:** An administrator plans a Conditional Access policy requiring compliant devices for all users and all cloud apps. Intune enrolment is at 60%. What is the correct deployment approach?

A. Exclude the Global Administrator role from the policy, so that the most privileged accounts can never be locked out of the tenant
B. Deploy in report-only mode, review the Conditional Access insights workbook, exclude two break-glass accounts, and roll out in stages as enrolment grows
C. Enable security defaults instead, which require MFA for everyone and apply a fixed baseline without waiting for Intune enrolment
D. Enable it for all users immediately, and have the 40% of users who are not enrolled enrol their devices when prompted at sign-in

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Report-only mode, break-glass exclusions, and staged rollout are expected in every Conditional Access answer. Immediate enforcement locks out 40% of the organization. Security defaults are all-or-nothing and disable Conditional Access. A role exclusion is not a break-glass account; break-glass means specific excluded cloud-only user accounts with monitoring.
</details>

---

### Question 8
**Scenario:** Twelve engineers hold permanent Global Administrator. Audit requires no standing privilege, approval before elevation, recorded justification, and quarterly recertification of eligibility. The tenant has Entra ID P2.

A. Conditional Access requiring MFA for administrators, so that each of the twelve signs in with a second factor every time before using the role
B. Remove the role from all twelve engineers and re-add it manually through a change ticket whenever a task needs it
C. Convert to PIM eligible assignments with approval and justification, enable PIM alerts, and configure a quarterly PIM access review
D. An entitlement management access package containing the role, with approval and expiry set on the request for each engineer

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** No standing privilege plus approval plus justification is PIM. Conditional Access adds a sign-in condition while leaving standing privilege in place. Access packages govern resource entitlement, not directory role activation. Manual add and remove has no approval or audit trail.
</details>

---

### Question 9
**Scenario:** Which role can reset the password of a user who holds the Application Administrator role?

A. Helpdesk Administrator, which can reset passwords for non-administrators and some limited roles but not for Application Administrators
B. Authentication Administrator, which manages authentication methods and passwords for non-administrator users only
C. User Administrator, which can create and manage users and groups and reset passwords for non-admin users
D. Privileged Authentication Administrator, which can reset passwords and authentication methods for users in privileged roles

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Only Privileged Authentication Administrator can manage authentication methods and credentials for users holding privileged roles. User Administrator, Authentication Administrator, and Helpdesk Administrator are all blocked from acting on privileged-role holders, which is a deliberate protection and a frequent exam point.
</details>

---

### Question 10
**Scenario:** A tenant has Entra ID P1 only. Which requirement cannot be met without a license upgrade?

A. Self-service password reset with writeback, which lets synced users reset passwords and have them applied to on-premises AD
B. Conditional Access requiring MFA, which applies grant controls to sign-ins by user, app and location
C. Risk-based Conditional Access using sign-in risk
D. Application Proxy for an on-premises web app, which publishes internal sites through connectors without opening inbound firewall ports

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Sign-in risk and user risk conditions come from Entra ID Protection, which requires P2. Conditional Access itself, SSPR with writeback, and Application Proxy are all P1 capabilities. License tier is the single most common decider on this exam.
</details>

---

### Question 11
**Scenario:** What is the difference between an application registration and an enterprise application?

A. The enterprise application is the older term and has been replaced by the app registration in the current portal
B. The registration is the global definition in the home tenant; the enterprise application is the service principal instance in each tenant that consents to it
C. The registration is for single-tenant apps and the enterprise application is for multi-tenant apps, so a tenant uses one or the other
D. They are two names for the same object, shown under different menus depending on the type of app

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Registering an app creates both objects in your tenant. Consenting to a third-party multi-tenant app creates only a service principal locally, because the registration lives in the vendor's tenant. You configure API permissions and credentials on the registration, and SSO, user assignment, and provisioning on the enterprise application.
</details>

---

### Question 12
**Scenario:** A company must ensure that a specific group of users can only sign in from managed devices located in their home country, and that a stolen refresh token cannot be replayed elsewhere.

A. Conditional Access requiring a compliant device plus a location condition, with token protection as a session control
B. An IP allowlist on the application, which accepts sign-ins only from the corporate address ranges but cannot check device state
C. A named location condition alone, which limits sign-ins to the home country but does not check the device
D. Sign-in frequency set to one hour, which forces frequent reauthentication but allows a stolen token to be replayed within that hour

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Device compliance and location are Conditional Access conditions and grant controls. Token protection binds a refresh token to the device it was issued to, which addresses replay. An IP allowlist alone does not verify the device. Sign-in frequency shortens the window but does not prevent replay within it.
</details>

---

### Question 13
**Scenario:** Which hybrid identity method allows Entra ID Protection to detect leaked credentials?

A. Federation with AD FS, where authentication happens on-premises and no password hashes are stored in Entra ID
B. Any of them, since detection of leaked credentials runs in the cloud regardless of which hybrid method is used
C. Pass-through authentication, where passwords are validated by agents on-premises and no hash is stored in the cloud directory
D. Password hash sync

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Leaked credential detection compares synced password hashes against credentials found in breach corpora, so it requires password hash sync. PTA and federation store no hash in Entra ID, so the detection cannot run. This is a common reason to enable password hash sync alongside another method.
</details>

---

### Question 14
**Scenario:** A regional helpdesk must reset passwords only for users in its own region. What should be configured?

A. A custom role scoped to a security group
B. An administrative unit containing the regional users, with the Helpdesk Administrator role assigned over it
C. A dynamic group of regional users with the helpdesk staff as its owners
D. A Conditional Access policy restricting the helpdesk to sign in from the regional office network and managed devices

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Administrative units scope a role assignment to a subset of the directory, which is exactly this delegation pattern. Roles are assigned over an administrative unit, not inside it. Conditional Access governs sign-in, not administrative scope. Group ownership does not confer password reset rights.
</details>

---

### Question 15
**Scenario:** An access review must remove access automatically from anyone whose reviewer does not respond. What setting achieves this?

A. Auto-apply results, with "If reviewers don't respond" set to Remove access, so silent reviewers lose access automatically
B. Recurring reviews with a manual apply step, so that an administrator confirms every result
C. Auto-apply results, with "If reviewers don't respond" set to No change
D. A lifecycle workflow triggered on the review end date, which runs a task to remove access for users whose review is incomplete

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Both settings are required: auto-apply enacts decisions without an administrator, and the no-response behavior determines what happens to unreviewed access. "No change" leaves access in place, which is the opposite of the requirement. A manual apply step contradicts "automatically". Lifecycle workflows handle joiner, mover, and leaver events, not review outcomes.
</details>

---

### Question 16
**Scenario:** Staff reach an on-premises HR application over a VPN that exposes the whole server subnet. Leadership wants HR staff to reach only that application, with MFA and a compliant device, and no inbound firewall ports opened. The Global Secure Access client is already deployed.

A. Publish the app through Microsoft Entra Internet Access with a web content filtering profile for the HR group
B. Keep the VPN and add a Conditional Access policy requiring MFA on the VPN server's enterprise application
C. Enable the Microsoft traffic profile and configure universal tenant restrictions for the HR group
D. Install a Private Access connector, publish the app's FQDN and port as an application, assign the HR group, and target it with Conditional Access

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Microsoft Entra Private Access gives per-application network access through an outbound-only connector, and each published application can carry its own Conditional Access policy. Internet Access governs internet and SaaS traffic, the Microsoft traffic profile covers Microsoft 365, and MFA on the VPN still leaves the whole subnet reachable after connection.
</details>

---

### Question 17
**Scenario:** A security team wants to stop employees from signing into other organizations' Microsoft 365 tenants, or personal accounts, from corporate devices, as a data exfiltration control.

A. Enable the Microsoft traffic profile in Global Secure Access and turn on universal tenant restrictions
B. Configure cross-tenant synchronization so other tenants' users are created as guests in this tenant
C. Block external collaboration in the tenant's B2B external collaboration settings
D. Create a Conditional Access policy that blocks all guest and external users from cloud apps

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Universal tenant restrictions, delivered through the Microsoft traffic profile, control which tenants your users can sign into from your managed devices. External collaboration settings and Conditional Access govern who can access your own tenant, which is the opposite direction, and cross-tenant synchronization provisions users rather than restricting sign-ins.
</details>

---

### Question 18
**Scenario:** An organization is creating its emergency access accounts. Which configuration follows Microsoft's guidance?

A. One synchronized on-premises account with Global Administrator, protected by the same Authenticator app the admins use daily
B. Two accounts eligible for Global Administrator in PIM, with activation requiring approval from the security team
C. Two cloud-only accounts on the onmicrosoft.com domain with permanent active Global Administrator, passkey (FIDO2) sign-in, exclusion from blocking Conditional Access policies, and an alert on every sign-in
D. Two cloud-only accounts with no MFA registered at all, so that an authentication outage cannot affect them

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Emergency accounts must survive the failures that lock out normal admins: synchronization and federation outages, PIM activation dependencies, and broken policies. Microsoft now recommends a phishing-resistant method that differs from everyday admin accounts, rather than no MFA, and an alert on every sign-in so use always gets reviewed.
</details>

---

### Question 19
**Scenario:** Administrators may browse the Conditional Access blade freely, but anyone who tries to change or delete a Conditional Access policy must have just satisfied phishing-resistant MFA from a compliant device.

A. Require phishing-resistant MFA for all directory roles in a Conditional Access policy targeting the Microsoft Admin Portals app
B. Assign an authentication context to the Conditional Access policy permissions as a protected action, and require the controls in a policy targeting that context
C. Make the Conditional Access Administrator role eligible in PIM with an approval step
D. Create an access review of the Conditional Access Administrator role every week

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Protected actions step up authentication at the moment a specific high-impact permission is used, regardless of role. A policy on the admin portals applies on every visit, not only to changes; PIM governs when the role is held, not individual operations; and access reviews check membership after the fact.
</details>

---

## Scoring guide

- **16-19 correct (85%+):** Ready. Spend remaining time in a trial tenant building Conditional Access policies.
- **12-15 correct (65-80%):** Review the license boundary table and the feature-boundary table in the [strategy notes](../../exams/azure/sc-300/strategy.md).
- **Below 12:** Work through the domain notes, then build the labs listed in the [practice plan](../../exams/azure/sc-300/practice-plan.md).

Two habits carry this exam: read the license tier first, and know precisely which of Conditional Access, PIM, entitlement management, and access reviews solves the stated problem.
