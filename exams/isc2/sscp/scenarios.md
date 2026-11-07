---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 7 min
---

# ISC2 SSCP Scenarios

Worked situations, each targeting a distinction the exam leans on.

---

## Scenario 1: The leaver

**Scenario**: A network administrator resigns and works out a notice period. HR sends the leaving date. On that date the help desk disables the person's directory account, but two weeks later the VPN still accepts a login from the same name.

**Solution Pattern**:
- Find the local VPN account or the certificate that was not tied to the directory
- Disable it, then review the logs for use since the leaving date
- Rotate any shared secret the administrator knew (device passwords, service account secrets)
- Fix the cause: deprovisioning must be driven from one authoritative source and cover every system

**Key Takeaway**: Orphaned accounts and shared secrets are the usual leaver gap. Deprovisioning is a process across all systems, not one click.

---

## Scenario 2: Priority is not just the score

**Scenario**: A scan reports a critical flaw on an isolated lab server and a medium flaw on an internet-facing customer portal that stores personal data.

**Solution Pattern**:
- Consider exploitability and exposure as well as severity
- The portal is reachable by anyone and holds sensitive data, so it comes first
- Record the lab server finding with a due date and compensating isolation

**Key Takeaway**: Prioritise by severity, exploitability, asset criticality and exposure together.

---

## Scenario 3: First action on a suspected compromise

**Scenario**: The SIEM shows a server making outbound connections to an unknown address and a new local admin account. The server runs a payment service.

**Solution Pattern**:
- Confirm and scope enough to be sure this is an incident, and open the incident record with a timeline
- Escalate under the plan and involve the service owner
- Contain: isolate the server from the network, ideally without powering it off, so memory is preserved
- Collect volatile evidence first, keep chain of custody, and work from forensic copies
- Eradicate by rebuilding from a known-good image, restore, and review

**Key Takeaway**: Analyse, escalate, contain, preserve evidence in order of volatility, then rebuild. Do not clean and carry on.

---

## Scenario 4: Choosing the recovery design

**Scenario**: A business impact analysis says order processing can be down 4 hours at most and can lose 15 minutes of data at most.

**Solution Pattern**:
- MTD is 4 hours, so the RTO must be shorter, for example 2 hours
- The RPO of 15 minutes means backups or replication at least every 15 minutes
- That points to a hot or warm site with continuous replication, not nightly tapes

**Key Takeaway**: RTO comes from downtime tolerance, RPO from data loss tolerance, and the two together choose the design.

---

## Scenario 5: A signature, not a hash

**Scenario**: A software vendor wants customers to be sure an update is genuine and unaltered. A colleague suggests publishing a SHA-256 hash next to the download.

**Solution Pattern**:
- A hash shows the file matches the hash, but an attacker who swaps the file can swap the published hash too
- Sign the update with the vendor's private key; customers verify with the public key from a certificate chain they trust
- Protect the signing key in a hardware security module

**Key Takeaway**: Integrity needs a hash; authenticity and non-repudiation need a signature.

---

## Scenario 6: The unpatchable camera

**Scenario**: Fifty IP cameras run firmware that the vendor no longer updates, and they sit on the main office network.

**Solution Pattern**:
- Put them on a dedicated segment with default-deny to the internet and to other VLANs
- Change default credentials and disable unused services
- Monitor their traffic for change
- Plan replacement; a compensating control is temporary, not a fix

**Key Takeaway**: End-of-life devices get isolation and monitoring now, and replacement on a schedule.
