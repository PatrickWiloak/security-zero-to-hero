---
last-updated: 2026-08-09
difficulty: intermediate
---

# Kubernetes and Cloud Native Security Associate (KCSA) - Practice Questions

15 questions for KCSA prep, weighted toward cluster component security (22%) and security fundamentals (22%), with the threat model and platform security at 16% each.

KCSA is knowledge-based multiple choice. It tests whether you can reason about Kubernetes threats, not whether you can type `kubectl` fast.

> **Cert page:** [exams/kubernetes/kcsa/](../../exams/kubernetes/kcsa/)

---

### Question 1
**Scenario:** The 4Cs of cloud native security, from outermost to innermost.

A. Compute, Cluster, Container, then Code, listed from outermost to innermost
B. Cloud, Cluster, Container, then Code
C. Cloud, Compliance, Container, then Code, listed from outermost to innermost
D. Code, Container, Cluster, Cloud

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Each layer sits inside the one before it, and a weakness in an outer layer cannot be fixed by hardening an inner one. If the cloud account is compromised, container hardening does not save you. The model is useful precisely because it forces you to name the layer a control belongs to.
</details>

---

### Question 2
**Scenario:** Which component, if compromised, gives an attacker the broadest control of the cluster?

A. CoreDNS
B. kube-proxy on one node
C. The API server
D. A single application pod

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Every read and write to cluster state passes through the API server, and it holds the credentials and authorization decisions. Compromising it is effectively compromising the cluster. kube-proxy and CoreDNS are serious but scoped, and a single pod is the narrowest of the four.
</details>

---

### Question 3
**Scenario:** etcd is exposed on the network without client certificate authentication. What is the impact?

A. Only metrics are exposed, since etcd serves read-only health and monitoring endpoints without client certificates
B. Slower API responses
C. Pods cannot schedule
D. Full read and write access to all cluster state, including secrets

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** etcd holds every object, and secrets are stored there. Direct access bypasses the API server entirely, which means it bypasses RBAC, admission control, and audit logging. This is why etcd must use mutual TLS and be reachable only from the control plane.
</details>

---

### Question 4
**Scenario:** In the order the API server processes a request, what comes after authentication?

A. Admission control, then authorization, with mutating webhooks running before the access decision
B. Audit, then authorization
C. Validation, then authentication
D. Authorization, then admission control

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The chain is authentication (who are you), authorization (may you do this), then admission control (mutating webhooks, then validating webhooks) before the object is persisted. Getting the order right matters: an admission policy cannot substitute for RBAC, because admission only sees requests that authorization already allowed.
</details>

---

### Question 5
**Scenario:** Which Kubernetes RBAC statement is true?

A. RBAC is additive: permissions are granted only, and the union of all matching bindings applies
B. A RoleBinding can grant permissions in any namespace
C. ClusterRoles can only be bound cluster-wide
D. RBAC supports deny rules that override allows

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** There is no deny rule in Kubernetes RBAC, so you reduce access by removing bindings, not by adding restrictions. A ClusterRole can be bound namespace-scoped with a RoleBinding, which is how the built-in `view` and `edit` roles get reused. A RoleBinding grants only within its own namespace.
</details>

---

### Question 6
**Scenario:** Which Pod Security Standard forbids running as root, requires seccomp `RuntimeDefault`, and drops all capabilities except `NET_BIND_SERVICE`?

A. Privileged - the fully unrestricted policy that allows known privilege escalations and host namespaces
B. Restricted
C. Baseline - a minimally restrictive policy that blocks known privilege escalations but still allows running as root
D. Default - not one of the three Pod Security Standards, though many clusters apply a similar default seccomp profile

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Restricted is the hardened profile and is the target for most application workloads. Baseline blocks known privilege escalations but permits running as root. Privileged is unrestricted. There is no profile called Default.
</details>

---

### Question 7
**Scenario:** A pod runs with `hostPID: true`. What does that enable?

A. Access to the host's file system through a mount of the node's root directory
B. Faster networking, because the pod skips the overlay network and talks to the NIC directly
C. A shared IP with the node, so the pod's traffic leaves with the node's address and bypasses network policy
D. Visibility of, and interaction with, every process on the node

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Sharing the host PID namespace lets the container see every process on the node, which frequently exposes credentials in command lines and enables process manipulation. `hostNetwork` is the shared IP case and `hostPath` is host storage. All of these are blocked by the Baseline standard.
</details>

---

### Question 8
**Scenario:** Which threat does image signing and verification primarily address?

A. Running an artifact that is not the one your build produced
B. Excessive resource consumption, which resource quotas and limit ranges address by capping CPU and memory
C. Denial of service
D. Weak passwords

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Signing binds an artifact to a producer and verification refuses anything unsigned or altered, which counters registry compromise, tag mutation, and typosquatted images. It says nothing about whether the signed image is free of vulnerabilities, which is what scanning is for.
</details>

---

### Question 9
**Scenario:** Where does a NetworkPolicy sit in the threat model?

A. It authenticates services
B. It encrypts the traffic between pods using certificates that it issues
C. It limits lateral movement after a pod is compromised
D. It prevents an attacker from gaining code execution inside a running pod

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** NetworkPolicy is a segmentation control: it does not stop the initial compromise, it shrinks what the attacker can reach next. Encryption and service identity come from a mesh with mTLS. Understanding which stage of an attack a control affects is the core KCSA skill.
</details>

---

### Question 10
**Scenario:** Which is an example of a supply chain attack against a Kubernetes workload?

A. A brute-force login against the dashboard
B. A malicious dependency pulled during the image build
C. A misconfigured Service exposing a port
D. A node running out of memory

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Supply chain attacks compromise something upstream of your deployment: dependencies, base images, build systems, or registries. The other options are access control, misconfiguration, and capacity problems respectively. SBOMs, pinned digests, and provenance attestation are the countermeasures.
</details>

---

### Question 11
**Scenario:** A cluster must satisfy an external benchmark of hardening settings.

A. The OWASP Top 10, a ranking of web application risks rather than a cluster hardening benchmark
B. CIS Kubernetes Benchmark, checked with a tool such as kube-bench
C. PCI DSS
D. SOC 2 Type I

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The CIS Benchmark is the configuration-level standard for Kubernetes, and kube-bench automates checking it. OWASP is application-focused, while SOC 2 and PCI DSS are organizational compliance frameworks that may require hardening but do not specify Kubernetes flags.
</details>

---

### Question 12
**Scenario:** What does a "confused deputy" look like in a Kubernetes context?

A. A workload using a privileged service account to act for a less privileged caller
B. A duplicate DNS record that sends in-cluster service traffic to the wrong cluster IP address
C. A pod with no resource limits, which can then use up all of the CPU and memory on its node
D. Two controllers that keep overwriting each other's changes to the same object during reconciliation

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The deputy has authority the requester lacks and does not check whether the requester should have it. In clusters this appears as CI runners, operators, and dashboards with cluster-admin acting on user input. The fix is to bind actions to the caller's identity rather than the service's.
</details>

---

### Question 13
**Scenario:** Which is the best description of defense in depth applied to a cluster?

A. Blocking all inbound traffic at the cluster edge, so that nothing inside needs any further protection
B. Encrypting everything
C. Layering independent controls so that failure of one does not grant full access
D. Choosing the single strongest control, such as a hardened API server, and relying on it alone

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The point is independence: RBAC, admission policy, network policy, runtime detection, and image provenance fail in different ways, so an attacker must defeat several. Relying on one control creates a single point of failure, and "encrypt everything" is one control among many.
</details>

---

### Question 14
**Scenario:** An organization wants to isolate tenants but keep one cluster. What is the honest assessment?

A. Namespaces with RBAC give soft isolation; hard isolation needs separate clusters
B. Namespaces alone provide strong isolation between tenants, even when the tenants do not trust each other
C. Separate clusters offer no benefit over namespaces, because each namespace gets its own isolated kernel
D. Isolation is a networking problem only, so one default-deny network policy per namespace is all that is needed

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Soft multi-tenancy is achievable and common between cooperating teams. Between mutually untrusted tenants the shared kernel and shared control plane remain a real risk, so the answer is separate clusters, separate node pools, or a sandboxed runtime such as gVisor or Kata.
</details>

---

### Question 15
**Scenario:** What should be in place before an incident so you can reconstruct what an attacker did in the cluster?

A. Dashboards showing CPU
B. A backup of etcd only
C. Audit logging with a policy retaining sensitive-resource requests, shipped off-cluster
D. Verbose application logs

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The API audit log is the record of who asked the API for what, and it must be shipped off the cluster so an attacker with node access cannot erase it. Metrics do not carry identity or intent, an etcd backup is a point-in-time snapshot rather than a history, and application logs miss control plane activity entirely.
</details>

---

## Where to go deeper

- [KCSA cert page](../../exams/kubernetes/kcsa/) - notes, practice plan, strategy
- [KCNA practice questions](https://cloud.noblerworks.com/resources/practice-questions/cncf-kcna/) - the fundamentals sibling
- [CKS practice questions](./kubernetes-cks.md) - the hands-on security exam
- [AI threat modeling](https://ai.noblerworks.com/safety/security/ai-threat-modeling/) - the same reasoning applied to AI systems
- **[📖 Kubernetes security concepts](https://kubernetes.io/docs/concepts/security/)** - primary source
