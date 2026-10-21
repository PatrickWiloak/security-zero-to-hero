---
last-updated: 2026-08-09
difficulty: advanced
---

# Certified Kubernetes Security Specialist (CKS) - Practice Questions

15 questions for CKS prep, weighted toward the three 20% domains: minimizing microservice vulnerabilities, supply chain security, and runtime security.

CKS is performance-based and requires a valid CKA. These questions reinforce the reasoning; the exam tests whether you can implement it under time pressure.

> **Cert page:** [exams/kubernetes/cks/](../../exams/kubernetes/cks/)

---

### Question 1
**Scenario:** An auditor asks you to prove which service accounts can create pods in the `payments` namespace.

A. Search the audit log for successful pod create requests in the payments namespace over the last 30 days and list the users behind them
B. Inspect the API server flags
C. `kubectl auth can-i --list --as=system:serviceaccount:payments:<sa> -n payments`
D. Read every RoleBinding and ClusterRoleBinding manifest in the git repository and work out the permissions from the roles they reference

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** `kubectl auth can-i` asks the API server's authorizer directly, so it accounts for every Role, ClusterRole, and binding that applies, including ones nobody remembered. Reading manifests misses bindings created outside git. The audit log shows what was done, not what is permitted. API server flags tell you which authorization modes are on, not the effective permissions.
</details>

---

### Question 2
**Scenario:** A pod does not use the Kubernetes API at all, but its service account token is mounted by default.

A. Delete the default service account in the namespace so that pods started there get no token
B. Set `automountServiceAccountToken: false` on the pod spec or the service account so the kubelet never mounts the token into the container
C. Add a NetworkPolicy that blocks egress to the API server address, so the token cannot be used even though it stays mounted
D. Set `runAsNonRoot: true` and a numeric `runAsUser` in the pod security context so that a compromised process cannot read the mounted token file

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** An unused token is free credential material for an attacker who gets code execution in the container. Turning off automount is the direct fix and can be set per pod or defaulted on the service account. Deleting the default service account does not help because the controller recreates it. A NetworkPolicy is a coarser control and does not remove the credential. `runAsNonRoot` is unrelated.
</details>

---

### Question 3
**Scenario:** You need to restrict which syscalls a container can make, using a profile shipped with the node.

A. `capabilities.drop: ["ALL"]` in the container security context, which removes every Linux capability and so restricts all privileged system calls
B. `seccompProfile` with `type: Localhost` and a `localhostProfile` path
C. SELinux options with a custom type in the security context, which labels the process and confines file access on the node
D. An AppArmor profile annotation on the pod that references a profile loaded on the node, which limits file, network and capability access

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** seccomp filters syscalls, and `Localhost` loads a profile from the node's seccomp directory. `RuntimeDefault` is the easier baseline when you do not need a custom profile. AppArmor and SELinux are mandatory access control for file and capability access rather than syscall filtering. Dropping capabilities removes privileged operations but does not filter the syscall surface.
</details>

---

### Question 4
**Scenario:** Pod Security Admission is enabled. A namespace is labeled `pod-security.kubernetes.io/enforce: baseline` and `pod-security.kubernetes.io/audit: restricted`. A pod that violates `restricted` but satisfies `baseline` is applied.

A. Rejected, because the `restricted` level is set on the namespace and any violation of the stricter profile blocks admission
B. Admitted with a warning shown to the user only, because the stricter `restricted` level is configured only in a warning mode
C. Admitted silently, because only the `enforce` label is evaluated and the `audit` label is ignored unless `warn` is also set
D. Admitted, with an audit annotation recorded on the audit event and no warning shown to the user, because each mode is evaluated independently

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The three modes are independent. `enforce` decides admission, `audit` writes an annotation to the audit event, and `warn` returns a message to the client. Since only `baseline` is enforced the pod is admitted, and because `restricted` is set to audit the violation is recorded for review. This staged pattern is how teams migrate toward `restricted` without breaking workloads.
</details>

---

### Question 5
**Scenario:** You must ensure only images signed by your organization can run.

A. A validating admission webhook or policy engine that verifies signatures before admission
B. An ImagePullPolicy of `Always` on every container, which makes the kubelet re-check the registry and so reject any image that is not trusted
C. `imagePullSecrets` on every pod, so the node authenticates to the registry and can only pull images that the organization has approved
D. A private registry with push access limited to the CI service account, so that only images built by the organization can ever be stored

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Signature verification has to happen at admission, before the workload is created. Tools like Sigstore policy controllers, Kyverno, or OPA Gatekeeper enforce it. Pull policy controls caching. A private registry controls who can push, not whether what runs was signed. Pull secrets are authentication for the pull, not integrity of the artifact.
</details>

---

### Question 6
**Scenario:** `kube-bench` reports that the API server allows anonymous authentication.

A. Set `--anonymous-auth=false` on the API server and then verify that health checks and bootstrap flows still work
B. Enable audit logging with a policy that records every request, so anonymous access can be reviewed later
C. Add a default-deny NetworkPolicy in `kube-system` so unauthenticated clients cannot reach the API server
D. Rotate the API server serving certificate and its signing CA so old credentials are rejected

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Anonymous auth is an API server flag, and disabling it stops unauthenticated requests being mapped to `system:anonymous`. Be aware that some health endpoints and bootstrap flows rely on it, so verify the cluster still comes up. NetworkPolicies do not apply to the control plane's own listener. Certificate rotation and audit logging are worthwhile but address different findings.
</details>

---

### Question 7
**Scenario:** A container is compromised and the attacker attempts to write to `/etc`. You want the write to fail regardless of the process's UID.

A. `runAsUser: 1000`, so the process runs as a non-root user and cannot write to system directories
B. `readOnlyRootFilesystem: true`, which makes the container's root filesystem read-only, so writes fail even for root
C. A ResourceQuota on the namespace, which caps storage and object counts the workloads can use
D. `allowPrivilegeEscalation: false`, which stops the process gaining more privileges than its parent through setuid binaries or file capabilities

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A read-only root filesystem makes the whole image layer immutable at runtime, so writes fail even as root. Pair it with `emptyDir` mounts for the paths the app genuinely needs to write. Running as a non-root UID helps but a misconfigured directory could still be writable. Privilege escalation controls are orthogonal.
</details>

---

### Question 8
**Scenario:** You need runtime detection of a shell being spawned inside a production container.

A. Falco with a rule matching shell execution in a container
B. `kubectl logs`, reviewed daily for shell prompts
C. Prometheus alerts on sustained CPU usage per container, since an attacker who opens a shell and runs tools will push CPU past its baseline
D. A validating admission webhook that inspects every pod spec and rejects any pod that lists a shell as its entrypoint or command

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Falco reads kernel syscall events and alerts on behavior at runtime, which is exactly "a shell started where one should not." Logs only show what the application chose to print. CPU metrics are a weak proxy. Admission controls act at create time and cannot see what happens inside a running container.
</details>

---

### Question 9
**Scenario:** A default-deny egress NetworkPolicy is applied to a namespace and every pod immediately fails to resolve service names.

A. DNS was blocked; allow egress to kube-dns on UDP and TCP port 53, since pods resolve names before connecting
B. CoreDNS crashed when the policy was applied and must be restarted in kube-system
C. The CNI plugin does not support NetworkPolicy, so the policy was applied incorrectly and has blocked all pod traffic cluster-wide
D. NetworkPolicies do not support egress rules, so it was read as deny-all

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Default-deny egress blocks DNS along with everything else, and almost every workload resolves names before it connects. The fix is an explicit egress rule to the kube-dns pods or namespace on port 53, both UDP and TCP. This is the single most common self-inflicted outage when adopting egress policy.
</details>

---

### Question 10
**Scenario:** You want stronger workload isolation for an untrusted tenant than a shared kernel provides.

A. A ServiceAccount with a narrowly scoped Role
B. A RuntimeClass backed by gVisor or Kata Containers
C. A separate namespace for the tenant with its own ResourceQuota and NetworkPolicies, which keeps their workloads apart from other tenants
D. A PodDisruptionBudget for the tenant workloads, which keeps a minimum number of replicas running during node drains and upgrades

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Namespaces are an API-level boundary, not a kernel boundary: pods in different namespaces still share the node's kernel. A RuntimeClass lets you schedule the workload onto a sandboxed runtime that intercepts syscalls (gVisor) or runs a lightweight VM (Kata). Service accounts and PDBs are unrelated to isolation.
</details>

---

### Question 11
**Scenario:** Secrets in etcd are stored unencrypted. What is the correct remediation?

A. Move secrets to ConfigMaps so that the values are stored in a separate resource type that the API server does not treat as sensitive
B. Base64-encode the values twice before they are stored, so that anyone reading the etcd files sees only the encoded text
C. Restrict `kubectl get secrets` with RBAC so that only a small set of administrators can read secret values through the API
D. Configure an `EncryptionConfiguration` with a KMS or aescbc provider on the API server, then rewrite every existing secret so it is stored encrypted

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Encryption at rest is an API server configuration pointing at a provider such as KMS or `aescbc`. The step teams forget is that enabling it does not re-encrypt existing data, so you must rewrite every secret (for example `kubectl get secrets -A -o json | kubectl replace -f -`). Base64 is encoding, not encryption. ConfigMaps are worse. RBAC is necessary but does not protect the etcd data files or backups.
</details>

---

### Question 12
**Scenario:** You want to reduce the attack surface of a container image before it ships.

A. Use `latest` tags in every Dockerfile and manifest so that fixes in the base image arrive automatically on the next pull
B. Add a shell and common debugging tools to the image so that engineers can diagnose problems in production without rebuilding
C. Use a minimal or distroless base, scan in CI, and fail the build on critical findings
D. Run the vulnerability scan after deployment on a schedule, so that running workloads are checked against the newest CVE database

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Fewer packages means fewer CVEs, and gating the build turns scanning into a control rather than a report. Adding a shell expands the surface. Scanning after deployment finds problems too late. `latest` makes deployments unreproducible and can silently change what runs, which is a supply chain risk rather than a fix.
</details>

---

### Question 13
**Scenario:** Audit logging is enabled but every request is recorded at `RequestResponse` level and the log volume is unmanageable.

A. Increase the disk size on every control plane node so that the large audit log files can be retained for longer
B. Disable audit logging on the API server entirely, since the cluster already records events and the storage is not worth it
C. Write an audit policy with per-resource rules: `Metadata` for most traffic, `RequestResponse` only for sensitive resources such as secrets
D. Sample the audit log randomly at the log shipper so that only a fraction of events are kept and the volume drops to a manageable level for the storage budget

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The audit policy file matches rules in order and assigns a level per rule, so you keep full fidelity where it matters and drop to metadata elsewhere. Common practice is `None` for high-volume read traffic from system components. Disabling loses the control entirely, and random sampling destroys the evidentiary value of the log.
</details>

---

### Question 14
**Scenario:** A ServiceAccount token should be short-lived and audience-bound rather than a permanent secret.

A. Use a static token file passed to the API server with `--token-auth-file`, which gives each workload a fixed, named credential
B. Rotate the Secret holding the token manually every month
C. Use a projected service account token volume with `audience` and `expirationSeconds`
D. Use basic authentication with a username and password stored in a Secret, rotated by the application on a schedule

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Projected tokens are issued by the TokenRequest API, expire, are bound to a specific audience, and are invalidated when the pod goes away. This is the default for the automounted token in modern clusters. Manual rotation is error-prone, and static token files and basic auth are deprecated mechanisms with no expiry at all.
</details>

---

### Question 15
**Scenario:** You need to confirm that a running cluster's node OS is not exposing the kubelet read-only port.

A. Check the API server flags for `--anonymous-auth=false`, which controls whether the control plane accepts unauthenticated requests
B. Check the Service definitions in kube-system to confirm no NodePort or LoadBalancer exposes port 10255 outside the cluster
C. Check the CNI configuration to confirm that no plugin rule allows inbound traffic to the node on the kubelet ports
D. Check `--read-only-port=0` in the kubelet configuration and verify port 10255 is closed

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The kubelet's read-only port 10255 serves unauthenticated pod and node information and should be disabled. It is a kubelet setting, not an API server one, and `kube-bench` flags it. Services and CNI configuration are not involved in exposing the kubelet.
</details>

---

## Where to go deeper

- [CKS cert page](../../exams/kubernetes/cks/) - notes, practice plan, strategy
- [KCSA practice questions](./cncf-kcsa.md) - the knowledge-based security counterpart
- [CKA practice questions](https://cloud.noblerworks.com/resources/practice-questions/kubernetes-cka/) - the prerequisite
- [Kubernetes security guide](https://cloud.noblerworks.com/topics/kubernetes/) - cross-pillar index
- **[📖 Kubernetes security documentation](https://kubernetes.io/docs/concepts/security/)** - allowed during the exam
