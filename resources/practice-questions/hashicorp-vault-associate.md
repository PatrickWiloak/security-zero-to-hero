---
last-updated: 2026-08-09
difficulty: intermediate
---

# HashiCorp Vault Associate (003) - Practice Questions

15 questions for Vault Associate prep, weighted toward secrets engines (20%), then authentication methods, policies, and the CLI (15% each).

> **Cert page:** [exams/hashicorp/vault-associate/](../../exams/hashicorp/vault-associate/)

---

### Question 1
**Scenario:** An application needs database credentials that are unique per instance and expire automatically.

A. Environment variables set at deploy time, which rotate automatically each time the pod restarts
B. The Transit engine, which returns a fresh database login for each instance as part of its encryption API
C. The Database secrets engine generating dynamic credentials with a lease
D. The KV secrets engine with one shared password stored at a path that every instance reads

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Dynamic secrets are Vault's distinguishing feature: Vault creates a credential on demand, hands it out with a lease, and revokes it when the lease expires. A compromised credential has a short useful life and is attributable to one requester. KV stores a static secret that everyone shares.
</details>

---

### Question 2
**Scenario:** An application must encrypt data without ever holding the encryption key.

A. The PKI engine, which issues certificates that the application then uses to encrypt its data in place
B. The Transit secrets engine, which performs encryption and decryption as a service
C. KV version 2, storing the key as a versioned secret that the application fetches at startup
D. The TOTP engine, which generates time-based codes that the application uses as its encryption key

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Transit is encryption as a service: the application sends plaintext and gets ciphertext back, and the key never leaves Vault. This also gives centralized key rotation, since old ciphertext remains decryptable by key version while new writes use the latest.
</details>

---

### Question 3
**Scenario:** A Vault policy must allow reading secrets under `secret/data/app/*` but not writing.

A. path "secret/data/app/*" { capabilities = ["deny"] }
B. path "secret/data/app/*" { capabilities = ["sudo"] }
C. path "secret/data/app/*" { capabilities = ["read", "list"] }
D. path "secret/data/app/*" { capabilities = ["create", "update", "patch"] }

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Vault policies are path-based and default-deny, so you grant only the capabilities needed. `read` and `list` cover retrieval and enumeration. Note the KV v2 path includes `data/` for reads and `metadata/` for versions and deletion, which is a frequent policy mistake.
</details>

---

### Question 4
**Scenario:** A Kubernetes pod must authenticate to Vault without a stored token.

A. The Kubernetes auth method, validating the pod's service account token
B. A root token stored in a ConfigMap and mounted into the pod, so no login step is needed
C. Userpass credentials stored in a Kubernetes Secret
D. A shared AppRole secret ID baked into the container image so every replica logs in the same way

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The Kubernetes auth method verifies the projected service account token with the cluster's API, so the workload's existing identity becomes its Vault identity and no secret needs distributing. This solves the secret zero problem, which is what every machine auth method is fundamentally about.
</details>

---

### Question 5
**Scenario:** What happens to dynamic credentials when their lease expires?

A. Nothing happens, because leases are advisory and the database user stays until an operator drops it by hand
B. They stay valid until the database's own password policy forces a change
C. Vault revokes them at the backend, so the database user is deleted and the login stops working
D. They become read-only, so the app can still query but not write

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Vault tracks leases and actively revokes at expiry, which is what makes the secret genuinely temporary rather than merely labeled as such. Clients renew before expiry if they need longer, and `vault lease revoke` can force early revocation during an incident.
</details>

---

### Question 6
**Scenario:** Vault is sealed after a restart.

A. Unseal with a quorum of Shamir key shares, or configure auto-unseal through a cloud KMS or HSM
B. Delete the storage backend and re-initialize Vault for a fresh instance
C. It is broken, and the data has to be restored from a snapshot before Vault can serve requests again at all
D. Restart it again, since a sealed state clears itself on the second start once storage is reachable again

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Sealed means the encryption key that protects the storage is not in memory. Shamir's Secret Sharing splits the unseal key into shares with a threshold, so no single operator can unseal alone. Auto-unseal delegates that to a KMS, which is the norm in production because manual unseal after every restart is operationally painful.
</details>

---

### Question 7
**Scenario:** A CI system needs a Vault identity with a distributed secret that is not in the code repository.

A. Userpass with one shared account for all pipelines, its password read from a file in the repository
B. A root token in the pipeline configuration, passed to each job as a masked variable
C. Basic auth with a username and password committed alongside the pipeline definition
D. AppRole, delivering the role ID with the application and the secret ID through a separate trusted channel

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** AppRole splits credentials in two so neither half alone is sufficient, and response wrapping is the usual way to deliver the secret ID: a single-use wrapping token that reveals tampering if it has already been unwrapped. Root tokens should be revoked after initial setup.
</details>

---

### Question 8
**Scenario:** A token's TTL has passed but the application is still working.

A. Tokens never expire once issued, so TTL only matters for audit
B. The TTL is advisory, and Vault only enforces it for tokens created in the root namespace
C. Vault is misconfigured and the clock is skewed, so it has not yet revoked the token
D. The token was renewed, or it is a periodic token renewed within each period

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Service tokens can be renewed up to a maximum TTL. Periodic tokens have no max TTL and can be renewed indefinitely as long as renewal happens within each period, which is how long-running services stay authenticated. Batch tokens, by contrast, are lightweight and not renewable.
</details>

---

### Question 9
**Scenario:** Vault must issue short-lived TLS certificates for internal services.

A. Manual certificate signing with an offline CA, issuing each certificate by ticket and tracking expiry in a spreadsheet that someone updates by hand
B. The PKI secrets engine, with a role that limits allowed domains and key types and sets a maximum TTL for each service
C. The KV engine storing certificates, with a scheduled job replacing them before they expire
D. The Transit engine, which signs certificate requests with a named key and returns an X.509 certificate

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** PKI turns certificate issuance into an API call, and short TTLs mean revocation matters less because certificates expire before a CRL would propagate. The role is where you constrain allowed domains, key types, and maximum TTL so a compromised client cannot mint arbitrary certificates.
</details>

---

### Question 10
**Scenario:** KV version 2 is in use and a secret was overwritten by mistake.

A. Read the previous version, since KV v2 is versioned, and undelete it if needed
B. Restore from a Raft snapshot taken before the change, since KV keeps no history of overwritten values
C. It is lost, because writing to the same path replaces the value and the old data is purged immediately
D. Recreate it manually from the application's configuration files, since versions cannot be read back through the API

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** KV v2 keeps a configurable number of versions with soft delete, undelete, and destroy operations. The distinction matters in policy design: `delete` is recoverable, `destroy` is not, and they are separate capabilities on the metadata path.
</details>

---

### Question 11
**Scenario:** Audit logging must record every request and response.

A. Audit is on by default for every request, writing to the operational log
B. Use application logs, since the client app can record the secrets it requests
C. Enable it only for failures, because successful reads are already recorded by the storage backend itself
D. Enable an audit device (file, syslog, or socket); Vault refuses requests if no device can log

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Audit devices are opt-in and log request and response metadata with sensitive values HMACed rather than in plaintext. The important operational fact is that if all audit devices fail to write, Vault stops serving requests: auditability is treated as a hard requirement, not a best effort.
</details>

---

### Question 12
**Scenario:** Vault namespaces are mentioned in a design discussion.

A. They replace policies, so ACL rules are no longer needed once a namespace exists
B. Namespaces are an Enterprise feature providing multi-tenancy with isolated policies, auth, and secrets
C. They are open source and available in every edition, used to group secrets engines by team
D. They are the same as paths, just a different name for mount points under one shared root

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Namespaces give each tenant what looks like its own Vault, with delegated administration. In Community Edition the equivalent isolation comes from path structure and careful policy design, or from running separate clusters. Knowing which features are Enterprise-only is examinable.
</details>

---

### Question 13
**Scenario:** Which storage backend is recommended for a production HA Vault cluster?

A. A single Consul agent running on the same host as the Vault node, with no other cluster members
B. The local filesystem on a shared NFS mount, so every node reads the same data directory
C. Integrated Storage (Raft), built into Vault and replicated across the nodes
D. In-memory storage, since it is the fastest option

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Integrated Storage uses Raft consensus inside Vault itself, removing the external dependency that the older Consul backend required. Filesystem storage supports only a single node and in-memory is for development, since it loses everything on restart.
</details>

---

### Question 14
**Scenario:** A CLI user must write a secret and read it back.

A. `vault write secret/app/config user=admin` only, since a successful write also prints the stored values
B. `vault kv put secret/app/config user=admin` then `vault kv get secret/app/config`
C. `vault login` followed by `vault status`, which writes and displays the stored secret data
D. `vault read secret/app/config` first, because reading a path that does not exist creates it

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The `kv` subcommands understand the KV v2 path layout, so you address `secret/app/config` rather than `secret/data/app/config`. Using the generic `vault read` against a v2 mount requires the `data/` segment, which is a frequent source of confusion on the exam and in practice.
</details>

---

### Question 15
**Scenario:** A response must be delivered to a client such that any interception is detectable.

A. Response wrapping, returning a single-use wrapping token that the recipient unwraps
B. Base64 encoding, which hides the value from casual observers
C. A long TTL token that outlives any delay between delivery and use
D. TLS alone, since transport encryption already makes interception visible

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** The wrapping token can be unwrapped exactly once, so if the intended recipient finds it already used, the secret is known to be compromised and can be rotated. This gives a tamper-evidence property that transport encryption alone does not.
</details>

---

## Where to go deeper

- [Vault Associate cert page](../../exams/hashicorp/vault-associate/) - notes, practice plan, strategy
- [Terraform Associate practice questions](https://cloud.noblerworks.com/resources/practice-questions/hashicorp-terraform-associate/) - the sibling HashiCorp exam
- [Secrets management](../../learn/concepts/secrets-management.md) - plain-English primer
- [Boundary Associate practice questions](./hashicorp-boundary-associate.md) - access rather than secrets
- **[📖 Vault documentation](https://developer.hashicorp.com/vault/docs)** - primary source
