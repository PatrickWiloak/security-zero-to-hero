---
last-updated: 2026-10-22
---

# Supply Chain Security for CKS

**[📖 Kubernetes Security - Supply Chain](https://kubernetes.io/docs/tasks/administer-cluster/verify-signed-artifacts/)** - Supply chain security overview

## Image Security Best Practices

### Minimal Base Images

**[📖 Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)** - Docker official best practices

#### Image Hierarchy (Most to Least Secure)
1. **scratch** - Empty image, smallest possible (0 bytes base)
2. **distroless** - Google's minimal images (no shell, no package manager)
3. **Alpine** - Minimal Linux distribution (~5MB)
4. **Slim variants** - Stripped-down versions of standard images (e.g., python:3.11-slim)
5. **Full images** - Standard images with full OS (e.g., ubuntu:22.04)

#### Secure Dockerfile Patterns
```dockerfile
# Multi-stage build - compile in build stage, copy binary to minimal image
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -o /app/server .

FROM gcr.io/distroless/static-debian12
COPY --from=builder /app/server /server
USER nonroot:nonroot
ENTRYPOINT ["/server"]
```

#### Dockerfile Security Rules
- **Use specific tags** - Never use `latest` or untagged images
- **Pin image digests** - Use `image@sha256:abc123...` for maximum reproducibility
- **Run as non-root** - Add `USER nonroot` or `USER 1000`
- **No secrets in images** - Never `COPY` or `ADD` secrets, credentials, or keys
- **Minimize layers** - Combine RUN commands to reduce attack surface
- **Remove unnecessary tools** - No curl, wget, bash in production images when possible
- **Use COPY over ADD** - ADD can unpack archives and fetch URLs, which is risky

### Image Scanning with Trivy

**[📖 Trivy Documentation](https://aquasecurity.github.io/trivy/)** - Comprehensive vulnerability scanner

#### Basic Scanning
```bash
# Scan an image for vulnerabilities
trivy image nginx:1.25

# Scan with severity filter
trivy image --severity HIGH,CRITICAL nginx:1.25

# Scan and fail on high/critical (for CI/CD)
trivy image --exit-code 1 --severity HIGH,CRITICAL myapp:v1.0

# Scan with JSON output
trivy image --format json --output report.json myapp:v1.0

# Scan a local Dockerfile
trivy config Dockerfile

# Scan a filesystem
trivy fs /path/to/project

# Scan Kubernetes manifests
trivy config /path/to/k8s-manifests/
```

#### Understanding Scan Results
- **CRITICAL** - Remotely exploitable, high impact, patch immediately
- **HIGH** - Significant risk, should be patched soon
- **MEDIUM** - Moderate risk, plan for remediation
- **LOW** - Minor risk, address during regular maintenance

#### Remediation Strategies
1. Update base image to latest patched version
2. Update specific vulnerable packages
3. Switch to a minimal base image (fewer packages = fewer vulnerabilities)
4. Use multi-stage builds to exclude build-time dependencies
5. Rebuild images regularly to pick up security patches

### Static Analysis of Kubernetes Resources

#### kubesec
**[📖 kubesec](https://kubesec.io/)** - Security risk analysis for Kubernetes resources

```bash
# Scan a Kubernetes manifest
kubesec scan pod.yaml

# Scan via HTTP API
curl -sSX POST --data-binary @pod.yaml https://v2.kubesec.io/scan
```

kubesec checks for:
- Containers running as root
- Privileged containers
- Missing resource limits
- Host namespace usage (hostPID, hostNetwork, hostIPC)
- Missing security contexts
- Writable root filesystem

#### conftest
```bash
# Test Kubernetes manifests against OPA policies
conftest test deployment.yaml --policy /path/to/policies/
```

#### hadolint
```bash
# Lint Dockerfiles for best practices
hadolint Dockerfile
```

## Admission Controllers for Image Policy

### ImagePolicyWebhook

**[📖 ImagePolicyWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook)** - Image policy admission controller

The ImagePolicyWebhook admission controller sends image information to an external webhook service that decides whether to allow or deny the image.

#### Configuration
```yaml
# /etc/kubernetes/admission-control/admission-config.yaml
apiVersion: apiserver.config.k8s.io/v1
kind: AdmissionConfiguration
plugins:
- name: ImagePolicyWebhook
  configuration:
    imagePolicy:
      kubeConfigFile: /etc/kubernetes/admission-control/imagepolicy-kubeconfig.yaml
      allowTTL: 50
      denyTTL: 50
      retryBackoff: 500
      defaultAllow: false  # IMPORTANT: deny if webhook unavailable
```

```yaml
# /etc/kubernetes/admission-control/imagepolicy-kubeconfig.yaml
apiVersion: v1
kind: Config
clusters:
- name: image-policy
  cluster:
    server: https://image-policy-webhook.security.svc:443
    certificate-authority: /etc/kubernetes/admission-control/ca.crt
users:
- name: api-server
  user:
    client-certificate: /etc/kubernetes/admission-control/client.crt
    client-key: /etc/kubernetes/admission-control/client.key
contexts:
- context:
    cluster: image-policy
    user: api-server
  name: default
current-context: default
```

#### API Server Configuration
```
--enable-admission-plugins=ImagePolicyWebhook
--admission-control-config-file=/etc/kubernetes/admission-control/admission-config.yaml
```

### OPA Gatekeeper for Registry Restrictions

**[📖 OPA Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/)** - Gatekeeper documentation

#### Allowed Registries Constraint
```yaml
apiVersion: templates.gatekeeper.sh/v1
kind: ConstraintTemplate
metadata:
  name: k8sallowedrepos
spec:
  crd:
    spec:
      names:
        kind: K8sAllowedRepos
      validation:
        openAPIV3Schema:
          type: object
          properties:
            repos:
              type: array
              items:
                type: string
  targets:
    - target: admission.k8s.gatekeeper.sh
      rego: |
        package k8sallowedrepos
        violation[{"msg": msg}] {
          container := input.review.object.spec.containers[_]
          satisfied := [good | repo = input.parameters.repos[_]; good = startswith(container.image, repo)]
          not any(satisfied)
          msg := sprintf("container <%v> has an invalid image repo <%v>, allowed repos are %v", [container.name, container.image, input.parameters.repos])
        }
        violation[{"msg": msg}] {
          container := input.review.object.spec.initContainers[_]
          satisfied := [good | repo = input.parameters.repos[_]; good = startswith(container.image, repo)]
          not any(satisfied)
          msg := sprintf("initContainer <%v> has an invalid image repo <%v>, allowed repos are %v", [container.name, container.image, input.parameters.repos])
        }
---
apiVersion: constraints.gatekeeper.sh/v1beta1
kind: K8sAllowedRepos
metadata:
  name: allowed-repos
spec:
  match:
    kinds:
    - apiGroups: [""]
      kinds: ["Pod"]
    namespaces: ["production"]
  parameters:
    repos:
    - "myregistry.io/"
    - "gcr.io/my-project/"
```

## Image Signing and Verification

### cosign (Sigstore)

**[📖 cosign Documentation](https://docs.sigstore.dev/cosign/signing/overview/)** - Container signing with cosign

```bash
# Generate a key pair
cosign generate-key-pair

# Sign an image
cosign sign --key cosign.key myregistry.io/myapp:v1.0

# Verify a signature
cosign verify --key cosign.pub myregistry.io/myapp:v1.0

# Keyless signing (uses OIDC identity)
cosign sign myregistry.io/myapp:v1.0

# Verify keyless signature
cosign verify --certificate-identity=user@example.com \
  --certificate-oidc-issuer=https://accounts.google.com \
  myregistry.io/myapp:v1.0
```

### Image Pull Policies

```yaml
# Always pull (verifies against registry)
spec:
  containers:
  - name: app
    image: myregistry.io/app:v1.0
    imagePullPolicy: Always

# Never pull (use local image only)
    imagePullPolicy: Never

# IfNotPresent (default for tagged images)
    imagePullPolicy: IfNotPresent
```

**Important:** Images with the `latest` tag default to `Always` pull policy. Tagged images default to `IfNotPresent`.

## Private Registry Configuration

### Using Private Registries in Kubernetes
```bash
# Create registry credentials secret
kubectl create secret docker-registry regcred \
  --docker-server=myregistry.io \
  --docker-username=user \
  --docker-password=pass \
  --docker-email=user@example.com \
  -n production
```

```yaml
# Reference in pod spec
spec:
  imagePullSecrets:
  - name: regcred
  containers:
  - name: app
    image: myregistry.io/app:v1.0
```

## SBOMs: knowing what is in an image

The curriculum asks you to "understand your supply chain", and the concrete artifact behind that phrase is the software bill of materials (SBOM). An SBOM is a machine-readable list of every package, library, and version inside an image. It matters for one practical reason: when the next Log4Shell lands, the team with SBOMs searches a file for the vulnerable version, and the team without them starts pulling and unpacking every image they run.

Two formats dominate. SPDX comes from the Linux Foundation and is an ISO standard (ISO/IEC 5962). CycloneDX comes from OWASP. On the exam you are more likely to be asked to produce or read one than to compare the formats, so know one tool well enough to do both.

```bash
# Generate an SBOM for an image with Trivy (CycloneDX or SPDX)
trivy image --format cyclonedx --output sbom.cdx.json nginx:1.27
trivy image --format spdx-json --output sbom.spdx.json nginx:1.27

# Scan an existing SBOM for known vulnerabilities, without pulling the image again
trivy sbom sbom.cdx.json

# Syft is the other common generator
syft nginx:1.27 -o spdx-json > sbom.spdx.json

# The Kubernetes project's own tool, bom, writes SPDX
bom generate --image nginx:1.27 --output sbom.spdx
```

A task might hand you an SBOM and ask which images contain a given library version. That is a `grep` or `jq` over the file, so read the format once before exam day and know where the package name and version fields sit.

**[📖 Trivy SBOM](https://trivy.dev/latest/docs/supply-chain/sbom/)** - generating and scanning SBOMs with Trivy
**[📖 Kubernetes bom](https://github.com/kubernetes-sigs/bom)** - the SPDX generator the Kubernetes project uses for its own releases

## Static analysis of workloads: Kubesec and KubeLinter

Static analysis reads a manifest before it reaches the cluster and flags risky settings: a container running as root, a missing read-only root filesystem, added Linux capabilities, no resource limits. The curriculum names Kubesec and KubeLinter as examples, so expect either.

Kubesec scores a manifest. Positive points go to hardening settings and a critical finding (such as `privileged: true`) makes the score negative. KubeLinter runs a set of named checks and prints each failure with a remediation hint. Both read YAML from a file, which makes them quick to run during a task.

```bash
# Kubesec: score a pod manifest and list what lowered the score
kubesec scan pod.yaml

# KubeLinter: run the default checks and print each failure with a fix hint
kube-linter lint pod.yaml
```

The exam pattern is "run the tool, then fix the manifest until it passes". Typical fixes are `runAsNonRoot: true`, `readOnlyRootFilesystem: true`, `allowPrivilegeEscalation: false`, and `capabilities: drop: ["ALL"]` in the container `securityContext`.

**[📖 Kubesec](https://kubesec.io/)** - security risk analysis for Kubernetes resources
**[📖 KubeLinter](https://docs.kubelinter.io/)** - static analysis checks for Kubernetes YAML and Helm charts

## CI/CD Security Integration

### Shift-Left Security Pipeline
1. **Code scanning** - SAST tools during development
2. **Dockerfile linting** - hadolint in pre-commit hooks
3. **Image building** - Multi-stage builds with minimal bases
4. **Image scanning** - Trivy scan before pushing to registry
5. **Image signing** - cosign sign after successful scan
6. **Admission control** - Gatekeeper/ImagePolicyWebhook at deploy time
7. **Runtime scanning** - Continuous scanning of running images

## Key Takeaways

1. **Minimal images** - Use distroless or scratch base images whenever possible
2. **Scan everything** - Scan images, Dockerfiles, and Kubernetes manifests
3. **Sign and verify** - Use cosign to sign images and verify signatures at admission
4. **Restrict registries** - Use admission controllers to allow only approved registries
5. **Pin versions** - Use specific tags or SHA digests, never `latest`
6. **Shift left** - Integrate security scanning into CI/CD pipelines
7. **Default deny** - Set `defaultAllow: false` on ImagePolicyWebhook
