---
last-updated: 2026-10-21
difficulty: beginner
reading-time: 11 min
---

# Least privilege explained

> **11-minute read. Builds on [IAM explained](./iam-explained.md).**

## The one-line answer

[Least privilege](../glossary.md#term-least-privilege) means every person, service and process gets **only the access it needs, only for as long as it needs it**, and nothing more. It does not stop the first mistake or the first stolen credential. It decides how bad that mistake gets. In incident reports, the difference between "one test bucket exposed" and "the whole company's data exfiltrated" is very often a role that had `*` where it needed one action on one resource.

## Why it matters so much

Assume something will be compromised: a developer laptop, a CI token, a vulnerable web app, a contractor's account. The attacker now holds whatever that identity holds. Least privilege is how you keep that small. Security people call this limiting the **blast radius**.

It also protects you from yourself. A deploy script with admin rights can delete production on a typo. A script that can only update one service cannot.

## The dimensions of "least"

People think of least privilege as "fewer permissions". It has more dimensions than that, and each one is a separate lever:

| Dimension | Question | Example of getting it right |
|---|---|---|
| **Actions** | Which operations? | `s3:GetObject`, not `s3:*` |
| **Resources** | On which things? | One bucket prefix, not every bucket |
| **Conditions** | Under what circumstances? | Only from the corporate network, only with MFA, only with a matching tag |
| **Time** | For how long? | Admin for 1 hour after approval, not permanently |
| **Identities** | Who holds it? | Two named on-call engineers, not the whole "engineering" group |
| **Data** | Which records? | This customer's rows, not the whole table |

A permission set that is narrow on actions but broad on resources (`s3:DeleteObject` on `*`) is not least privilege.

## Related principles you will hear alongside it

- **Need to know**: access to information is granted because a task requires it, not because of rank. The data-access version of least privilege.
- **Separation of duties**: no single person can complete a sensitive task alone. The person who writes a payment cannot also approve it; the developer who writes code cannot also push it to production unreviewed.
- **Just-in-time (JIT) access**: no standing admin rights. People request elevation for a specific task and it expires on its own.
- **Default deny**: start from nothing and add, rather than start from everything and remove.

## How to actually achieve it

The honest problem: nobody knows in advance exactly which permissions an application needs, and getting it wrong breaks things. So least privilege is a process, not a one-time design.

### 1. Start from a known baseline

Use the provider's job-function or managed policies to get working, but treat them as a starting point. `ReadOnlyAccess` or a broad `Contributor` role is fine for day one of a sandbox and wrong for month six of production.

### 2. Observe what is actually used

Every major cloud can tell you which permissions an identity has used:

- **AWS IAM Access Analyzer** can generate a policy from CloudTrail activity, and shows last-accessed information per service and action.
- **Google Cloud IAM recommender** flags permissions unused for 90 days and suggests smaller roles.
- **Microsoft Entra** access reviews and Permissions Management show unused and over-privileged identities.

### 3. Tighten, test, repeat

Replace the broad policy with the observed set, scoped to specific resources. Deploy to a test environment, watch for `AccessDenied` errors, add exactly what is missing. Repeat on a schedule, because applications change.

### 4. Put guardrails above individual policies

Organisation-level controls set a ceiling that no account-level policy can exceed: AWS Service Control Policies, Azure Policy and management group assignments, and Google Cloud Organization Policies. Use them for the "never, under any circumstances" rules: no disabling audit logs, no regions you do not operate in, no public storage buckets.

### 5. Remove standing privilege

Use Azure Privileged Identity Management, AWS IAM Identity Center with temporary elevated access, or Google Cloud's Privileged Access Manager so admin roles are activated on demand with a reason, an approval and an expiry.

**[📖 AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)** - least privilege, Access Analyzer and temporary credentials

**[📖 Google Cloud: Role recommendations](https://cloud.google.com/policy-intelligence/docs/role-recommendations-overview)** - how the IAM recommender finds excess permissions

**[📖 Microsoft Entra Privileged Identity Management](https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-configure)** - just-in-time admin roles

## A worked example

A nightly job reads order files from one bucket and writes a report to another. It was set up with this AWS policy:

```json
{
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*"
}
```

If the job's credentials leak, the attacker can read, overwrite and delete every bucket in the account, and change bucket policies to make them public.

A least-privilege version:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadOrders",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::acme-orders/incoming/*"
    },
    {
      "Sid": "WriteReports",
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::acme-reports/nightly/*"
    }
  ]
}
```

Then three more steps finish the job:

- Run it as an **IAM role** attached to the compute, so there are no long-lived keys to leak at all.
- If the files are encrypted with a customer-managed key, grant `kms:Decrypt` on **that key only**.
- Add a bucket policy condition so `acme-orders` can only be read from inside the VPC.

Now a leak exposes one prefix, read-only, from one network location.

## Common mistakes

- **Wildcards that were meant to be temporary.** `"Action": "*"` added to unblock a deploy and never removed.
- **Privilege by group membership.** "All engineers" in a group with production write access. Group sprawl is one of the most common audit findings.
- **Permissions that escalate.** Some permissions are admin in disguise: `iam:PassRole` with `*`, `iam:CreatePolicyVersion`, `iam:AttachUserPolicy`, the ability to edit a CI pipeline that deploys with admin, or Kubernetes rights to create pods in a privileged namespace. Least privilege has to consider what a permission lets you *become*.
- **Orphaned access.** Accounts and keys of people who changed teams or left. Tie access to your HR system and review it on a schedule.
- **Shared accounts.** One login used by five people destroys accountability and makes revocation all-or-nothing.
- **Ignoring non-human identities.** Service accounts, CI tokens and API keys usually outnumber humans and are less reviewed.
- **Making it so painful nobody follows it.** If getting a permission takes two weeks, people find a workaround with more privilege. Fast, self-service, time-bound access requests are part of the design.

## How exams test this

Least privilege is the most reliable "tie-breaker" in exam scenarios. When two answers both work, the one that grants less, for less time, to fewer identities is almost always correct.

- **Security+, ISC2 CC, CISSP**: definitions and differences between least privilege, need to know and separation of duties, plus privilege creep in role changes.
- **AWS security and architect exams**: scoping policies by resource and condition, SCPs as guardrails, roles over access keys, Access Analyzer.
- **Azure AZ-500, SC-300**: PIM, built-in vs custom roles, scope (management group, subscription, resource group, resource).
- **GCP Cloud Security Engineer**: predefined over basic roles, the IAM recommender, organization policies.
- **CISA and CISM**: access review processes and evidence that access is appropriate.

## What to look at next

- **[IAM explained](./iam-explained.md)** - the building blocks least privilege is made of
- **[Zero trust explained](./zero-trust-explained.md)** - least privilege applied to every request
- **[Network security basics](./network-security-basics.md)** - least privilege for network paths
- **[Identity and IAM topic index](../../topics/iam.md)** - everything on this site about identity
