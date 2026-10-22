---
last-updated: 2026-10-22
difficulty: advanced
---

# CISM - Certified Information Security Manager - Practice Questions

19 questions across the four CISM domains: information security governance, information security risk management, information security program development and management, and incident management. Questions 16 to 19 cover enterprise architecture and information security architecture, the content areas the 2026 exam content outline adds from November 3, 2026.

CISM is a management exam. When two answers are both technically defensible, the correct one is usually the one that aligns to business objectives, involves the right stakeholders, or follows governance process.

> **Cert page:** [exams/isaca/cism/](../../exams/isaca/cism/)

---

### Question 1
**Scenario:** What most influences the design of an information security strategy?

A. Available security products, since the capabilities of the tools the organization can buy set what the strategy can achieve
B. Peer organizations' programs, adopting the controls and structure that comparable firms in the same sector already use
C. The organization's business objectives and risk appetite
D. The latest threat intelligence, so the strategy changes direction each time a new adversary technique is reported

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Alignment to business objectives is the recurring CISM theme, and it is what separates a security program from a shopping list. Threats inform the risk assessment, but they do not set the strategy's direction on their own.
</details>

---

### Question 2
**Scenario:** Senior management does not support a proposed security investment.

A. Reduce the scope silently to fit the approved budget, and drop the controls that management is unlikely to fund
B. Escalate to the board at once, bypassing senior management, because the security manager's view should prevail
C. Implement it anyway under the manager's own authority, because the risk justifies acting without agreement
D. Present a business case quantifying risk reduction in business terms, with options, costs, and the residual risk of each

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Communicating risk in business language is a core CISM competency, and "we need it for security" is not a business case. Offering options with their residual risk lets management make an informed decision, which is where the decision belongs.
</details>

---

### Question 3
**Scenario:** Who should own the risk acceptance decision for a residual risk?

A. The business owner accountable for the affected process, at a level matching the risk
B. The security manager, who understands the technical exposure best and is therefore the right person to accept it on behalf of the business
C. The IT department, because it operates the systems and applications where the residual risk actually sits
D. The auditor, whose independent view of the control weaknesses makes the sign-off on acceptance more objective

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Security advises, the business accepts. A security manager accepting risk on the business's behalf misplaces accountability, which is why the seniority of the accepting party should scale with the size of the risk.
</details>

---

### Question 4
**Scenario:** Which best demonstrates the value of the security program to the board?

A. Metrics tied to business outcomes: risk reduction against appetite, control coverage of critical assets, and incident impact trends
B. Patch counts per month, showing how many systems were updated and how quickly, as a measure of how well the program is run
C. The number of attacks blocked by the perimeter tools each quarter, trended to show that the controls are working
D. A full tool inventory with licence counts and coverage per business unit, which shows the investment the program has made

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Activity counts show effort, not effectiveness, and blocked attacks in particular reward noisy environments. Board-level metrics answer whether risk is inside appetite and moving in the right direction.
</details>

---

### Question 5
**Scenario:** A risk assessment identifies a high risk with an expensive control.

A. Evaluate the treatment options - mitigate, transfer, avoid, or accept - against cost and business impact, and recommend
B. Always implement the control, because a high-rated risk must be reduced whatever the cost of the control
C. Transfer it through insurance in every case, since that removes the financial, regulatory, and reputational consequences of any breach
D. Accept the risk and record it in the register without review, since the control is too expensive to justify

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** A control costing more than the risk it removes is a poor decision even when the risk is high. Insurance transfers financial loss but not regulatory or reputational consequence, which is the limit of transfer as a strategy.
</details>

---

### Question 6
**Scenario:** What is the primary purpose of information security governance?

A. To pass audits and certifications, so the organization can show external parties that its controls meet the stated standard
B. To implement and operate controls day to day, so that the technical measures are installed and kept working correctly
C. To ensure security supports and aligns with business strategy, with clear accountability and measurable outcomes
D. To manage the security team's staffing, budget, and daily tasks so work is assigned on time

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Governance sets direction and accountability; management executes within it. The six outcomes ISACA names are strategic alignment, risk management, value delivery, resource management, performance measurement, and assurance process integration.
</details>

---

### Question 7
**Scenario:** A new regulation applies to the organization.

A. Buy a compliance tool that maps controls to the regulation, and rely on its dashboard to show where the organization stands
B. Wait for enforcement action to show how the regulator reads the rules, then change controls to match that interpretation
C. Perform a gap analysis against current controls, assess risk and effort, and build a prioritized remediation plan
D. Implement every requirement immediately, whether or not an existing control already meets it

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Gap analysis before action is the manager's move. Many requirements will already be satisfied by existing controls, and identifying those first is what makes the remaining plan proportionate rather than a wholesale rebuild.
</details>

---

### Question 8
**Scenario:** During an incident, who decides whether to shut down a critical production system?

A. The security analyst on duty, who has the most detailed view of the compromise and the technical risk of leaving it running
B. The system administrator, who owns the platform and can judge the effect of a shutdown on the application
C. The CISO alone, because the security function owns incident response and should not wait for other approval
D. Business management, informed by security's assessment, following the escalation path in the incident response plan

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Containment that stops the business is a business decision, and the time to agree who decides is before the incident, not during it. Predefined escalation criteria are what stop the argument happening at 3am.
</details>

---

### Question 9
**Scenario:** What is the first phase of incident response?

A. Eradication, which removes the cause of the incident from the environment before anything else can be done
B. Preparation, including the plan, roles, tooling, and training
C. Detection, because response cannot begin until an event is spotted and confirmed as a security incident
D. Containment, because limiting the spread of the incident is the most urgent action once it is known

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Preparation is the phase you cannot do during an incident, and it is where most response failures originate. The sequence continues through detection and analysis, containment, eradication, recovery, and lessons learned.
</details>

---

### Question 10
**Scenario:** Post-incident review identifies the same root cause as three previous incidents.

A. Retrain the team on the procedure that failed, because repeats point to a knowledge gap
B. Escalate it as a systemic issue requiring a governance-level decision on remediation and resourcing, with an owner
C. Add monitoring for that cause so the next occurrence is spotted sooner, leaving the fault in place
D. Close the incident as resolved, since it was handled in line with the response plan on each earlier occasion, with nothing more to do

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Recurrence means the earlier corrective actions did not address the cause, or were never funded. Treating the fourth occurrence as another incident rather than a program failure guarantees a fifth.
</details>

---

### Question 11
**Scenario:** A third-party vendor will process sensitive data.

A. Prohibit third parties from handling sensitive data, so the organization carries no supplier risk at all
B. Require an on-site audit of every vendor before any contract, whatever the sensitivity of the data they will process
C. Do due diligence proportionate to the risk, set security terms with a right to audit in the contract, and monitor throughout
D. Rely on their certifications, such as an ISO 27001 certificate, as proof that the service in scope is adequately controlled, with no further testing

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Certifications are a point-in-time input, not the whole assessment, and they may not cover the service you are buying. The lifecycle view is what CISM tests: due diligence, contractual requirements, ongoing monitoring, and a defined exit.
</details>

---

### Question 12
**Scenario:** Security policies exist but staff do not follow them.

A. Remove the policies, since rules that staff do not follow create a false record of control and expose the company to audit findings
B. Discipline offenders under the HR process, so that the cost of ignoring the policies is clear to everyone else
C. Add more policies covering each behaviour seen, so that the gaps staff are using are closed with explicit rules
D. Investigate why: unclear, impractical, unenforced, or poorly communicated, then fix the cause

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Policies that conflict with how work actually gets done are routed around, and no amount of enforcement changes that. Diagnosing the cause before choosing the remedy is the management answer.
</details>

---

### Question 13
**Scenario:** Which is the best indicator that a security awareness program is effective?

A. Behavioral change: fewer phishing simulation clicks, more reports of suspicious email, and fewer policy violations
B. Total training hours delivered per employee over the year, compared with the target in the awareness plan
C. Completion rates for the mandatory course, showing that nearly every employee finished the content on time, in every department
D. Satisfaction scores from post-course surveys, showing that staff found the sessions clear, useful, engaging, and well presented

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Completion measures attendance rather than learning. Reporting rate is often the more valuable metric than click rate, because a workforce that reports quickly shortens detection time even when someone does click.
</details>

---

### Question 14
**Scenario:** A business unit deploys a cloud service without security review.

A. Report the business unit to internal audit and senior management, so the breach of process is on record
B. Assess the risk, work with the unit to bring the service into compliance, and address the process gap that let it skip security review
C. Ignore it for now, since the service is already running and the unit has taken on the business risk of the cloud service
D. Shut it down immediately and block the vendor's domain, whatever the business impact on the unit's operations

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Shadow IT usually signals that the sanctioned path is too slow, so punishing the symptom drives the behavior further underground. Fixing the intake process is what reduces recurrence.
</details>

---

### Question 15
**Scenario:** How should the security program's risk register be maintained?

A. Annually, in time for the board's yearly review, which keeps the register stable and comparable from one year to the next for trend reporting
B. Continuously, with named business owners, consistent ratings, tracked treatment decisions, and review on a defined cadence
C. Only after incidents, when real events show which risks were underrated and which scenarios should be added to it
D. By the security team alone, so ratings are consistent and the register is not skewed by business unit interests or internal lobbying

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A register maintained by security alone becomes security's list of worries rather than the organization's risk position. Named business owners and a consistent rating method are what make it usable for decisions.
</details>

---

### Question 16
**Scenario:** A newly appointed information security manager must build a three-year security strategy. The enterprise architecture team has published a target state that moves core systems to SaaS and retires the on-premises ERP.

A. Benchmark the security budget against industry peers and request the same percentage of IT spend
B. Refresh the security tooling on every current system, starting with the on-premises ERP because it holds the most data
C. Align the security strategy and roadmap to the enterprise architecture target state and the business objectives behind it
D. Ask the architecture team to delay the SaaS moves until the security program has caught up

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Enterprise architecture states where the business is going, so a strategy aligned to it funds controls for systems that will exist and anchors risk work to real data flows. Investing in a system scheduled for retirement wastes resources, peer benchmarking ignores the organization's own needs, and delaying the business to suit security inverts the manager's role.
</details>

---

### Question 17
**Scenario:** Business units keep launching cloud applications that each implement authentication, logging, and network controls differently, and audit findings are rising. What should the information security manager do FIRST?

A. Block all new cloud applications until a full audit of existing ones is complete
B. Establish an information security architecture with principles and reference patterns, enforced through architecture review in the project life cycle
C. Purchase a cloud security posture management tool and assign it to the infrastructure team
D. Require each business unit to hire its own security architect

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** A governed security architecture makes the secure way the standard, reusable way, and architecture review is where projects are held to it. A tool finds deviations after the fact without setting the standard, a blanket block stops the business, and separate architects per unit would multiply the inconsistency.
</details>

---

### Question 18
**Scenario:** A project cannot meet a security architecture principle requiring central logging, because its SaaS platform cannot forward logs. The launch date is fixed by a regulatory deadline.

A. The security manager approves the deviation personally so the project can launch on time
B. The security manager blocks the launch until the vendor adds log forwarding
C. The project team decides on its own whether logging is needed, since it owns the delivery date
D. Document the exception, assess the residual risk, and have the business risk owner accept it with a compensating control and a remediation date

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Architecture deviations are risk decisions, and CISM expects them to go through the risk process with the business owner accountable. Approving or blocking unilaterally puts the decision with the wrong person, and leaving it to the project team bypasses governance entirely.
</details>

---

### Question 19
**Scenario:** Which BEST describes the value of enterprise architecture to information security risk management?

A. It maps business capabilities, data flows, applications, and third parties, giving risk assessments the context of what the business depends on
B. It replaces the need for a risk register by documenting every system in one place
C. It provides the technical configuration baselines that vulnerability scans are measured against
D. It assigns risk ownership automatically to the architects who design each system

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** EA supplies the asset and dependency context that makes risk assessment complete and business-relevant. It does not replace the risk register, configuration baselines belong to technical standards, and risk ownership sits with business owners rather than architects.
</details>

---

## Where to go deeper

- [CISM cert page](../../exams/isaca/cism/) - notes, practice plan, strategy
- [CISA practice questions](./isaca-cisa.md) - the audit counterpart
- [CISSP practice questions](./isc2-cissp.md) - the broader security professional exam
- [SOC 2 guide](../compliance-guides/soc2.md) - a control framework managers are held to
- **[📖 ISACA CISM](https://www.isaca.org/credentialing/cism)** - official exam content outline
