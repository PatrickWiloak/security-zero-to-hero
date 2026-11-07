---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 12 min
---

# 04 - AI security and safety; cloud and AI security

**Modules 7 and 8 of 10 (6 exam questions each).** CSA's titles: "Introduction to AI Security and Safety" and "Cloud and AI Security". CSA's launch article groups part of this as cloud security and incident response in AI environments.

---

## Module 7: Introduction to AI security and safety

**Security and safety are related but different.** Security protects the system and its data from adversaries (confidentiality, integrity, availability). Safety is about preventing harm from the system's behavior, whether or not anyone attacks it. NIST lists "safe" and "secure and resilient" as separate trustworthy-AI characteristics and notes that systems should not endanger human life, health, property or the environment under defined conditions.

**Two sides of generative AI and security.** NIST AI 600-1 says generative AI creates two primary information security risks: it can lower barriers for offensive cyber capabilities such as hacking, malware and phishing, and it expands the available attack surface because the system itself is vulnerable to attacks such as prompt injection and data poisoning. Information security for generative AI includes maintaining availability and the integrity and, when applicable, confidentiality of the code, training data and model weights.

**Core defensive controls.**

- **Least privilege for tools and agents**, because excessive functionality, permissions or autonomy is the root of OWASP's Excessive Agency (LLM06).
- **Input and output handling**: treat model output as untrusted (LLM05), and use layered defenses against prompt injection rather than a single filter.
- **Keep secrets out of prompts**: system prompts can leak (LLM07), so enforce access controls outside the model.
- **Resource limits** and rate limiting against Unbounded Consumption (LLM10).
- **Authorized adversarial testing (red teaming)** and threat modeling before release and on a schedule.
- **Monitoring and logging** of prompts, outputs and tool calls, protected as sensitive data.
- **Human oversight** for high-impact actions.

**Safety controls.** Content filtering, refusal behavior, restrictions on dangerous capabilities, testing for harmful outputs and bias, and a way to switch the system off or fall back to a human process. NIST AI 600-1 lists dangerous, violent or hateful content and CBRN information or capabilities among generative AI risks.

**Incident response.** Prepare for AI incidents: harmful outputs at scale, data leakage through prompts or outputs, poisoned data found after release, and vendor model changes. Keep prompts, outputs, model versions and logs for investigation, define who can disable the system, and communicate to affected parties. NIST MANAGE 4 asks for post-deployment monitoring plans that include appeal and override, decommissioning, incident response, recovery and change management, and for incidents and errors to be communicated to relevant parties including affected communities.

## Module 8: Cloud and AI security

Most AI runs in the cloud, so cloud security fundamentals apply: identity and access management, network segmentation, encryption and key management, logging, configuration management, and vulnerability management. The AI-specific additions are protecting training data, model artifacts and endpoints, GPU and accelerator resources, and managed AI services.

**Shared responsibility across the AI stack.** CSA's AI Controls Matrix defines five roles with their own implementation and auditing guidelines: model provider, orchestrated service provider, application provider, AI customer and cloud service provider. Each is responsible for controls addressing security, privacy and compliance risks within its layer. The practical lesson: identify your role, read what the layer below provides, and cover the rest yourself. Do not assume the provider handles data protection, logging or access control for your application.

**[📖 CSA AI Controls Matrix](https://cloudsecurityalliance.org/artifacts/ai-controls-matrix)** - the five roles and 243 control objectives across 18 domains

**Cloud-specific considerations.**

- **Identity**: workload identities with least privilege for model endpoints, pipelines and data stores; avoid long-lived shared keys.
- **Data location and residency**: where training data, prompts and logs are stored and processed.
- **Network**: private connectivity to managed AI services where available; egress control for agents.
- **Supply chain**: pin and verify model artifacts and dependencies; NIST notes value chains involve many third-party components that may not be properly vetted.
- **Cost and availability**: OWASP describes Unbounded Consumption as excessive and uncontrolled inference leading to denial of service, economic loss, model theft and service degradation, a particular concern with pay-per-use cloud AI.
- **Provider assurance**: look for independent audit evidence and certifications, and read the scope.

CSA's CCSK covers cloud security fundamentals in more depth: see [CCSK](../../ccsk/).

> **Exam habit:** in cloud and AI questions, first decide who owns the layer in question, then pick the control that fits that owner.

---

## Key terms

- **AI security** - protecting AI systems and their data from adversaries
- **AI safety** - preventing harm arising from AI system behavior
- **Red teaming** - authorized adversarial testing that probes an AI system for failures and weaknesses
- **Least privilege** - granting only the access and functionality needed to perform a task
- **Excessive agency** - the vulnerability that lets damaging actions occur in response to unexpected, ambiguous or manipulated LLM output (OWASP LLM06)
- **System prompt leakage** - exposure of instructions that may contain sensitive information (OWASP LLM07)
- **Unbounded consumption** - uncontrolled inference leading to denial of service, economic loss and model theft (OWASP LLM10)
- **Model provider** - AICM role for the party that builds and supplies the model
- **Orchestrated service provider** - AICM role for the party that combines models and components into a service
- **Application provider** - AICM role for the party that builds the application on top of AI services
- **AI customer** - AICM role for the organization that uses the AI application or service
