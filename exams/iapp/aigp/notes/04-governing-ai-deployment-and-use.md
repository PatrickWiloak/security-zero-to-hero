---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 14 min
---

# 04 - Governing AI deployment and use

**Domain IV: Understanding how to govern AI deployment and use (21-25 questions)** - competencies IV.A to IV.C of the v2.1 blueprint.

The blueprint says this domain applies "in any deployment context, such as a company deploying its own proprietary model or one from a third party". It starts from the point of choosing a model, and runs through responsible use and the ability to switch it off. Most organizations live here, because most buy or license models rather than build them.

---

## IV.A Evaluate key factors and risks relevant to the decision to deploy (6-8 questions)

Before choosing a system, **understand the context of the use case**: business objectives, performance requirements, data availability, ethical considerations and workforce readiness. Workforce readiness is easy to overlook. If the people who will use the system are not trained to question its output, the risk is higher however good the model is.

Then know the **differences in model types**, since each changes the risk profile:

| Choice | Governance consequence |
|---|---|
| Classic vs generative | Generative adds fabricated output, IP and content-misuse questions |
| Proprietary vs open source | Open models give control and inspection but shift more responsibility to you; proprietary models give less visibility and more vendor dependency |
| Small vs large | Smaller models are cheaper and easier to run locally; larger ones are broader but costlier and harder to test |
| Language vs multimodal | Multimodal inputs widen the data you handle (images, audio) and the attack surface |

And the **differences in deployment options**: cloud versus on-premise versus edge, and whether the model is used as is or adapted through **fine-tuning**, **retrieval augmented generation** (RAG, where the model retrieves your documents at query time to ground its answer) or **agentic architectures** (where the model can call tools and take actions). Each adaptation adds governance work. Fine-tuning changes the model and needs its own data governance and testing. RAG creates a data access question: the model should only retrieve what the user is allowed to see. Agents need limits on what actions they may take and a way for a human to approve or stop them.

## IV.B Perform key activities to assess the AI system (5-7 questions)

**Perform or review an impact assessment** on the selected system, just as in development but for the use you plan. The EU AI Act asks certain deployers of high-risk systems to carry out a fundamental rights impact assessment (Article 27).

**Assess the vendor or licensing agreement.** The blueprint asks you to identify and evaluate key terms and risks. In practice that means reading for: who owns inputs and outputs; whether your data is used to train the vendor's models; confidentiality and data location; security commitments and audit rights; indemnity for IP claims; performance and uptime commitments; incident notification; documentation the vendor will supply (which you need to meet your own duties); change notification when the model is updated; and exit terms. NIST GOVERN 6 and MANAGE 3 both address third-party risk: policies for it, and regular monitoring of third-party benefits and risks with controls applied and documented.

**Understand the risks unique to deploying your own proprietary model.** The blueprint's examples are "increased obligations and higher potential liability". If you build and put your name on a model you move from deployer to provider, with the heavier legal duties that follow (see [note 02](./02-laws-standards-and-frameworks.md)).

**Apply policies and practices to deployment**: data governance, risk management, issue management and user training. Users need to know what the system is for, what it is not for, how to spot a bad output, and how to report problems.

## IV.C Govern the deployment and use of the AI system (9-11 questions)

The largest slice of the exam.

**Monitoring and maintenance.** Continue monitoring the model and system, with a regular schedule for maintenance, updates and retraining. As a deployer you may not control the model, so monitor what you can: output quality, complaint and override rates, drift in your own input data, and vendor change notices.

**Periodic assessment.** Audits, red teaming, threat modeling and security testing, as in Domain III, now applied to the system in your environment and use. Watch for AI-specific security issues such as prompt injection, where crafted input makes a language model ignore its instructions, and sensitive data leaking through prompts or outputs. For deeper treatment of these from the security side, see the [AI safety pillar at ai.noblerworks.com](https://ai.noblerworks.com/safety/).

**Documentation.** Document incidents, issues, risks and post-market monitoring plans. Under the EU AI Act, deployers of high-risk systems must use them according to the instructions, assign competent human oversight, monitor operation, keep the logs they control, and inform the provider and authorities of serious incidents (Article 26).

**Anticipate misuse.** The blueprint asks you to "forecast and reduce risks of secondary or unintended uses and downstream harms". Ask what else this system could be used for by staff or customers, and what happens if outputs feed other systems. A tool approved for drafting emails can quietly become a tool for screening applicants.

**External communication.** Establish plans for communicating with users, regulators and the public about the AI, its limits and any incident. Transparency duties such as Article 50 notices (tell people they are interacting with AI, label synthetic content) live here.

**Deactivation.** Create and implement a policy and controls to **deactivate or localize** an AI system as necessary, for example because of regulatory requirements or performance issues. A kill switch that nobody is authorized to press, or that breaks dependent processes, is not a control. Decide who can invoke it, what the fallback process is, and test it.

> **Exam habit:** In deployment scenarios the strongest answer usually combines a documented owner, a monitoring signal, a communication step and a defined way to roll back or switch off.

---

## Key terms

- **Fine-tuning** - further training of a pre-trained model on specific data to adapt its behavior
- **Retrieval augmented generation (RAG)** - a pattern where a model retrieves relevant documents at query time and uses them to ground its answer
- **Agentic architecture** - a design where an AI model can call tools and take actions toward a goal with limited step-by-step human direction
- **Prompt injection** - crafted input that causes a language model to ignore or override its intended instructions
- **Open-source model** - a model whose weights and license allow access, use, modification and distribution
- **Secondary use** - use of a system for a purpose other than the one it was approved for
- **Deactivation** - the ability to switch off or restrict an AI system, for example for regulatory or performance reasons
- **Vendor risk** - the risk created by dependence on a third party's model, data or service
- **Human oversight** - arrangements that let people monitor, interpret and intervene in an AI system's operation
