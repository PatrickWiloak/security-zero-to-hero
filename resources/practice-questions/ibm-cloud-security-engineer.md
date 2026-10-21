---
last-updated: 2026-08-09
difficulty: advanced
---

# IBM Cloud Security Engineer - Practice Questions

15 questions for this exam, weighted toward identity and access management (25%), then data protection and network security (20% each), monitoring and compliance (15%), and application and specialized security.

> **Cert page:** [exams/ibm/cloud-security-engineer/](../../exams/ibm/cloud-security-engineer/)

---

### Question 1
**Scenario:** Permissions must be granted to 40 engineers with identical needs.

A. Individual policies per user, written once for each engineer so that each person's access can be traced to a single policy
B. Shared credentials for the team, kept in one place so that nobody waits for a policy change when they join
C. An access group with the policies attached, and users added to it
D. Administrator for every engineer, with the unneeded access removed later once the team's actual usage is known

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Access groups are the manageable unit in IBM Cloud IAM: change the policy once and it applies to all members, and joiners are handled by group membership. Forty individual policy sets diverge within months and cannot be reviewed meaningfully.
</details>

---

### Question 2
**Scenario:** An application needs to call IBM Cloud APIs without a human account.

A. A personal API key belonging to the engineer who built the application, since it already carries the permissions the application needs
B. Root credentials of the account owner, stored in the application's configuration so that calls never fail on permissions
C. A service ID with its own API key or trusted profile, scoped to the required services
D. A shared user account with a long-lived password kept in the deployment pipeline, used by every service that calls the APIs

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Service IDs decouple application access from any individual, so nothing breaks when a person leaves and the access is attributable to the workload. Trusted profiles go further by letting a compute resource assume an identity without a stored key at all.
</details>

---

### Question 3
**Scenario:** Encryption keys must be under customer control in a dedicated HSM.

A. Application-level encryption only, with the keys held in the application's own configuration files and rotated by the team
B. Hyper Protect Crypto Services with Keep Your Own Key, so IBM cannot reach the key material
C. Key Protect only, since it is a dedicated single-tenant HSM whose master keys IBM can never access or use
D. Provider-managed keys, which IBM generates and rotates so that the customer never has to look after key material

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Key Protect is the multi-tenant managed KMS and is the right default for most workloads. HPCS adds a single-tenant FIPS-validated HSM with customer-controlled master keys, which is what a "the provider must not be able to decrypt" requirement demands.
</details>

---

### Question 4
**Scenario:** Data must be protected while it is being processed.

A. TLS on every connection, which also protects data in memory
B. Disk encryption with a customer-managed key
C. A firewall around the subnet, which stops a compromised hypervisor reading memory
D. Confidential computing with IBM Secure Execution or Hyper Protect, isolating data in use from privileged operators

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Encryption at rest and in transit leave a gap while data is in memory, which is where a compromised hypervisor or a malicious operator would look. Confidential computing closes that with hardware-enforced isolation, which is IBM's strongest differentiator here.
</details>

---

### Question 5
**Scenario:** A VPC workload must reach IBM Cloud services without traversing the public internet.

A. A VPN to the internet, with an IPsec tunnel to the service's public endpoint
B. Virtual private endpoints or the private service endpoint network, which keep traffic on the IBM Cloud private network
C. Public endpoints with an allowlist of the VPC's floating IPs
D. A public gateway that hides the workload's private address

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Private endpoints keep traffic on the IBM Cloud private network with an address inside your VPC. An allowlist on a public endpoint reduces exposure but the traffic still leaves your network, which is usually not what the requirement means.
</details>

---

### Question 6
**Scenario:** VPC network traffic must be filtered at two levels.

A. Host firewalls only, such as iptables rules on each virtual server, because filtering at the guest keeps the policy next to the workload
B. Network ACLs only, applied to subnets, since they track connections
C. Security groups only, applied to subnets
D. Security groups (stateful, on network interfaces) and network ACLs (stateless, on subnets)

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The stateful versus stateless distinction is the operational trap: a security group allows return traffic automatically, while an ACL needs an explicit rule for the ephemeral port range in the opposite direction. Layering both gives defense in depth.
</details>

---

### Question 7
**Scenario:** Secrets used by applications must be centrally managed and rotated.

A. Secrets Manager, with rotation policies and short-lived dynamic credentials where supported
B. Environment variables set in the deployment manifest, which keep secrets out of the image and so make rotation unnecessary
C. A configuration file in the repository, encrypted with a key committed beside it
D. A shared password vault spreadsheet on the team drive, with one row per secret and a column for the last date changed

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Central management gives one place to rotate, audit, and revoke. Dynamic secrets are the stronger form: a credential created per consumer with a lease, so a leaked value expires on its own rather than living until someone notices.
</details>

---

### Question 8
**Scenario:** Compliance posture must be evaluated continuously against a control framework.

A. Manual checklists completed by each team every quarter and signed off by the security lead before the next audit
B. Security and Compliance Center evaluating resources against profiles, with attachments scoped to accounts
C. Provider attestations only, since IBM's certifications cover the customer's own configuration of every service as well
D. An annual audit by an external assessor

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Continuous evaluation detects drift between audits, which is when non-compliance actually appears. The provider's own attestations cover their layer, not your configuration, which is the shared responsibility boundary in practice.
</details>

---

### Question 9
**Scenario:** Security events across the account must be centralized for investigation.

A. Activity Tracker events and logs forwarded to a SIEM, with retention matching the investigation requirement
B. Per-service consoles, checked one at a time by whoever is on call, using each service's own log viewer
C. Nothing is available, since events remain inside each service and cannot be exported to another tool
D. Screenshots of the dashboards saved to a shared folder at the end of each incident, with notes on what was seen on each screen

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Activity Tracker records who performed which API action, which is the control plane record an investigation starts from. Forwarding to a SIEM gives correlation with other sources and retention beyond the platform's own window.
</details>

---

### Question 10
**Scenario:** Container images must be checked before deployment.

A. Trust the registry, since images pulled from a vendor's public registry have already been scanned by the publisher
B. Vulnerability scanning in the registry and pipeline, with a gate rejecting images over a severity threshold
C. Scan after deployment, with a scheduled job over the running containers that raises tickets for anything critical or high
D. Only scan base images

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Scanning becomes a control only when something fails on the result. Scanning after deployment produces a report about a vulnerability that is already running, which is detection rather than prevention.
</details>

---

### Question 11
**Scenario:** A Kubernetes or OpenShift cluster must limit what workloads can do.

A. Trust developers to follow the guidelines, with a review by the platform team after each release has gone out
B. Cluster admin for all developers, so that no workload is blocked from creating whatever resources it needs
C. RBAC per namespace, security context constraints or Pod Security Standards, and network policies
D. Node-level firewalls only, which filter traffic on each worker and so also control what the pods may do on the node

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Three independent layers: who may call the API, what a pod may do on the node, and what it may reach on the network. OpenShift's SCCs are stricter by default than upstream Kubernetes, which is a distinction worth knowing on an IBM exam.
</details>

---

### Question 12
**Scenario:** A DDoS and application-layer attack must be mitigated for a public web application.

A. Larger instances behind the load balancer
B. A security group that blocks the offending source addresses
C. More replicas spread across zones
D. A CDN and WAF in front of the application, with rate limiting and managed rule sets

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Absorbing and filtering at the edge keeps the traffic away from origin capacity. Security groups operate at layer 3 and 4 and cannot inspect a request, so they cannot distinguish a legitimate request from an injection attempt.
</details>

---

### Question 13
**Scenario:** An account's root-equivalent access must be constrained.

A. Restrict the account owner, use named administrator identities with MFA, and require IAM policies for privileged actions
B. Use the account owner for daily work, since it avoids the delay of requesting access each time something needs changing in the account
C. Disable MFA for convenience on administrator accounts
D. Share the owner credentials among the administrators in a password vault so that someone is always available to act at any hour

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The account owner is a break-glass identity, so daily work under it destroys attribution and puts the most powerful credential in routine circulation. Named identities with MFA give both accountability and a revocation path.
</details>

---

### Question 14
**Scenario:** Data classification must drive protection controls.

A. Classification is documentation only, and has no effect on which controls apply to any particular dataset or environment
B. Protect only production, because test environments never hold sensitive data
C. Classify data, then apply controls proportionate to sensitivity: keys, access scope, retention, residency
D. Encrypt everything the same way with one key

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Uniform controls are either too weak for the sensitive data or too expensive for the rest. Classification is what lets you justify HSM-backed keys and restricted access for a small subset while keeping the majority operationally simple.
</details>

---

### Question 15
**Scenario:** An incident response plan must exist for cloud workloads.

A. Define roles, detection sources, cloud containment actions (isolate, snapshot, revoke credentials) and evidence preservation, and rehearse it
B. Rely on the provider, whose security operations team will detect and contain incidents in the customer's own workloads under the shared responsibility model
C. Handle it when it happens, using the people who are on shift and the tools that are already to hand
D. Restore from backup only, as returning to a known-good state removes the need to investigate what happened

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Cloud changes the containment toolkit: revoking an API key or detaching a network interface is faster than physical isolation, and snapshotting preserves evidence before you terminate anything. Rehearsal is what reveals that the on-call engineer lacks the permission to do any of it.
</details>

---

## Where to go deeper

- [IBM Cloud Security Engineer cert page](../../exams/ibm/cloud-security-engineer/) - notes, practice plan, strategy
- [IBM Cloud Solution Architect practice questions](https://cloud.noblerworks.com/resources/practice-questions/ibm-cloud-solution-architect/) - the architecture counterpart
- [Zero trust architecture](../architecture-patterns/zero-trust-architecture.md) - the identity model behind several answers
- [Security topic index](../../topics/security.md) - security across the repo
- **[📖 IBM Training](https://www.ibm.com/training/)** - official certification pages
