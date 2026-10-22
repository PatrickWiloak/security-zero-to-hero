---
last-updated: 2026-10-22
difficulty: advanced
reading-time: 25 min
---

# CISM 2026 - Enterprise and Information Security Architecture for Managers

ISACA updates the CISM exam content outline **effective November 3, 2026**. Candidates testing before that date sit the 2022 outline; anyone testing on or after it is assessed on the 2026 outline. The four domains keep their names, the weights shift slightly, and ISACA adds **two new content areas: enterprise architecture and information security architecture**, with greater emphasis on information security strategy and program development.

This page teaches the two new areas at the depth a security manager needs. CISM does not turn you into an architect; it expects you to understand architecture well enough to govern it, fund it, and hold it to the business's risk appetite.

**[📖 ISACA: CISM Job Practice Update 2026](https://support.isaca.org/s/article/Certification-CISM-Job-Practice-Update-2026)** - effective date, weights, and the new content areas
**[📖 ISACA press release on the updated outline](https://www.isaca.org/about-us/newsroom/press-releases/2026/isaca-updates-cism-exam-content-outline-factoring-in-todays-technologies-security-responsibilities)** - what changes and why
**[📖 CISM Exam Content Outline](https://www.isaca.org/credentialing/cism/cism-exam-content-outline)** - the outline page (it still showed the 2022 task and knowledge statements on 2026-10-22)

## What changes on November 3, 2026

| Domain | 2022 outline | 2026 outline |
|--------|------------:|-------------:|
| 1. Information Security Governance | 17% | 18% |
| 2. Information Security Risk Management | 20% | 20% |
| 3. Information Security Program | 33% | 33% |
| 4. Incident Management | 30% | 29% |

The format stays 150 questions in four hours. ISACA states the update places greater emphasis on information security strategy and program development, and adds the two architecture areas "reflecting the need to understand the technologies under a security manager's purview." ISACA had not published the full 2026 task and knowledge statements on its outline page when this note was written; when it does, check which subdomain holds the architecture content. The guidance below does not depend on that placement.

ISACA also notes that older review materials were withdrawn from sale on September 1, 2026, and that 2022-edition prep materials do not cover the new areas. If you test on or after November 3, use the 2026 edition of the Review Manual and QAE database.

---

## Enterprise architecture

### What it is

**Enterprise architecture (EA)** is the organized description of how a business works and how its technology supports it. It typically has four layers:

- **Business architecture**: capabilities (what the business does, such as "process customer payments"), value streams, and organizational structure.
- **Data (information) architecture**: what data exists, where it lives, who owns it, and how it flows between capabilities.
- **Application architecture**: which applications deliver which capabilities, and how they integrate.
- **Technology architecture**: the platforms, cloud services, networks, and infrastructure underneath.

Frameworks such as **TOGAF** (a method for developing and governing an architecture) and the **Zachman Framework** (a classification matrix of who, what, where, when, why, and how across perspectives) give structure. CISM does not test framework mechanics; it tests why EA matters to security.

### Why a security manager needs it

Three reasons, each of which maps to how CISM questions are written.

1. **You cannot assess risk to things you cannot see.** EA is the map of business capabilities, the data flows between them, the applications, the cloud platforms, and the third parties involved. A risk assessment that is not anchored to that map misses the payment flow that passes through a forgotten integration server.
2. **Security strategy must align to business strategy.** EA states where the business is going: consolidating onto one cloud, acquiring a company, retiring a mainframe. A security strategy that ignores the target architecture funds controls for systems that will not exist in two years.
3. **Architecture decisions are where security is cheapest.** A control designed into the target state costs a fraction of the same control retrofitted after go-live. The security manager's lever is a seat on the **architecture review board** and security requirements written into architecture principles.

### Worked scenario

A retailer's EA team publishes a three-year target state: move order management to a SaaS platform, integrate it with a new third-party logistics provider through APIs, and decommission the on-premises ERP. The information security manager uses it to reshape the security program: third-party risk assessments for the SaaS vendor and logistics provider move to this year, API security standards are written before integration design starts, data classification is applied to the order data flows so contracts specify handling, and the planned refresh of on-premises ERP security tooling is cancelled because the system is being retired. The program's budget request cites the EA roadmap as its basis, which makes it easier for the steering committee to approve.

### How the exam tests this

CISM answers favor the option that **aligns security with business objectives through existing governance structures**. When a question describes a new initiative, the best first step is usually to understand the business and architecture context (or to engage through the architecture review process), not to select a technical control. Distractors propose the right control at the wrong time, or have the security manager design the architecture personally.

---

## Information security architecture

### What it is

**Information security architecture** is the part of the architecture that describes how security is achieved across the enterprise: the security principles, the control layers, and the shared security services that projects reuse. ISACA's press material and the training providers' summaries point to the same themes: identity models, segmentation, control layering, resilience design, secure integration patterns, and the trade-offs between them across hybrid and cloud environments.

The building blocks a manager should be able to explain:

- **Security principles** such as least privilege, defense in depth, secure by default, fail securely, and separation of duties, written as architecture principles that every project must satisfy.
- **Identity model**: identity as the control plane. Centralized identity (a single identity provider, federation, strong authentication, privileged access management) is the foundation every other control relies on.
- **Segmentation**: dividing networks and environments so a compromise in one zone does not spread. In cloud estates, segmentation is expressed through accounts or subscriptions, virtual networks, and policy, not only firewalls.
- **Zero Trust**: no implicit trust from network location; every request is authenticated, authorized, and evaluated in context.
- **Control layering**: preventive, detective, and corrective controls at several layers, so one failure is not fatal.
- **Resilience design**: redundancy, immutable backups, and tested recovery, so the architecture fails gracefully.
- **Secure integration patterns**: standard, approved ways to connect systems (API gateways, managed identities, message queues) instead of each project inventing its own.
- **Reference architectures and security services**: reusable, pre-approved designs (for example, "internet-facing web application on our cloud platform") that make the secure path the easy path.

### The manager's role

A security architect designs. A security manager **governs** the architecture: sets the principles, ensures every significant project passes architecture review, funds shared security services, measures conformance, and handles exceptions through the risk process. When a project cannot meet a principle, the manager does not simply approve or block it; the deviation is documented, the residual risk is assessed, and the **risk owner** accepts it or funds a compensating control.

### Trade-offs managers must weigh

- **Standardization versus flexibility.** A single reference architecture is cheaper to secure and audit; teams with special needs push back. The answer is a governed exception process, not unlimited variation.
- **Centralization versus resilience.** A single identity provider simplifies control but is a concentration risk; the architecture needs break-glass access and provider resilience.
- **Security versus usability and cost.** Strong segmentation and inspection add latency, operational effort, and spend. The level should follow the classification of what is protected and the organization's risk appetite.

### Worked scenario

A business unit wants to launch a customer portal in six weeks using a cloud service the company has never used. The security architecture defines a reference pattern for internet-facing applications (web application firewall, identity through the corporate identity provider, data encrypted with managed keys, logging to the central SIEM) that the new service cannot fully support: it cannot send logs to the SIEM. The manager's response follows governance: the architecture review records the deviation, the risk is assessed against the portal's data classification, the business owner accepts the residual risk for a defined period with a compensating control (logs exported daily from the service's native console to the SIEM), and a dated remediation item is added to the program roadmap.

### How the exam tests this

Expect manager-level questions: what is the **primary** benefit of a security architecture (consistent, reusable controls aligned to business needs), the **best** way to ensure new projects follow it (architecture review in the project life cycle), and how to handle a project that cannot comply (risk-based exception with an owner, not a unilateral decision by security). Answers that jump to a specific product or let security override the business without risk analysis are the usual distractors.

---

## How this connects to the rest of the outline

- **Domain 1 (governance):** architecture principles are an expression of security strategy, approved through governance.
- **Domain 2 (risk):** EA supplies the asset and data-flow context for risk assessment; architecture exceptions are risk decisions.
- **Domain 3 (program):** reference architectures and shared security services are program deliverables, and conformance is a program metric.
- **Domain 4 (incidents):** segmentation and resilience design decide how far an incident spreads and how fast recovery happens.

## Related

- [Notes 01: information security governance](./01-information-security-governance.md)
- [Notes 03: information security program](./03-information-security-program.md) - includes the existing security architecture section
- [Zero trust explained](../../../../learn/concepts/zero-trust-explained.md)
- [Least privilege explained](../../../../learn/concepts/least-privilege-explained.md)
