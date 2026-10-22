---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 15 min
---

# 02 - Security governance

**Domain 2: Security Governance (17.3%)** - new in the outline effective September 1, 2026.

This domain pulls together four things the old outline scattered or skipped: governance, risk, and compliance as a program (2.1), redundancy through business continuity and disaster recovery (2.2), security awareness and culture (2.3), and measuring whether security is working (2.4). If Domain 1 is the vocabulary, Domain 2 is how an organization runs security as an ongoing business function.

---

## 2.1 Governance, risk, and compliance (GRC)

### What GRC is

**Governance, risk, and compliance (GRC)** is the practice of running three related activities as one program instead of three separate efforts. **Governance** sets direction: who is accountable, what the policies say, and how decisions get made. **Risk management** finds and treats the things that could stop the organization reaching its goals (the lifecycle is in [notes 01](./01-security-principles.md#12-risk-management)). **Compliance** shows that the organization meets the laws, regulations, contracts, and internal policies that apply to it.

### Why it matters

The **purpose** of GRC is to make sure security effort goes where the business needs it and can be proven. Without it, three predictable things happen. Teams buy tools that address the risks they find interesting rather than the ones that matter most. The same evidence gets collected three times for three different audits. And when something goes wrong, nobody can show what was decided, by whom, or why.

The **importance** of GRC shows up most clearly in accountability. Senior leadership, usually the board, owns risk to the organization. Security teams advise and operate controls, but they do not get to accept major risks on the business's behalf. GRC is the structure that gets the right decisions in front of the right people.

### Frameworks and tools

Organizations rarely invent their GRC approach. They adopt **frameworks**, such as the NIST Cybersecurity Framework (whose Govern function, added in version 2.0, is essentially GRC), ISO/IEC 27001 for an information security management system, and COBIT for governance of IT more broadly. One control can satisfy several frameworks at once, so mature programs map controls to every framework they answer to and test each control once.

The **tools** are often a GRC platform: software that holds the risk register, the policy library, control mappings, audit evidence, and vendor assessments in one place. Smaller organizations do the same job with spreadsheets and a document library. The tool matters less than the discipline of keeping one source of truth.

AI has become a GRC topic in its own right. An organization adopting AI tools needs an owner for AI risk, a policy on acceptable AI use, an inventory of which AI systems are in use, and frameworks such as the NIST AI Risk Management Framework or ISO/IEC 42001 to structure the work.

---

## 2.2 Redundancy: business continuity and disaster recovery

The outline frames business continuity and disaster recovery under "redundancy", which is a helpful lens: both depend on having a second way to do something when the first way fails. Incident response is the third discipline people confuse with these two; it lives in [notes 05](./05-security-operations-and-incident-response.md#53-incident-response).

### Three disciplines, one bad day

| Discipline | Question it answers |
|---|---|
| **Incident response (IR)** | Something bad is happening. How do we handle the event itself? |
| **Business continuity (BC)** | How does the business keep functioning meanwhile? |
| **Disaster recovery (DR)** | How do we get the technology back? |

A ransomware attack invokes all three, and the exam asks which one owns a described activity. Isolating a network segment is IR. Switching clinicians to paper forms is BC. Restoring servers from backup is DR.

### Business continuity

**Business continuity (BC)** keeps critical business functions running during a disruption, whatever caused it: a cyberattack, a flood, a supplier failure, or a pandemic.

It starts with a **business impact analysis (BIA)**, which identifies the critical business functions, what they depend on, how much harm their loss causes over time, and the **maximum tolerable downtime** for each. The BIA comes first because every later decision depends on it. A continuity plan written without one is guessing at what matters.

The **business continuity plan** then sets out the alternative ways of working, who activates the plan and when, how staff and customers are told, and who does what. It must be **tested** and kept current. An untested plan is an assumption, not a plan.

### Disaster recovery

**Disaster recovery (DR)** restores the technology, data, and facilities the business depends on. Two objectives, set from the BIA, drive the design, and they are the most confused pair on the exam:

- **Recovery time objective (RTO)**: the maximum acceptable **downtime**. It drives recovery capability, such as standby systems.
- **Recovery point objective (RPO)**: the maximum acceptable **data loss**, measured in time. It drives how often you back up or replicate.

Nightly backups give an RPO of up to 24 hours, however fast the restore is. A 6-hour restore misses a 2-hour RTO, however recent the backup is. They are fixed by different things.

**Backup types** trade backup speed against restore speed:

| Type | Copies | Restore needs | Backup speed |
|---|---|---|---|
| **Full** | Everything | The full backup only | Slowest |
| **Incremental** | Changes since the **last backup of any type** | The full plus **every** incremental since | Fastest |
| **Differential** | Changes since the **last full backup** | The full plus the **latest** differential | Middle |

The **3-2-1 rule** keeps three copies of the data, on two types of media, with one copy offsite. Against ransomware, at least one copy should also be offline or immutable, because attackers deliberately look for and destroy reachable backups.

**Recovery sites** are redundancy for the whole facility:

| Site | Equipment | Data | Time to operate | Cost |
|---|---|---|---|---|
| **Hot** | Fully equipped and running | Current | Minutes to hours | Highest |
| **Warm** | Equipped | Synced periodically | Hours to days | Medium |
| **Cold** | Space and utilities only | None | Days to weeks | Lowest |

Cloud-based recovery has largely replaced dedicated warm and cold sites, because standby capacity can be paid for only when it runs.

**Redundancy inside systems** follows the same idea at smaller scale: redundant power supplies, RAID disks, clustered servers, multiple network paths, and a generator plus a UPS. Each removes a **single point of failure**, a component whose loss stops the whole service.

**Testing** progresses from least to most disruptive: a read-through (checklist) review, a tabletop exercise, a walkthrough, a simulation, a parallel test (the recovery site runs alongside production), and a full interruption test (production is shut down). Full interruption tests carry real risk and are rarely run.

---

## 2.3 Security awareness

### Organizational culture

Technology cannot fully stop an attacker who convinces an employee to help them, so people are both the most targeted part of an organization and a large part of its defense. **Security culture** is what people actually do when nobody is checking: whether they report a suspicious email, challenge a stranger at the door, or quietly work around a control that slows them down.

The outline stresses two drivers of culture. The first is the **importance of security** being understood, which comes from explaining why rules exist rather than only listing them. The second is **security leadership**: people copy what leaders do. If executives skip MFA or ask for exceptions, staff learn that security is optional. A good culture also treats reporting as a success. An employee who clicks a phishing link and reports it at once has limited the damage; punishing them teaches everyone else to stay quiet.

### Concepts every employee should know

**Social engineering** is manipulating people rather than technology. Attackers use authority ("this is the CEO"), urgency ("the account closes in an hour"), and helpfulness ("could you hold the door?"). **Pretexting** is building a believable false story to get information, and **baiting** leaves an infected USB stick where someone will plug it in.

**Phishing** is fraudulent messaging that tries to get credentials, money, or a click. **Spear phishing** targets a specific person, **whaling** targets executives, **vishing** uses voice calls, and **smishing** uses text messages. **Business email compromise** impersonates an executive or supplier to redirect a payment. AI has made all of these cheaper and more convincing: well-written phishing in any language, and **deepfake** voice or video of a real executive. The awareness response is a verification habit: confirm any unusual request, especially one involving money or credentials, through a separate channel you already trust.

**Password protection** covers using long, unique passwords (a password manager makes that practical), never sharing or reusing them, enabling MFA everywhere it is offered, and never entering credentials on a page reached from a link in an unexpected message.

### Running an awareness program

Training is an **administrative, preventive** control, and it works best when it is short, frequent, and relevant to each role. **Phishing simulations** measure and reinforce it, as long as they are used to teach rather than to shame. Finance staff need extra training on payment fraud, developers on secret handling, and executives on whaling and deepfakes.

---

## 2.4 Measuring cybersecurity effectiveness

### Metrics, KPIs, and KRIs

You cannot manage what you do not measure, and leadership cannot fund what it cannot see. The outline names **key metrics** and **key risk indicators (KRIs)**.

A **metric** is any measurement, such as the number of phishing emails blocked last month. A **key performance indicator (KPI)** measures how well a security process is performing against a target, looking backward: the percentage of critical patches applied within 14 days, or the mean time to detect an incident. A **key risk indicator (KRI)** is forward-looking and signals that risk is rising before something goes wrong: the number of internet-facing systems missing critical patches, the phishing simulation click rate going up, or the count of accounts belonging to people who have left.

The difference is directly testable. A KPI says "how well are we doing the work?" A KRI says "how close are we to trouble?" Good KRIs have a **threshold** agreed in advance, so crossing it triggers action rather than debate.

Useful measures share a few traits. They are tied to a risk or goal the business cares about, they can be gathered reliably and repeatedly, and they show a trend over time. A count with no target and no trend, such as "we blocked 2 million attacks", is a **vanity metric**: it sounds impressive and drives no decision.

### Dashboards, scorecards, and reports

The same data is presented differently for different audiences. A **dashboard** is a live or frequently refreshed view for people who act on it daily, such as a security operations team watching alert volumes. A **scorecard** compares current results against targets, often with red, amber, and green ratings, and suits a monthly management review. A **report** gives context and narrative for leadership or the board: what changed, why it matters, and what decision is needed.

The rule for all three is to match the audience. A board needs a handful of KRIs tied to business risk, with trends and a clear ask. It does not need firewall rule counts.

---

## Key terms

- **GRC** - governance, risk, and compliance run as one coordinated program rather than separate efforts
- **Governance** - the structure of accountability, policy, and decision-making that directs security
- **Compliance** - demonstrating that the organization meets applicable laws, regulations, contracts, and internal policies
- **GRC platform** - software holding the risk register, policies, control mappings, and audit evidence in one place
- **Business continuity** - keeping critical business functions running during a disruption
- **Disaster recovery** - restoring technology, data, and facilities after a disruptive event
- **Business impact analysis** - the study identifying critical functions, their dependencies, and the impact of losing them
- **Maximum tolerable downtime** - the longest a business function can be unavailable before unacceptable harm
- **RTO** - recovery time objective, the maximum acceptable downtime
- **RPO** - recovery point objective, the maximum acceptable data loss measured in time
- **Full backup** - a complete copy of all selected data
- **Incremental backup** - a copy of changes since the last backup of any type, fast to create and slow to restore
- **Differential backup** - a copy of changes since the last full backup, slower to create and faster to restore
- **3-2-1 rule** - three copies of data, on two media types, with one copy offsite
- **Hot site** - a fully equipped alternate site with current data, able to operate almost immediately
- **Cold site** - an alternate site with space and utilities but no equipment or data
- **Single point of failure** - a component whose failure stops the whole service
- **Tabletop exercise** - a discussion-based test of a plan without touching production systems
- **Security culture** - the security behaviors people actually show when nobody is checking
- **Social engineering** - manipulating people, rather than technology, into giving access or information
- **Pretexting** - building a believable false scenario to obtain information or access
- **Spear phishing** - phishing aimed at a specific individual or group
- **Whaling** - phishing aimed at senior executives
- **Business email compromise** - impersonating an executive or supplier by email to redirect payments or data
- **Deepfake** - AI-generated audio, image, or video that convincingly imitates a real person
- **Security awareness training** - an administrative preventive control addressing the human attack surface
- **KPI** - key performance indicator, a backward-looking measure of how well a security process meets its target
- **KRI** - key risk indicator, a forward-looking measure that signals rising risk before an incident
- **Vanity metric** - a measurement that sounds impressive but drives no decision
- **Dashboard** - a frequently refreshed view of security data for people who act on it daily
- **Scorecard** - a periodic comparison of results against targets, often rated red, amber, or green

---

## Related

- [Notes 01: security principles](./01-security-principles.md) - the risk lifecycle GRC runs on
- [Notes 03: identity and access management](./03-identity-and-access-management.md)
- [Scenarios](../scenarios.md) - scenarios 5, 6, and 9
- [Disaster recovery patterns](https://cloud.noblerworks.com/resources/architecture-patterns/disaster-recovery-patterns/)
- **[📖 NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)** - the Govern function in CSF 2.0
- **[📖 NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)** - structuring AI risk inside a GRC program
