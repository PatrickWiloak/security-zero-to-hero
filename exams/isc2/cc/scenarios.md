---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 8 min
---

# ISC2 CC High-Yield Scenarios

CC questions are shorter than these, but working through scenarios is the fastest way to make the definitions stick. Each one targets a distinction the exam tests.

---

## Scenario 1: Classifying a control

**Scenario**: A company installs a badge reader on the server room door, posts a sign warning that the area is monitored, records entries in a log, and reviews the log monthly.

**Solution Pattern**:
- **Badge reader**: a **physical, preventive** control. It stops unauthorized entry
- **Warning sign**: a **physical (or administrative), deterrent** control. It discourages rather than prevents
- **Entry log**: a **technical or physical, detective** control. It records what happened
- **Monthly review**: an **administrative, detective** control. The process of examining the evidence

**Key Takeaway**: Control **type** (technical, administrative, physical) and control **function** (preventive, detective, corrective, deterrent, compensating) are independent axes. One control has both, and questions ask for one or the other.

---

## Scenario 2: Threat, vulnerability, or risk

**Scenario**: A web server runs an unpatched version of a library with a known remote code execution flaw. Attack groups are actively scanning the internet for it. The server holds customer payment records.

**Solution Pattern**:
- **Vulnerability**: the unpatched library with the known flaw
- **Threat**: the attack groups scanning for it, and their capability to exploit it
- **Asset**: the server and, more importantly, the customer payment records
- **Risk**: the combination of the likelihood that the flaw is exploited and the impact of losing payment records
- **Risk treatment options**: patch (mitigate), take the server offline (avoid), buy cyber insurance (transfer), or document and accept it (accept, which would be indefensible here)

**Key Takeaway**: Vulnerability is the weakness, threat is what could exploit it, risk combines likelihood and impact. Treatment is one of avoid, mitigate, transfer, accept.

---

## Scenario 3: Least privilege or need to know

**Scenario**: An HR analyst can read all employee records for their own region but cannot modify them, and cannot see records for other regions even though the system technically permits reading them.

**Solution Pattern**:
- **Least privilege**: read-only rather than read-write. Their permissions are limited to what the job requires
- **Need to know**: restricted to their own region. Even where access is technically possible, they are limited to the information their duties require
- Both apply here, and they are distinct principles
- The access control model expressing this by job function is **RBAC**; if the region restriction is evaluated from an attribute at access time, it is **ABAC**

**Key Takeaway**: Least privilege limits what you can **do**. Need to know limits what you can **see**. Questions often use one term where the other applies.

---

## Scenario 4: Which access control model

**Scenario**: Four organizations describe their access rules:
1. A government agency where documents are labeled Secret and Top Secret, and the system enforces clearance levels that users cannot override
2. A company where a Sales Manager role carries a fixed set of permissions, and users get permissions by being assigned that role
3. A file server where the person who creates a file decides who else may read it
4. A system that grants access based on the user's department, the device's compliance state, and the time of day

**Solution Pattern**:
1. **MAC** (mandatory access control): the system enforces labels and clearances; users cannot change them
2. **RBAC** (role-based access control): permissions attach to roles, users attach to roles
3. **DAC** (discretionary access control): the data owner decides
4. **ABAC** (attribute-based access control): the decision is evaluated from multiple attributes at access time

**Key Takeaway**: MAC is system-enforced and label-based, DAC is owner-discretionary, RBAC is role-based, ABAC evaluates attributes. All four appear as options together.

---

## Scenario 5: Which discipline owns this

**Scenario**: A ransomware attack encrypts a hospital's file servers. Several activities follow:
1. Isolating the affected network segment
2. Switching clinical staff to paper forms so patient care continues
3. Restoring the file servers from backup
4. A meeting two weeks later to work out how the attacker got in

**Solution Pattern**:
1. **Incident response** - containment phase
2. **Business continuity** - keeping the business function running while systems are unavailable
3. **Disaster recovery** - restoring the technology
4. **Incident response** - post-incident activity, or lessons learned

**Key Takeaway**: BC keeps the business running, DR restores technology, IR handles the security event. A real incident invokes all three, and the exam asks which one owns a specific activity.

---

## Scenario 6: RTO and RPO

**Scenario**: A payments company states that it can tolerate at most 15 minutes of lost transactions, and that the service must be back within 2 hours of a failure. Backups currently run nightly and a full restore takes about 6 hours.

**Solution Pattern**:
- **RPO = 15 minutes**: the maximum acceptable data loss. Nightly backups give an RPO of up to 24 hours, so they fail this by a wide margin. Meeting it needs continuous replication or transaction log shipping
- **RTO = 2 hours**: the maximum acceptable downtime. A 6-hour restore fails this. Meeting it needs a warm or hot standby rather than a restore from backup
- Both objectives are currently unmet, and they require different fixes: RPO drives **backup and replication frequency**, RTO drives **recovery capability**

**Key Takeaway**: RPO is about data loss and is fixed by backup frequency. RTO is about downtime and is fixed by recovery architecture. Confusing them is the classic error.

---

## Scenario 7: Which cryptography

**Scenario**: A system needs three things: to store user passwords so they cannot be recovered, to encrypt a large database file efficiently, and to let two parties who have never met exchange a key securely.

**Solution Pattern**:
- **Passwords**: **hashing**, with a salt. Hashing is one way; the point is that the original cannot be recovered. Storing passwords encrypted would be wrong, because encryption is reversible
- **Large database file**: **symmetric** encryption (such as AES). It is fast and suited to bulk data
- **Key exchange between strangers**: **asymmetric** encryption. It solves key distribution, and is also what enables digital signatures
- The common real-world pattern combines them: asymmetric to exchange a symmetric key, then symmetric for the bulk data

**Key Takeaway**: Hashing for integrity and password storage, symmetric for bulk speed, asymmetric for key exchange and signatures. Hashing is not encryption.

---

## Scenario 8: Shared responsibility

**Scenario**: A company asks who is responsible for four things across its cloud estate: patching the hypervisor, patching the guest operating system on its virtual machines, configuring who can access its SaaS CRM, and physical security of the datacenter.

**Solution Pattern**:
- **Hypervisor patching**: the **provider**, in every service model
- **Guest OS patching**: the **customer** in IaaS; the **provider** in PaaS and SaaS
- **Access configuration in SaaS**: the **customer**. Identity and access configuration is always the customer's responsibility, in every model
- **Physical datacenter security**: the **provider**, always

**Key Takeaway**: Responsibility shifts toward the provider as you move from IaaS to PaaS to SaaS. Two things never shift: physical security is always the provider's, and data and access configuration are always the customer's.

---

## Scenario 9: KPI or KRI

**Scenario**: A security manager is building a monthly scorecard for leadership. She has four candidate measures: the percentage of critical patches applied within 14 days; the number of internet-facing servers currently missing a critical patch; the phishing simulation click rate, which has risen for three months in a row; and the total number of spam emails blocked.

**Solution Pattern**:
- **Critical patches applied within 14 days**: a **KPI**. It measures how well the patching process performs against a target, looking back
- **Internet-facing servers missing a critical patch**: a **KRI**. It signals exposure right now and rises before a breach does
- **Rising phishing click rate**: a **KRI**. The trend says the risk of a successful phish is growing, which should trigger action before an incident
- **Spam emails blocked**: a **vanity metric**. It sounds impressive, has no target, and drives no decision

**Key Takeaway**: A KPI asks how well the work is being done; a KRI asks how close the organization is to trouble. Leadership scorecards should lead with a few KRIs that have agreed thresholds.

---

## Scenario 10: Red, blue, or purple

**Scenario**: A company wants to know three things: whether its security operations team would notice a skilled attacker; how to improve its detection of credential theft techniques as quickly as possible; and whether reception staff challenge a visitor claiming to be a fire safety inspector.

**Solution Pattern**:
- **Would the team notice a skilled attacker?** A **red team** exercise. The red team emulates a real adversary toward a goal, and the blue team is not told in advance, so the result measures real detection and response
- **Improve credential theft detection fast?** **Purple teaming**. Red runs each technique openly while blue checks its detections and tunes them on the spot
- **Do staff challenge an impostor?** A **physical penetration test** using **impersonation**, with written authorization and agreed rules of engagement

**Key Takeaway**: Red measures, purple improves, blue defends. Physical penetration tests cover the human and physical controls that technical tests miss, and their results feed security awareness training.

---

## Related

- [Practice plan](./practice-plan.md)
- [Strategy](./strategy.md)
- [Notes](./notes/)
- [Shared responsibility model](../../../learn/concepts/shared-responsibility-model.md)
- [Practice questions](../../../resources/practice-questions/isc2-cc.md)
