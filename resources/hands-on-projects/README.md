---
last-updated: 2026-05-03
---

# Hands-on projects

Fifteen guided builds: ten cloud, five AI. Each has an estimated time, a goal you can articulate to an interviewer, and inline code or commands. Most run on free-tier accounts; the AI builds list cheap cloud-GPU options where local hardware isn't enough.

## Cloud builds (10)

| Build | Time | What you'll have at the end |
|---|---|---|
| [Deploy a 3-tier app](https://cloud.noblerworks.com/resources/hands-on-projects/deploy-3-tier-app/) | 3-4 hours | LB → app servers → DB on AWS, Azure, or GCP |
| [Build a CI/CD pipeline](https://cloud.noblerworks.com/resources/hands-on-projects/build-ci-cd-pipeline/) | 4-5 hours | Auto-build, test, and deploy on commit |
| [Set up a monitoring stack](https://cloud.noblerworks.com/resources/hands-on-projects/setup-monitoring-stack/) | 3-4 hours | Prometheus + Grafana + alertmanager wired end-to-end |
| [Implement zero-trust security](./implement-zero-trust.md) | 4-5 hours | Identity-aware access, no-implicit-trust networking |
| [Build a data pipeline](https://data.noblerworks.com/resources/hands-on-projects/build-data-pipeline/) | 4-5 hours | Ingest → transform → load with scheduled runs |
| [Deploy an ML model](https://ai.noblerworks.com/build/projects/deploy-ml-model/) | 3-4 hours | Trained model behind an API endpoint |
| [Set up a Kubernetes cluster](https://cloud.noblerworks.com/resources/hands-on-projects/kubernetes-cluster-setup/) | 4-5 hours | Production-shaped cluster, ingress, observability |
| [Build infra with Terraform](https://cloud.noblerworks.com/resources/hands-on-projects/terraform-infrastructure/) | 3-4 hours | VPC + compute + DB declared as code, with state |
| [Build a serverless app](https://cloud.noblerworks.com/resources/hands-on-projects/serverless-application/) | 3-4 hours | API + queue + function + storage, event-driven |
| [Run a DR drill](https://cloud.noblerworks.com/resources/hands-on-projects/disaster-recovery-drill/) | 4-6 hours | Tested failover, measured RTO/RPO |

## AI builds (5)

| Build | Time | What you'll have at the end |
|---|---|---|
| [Build a RAG pipeline](https://ai.noblerworks.com/build/projects/build-rag-pipeline/) | ~30 min | Docs → chunks → pgvector → Claude with retrieval + evals |
| [Build a Claude agent with MCP](https://ai.noblerworks.com/build/projects/build-claude-agent-with-mcp/) | ~30 min | Agent SDK + custom MCP server reading files + SQLite |
| [Run Llama on a single GPU](https://ai.noblerworks.com/build/projects/run-llama-on-single-gpu/) | ~45 min | Open-weights model serving locally or on a cheap rented GPU |
| [Set up an eval harness](https://ai.noblerworks.com/build/projects/set-up-eval-harness/) | ~30 min | Reproducible eval suite for prompt and model comparisons |
| [Fine-tune with LoRA](https://ai.noblerworks.com/build/projects/fine-tune-with-lora/) | 1-2 hours | LoRA-trained small model, merged + served + benchmarked |

## How to pick

- **First-ever cloud build:** [Deploy a 3-tier app](https://cloud.noblerworks.com/resources/hands-on-projects/deploy-3-tier-app/). Touches networking, compute, identity, and storage in one project.
- **First-ever AI build:** [Build a RAG pipeline](https://ai.noblerworks.com/build/projects/build-rag-pipeline/). Most hireable AI pattern in 2026.
- **Interview prep:** [Set up a Kubernetes cluster](https://cloud.noblerworks.com/resources/hands-on-projects/kubernetes-cluster-setup/), [Build infra with Terraform](https://cloud.noblerworks.com/resources/hands-on-projects/terraform-infrastructure/), [Build a CI/CD pipeline](https://cloud.noblerworks.com/resources/hands-on-projects/build-ci-cd-pipeline/). These map to the most common practitioner questions.
- **Cheapest to run:** the five AI builds (under $5 each on rented GPUs); serverless and Terraform on the cloud side (free-tier friendly).
- **Most production-shaped:** [Implement zero-trust](./implement-zero-trust.md), [Run a DR drill](https://cloud.noblerworks.com/resources/hands-on-projects/disaster-recovery-drill/), [Set up a monitoring stack](https://cloud.noblerworks.com/resources/hands-on-projects/setup-monitoring-stack/).

## Related

- [Concepts](../../learn/concepts/) - the "why" behind each pattern
- [Architecture patterns](../architecture-patterns/) - reference designs each build follows
- [Topic indexes](../../topics/) - all four pillars per subject

## Which lab for which cert

Each lab maps to the certs it exercises. The reverse index lives in [labs-by-cert.md](./labs-by-cert.md).

<!-- BEGIN GENERATED: lab-cert-map - run .github/scripts/build-lab-map.py -->

| Lab | Certs it supports |
|------|-------------------|
| [Hands-On Project: Implement Zero Trust Security](./implement-zero-trust.md) | [CCSK v5 - Certificate of Cloud Security Knowledge](../../exams/cloud-security-alliance/ccsk/), [AZ-500](../../exams/azure/az-500/), [SCS-C02](../../exams/aws/specialty/security-scs-c02/), [Google Cloud Professional Cloud Security Engineer Certification](../../exams/gcp/cloud-security-engineer/), [CKS](../../exams/kubernetes/cks/) |

<!-- END GENERATED: lab-cert-map -->
