---
last-updated: 2026-10-22
difficulty: advanced
---

# Certified Kubernetes Security Specialist (CKS) - Practice Questions

30 questions for CKS prep, weighted toward the three 20% domains: minimizing microservice vulnerabilities, supply chain security, and runtime security.

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

### Question 16 - Domain 1: Cluster Setup
**Scenario:** Pods in a cloud-hosted cluster can reach the instance metadata endpoint at `169.254.169.254`, which hands out the node's cloud credentials. Application pods have no reason to call it. What is the best control?

A. Remove the node's cloud IAM role entirely, so the metadata endpoint has no credentials left to return to anyone
B. Set `hostNetwork: false` on every application pod, so its traffic cannot reach link-local addresses on the node
C. Apply an egress NetworkPolicy that allows `0.0.0.0/0` with an `except` entry for `169.254.169.254/32`
D. Rotate the node's cloud credentials daily, so any credential a pod reads expires before it can be misused

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** An egress NetworkPolicy with an `ipBlock` exception blocks the metadata address for the selected pods while leaving other egress alone. It needs a CNI that enforces NetworkPolicy, and cloud-side settings such as a metadata hop limit are a good second layer. Removing the node role (A) breaks the node itself, because the kubelet, CNI and image pulls often depend on it. `hostNetwork: false` (B) is already the default, and pod traffic is still routed to the metadata address. Daily rotation (D) shortens the window but leaves the credentials readable by every pod.
</details>

---

### Question 17 - Domain 1: Cluster Setup
**Scenario:** Before a node upgrade, an engineer downloads the `kubelet` and `kubectl` binaries from a mirror inside the company network. You want assurance that the binaries are exactly the ones the Kubernetes project released.

A. Compute `sha512sum` of each binary and compare it with the checksum published for that Kubernetes release
B. Run `kubelet --version` and confirm the reported version matches the one the upgrade plan calls for
C. Check that the files are owned by root with mode 0755, so no ordinary user could have changed them
D. Scan each binary with the CI vulnerability scanner and approve it if no critical CVEs are reported

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A cryptographic hash compared against the value the project publishes proves the file is byte-identical to the official release. Any tampering on the mirror changes the hash. The version string (B) is just output from the binary, and a modified binary can print anything. File ownership and mode (C) say nothing about what happened to the file before it reached the node. A vulnerability scan (D) looks for known CVEs, not for tampering, so a backdoored binary can pass it cleanly.
</details>

---

### Question 18 - Domain 2: Cluster Hardening
**Scenario:** A CI pipeline service account is bound to `cluster-admin` through a ClusterRoleBinding. It only ever applies Deployments, Services and ConfigMaps in the `shop` namespace. What change follows least privilege?

A. Keep the binding but turn on audit logging for the service account, so any misuse is recorded for review later
B. Swap `cluster-admin` for the built-in `edit` ClusterRole, still bound cluster-wide so the pipeline keeps working
C. Move the pipeline's credentials into an external vault and rotate them weekly, leaving the binding as it is
D. Delete the ClusterRoleBinding, then grant only the needed verbs on those resources with a Role and RoleBinding in `shop`

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A namespaced Role bound with a RoleBinding limits the account to the one namespace and the few resource types it actually touches. Check the result with `kubectl auth can-i`. Audit logging (A) detects misuse after the fact but leaves full cluster control in place. The `edit` role (B) is smaller than `cluster-admin`, but bound cluster-wide it still reaches every namespace and can read Secrets. Rotating credentials (C) protects the credential, not the scope of what it can do.
</details>

---

### Question 19 - Domain 2: Cluster Hardening
**Scenario:** A cluster runs a Kubernetes minor version that no longer gets security patches. The current release is three minor versions ahead. How should you plan the upgrade?

A. Upgrade the worker node kubelets first, so the data plane is patched before anything in the control plane changes
B. Step up one minor version at a time, upgrading the control plane first and then each node's kubelet after draining it
C. Move the control plane straight to the newest minor version in one step, since each release contains the earlier fixes
D. Stay on the current version and add stricter NetworkPolicies, since upgrades carry more risk than unpatched CVEs

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The Kubernetes project patches only the most recent few minor versions, so an old cluster gets no CVE fixes. Tools like `kubeadm` upgrade one minor version at a time, and the version skew policy says a kubelet must never be newer than the API server. That is why the control plane goes first and nodes follow, drained one by one. Kubelets first (A) breaks the skew policy. Skipping minor versions (C) is not supported and skips required migrations. Staying put (D) leaves known, published vulnerabilities open.
</details>

---

### Question 20 - Domain 3: System Hardening
**Scenario:** An AppArmor profile named `k8s-deny-write` is loaded on every node. You need a pod's container to run under it on a current Kubernetes release.

A. Set `securityContext.appArmorProfile` with `type: Localhost` and `localhostProfile: k8s-deny-write`
B. Set `seccompProfile` with `type: Localhost` and a `localhostProfile` path pointing at the AppArmor file
C. Add the profile name to the container's `capabilities.add` list so the runtime applies it on start
D. Label the namespace `pod-security.kubernetes.io/enforce: restricted` so the profile applies to all pods

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Since Kubernetes 1.30 the `appArmorProfile` field in the security context is the supported way to set AppArmor, replacing the older beta annotation. The profile must already be loaded on whichever node the pod lands on, or the container will not start. seccomp (B) is a separate mechanism with its own profile format and cannot load an AppArmor profile. Capabilities (C) are Linux privileges, not profile references. Pod Security Admission (D) checks that pods do not set AppArmor to unconfined, but it never applies a profile.
</details>

---

### Question 21 - Domain 3: System Hardening
**Scenario:** A CIS scan of a worker node shows an FTP server and a print service listening on network ports. Nothing in the cluster uses either.

A. Add a NetworkPolicy in every namespace that denies ingress to those two ports on the node's IP address
B. Leave both services running but move them to high port numbers, so scanners are less likely to find them
C. Confirm with `ss -tlnp`, then `systemctl disable --now` both services and remove their packages from the image
D. Drain the node with `kubectl drain` and keep it cordoned until the next scheduled OS patching window arrives

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Unused services are pure attack surface on the host. The fix is to stop them, disable them so they do not come back on reboot, and remove the packages from the node image so new nodes start clean. NetworkPolicy (A) governs pod traffic, not processes running directly on the host. Changing ports (B) is obscurity, not hardening. Draining the node (D) moves workloads but leaves the services running, and the next node built from the same image has them too.
</details>

---

### Question 22 - Domain 4: Minimize Microservice Vulnerabilities
**Scenario:** Tenant teams keep creating Services of type `NodePort` and `LoadBalancer`, exposing workloads directly. You want the API server to reject these in tenant namespaces with built-in features only, and no webhook to run.

A. A Pod Security Admission label of `enforce: restricted` on each tenant namespace, which blocks exposed workloads
B. A `ValidatingAdmissionPolicy` with a CEL rule on `object.spec.type`, plus a binding that selects tenant namespaces
C. An RBAC Role without the `create` verb on Services for tenant users, so they can only make ClusterIP Services
D. A default-deny ingress NetworkPolicy in each tenant namespace, so traffic arriving on a node port is dropped

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** ValidatingAdmissionPolicy (GA since 1.30) runs CEL expressions inside the API server, so it can inspect a field such as `spec.type` and reject the request with no external webhook. The `ValidatingAdmissionPolicyBinding` scopes it to the tenant namespaces. Pod Security Admission (A) only evaluates pods, never Services. RBAC (C) works on verbs and resources, not field values, so removing `create` blocks every Service type. A NetworkPolicy (D) may drop some traffic, but the Service and any cloud load balancer still get created.
</details>

---

### Question 23 - Domain 4: Minimize Microservice Vulnerabilities
**Scenario:** An app reads a database password from a Secret exposed as an environment variable. A crash reporter it uses uploads the full process environment with every error report.

A. Base64-encode the password in the Secret a second time, so the value that appears in crash reports is unreadable
B. Mark the Secret as `immutable: true`, so its value can no longer change or be copied anywhere else in the cluster
C. Move the password into a ConfigMap referenced by the Deployment, so the app no longer treats it as a Secret value
D. Mount the Secret as a read-only volume file that the app reads at startup, so the value is not in the environment

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Environment variables are inherited by child processes and are routinely captured by crash reporters, debug endpoints and diagnostic dumps. A mounted file keeps the value out of the environment, and mounted Secrets can also pick up a rotated value without a restart. Extra base64 (A) is reversible encoding, not protection. `immutable` (B) stops updates to the Secret object but does nothing about how the app exposes the value. A ConfigMap (C) is meant for non-sensitive data and is often readable by more people.
</details>

---

### Question 24 - Domain 4: Minimize Microservice Vulnerabilities
**Scenario:** A compliance review requires that all pod-to-pod traffic in the `payments` namespace is encrypted, and that each side proves its workload identity.

A. Apply a default-deny NetworkPolicy and allow only the specific pod-to-pod flows the payments services need
B. Put the payments services behind an Ingress with a TLS certificate, so traffic is encrypted at the cluster edge
C. Use a service mesh such as Istio or Linkerd with mutual TLS in strict mode for the payments namespace
D. Enable encryption at rest for Secrets in etcd, so the payment data the cluster handles is stored encrypted

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A mesh issues each workload a certificate tied to its identity, and mutual TLS both encrypts the connection and authenticates both ends. Strict mode rejects plaintext connections. CNI-level encryption such as WireGuard covers the encryption half too. A NetworkPolicy (A) limits who can talk but sends traffic in clear text. An Ingress with TLS (B) protects only traffic entering the cluster, not traffic between pods. Encryption at rest (D) protects stored data, not data on the wire.
</details>

---

### Question 25 - Domain 5: Supply Chain Security
**Scenario:** A Deployment references `registry.example.com/api:1.4`. Last week someone re-pushed that tag with different contents, and nodes ended up running two different images under one name. You need every node to run exactly the image that was reviewed.

A. Reference the image by digest, such as `api@sha256:<digest>`, in the manifest
B. Set `imagePullPolicy: Always` so every node pulls the newest copy of the tag
C. Switch the tag to `latest` so all nodes converge on the same current image
D. Add an `imagePullSecrets` entry so only authenticated nodes can pull the tag

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A digest is a hash of the image content, so it can only ever resolve to that exact image. Tags are mutable pointers. Turning on tag immutability in the registry is a good second layer. `Always` (B) makes nodes agree on whatever the tag points to now, which may be the unreviewed image. `latest` (C) is the most mutable tag of all. Pull secrets (D) control who can pull, not what content they receive.
</details>

---

### Question 26 - Domain 5: Supply Chain Security
**Scenario:** Reviewers keep catching manifests with `privileged: true` or missing resource limits during code review, after hours of work. You want these caught automatically before anything reaches the cluster.

A. Rely on Pod Security Admission in the cluster, since it already rejects every insecure manifest at apply time
B. Run a static analysis tool such as kubesec or kube-linter on the manifests in CI and fail the pipeline on findings
C. Scan the container images with an image scanner in CI, since image scanning also checks the pod spec settings
D. Enable audit logging at `RequestResponse` level, so insecure manifests are recorded whenever they are applied

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Static analysis of manifests catches risky settings at the pull request, the cheapest place to fix them, and gating the pipeline makes it a control. Admission policy in the cluster stays as the backstop. Pod Security Admission (A) acts late, at apply time, and does not check resource limits at all. Image scanning (C) inspects the packages inside the image, not the pod spec; manifest checks are a separate mode or tool. Audit logging (D) records what happened after the manifest is already applied.
</details>

---

### Question 27 - Domain 5: Supply Chain Security
**Scenario:** A critical CVE is announced in a widely used logging library. Security asks which of the 400 images your teams have shipped contain the affected version, and needs an answer within the hour.

A. Exec into a sample of running containers and search their filesystems for the library's package files
B. Ask each team to check their own dependency files and report back by email whether they use the library
C. Rescan only the images running in production right now, since images sitting in the registry do not matter
D. Query the SBOMs generated for each image at build time, for example by Syft, and stored alongside the image

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** A Software Bill of Materials lists every component and version in an image, so a new CVE becomes a query across stored SBOMs rather than a hunt. Attaching the SBOM to the image as a signed attestation also proves where it came from. Sampling containers (A) misses images and needs shell access to production. Asking teams (B) is slow and misses transitive dependencies. Scanning only what runs now (C) ignores registry images that will be deployed, scaled up or rolled back to later.
</details>

---

### Question 28 - Domain 6: Monitoring, Logging and Runtime Security
**Scenario:** Falco alerts that a pod in production opened an outbound connection to a known cryptocurrency mining pool. You need to stop the activity while keeping evidence for the investigation.

A. Delete the pod at once so the process stops, and let the Deployment schedule a clean replacement pod
B. Scale the Deployment to zero replicas, then restore the namespace from the latest cluster backup
C. Relabel the pod out of its Service, isolate it with a deny-all NetworkPolicy, then capture evidence
D. Reboot the node so every container on it restarts from its image and the process is cleared away

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Containment first, evidence second. Changing the pod's labels drops it from its Service and ReplicaSet, and a deny-all NetworkPolicy matching a quarantine label cuts its traffic, while the container and its memory stay intact for capture. Cordon the node next so nothing new lands on it. Deleting the pod (A), scaling to zero (B) and rebooting the node (D) all stop the process but destroy the evidence you need to learn how it got in, and the same weakness may be in the replacement.
</details>

---

### Question 29 - Domain 6: Monitoring, Logging and Runtime Security
**Scenario:** A Secret named `db-creds` in the `billing` namespace disappeared overnight. Audit logging records Secrets at `Metadata` level. You need to find out who removed it.

A. Search the audit log for `verb: delete`, `objectRef.resource: secrets` and `objectRef.name: db-creds`, then read `user.username`
B. Run `kubectl get events -n billing` and look for a deletion event that names the user who removed the Secret
C. Check the API server's container logs in `kube-system`, which list every request with the identity that sent it
D. Read the etcd revision history for the key, which stores the identity of the client that wrote each change

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Each audit event records the verb, the object and the authenticated user, and `Metadata` level is enough to answer "who deleted what, and when." Filtering with a tool like `jq` gets there quickly. Kubernetes Events (B) come from controllers, do not record the requesting user, and expire after about an hour by default. The API server's own logs (C) are operational output, not a per-request record. etcd (D) only sees the API server as its client, so it holds no Kubernetes user identity.
</details>

---

### Question 30 - Domain 6: Monitoring, Logging and Runtime Security
**Scenario:** A runtime alert on a worker node gives only a container ID and a process name. You need to know which pod and namespace the container belongs to before you act.

A. Run `kubectl top pods -A` and pick the busiest pod, since the alerted process is most likely using the most CPU
B. On the node, run `crictl ps` and `crictl inspect <container-id>`, then read the pod name and namespace labels
C. Search every Deployment manifest in git for the process name, since it should appear in a container command
D. Run `docker ps` on the node, since the kubelet still starts all containers through Docker on current releases

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** `crictl` talks to the CRI runtime (containerd or CRI-O), and the container's labels include `io.kubernetes.pod.name` and `io.kubernetes.pod.namespace`, so the mapping is exact. Guessing by CPU (A) can point at the wrong pod. A suspicious process (C) is usually not the one the manifest starts, so the search finds nothing. Dockershim was removed in Kubernetes 1.24 (D), so on current nodes `docker ps` either is not installed or does not show Kubernetes containers.
</details>

---

## Where to go deeper

- [CKS cert page](../../exams/kubernetes/cks/) - notes, practice plan, strategy
- [KCSA practice questions](./cncf-kcsa.md) - the knowledge-based security counterpart
- [CKA practice questions](https://cloud.noblerworks.com/resources/practice-questions/kubernetes-cka/) - the prerequisite
- [Kubernetes security guide](https://cloud.noblerworks.com/topics/kubernetes/) - cross-pillar index
- **[📖 Kubernetes security documentation](https://kubernetes.io/docs/concepts/security/)** - allowed during the exam
