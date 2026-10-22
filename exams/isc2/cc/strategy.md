---
last-updated: 2026-10-22
difficulty: beginner
reading-time: 5 min
---

# ISC2 CC Study Strategy

## This is a vocabulary exam

CC tests whether you know what things are and how they relate, not whether you can configure them. The single highest-value study activity is building precise definitions for terms that sound similar and are constantly offered as each other's distractors.

Make a list, write your own definition of each, then check it against the ISC2 exam outline. The pairs that matter most are in the [practice plan readiness check](./practice-plan.md#readiness-check).

## The distinctions the exam lives on

**Threat, vulnerability, risk.** A vulnerability is a weakness. A threat is something that could exploit it. Risk is the combination of likelihood and impact. A locked door with a weak hinge has a vulnerability; a burglar is the threat; the chance and cost of a break-in is the risk.

**Control type versus control function.** These are two independent axes, and questions often ask for one when you are thinking of the other:

| | Preventive | Detective | Corrective |
|---|---|---|---|
| **Technical** | Firewall | IDS | Automatic patching |
| **Administrative** | Security policy | Audit | Incident response plan |
| **Physical** | Lock | CCTV | Fire suppression |

Plus **deterrent** (discourages: a warning sign, visible cameras) and **compensating** (an alternative when the primary control is not feasible).

**Authentication, authorization, accounting.** Who you are, what you may do, what you did.

**BC, DR, IR.** Business continuity keeps the business functioning. Disaster recovery restores technology. Incident response handles the security event. A ransomware attack invokes all three, and questions frequently ask which one a described activity belongs to.

**RTO and RPO.** Recovery **time** objective is how long until service is back. Recovery **point** objective is how much data you can afford to lose. RPO drives backup frequency; RTO drives recovery capability.

## Phase 1: Principles (week 1)

24% of the exam and the vocabulary the other domains use. Learn the risk terms, the risk management lifecycle in order, and the control taxonomy properly here, and the rest of the exam gets easier.

The **ISC2 Code of Ethics** canons are directly testable, including their **order**, because the code says they apply in order of precedence:

1. Protect society, the common good, necessary public trust and confidence, and the infrastructure
2. Act honorably, honestly, justly, responsibly, and legally
3. Provide diligent and competent service to principals
4. Advance and protect the profession

**Governance documents** are also directly testable: a **policy** is high level and mandatory, a **standard** is a mandatory specific requirement, a **procedure** is step by step, and a **guideline** is recommended rather than mandatory. New in 2026 is **due diligence versus due care**: diligence is investigating what is needed, care is doing it.

## Phase 2: Networking and cloud (week 2)

21.3%, and the hardest domain for beginners. Start it early rather than leaving it to the end.

You do not need to configure anything, but you do need to know what happens at each OSI layer, what the common devices do, what the common protocols are for, and what the common attacks are. Learn the common ports (22, 25, 53, 80, 443, 3389) because they appear as answer options. The 2026 outline adds wireless (Wi-Fi and Bluetooth), embedded systems, IoT, and industrial control systems, and names firewall zones, VLANs, and microsegmentation as the forms of segmentation.

Cloud is now in the domain title: the five cloud characteristics, the service models (IaaS, PaaS, SaaS), the deployment models, and the **shared security model**. The question shape is "who is responsible for X", and the answer moves toward the provider as you go from IaaS to SaaS.

## Phase 3: Identity and governance (week 3)

**Identity and access management** (20%) is now about the identity life cycle as much as access rules. Know the order (roles definition, provisioning, review, deprovisioning), why privilege creep happens, and the difference between least privilege and need to know: least privilege limits what you can do, need to know limits what you can see.

**Security governance** (17.3%) is the newest domain and the one older study material misses. Four things to be able to explain: what GRC is for, how BC and DR differ (BC keeps the business running, DR restores the technology), why culture and leadership matter to awareness, and the difference between a **KPI** (how well a process performs) and a **KRI** (a warning that risk is rising).

## Phase 4: Operations and incident response (week 4)

17.3%, and broader than it looks. Encryption is the place to be careful: **symmetric** is fast and uses one shared key, **asymmetric** solves key distribution and enables digital signatures, **hashing** is one-way and provides integrity rather than confidentiality. **Quantum-resistant cryptography** is new: know why it matters now (harvest now, decrypt later) and that it mainly threatens asymmetric algorithms.

Know the **incident response phases in order**: preparation, detection and analysis, containment, eradication, recovery, post-incident activity. Then the new material: threat actor types and motivations, what threat intelligence and MITRE ATT&CK are for, why end-of-life software is a risk, and the difference between red, blue, and purple teams, static and dynamic analysis, and vulnerability scanning and threat modeling.

## Common traps

| Trap | Reality |
|---|---|
| Confusing threat with vulnerability | A vulnerability is the weakness; the threat is what exploits it |
| Mixing control type with control function | Two independent axes; read which one is asked |
| Assuming a guideline is mandatory | Guidelines are recommended; standards and policies are mandatory |
| Confusing RTO with RPO | Time to restore versus data you can afford to lose |
| Treating a KPI as a KRI | A KPI measures process performance; a KRI warns that risk is rising |
| Swapping due care and due diligence | Diligence investigates what is needed; care does it |
| Thinking a purple team is a third team | Purple is red and blue working together openly |
| Thinking hashing is encryption | Hashing is one way and gives integrity, not confidentiality |
| Treating DR and BC as the same | DR restores technology; BC keeps the business running |
| Over-thinking the question | CC answers are usually the direct, textbook one |

## Exam day

- The exam is adaptive: 100 to 125 items in 120 minutes, and it stops once it is confident of your result. Pace for 125, which is just under a minute each.
- Under adaptive testing you cannot skip, flag, or go back. Read each question once carefully, answer, and move on.
- 700/1000 to pass; the score is scaled, so do not try to count. Finishing early says nothing about whether you passed.
- No penalty for a wrong answer; answer every item.
- Choose the **textbook** answer. CC rewards the standard definition over the clever real-world nuance.

## After you pass

Certification requires agreeing to the ISC2 Code of Ethics and paying the Annual Maintenance Fee. Maintain it with CPE credits over the three-year cycle. If you do not complete the requirements you remain a candidate rather than certified, so check the current terms on the ISC2 site.

## Related

- [Practice plan](./practice-plan.md)
- [Scenarios](./scenarios.md)
- [Fact sheet](./fact-sheet.md)
- [Study strategies](../../../resources/study-strategies.md)
- [Exam day checklist](../../../resources/exam-day-checklist.md)
