---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 7 min
---

# CompTIA SecurityX (CAS-005) Scenarios

Worked design and response situations. Each has several workable answers; the point is to pick the best fit for the constraint.

---

## Scenario 1: Unmanaged devices and a SaaS file store

**Scenario**: Contractors use their own laptops to reach the company's sanctioned SaaS file store. The company must stop sensitive files being shared publicly and must find existing public links, without installing agents on the contractors' machines.

**Solution Pattern**:
- An API-based CASB connects to the SaaS provider, scans data at rest and finds existing public shares
- It can remediate retroactively (remove the link) and works for unmanaged devices
- Add conditional access so unmanaged devices get web-only, no-download sessions

**Key Takeaway**: Inline proxies need traffic steering that unmanaged devices will not provide; API-based CASB sees the data in the service.

---

## Scenario 2: Test data

**Scenario**: Developers copy a production customer database into a test environment with weaker access controls. Auditors object.

**Solution Pattern**:
- Replace copies with synthetic data or masked and tokenised extracts
- Apply the same classification and retention rules to non-production
- Add a data governance rule and a gate in the pipeline preventing production data from entering test

**Key Takeaway**: Data governance covers production, development, test and QA.

---

## Scenario 3: Critical flaw on a system that cannot be patched

**Scenario**: A scanner reports a critical CVE on a legacy manufacturing controller that the vendor will not patch.

**Solution Pattern**:
- Check exploitation in the wild and exposure (is it reachable from untrusted networks?)
- Isolate it in a secure zone with microsegmentation and strict allow-listed flows
- Add monitoring and a virtual patch at the gateway; document the exception with an owner and expiry
- Plan replacement

**Key Takeaway**: Severity is not risk; compensate when you cannot remediate.

---

## Scenario 4: Long-lived confidential data

**Scenario**: A company archives data that must stay confidential for 25 years and is sent over public networks today.

**Solution Pattern**:
- The concern is harvest now, decrypt later against public key exchange
- Inventory where public key cryptography protects this data
- Use hybrid key exchange combining classical and post-quantum algorithms (ML-KEM, FIPS 203) where supported
- Build crypto-agility so algorithms can be replaced

**Key Takeaway**: Long confidentiality lifetimes make post-quantum planning urgent now.

---

## Scenario 5: A hunt becomes a detection

**Scenario**: A hunter hypothesises that an adversary is using scheduled tasks for persistence. Searching endpoint logs finds one rare task created by an Office process.

**Solution Pattern**:
- Validate with context (parent process, user, timing) and scope with hash and name searches
- If malicious, start incident response: contain, collect, analyse
- Write the behaviour as a Sigma rule and map it to the ATT&CK technique so it runs continuously
- Measure false positives and tune

**Key Takeaway**: Hunting finds what rules missed; the output is a durable detection.

---

## Scenario 6: Choosing zero trust first steps

**Scenario**: The board wants zero trust but there is little budget.

**Solution Pattern**:
- Start with strong identity and MFA for all access
- Add device posture checks for access to sensitive applications
- Define subject-object relationships for the crown jewels and enforce least privilege there first
- Add microsegmentation and monitoring over time

**Key Takeaway**: Zero trust is a direction built incrementally, starting with identity and the most valuable assets.
