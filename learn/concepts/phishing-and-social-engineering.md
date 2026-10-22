---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 11 min
---

# Phishing and social engineering

> **11-minute read. No prerequisites. Written from the defender's side: how to recognise, prevent and respond.**

## The one-line answer

Social engineering is manipulating people, rather than computers, into doing something that helps an attacker: handing over a password, approving a login, paying a fake invoice, resetting someone else's MFA. [Phishing](../glossary.md#term-phishing) is the most common form, delivered by email, text, phone or chat. It works because it targets trust, urgency and helpfulness, which no patch can remove. The defence is layered: technical controls that stop most messages and make stolen credentials useless, processes that require verification for risky requests, and a culture where reporting a suspicious message is easy and praised.

## Why it works

Social engineering exploits normal, useful human traits:

- **Authority**: the message appears to come from a boss, IT, a bank or a government agency.
- **Urgency**: "your account will be closed in 24 hours", "the CEO needs this before the board meeting".
- **Fear or reward**: a failed payment, a parcel that can't be delivered, a bonus.
- **Helpfulness**: the help desk wants to unblock a caller who sounds stressed.
- **Familiarity**: the message names a real colleague, a real vendor, a real project, often scraped from LinkedIn or a previous breach.

The goal is to make the target act before they think. Every defence below either slows that moment down or makes the action harmless.

## The common forms

| Form | What it looks like | What the attacker wants |
|---|---|---|
| **Credential phishing** | Email with a link to a fake login page (Microsoft 365, Google, a bank) | Username, password and, with real-time proxy kits, the MFA code and session cookie |
| **Spear phishing** | A targeted message using personal or company details | Higher success against a specific person |
| **Whaling** | Spear phishing aimed at executives | Access to high-authority accounts and decisions |
| **Business email compromise (BEC)** | "Please update our bank details for the next invoice" from a real or look-alike vendor address | A fraudulent payment; consistently among the costliest cybercrimes reported to the FBI |
| **Smishing / vishing** | Phishing by SMS or voice call | Codes, credentials or a payment |
| **Help-desk social engineering** | A caller impersonates an employee and asks for a password or MFA reset | An account takeover that bypasses MFA entirely |
| **MFA fatigue** | Repeated push prompts until the user taps Approve | MFA bypass with an already-stolen password |
| **Malicious attachments** | Invoices, "scanned documents", shared-file notifications | Malware on the endpoint |
| **QR code phishing (quishing)** | A QR code in an email or on a poster leading to a fake login | Moves the victim to a phone, outside corporate email filtering |
| **Consent phishing** | "This app wants access to your mailbox" via a real OAuth consent screen | A token for the victim's data, with no password involved |
| **Pretexting** | A believable story built over several contacts | Information or access, gathered gradually |

Generative AI has made phishing more fluent: spelling mistakes and awkward grammar are no longer reliable tells, and voice cloning makes "the CFO called me" requests more convincing. That shifts the emphasis further toward verification processes and phishing-resistant technology.

## Recognising a phishing attempt

Training should teach patterns, not a checklist of typos:

- **The request is unusual for the channel or the person.** A vendor changing bank details by email; an executive asking for gift cards; IT asking for your password (real IT never needs it).
- **Pressure to act now** and to skip normal process or keep it quiet.
- **The sender or link doesn't match.** A display name of "Microsoft" with an unrelated address; a link that reads `login.micros0ft-support.com`. Hover before clicking; on mobile, long-press.
- **An unexpected login or MFA prompt.** If you did not just try to log in, the correct response is Deny, then report.
- **A login page reached from a link** rather than from your bookmark or by typing the address.

## Technical controls

### Email authentication: SPF, DKIM and DMARC

These three DNS-based standards let receiving mail servers check whether a message claiming to be from your domain really is:

- **SPF** lists the servers allowed to send mail for your domain.
- **DKIM** adds a cryptographic signature so receivers can check the message was not altered and came from an authorised sender.
- **DMARC** tells receivers what to do when a message fails those checks (`p=none` to monitor, `p=quarantine`, `p=reject`) and sends you reports.

Moving to `p=reject` stops attackers sending email that exactly spoofs your domain. It does not stop look-alike domains, which is why the other layers matter. Major mailbox providers now require SPF, DKIM and DMARC for bulk senders.

**[📖 DMARC.org overview](https://dmarc.org/overview/)** - how SPF, DKIM and DMARC fit together

The deep dive, with alignment, reports and a worked rollout to `p=reject`, is **[Email security: SPF, DKIM and DMARC](./email-security-spf-dkim-dmarc.md)**.

**[📖 Google: Email sender guidelines](https://support.google.com/a/answer/81126)** - authentication requirements for sending to Gmail

### Filtering and browsing protection

- Secure email gateways and built-in protection (Microsoft Defender for Office 365, Google Workspace) scan links and attachments, sandbox suspicious files and flag external senders.
- DNS filtering and secure web gateways block known phishing domains at click time.
- Browser protections such as Safe Browsing warn on known malicious pages.

### Make stolen credentials useless

The strongest control is to make the thing phishing steals worthless:

- **[Phishing-resistant MFA](./mfa-and-passkeys.md)** (passkeys, FIDO2 security keys) cannot be relayed by a fake site. This one control defeats most credential phishing, including real-time proxy kits.
- **Number matching** on push MFA stops blind approvals.
- **Conditional access** that requires a managed device means a stolen password from an unknown laptop gets nowhere.
- **Restricting OAuth app consent** so users cannot grant mailbox access to unverified apps.

### Endpoint controls

EDR, application allowlisting, blocking macros in documents from the internet, and keeping browsers and operating systems patched limit what a malicious attachment can do.

## Process controls

Many of the costliest attacks involve no malware at all, only a convincing request. These need process:

- **Out-of-band verification for money and access changes.** Any change of bank details, or any urgent payment request, is confirmed by calling a known number from your records, never the number in the email.
- **Two-person approval** for payments above a threshold.
- **Help-desk identity verification** that does not rely on information an attacker can find (date of birth, employee ID). Use video verification against an ID photo, a manager's approval, or a callback to a registered number, and require extra steps for privileged accounts.
- **Alerting users when their MFA or password changes**, so a victim notices quickly.

## Culture and training

- **Make reporting easy**: a "Report phishing" button in the mail client, and a quick thank-you every time someone uses it, even for false alarms.
- **Never punish clicking.** People who fear punishment stop reporting, and late reporting is what turns a click into a breach.
- **Train on current, relevant examples** for each role. Finance needs BEC scenarios; the help desk needs impersonation scenarios; developers need consent phishing and fake package notifications.
- **Phishing simulations** are useful for awareness if they are educational and measure reporting rate, not just click rate. A rising reporting rate is the metric that matters.

**[📖 CISA: Phishing guidance, stopping the attack cycle at phase one](https://www.cisa.gov/resources-tools/resources/phishing-guidance-stopping-attack-cycle-phase-one)** - joint government guidance for organisations

## When someone has clicked

Speed matters more than blame. A good short runbook:

1. The user reports immediately (and is thanked).
2. If credentials were entered: reset the password, **revoke all sessions and tokens**, review and remove any MFA methods or mailbox rules the attacker added (forwarding rules to external addresses are a classic sign).
3. If an attachment was opened: isolate the device and let EDR or the security team investigate.
4. Search mail for the same message and remove it from every inbox.
5. Block the sender, domain and URLs.
6. Check sign-in logs for activity from the attacker's IP or device.

See [Incident response basics](./incident-response-basics.md) for the wider process.

## How exams test this

- **Security+ and ISC2 CC**: identify the attack type from a scenario (phishing vs spear phishing vs whaling vs vishing vs smishing vs pretexting vs BEC), the psychological principles (authority, urgency, scarcity, familiarity), and the best mitigation, which is often user awareness training plus a technical control.
- **SC-200 and SC-900**: Defender for Office 365 features, user-reported messages, automated investigation of phishing.
- **CySA+**: analysing email headers and authentication results (SPF/DKIM/DMARC pass or fail) to decide whether a message is malicious.
- **CISSP**: security awareness programmes and their measurement.

## What to look at next

- **[MFA and passkeys](./mfa-and-passkeys.md)** - the control that defeats most credential phishing
- **[Security awareness training](./security-awareness-training.md)** - running the programme: role-based content, reporting culture and metrics beyond click rate
- **[Incident response basics](./incident-response-basics.md)** - what to do after a successful phish
- **[Logging and detection](./logging-and-detection.md)** - detecting suspicious sign-ins and mailbox rules
