---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 12 min
---

# 01 - Foundations of AI governance

**Domain I: Understanding the foundations of AI governance (16-20 questions)** - competencies I.A to I.C of the v2.1 blueprint.

This domain is about what you are governing and how you organize yourself to do it. It reads easy, and that is the trap: the questions reward precise vocabulary and a clear sense of who owns what.

---

## I.A Understand what AI is and why it needs governance (4-6 questions)

You need the generally accepted definition. The EU AI Act defines an AI system as a machine-based system designed to operate with varying levels of autonomy, that may exhibit adaptiveness after deployment, and that infers from its input how to generate outputs such as predictions, content, recommendations or decisions that can influence physical or virtual environments. The OECD wording is almost the same, which is no accident: the Act's definition follows the OECD's. Read both once and notice the shared pieces: a machine, some autonomy, inference rather than fixed rules, and outputs that affect something.

**[📖 EU AI Act, Article 3 definitions](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)** - the legal definition of AI system, provider, deployer and general-purpose AI model
**[📖 OECD AI Principles](https://oecd.ai/en/ai-principles)** - the OECD definition of an AI system and the five values-based principles

Know the **types of AI** at the level a manager needs: classic machine learning that predicts or classifies, generative AI that produces text, images or code, and agentic systems that take actions toward a goal. The blueprint expects you to tell these apart because the risks differ. A classifier's main risk is wrong or biased predictions. A generative model adds fabricated output, leakage of training data and misuse. An agent adds the chance that an unintended action actually happens.

The blueprint asks you to identify the **harms** AI can cause to individuals, groups, organizations and society, and gives examples: misalignment with objectives, ethics and bias risk, and complexity and scalability. Think of harm in four layers. An individual can be denied a loan unfairly. A group can be systematically disadvantaged. An organization can suffer legal, financial or reputational damage. Society can be affected through, for example, misinformation at scale.

Why does AI need its own governance rather than just IT policy? The blueprint lists the characteristics: complexity, opacity, autonomy, speed and scale, potential for harm or misuse, data dependency, and probabilistic versus deterministic outputs. Opacity means you may not be able to explain a decision. Probabilistic output means the same input can give different answers, so testing once proves little. Data dependency means a flaw in data becomes a flaw in decisions. Speed and scale mean one error repeats millions of times before anyone notices.

The **principles of responsible AI** in the blueprint are fairness, safety and reliability, privacy and security, transparency and explainability, accountability, and human-centricity. The NIST AI RMF names a similar set as the characteristics of trustworthy AI: valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed. NIST adds a point that exam scenarios like: these characteristics pull against each other. A highly secure but unfair system, or an accurate but opaque one, is undesirable, so governance means balancing trade-offs deliberately and documenting the choice.

**[📖 NIST AI RMF 1.0 (NIST AI 100-1), Section 3](https://doi.org/10.6028/NIST.AI.100-1)** - the characteristics of trustworthy AI and why they must be balanced

## I.B Establish and communicate organizational expectations (5-7 questions)

Governance is a people problem first. You **define roles and responsibilities** for stakeholders and set up **cross-functional collaboration** so the program has legal, privacy, security, data science, product, HR and business voices. The blueprint's reason is "efficacy and diversity of expertise and perspective". A governance board made only of lawyers misses technical failure modes. One made only of engineers misses legal duties.

You also **create and deliver training and awareness** on AI terminology, strategy and governance to all stakeholders. The EU AI Act makes a version of this a legal duty (Article 4, AI literacy), which is a good example of Domain I and Domain II meeting.

**Approaches differ by organization.** The blueprint asks you to differentiate approaches by company size, maturity, industry, products and services, objectives and risk tolerance. A ten-person startup using one vendor tool does not need the same machinery as a bank training its own credit models. The right answer in a scenario is usually proportionate: enough process to manage the real risk, no more.

Finally, **roles in the AI value chain**: developers, providers, deployers and users. The blueprint says some laws separate developers from deployers to assign liability, but that the certification uses the labels to describe distinct tasks, and many organizations fill both roles. Under the EU AI Act, a provider develops an AI system or model (or has it developed) and places it on the market under its own name; a deployer uses an AI system under its authority. A company that buys a tool and uses it internally is a deployer. If it builds the tool, or puts its own name on a system built by others, it is a provider.

## I.C Establish policies and procedures that apply throughout the AI life cycle (6-8 questions)

A policy set that follows the life cycle covers, in the blueprint's list: use case assessment, risk management, ethics by design, data acquisition and use, model and system development, training and testing, deployment and monitoring, documentation and reporting, and incident management. Put differently, there is a gate at each stage where someone asks the right question and records the answer.

Two moves matter. First, **evaluate and update existing policies** for AI rather than writing everything new: data privacy, security, data governance and intellectual property policies all need an AI lens (can staff paste customer data into a public chatbot, who owns generated output, how is training data approved). Second, **manage third-party risk** through procurement, supply chain, human resources and acceptable use policies, plus contracts and assessments. Most organizations deploy other people's models, so the vendor questionnaire, the contract clauses and the acceptable use policy do most of the governance work.

For the NIST view of this, the GOVERN function is described as cross-cutting and infused throughout risk management, setting policies, accountability structures, culture and third-party handling that the other functions depend on. See [note 02](./02-laws-standards-and-frameworks.md) for the full set of functions.

> **Exam habit:** When a scenario describes a problem in an AI program, look for the missing structure first (owner, policy, inventory, review gate) before reaching for a technical fix.

---

## Key terms

- **AI system** - a machine-based system designed to operate with varying levels of autonomy that infers from its input how to generate outputs such as predictions, content, recommendations or decisions (EU AI Act, Article 3)
- **Provider** - a person or body that develops an AI system or general-purpose AI model, or has one developed, and places it on the market or puts it into service under its own name or trademark (EU AI Act)
- **Deployer** - a person or body using an AI system under its authority, other than for personal non-professional activity (EU AI Act)
- **Trustworthy AI characteristics** - valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed (NIST AI RMF)
- **Opacity** - the difficulty of explaining why an AI system produced a given output
- **Probabilistic output** - output that can vary between runs on the same input, unlike a deterministic program
- **Cross-functional collaboration** - involving legal, privacy, security, technical and business roles in AI governance decisions
- **Third-party risk** - risk from AI models, data or services supplied by vendors, managed through procurement, contracts and acceptable use rules
