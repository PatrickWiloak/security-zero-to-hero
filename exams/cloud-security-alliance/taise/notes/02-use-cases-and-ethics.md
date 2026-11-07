---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 11 min
---

# 02 - Generative AI use cases; ethics, transparency and explainability

**Modules 3 and 4 of 10 (6 exam questions each).** CSA's titles: "Generative AI Use Cases and Applications" and "Ethics, Transparency, and Explainability in AI". CSA's launch article describes the topic as AI use cases and ethical implications.

---

## Module 3: Generative AI use cases and applications

Common applications: drafting and summarizing text, customer support assistants, code generation, search and question answering over company documents, image and media generation, data analysis, and security operations support. For each use case, ask three questions: what value does it deliver, what could go wrong, and who is affected?

NIST AI 600-1 gives the "what could go wrong" list for generative AI. Its twelve risk areas are: CBRN information or capabilities, confabulation, dangerous, violent or hateful content, data privacy, environmental impacts, harmful bias and homogenization, human-AI configuration, information integrity, information security, intellectual property, obscene, degrading and abusive content, and value chain and component integration. Pair a use case with its dominant risks:

| Use case | Dominant risks |
|---|---|
| Customer support bot | Confabulation, data privacy, information security (prompt injection) |
| Code assistant | Intellectual property, information security, confabulation |
| Document Q&A (RAG) | Data privacy, information security, value chain |
| Content generation | Information integrity, intellectual property, harmful bias |
| Decision support (hiring, credit) | Harmful bias, human-AI configuration |

**Confabulation** is confidently stated but erroneous or false output. It is a natural result of how generative models work, so controls focus on grounding, verification and human review rather than expecting it to disappear. **Human-AI configuration** covers risks from how people interact with the system, such as over-reliance or automation bias.

**Risk-based adoption.** Not all uses deserve the same scrutiny. The EU AI Act sorts uses into prohibited practices (Article 5), high-risk systems (Article 6 and Annex III, for example employment and recruitment, education, essential services including creditworthiness) and transparency-only systems (Article 50). A low-risk internal summarizer needs lighter governance than a system that screens job applicants.

## Module 4: Ethics, transparency and explainability in AI

**Principles.** The OECD AI Principles give a widely used statement: inclusive growth, sustainable development and well-being; human rights and democratic values, including fairness and privacy; transparency and explainability; robustness, security and safety; and accountability. The NIST trustworthy-AI characteristics overlap with them.

**Transparency** means people can know when AI is in use and understand how it behaves. The EU AI Act turns parts of this into duties (Article 50): inform people they are interacting with an AI system unless it is obvious, mark synthetic audio, image, video and text as artificially generated in a machine-readable way, inform people exposed to emotion recognition or biometric categorization, and disclose deep fakes. The information must be clear and given no later than the first interaction or exposure.

**Explainability and interpretability.** NIST separates the two ideas: explainability concerns a representation of the mechanisms underlying the system's operation, and interpretability the meaning of its output in the context of its designed functional purpose. For a security professional the practical point is that decisions affecting people need documentation and explanation fit for the audience, and that more opaque models need more testing and monitoring.

**Fairness and bias.** NIST states the characteristic as "fair, with harmful bias managed". It accepts bias cannot always be eliminated, but it must be identified, measured and managed. Bias enters through data, design choices and human use. EU AI Act Article 10 requires examining data for biases likely to affect health and safety or lead to prohibited discrimination in high-risk systems.

**Accountability and human oversight.** Someone must own each AI system's outcomes. High-risk systems under the Act must be designed so natural persons can oversee them effectively (Article 14). Oversight only works if the humans have competence and authority.

> **Exam habit:** ethics questions are usually about which control makes a principle real: disclosure for transparency, testing for fairness, documentation and ownership for accountability.

---

## Key terms

- **Confabulation** - confidently stated but erroneous or false content produced by a generative AI system (NIST AI 600-1)
- **Human-AI configuration** - risks arising from how people interact with and rely on AI systems (NIST AI 600-1)
- **Information integrity** - the spectrum of information and associated patterns of its creation, exchange and consumption in society; high-integrity information can be trusted and distinguishes fact from fiction (NIST AI 600-1)
- **Harmful bias and homogenization** - unfair outcomes for groups and reduced diversity of outputs (NIST AI 600-1)
- **Transparency** - people can know AI is in use and understand its behavior at a level fit for the purpose
- **Explainability** - a representation of the mechanisms underlying an AI system's operation
- **Interpretability** - the meaning of an AI system's output in the context of its designed purpose
- **Accountability** - clear ownership of an AI system's outcomes and its governance
- **Deep fake** - AI-generated or manipulated image, audio or video content that resembles existing persons, objects, places, entities or events and would falsely appear authentic or truthful (EU AI Act)
