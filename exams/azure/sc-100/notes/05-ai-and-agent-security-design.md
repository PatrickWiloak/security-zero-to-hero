---
last-updated: 2026-10-22
difficulty: advanced
reading-time: 25 min
---

# 05 - AI and agent security design

The SC-100 skills outline measured as of October 21, 2026 threads AI through three of the four domains. This page teaches those objectives as a design topic in their own right, because the exam now expects an architect to place AI workloads and AI agents inside the same Zero Trust, benchmark, and data-protection frameworks as everything else.

**[📖 SC-100 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-100)** - skills measured as of October 21, 2026, with the change log

## What changed in the outline

Comparing the April 27, 2026 outline with the October 21, 2026 outline line by line:

| Domain | Removed or reworded | Added |
|--------|---------------------|-------|
| 1. Best practices and priorities | "Design solutions that align with best practices for Zero Trust security, including A Rapid modernization plan for Zero Trust (RaMP)" | "Design solutions that align with the Zero Trust adoption framework"; "Design AI solutions that align to the Microsoft Cloud Security Benchmark"; "Design a strategy for secure AI adoption" |
| 2. Security operations, identity, compliance | "Design a solution to address privacy requirements, including Microsoft Priva"; SOAR reworded to "security orchestration, automation, and response" | "Design a solution for agent identities using Microsoft Entra Agent ID and conditional access policies" |
| 4. Applications and data | "Microsoft Copilot for Microsoft 365 services" renamed "Microsoft 365 Copilot" | "Design security for data used in AI workloads" |

Microsoft's own change log for the October update lists two skill groups as minor changes (*Design solutions for security operations* and *Evaluate solutions for securing Microsoft 365*); the other differences above landed between April and October. The domain weights in the current outline are 20-25%, 25-30%, 25-30%, and 20-25%, so infrastructure now carries as much weight as security operations, identity, and compliance.

Two removals matter for study time. **RaMP** as a named plan is gone; the Zero Trust *adoption framework* replaced it (see below). **Microsoft Priva** is no longer an outline bullet, so privacy-management product detail can drop down your list, though privacy as a compliance requirement still appears through Purview.

---

## A strategy for secure AI adoption

### The architect's problem

Most organizations meet AI in three ways at once: employees use AI assistants such as Microsoft 365 Copilot and public chatbots, developers build AI applications on Azure AI services, and teams start to deploy agents that act with their own permissions. Each brings a different risk. Assistants surface whatever data the user can already reach, so oversharing becomes exposure. Custom AI apps add new attack surface such as prompt injection and model abuse. Agents add identities that act autonomously, sometimes at machine speed.

A secure AI adoption strategy is the plan that lets the business move forward on all three without creating ungoverned risk. The Cloud Adoption Framework's AI scenario frames it in phases: **govern** AI (policies on approved uses and data), **manage** AI (operations, cost, model lifecycle), and **secure** AI (protect the platform, the data, and the outputs). The exam objective is the security strand of that plan.

### The building blocks

- **Discover and govern use.** Find out which AI apps people already use. Defender for Cloud Apps discovers and can sanction or block generative AI SaaS apps. Purview Data Security Posture Management (DSPM) for AI shows which sensitive data flows into AI interactions.
- **Fix oversharing before rollout.** Copilot respects existing permissions, so the first Copilot security project is usually a permissions and labeling clean-up: restricted SharePoint sites, sensitivity labels with encryption on the most sensitive content, and access reviews on overshared sites.
- **Protect the platform.** For custom AI apps on Azure, apply the same landing-zone controls as any workload: private endpoints, managed identities instead of keys, network isolation, and Defender for Cloud's AI threat protection for prompt-injection and abuse signals.
- **Protect the outputs.** Content filtering (Azure AI Content Safety, including prompt shields) and grounding reduce harmful or manipulated responses.
- **Govern the agents.** Give each agent its own identity, scope its permissions, and put it under Conditional Access and lifecycle governance (next sections).

### Worked scenario

A bank's leadership wants Microsoft 365 Copilot for 5,000 staff within a quarter, while a data science team builds a customer-facing assistant on Azure OpenAI. The security architect proposes: a pilot of Copilot for 200 users after running DSPM for AI and an oversharing assessment on SharePoint; sensitivity labels with encryption on board and M&A sites so Copilot cannot summarize them for users without rights; blocking unsanctioned generative AI apps in Defender for Cloud Apps; and, for the custom assistant, a landing zone with private endpoints, managed identity, Content Safety prompt shields, and Defender for Cloud AI threat protection, with alerts flowing to Sentinel. Each element maps to one of govern, manage, or secure.

### How the exam tests this

Expect a scenario with an AI rollout and a constraint ("before broad Copilot deployment", "with the least administrative effort", "without changing permissions model"). The right answer usually fixes the data foundation first (labels, oversharing) rather than adding an AI-specific product on top of a broken permission model.

- **[📖 AI adoption in the Cloud Adoption Framework](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/ai/)** - govern, manage, and secure AI
- **[📖 Data Security Posture Management for AI](https://learn.microsoft.com/en-us/purview/dspm-for-ai)** - visibility into AI data use

---

## Aligning AI solutions to the Microsoft Cloud Security Benchmark

The **Microsoft Cloud Security Benchmark (MCSB)** is Microsoft's catalog of security controls for cloud workloads, and the default standard in Defender for Cloud. Version 2 adds an **Artificial Intelligence Security** control domain, with controls identified as AI-1, AI-2 and so on, covering three areas: AI platform security, AI application security, and AI security monitoring. Each control comes with Azure Policy definitions, so compliance can be measured continuously.

**What "align to MCSB" means in a design:** for every AI component, you can point to the benchmark control it satisfies and the policy that proves it. In practice that means:

- **Platform:** AI services reachable only over private endpoints, local key authentication disabled in favor of Entra ID, customer-managed keys where policy requires them, diagnostic logs enabled.
- **Application:** input and output filtering, least-privilege identities for the app and its plugins, and protection of the data the model grounds on.
- **Monitoring:** AI threat protection enabled, logs flowing into the SIEM, and detections for abuse such as jailbreak attempts.

**Trade-off:** MCSB alignment is a floor, not a design. A benchmark can say "use private networking"; it cannot tell you which data an assistant should be allowed to ground on. That judgment is still the architect's.

**How the exam tests this:** "Demonstrate continuously that AI resources follow Microsoft's security baseline" is the MCSB standard in Defender for Cloud's regulatory compliance dashboard, backed by Azure Policy. Distractors offer one-off assessments or manual checklists.

- **[📖 Microsoft Cloud Security Benchmark introduction](https://learn.microsoft.com/en-us/security/benchmark/azure/introduction)** - control domains and how they map to policy

---

## The Zero Trust adoption framework

The earlier outline named **RaMP**, the Rapid Modernization Plan, a prioritized list of Zero Trust initiatives. The October outline replaces it with the **Zero Trust adoption framework**, which organizes adoption around three layers:

- **Business scenarios** answer *why*: the outcomes leadership cares about, such as rapidly modernizing the security posture, securing remote and hybrid work, identifying and protecting sensitive business data, preventing or reducing damage from breaches, and meeting regulatory and compliance requirements.
- **Security disciplines** answer *what*: the strategy, architecture, and process capabilities needed to deliver those outcomes.
- **Technology pillars** answer *where*: identity, endpoints, data, apps, infrastructure, and network, which is where the controls are implemented.

The shift matters for how you answer design questions. RaMP was a technical to-do list. The adoption framework starts from a business scenario, so the "best" answer is the one that delivers the stated business outcome, sequenced so leadership sees value early. If the stem says "the board's priority is ransomware resilience", start from the *prevent or reduce business damage from a breach* scenario and work down to the pillars.

- **[📖 Zero Trust adoption framework: business scenarios](https://learn.microsoft.com/en-us/security/zero-trust/security-adoption-business-scenarios-overview)** - scenarios, disciplines, and pillars

---

## Agent identities with Microsoft Entra Agent ID and Conditional Access

### Why agents need their own identity

An AI agent that summarizes a user's email is acting for that user. An agent that runs nightly, triages tickets, and updates a database is acting for itself. If both run under a shared service account or an API key, you cannot tell which agent did what, cannot scope permissions per agent, and cannot apply policy. **Microsoft Entra Agent ID** gives agents first-class identities in the directory so the same Zero Trust controls that protect people and workloads can protect them.

### Three access patterns, three policy targets

Microsoft's Conditional Access documentation distinguishes how an agent gets its token, and the policy must target the identity that is the *subject* of that token:

| Agent behavior | Access pattern | Conditional Access targets |
|----------------|----------------|----------------------------|
| Acts for a signed-in user | On-behalf-of (delegated) | The **user** |
| Acts on its own, no user present | Application-only (client credentials) | The **agent identity**, or the **agent identity blueprint** it was created from |
| Acts as a digital worker with its own account and mailbox | Agent-user access | The **agent's user account** (the *Agents* assignment, not *Users*) |

The traps follow directly from that table. A policy on an agent identity does not cover the same agent's on-behalf-of calls, because the user is the subject there. A policy scoped to "All users" does not apply to agent user accounts; you must target agent users explicitly. And Conditional Access only protects tokens issued by Entra ID: an agent that calls a resource with an API key bypasses it entirely, which is why designs should remove key-based access.

### Designing for scale

Individually targeting hundreds of agents does not scale. Two mechanisms help:

- **Agent identity blueprints** define the configuration for a class of agents. A policy targeting a blueprint covers every agent identity created from it, including future ones.
- **Custom security attributes** label agents (and resources) with business categories, such as `AgentTier=Approved`. A policy can allow only agents carrying an approved attribute and block the rest.

Conditional Access can also block agents that ID Protection flags as high risk. Licensing is a design input: Conditional Access for agents requires a Microsoft Agent 365 license with Entra ID P1 or higher (or a plan that bundles both).

### Worked scenario

A company is piloting a dozen autonomous agents built by different teams. Security wants only reviewed agents to reach SharePoint and Graph, and wants new agents blocked by default. The design: every agent is created from an approved blueprint and tagged with a custom security attribute after security review; a Conditional Access policy targets all agent identities, blocks access to the protected resources, and excludes agents whose attribute marks them as approved; a second policy blocks high-risk agents; all agent sign-ins flow to Sentinel. API keys on the target resources are disabled so no agent can route around the policy.

### How the exam tests this

Questions turn on the token subject. Read the stem for "on behalf of the user", "without user interaction", or "its own mailbox", and pick the policy target accordingly. Answers that apply MFA to an autonomous agent are wrong, because there is no person to satisfy it.

- **[📖 Conditional Access for agents](https://learn.microsoft.com/en-us/entra/identity/conditional-access/agent-id)** - access patterns, blueprints, and limitations

---

## Security for data used in AI workloads

Data is the part of an AI system that leaks. The new Domain 4 objective asks you to design protection for three kinds of data:

- **Grounding and retrieval data.** The documents and records an assistant retrieves to answer a prompt. If the retrieval index ignores source permissions, any user can ask the assistant for content they could never open directly. The design rule is to preserve per-user authorization through retrieval (security trimming), and to keep sensitivity labels and encryption on the source content.
- **Training and fine-tuning data.** Copied into storage accounts and pipelines, often with less control than its source. Apply classification, storage encryption, private networking, and access limited to the training identity; scan with Purview so sensitive data is known before it is used.
- **Prompts and responses.** Users paste sensitive data into prompts, and responses can contain it. Purview DLP and DSPM for AI can detect and restrict sensitive information in AI interactions, and audit captures them for investigation.

**Trade-off:** aggressive filtering and trimming reduces usefulness; an assistant that can see little answers little. The architect's job is to match protection to sensitivity, not to block AI wholesale.

**How the exam tests this:** "Users must not be able to retrieve, through the assistant, documents they cannot open directly" is permission-aware retrieval plus labels. "Detect sensitive data in Copilot prompts" is Purview DLP and DSPM for AI. Answers that rely on telling the model not to reveal data are wrong: instructions are not access control.

---

## Related

- [Notes 01: security strategy and frameworks](./01-security-strategy-and-frameworks.md) - MCRA, MCSB, CAF, and Well-Architected
- [Notes 02: security operations, identity, and compliance](./02-security-operations-identity-compliance.md) - Conditional Access for people and workloads
- [Notes 04: application and data security](./04-application-and-data-security.md) - Purview and Microsoft 365 Copilot controls
- [AI safety and security](https://ai.noblerworks.com/safety/) - the AI Zero to Hero pages on securing AI systems
