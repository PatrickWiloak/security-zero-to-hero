# 💡 Concepts - Bite-Size Topic Pages

> **Single-topic explanations. 5-15 minute reads. No exam scaffolding.**
>
> Read one when you keep seeing a term and want to actually understand it.

---

## How these are organized

Each page covers one concept:
- What it is, in plain English
- Why it exists (the problem it solves)
- A small concrete example
- What to look at next

These are not exam-objective summaries. They're "explain it like I'm a smart engineer who just hasn't been exposed to this yet."

If you want exam coverage, head back to the [Study Hub](../../STUDY-HUB.md).

**Brand new to all of this?** Start with **[Day One](https://cloud.noblerworks.com/learn/day-one/)** - terminal, git, HTTP, and servers - then come back here once that vocabulary feels familiar.

**Want a curated path through these?** **[Security from Scratch](../security-from-scratch.md)** orders the security concepts into a path from zero to security engineer. The cloud, data and AI concepts listed below live on the sibling Zero to Hero sites, and their own paths are [Cloud from Scratch](https://cloud.noblerworks.com/learn/cloud-from-scratch/) and [AI from Scratch](https://ai.noblerworks.com/learn/start-here/zero-to-hero-path/).

**Want them grouped by subject?** See the **[topic indexes](../../topics/)**.

---

## 🔐 Identity and access

| Topic | Read when... |
|-------|--------------|
| [IAM explained](./iam-explained.md) | "Roles vs policies vs federation" is fuzzy |
| [MFA and passkeys](./mfa-and-passkeys.md) | You want to know why SMS codes get phished and passkeys don't |
| [OAuth and OIDC explained](./oauth-and-oidc-explained.md) | "Log in with..." and access tokens feel like magic |
| [Least privilege explained](./least-privilege-explained.md) | You need to shrink what a stolen credential can do |
| [Zero trust explained](./zero-trust-explained.md) | Someone said "never trust, always verify" and you want specifics |

## 🔒 Protecting data

| Topic | Read when... |
|-------|--------------|
| [Encryption explained](./encryption-explained.md) | "Encrypted at rest" sounds safer than it is and you want to know why |
| [Hashing and password storage](./hashing-and-password-storage.md) | You need to store passwords, or know why SHA-256 is wrong for them |
| [Secrets management](./secrets-management.md) | You need credentials in an app without leaving copies everywhere |
| [TLS and HTTPS](./tls-and-https.md) | You want to know what the lock icon actually means |
| [Data loss prevention explained](./data-loss-prevention-explained.md) | You need to stop sensitive data leaving by email, upload or USB |
| [Backup and ransomware resilience](./backup-and-ransomware-resilience.md) | You want backups an attacker cannot delete, and proof they restore |

## 🌐 Network security

| Topic | Read when... |
|-------|--------------|
| [Network security basics](./network-security-basics.md) | Security groups vs NACLs vs WAFs keeps tripping you up |
| [DNS explained](https://cloud.noblerworks.com/learn/concepts/dns-explained/) | You want to understand how the internet finds things |

## 🛡️ Application and supply chain security

| Topic | Read when... |
|-------|--------------|
| [OWASP Top 10 explained](./owasp-top-10-explained.md) | You build or review web apps and want the common risks, defensively |
| [Threat modeling explained](./threat-modeling-explained.md) | You want to find design flaws before they are code |
| [Software supply chain security](./software-supply-chain-security.md) | Most of your code is dependencies and you want to trust them |

## ☁️ Cloud and container security

| Topic | Read when... |
|-------|--------------|
| [CSPM and CNAPP explained](./cspm-and-cnapp-explained.md) | A posture tool found 30,000 misconfigurations and you need the ten that matter |
| [Container security basics](./container-security-basics.md) | Your images carry hundreds of CVEs and run as root |
| [Kubernetes security basics](./kubernetes-security-basics.md) | You run a cluster and want RBAC, pod security and network policies right |

## 🚨 Detect and respond

| Topic | Read when... |
|-------|--------------|
| [Logging and detection](./logging-and-detection.md) | You collect logs but nothing tells you when something is wrong |
| [Incident response basics](./incident-response-basics.md) | You want a plan before the bad day, not during it |
| [Vulnerability management](./vulnerability-management.md) | The scanner found 4,000 issues and you need to know which matter |
| [Phishing and social engineering](./phishing-and-social-engineering.md) | You want to stop people being tricked, not just blame them |
| [Security awareness training](./security-awareness-training.md) | Everyone finished the annual module and nothing changed |
| [Email security: SPF, DKIM and DMARC](./email-security-spf-dkim-dmarc.md) | Attackers can send mail that looks like it came from your domain |
| [Endpoint security: EDR and XDR](./endpoint-security-edr-xdr.md) | Antivirus is not enough and you want to know what replaces it |

## 📋 Governance and risk

| Topic | Read when... |
|-------|--------------|
| [Risk management basics](./risk-management-basics.md) | You have more problems than budget and need to decide what to fix |

## ☁️ Cloud Computing

| Topic | Read when... |
|-------|--------------|
| [What is cloud computing?](https://cloud.noblerworks.com/learn/concepts/what-is-cloud-computing/) | You want the foundational mental model |
| [IaaS vs PaaS vs SaaS](https://cloud.noblerworks.com/learn/concepts/iaas-paas-saas/) | The three terms keep coming up |
| [Regions and availability zones](https://cloud.noblerworks.com/learn/concepts/regions-and-availability-zones/) | You're asking "where does my code actually run?" |
| [Shared responsibility model](./shared-responsibility-model.md) | You're wondering "what's AWS's job vs mine?" |
| [VPC explained](https://cloud.noblerworks.com/learn/concepts/vpc-explained/) | Networking inside the cloud confuses you |
| [IAM explained](./iam-explained.md) | "Roles vs policies vs federation" is fuzzy |
| [Serverless explained](https://cloud.noblerworks.com/learn/concepts/serverless-explained/) | You keep hearing "serverless" without a clear definition |
| [CDN explained](https://cloud.noblerworks.com/learn/concepts/cdn-explained/) | You see CloudFront/CloudFlare/Akamai and wonder what they do |
| [Caching explained](https://cloud.noblerworks.com/learn/concepts/caching-explained/) | You want to know why caches are fast and why they lie |
| [Load balancing explained](https://cloud.noblerworks.com/learn/concepts/load-balancing-explained/) | "Layer 4 vs layer 7" keeps coming up and you want specifics |
| [Autoscaling explained](https://cloud.noblerworks.com/learn/concepts/autoscaling-explained/) | You want capacity to follow demand without an outage |
| [Cloud cost basics](https://cloud.noblerworks.com/learn/concepts/cloud-cost-basics/) | The bill went up and nobody decided to spend more |

## ☸️ Containers and Orchestration

| Topic | Read when... |
|-------|--------------|
| [Containers vs VMs](https://cloud.noblerworks.com/learn/concepts/containers-vs-vms/) | You don't know why containers replaced VMs |
| [Kubernetes in 10 minutes](https://cloud.noblerworks.com/learn/concepts/kubernetes-in-10-minutes/) | Everyone uses K8s; you want to know why |
| [Container security basics](./container-security-basics.md) | You want small, scanned, non-root images |
| [Kubernetes security basics](./kubernetes-security-basics.md) | You want to lock down a cluster |

## 🛠️ DevOps / Infrastructure

| Topic | Read when... |
|-------|--------------|
| [Terraform explained](https://cloud.noblerworks.com/learn/concepts/terraform-explained/) | You want to understand IaC without diving into HCL |
| [CI/CD explained](https://cloud.noblerworks.com/learn/concepts/cicd-explained/) | "Pipelines" is hand-waved everywhere; you want specifics |
| [Observability basics](https://cloud.noblerworks.com/learn/concepts/observability-basics/) | "Logs vs metrics vs traces" needs a one-page answer |
| [Idempotency explained](https://cloud.noblerworks.com/learn/concepts/idempotency-explained/) | You're worried about retries doing things twice |
| [Eventual consistency](https://data.noblerworks.com/learn/concepts/eventual-consistency/) | A read returned stale data and you want to know why |
| [Queues vs streams](https://data.noblerworks.com/learn/concepts/queues-vs-streams/) | You can't pick between SQS and Kinesis |
| [Deployment strategies](https://cloud.noblerworks.com/learn/concepts/deployment-strategies/) | Rolling, blue-green, canary: which and when |

## 🗄️ Data and Databases

| Topic | Read when... |
|-------|--------------|
| [SQL vs NoSQL](https://data.noblerworks.com/learn/concepts/sql-vs-nosql/) | You're choosing a database and the options blur together |
| [Eventual consistency](https://data.noblerworks.com/learn/concepts/eventual-consistency/) | A read returned stale data and you want to know why |
| [Caching explained](https://cloud.noblerworks.com/learn/concepts/caching-explained/) | You want to know why caches are fast and why they lie |
| [Warehouses, lakes, and lakehouses](https://data.noblerworks.com/learn/concepts/warehouses-lakes-lakehouses/) | Someone said "lakehouse" and you nodded |
| [ETL vs ELT](https://data.noblerworks.com/learn/concepts/etl-vs-elt/) | You want to know why the transform moved after the load |
| [Batch vs streaming](https://data.noblerworks.com/learn/concepts/batch-vs-streaming/) | You're deciding whether a pipeline needs to be real-time |
| [Data modeling for analytics](https://data.noblerworks.com/learn/concepts/data-modeling-for-analytics/) | A report double-counted and you need to know how |
| [File formats and partitioning](https://data.noblerworks.com/learn/concepts/file-formats-and-partitioning/) | A query is slow or a warehouse bill is high |
| [Data pipelines and orchestration](https://data.noblerworks.com/learn/concepts/data-pipelines-and-orchestration/) | Your cron jobs have started depending on each other |
| [Data quality and lineage](https://data.noblerworks.com/learn/concepts/data-quality-and-lineage/) | A dashboard showed a wrong number and nothing errored |

## 🤖 AI / Machine Learning - foundations

| Topic | Read when... |
|-------|--------------|
| [LLM basics](https://ai.noblerworks.com/learn/concepts/llm-basics/) | You want to understand what a language model actually does |
| [Transformer architecture](https://ai.noblerworks.com/learn/concepts/transformer-architecture/) | You're ready to look inside the model |
| [Embeddings and vector search](https://ai.noblerworks.com/learn/concepts/embeddings-and-vector-search/) | You want to understand semantic search |
| [Context windows and management](https://ai.noblerworks.com/learn/concepts/context-windows-and-management/) | You're hitting token limits in production |
| [Multimodal models](https://ai.noblerworks.com/learn/concepts/multimodal-models/) | You want to use images / audio / video in prompts |

## 🤖 AI / Machine Learning - building with LLMs

| Topic | Read when... |
|-------|--------------|
| [Prompt engineering](https://ai.noblerworks.com/learn/concepts/prompt-engineering/) | You want to write prompts that actually work |
| [Tool use and function calling](https://ai.noblerworks.com/learn/concepts/tool-use-and-function-calling/) | You want the model to call your code |
| [MCP explained](https://ai.noblerworks.com/learn/concepts/mcp-explained/) | "Model Context Protocol" keeps coming up |
| [Structured outputs](https://ai.noblerworks.com/learn/concepts/structured-outputs/) | You want guaranteed-valid JSON from the model |
| [RAG explained](https://ai.noblerworks.com/learn/concepts/rag-explained/) | "Retrieval-augmented generation" is everywhere |
| [Fine-tuning vs RAG](https://ai.noblerworks.com/learn/concepts/fine-tuning-vs-rag/) | You want to know which one to reach for |
| [AI agents explained](https://ai.noblerworks.com/learn/concepts/agents-explained/) | You're trying to figure out what "agent" really means |
| [Agentic loops](https://ai.noblerworks.com/learn/concepts/agentic-loops/) | You want the deep-dive on the loop, not just the concept |
| [Prompt caching](https://ai.noblerworks.com/learn/concepts/prompt-caching/) | Your input costs are higher than they should be |

## 🤖 AI / Machine Learning - operations

| Topic | Read when... |
|-------|--------------|
| [Evals for LLMs](https://ai.noblerworks.com/learn/concepts/evals-for-llms/) | You're shipping LLM features and wondering how to test them |
| [Guardrails and safety](https://ai.noblerworks.com/learn/concepts/guardrails-and-safety/) | You're worried about prompt injection or unsafe output |
| [Prompt injection explained](https://ai.noblerworks.com/safety/security/prompt-injection-explained/) | You want to know why prompt injection has no clean fix |
| [AI threat modeling](https://ai.noblerworks.com/safety/security/ai-threat-modeling/) | You're designing an AI feature and want to find the risk early |
| [Inference servers](https://ai.noblerworks.com/learn/concepts/inference-servers/) | You're considering self-hosting an open-weights model |
| [Quantization and distillation](https://ai.noblerworks.com/learn/concepts/quantization-and-distillation/) | You want a smaller, faster model |
| [GPUs for AI](https://ai.noblerworks.com/learn/concepts/gpus-for-ai/) | You want to know what VRAM, FLOPS, and bandwidth actually decide |

---

## 🔁 Companion docs

- **[Glossary](../glossary.md)** - 200+ terms, one-line definitions
- **[Cloud from Scratch](https://cloud.noblerworks.com/learn/cloud-from-scratch/)** - structured 8-phase cloud path
- **[AI from Scratch](https://ai.noblerworks.com/learn/start-here/zero-to-hero-path/)** - structured AI/LLM learning path
- **[YouTube curation](../youtube.md)** - videos for visual learners
- **[Topic indexes](../../topics/)** - browse Learn + Build + Compare + Certify by subject

---

## 🤝 Suggest a topic

Missing a concept you keep getting asked about? Open an issue or PR. Criteria for new pages:
- One topic, focused
- 5-15 minute read
- Plain English, no exam framing
- Concrete example included

[Contributing Guide](../../CONTRIBUTING.md)
