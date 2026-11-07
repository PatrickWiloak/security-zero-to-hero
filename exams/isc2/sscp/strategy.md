---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 5 min
---

# ISC2 SSCP Study Strategy

## What kind of exam this is

SSCP is a practitioner exam: it asks what you would do at the console, within your authority, in an operational situation. The vocabulary matters, but you win marks by choosing the right action from four plausible ones.

It is a computerized adaptive test (CAT) of 100-125 items in 2 hours. You cannot skip back, so commit to an answer and move on.

## Reading questions

1. Find the role. Are you the administrator, the analyst, or the manager? Practitioner answers fix, document and escalate; they do not accept risk or set policy.
2. Find the lifecycle stage. In incident response, "first" and "next" depend on the phase. In change management, testing precedes production.
3. Strike answers that break a principle: shared accounts, skipping approval, deleting evidence, trusting a network location.
4. Between two good answers, prefer the one that is preventive and scalable over the one that is manual and reactive, unless the question says an incident is under way.

## Distinctions to own

- **Preventive, detective, corrective, deterrent, compensating.** Name the function before looking at the options.
- **RTO, RPO and MTD.** Time to restore, data you can lose, and the limit of survival.
- **Hash, MAC, signature.** Integrity; integrity with a shared key; integrity with proof of origin.
- **Authentication, authorization, accounting.**
- **IDS and IPS; RADIUS and TACACS+; stateful and application firewalls.**
- **Containment, eradication, recovery.**

## Weights

| Domain | Weight | Time share |
|---|---:|---|
| Security Concepts and Practices | 16% | Steady |
| Network and Communications Security | 16% | Steady, start early |
| Access Controls | 15% | Steady |
| Risk Identification, Monitoring and Analysis | 15% | Steady |
| Systems and Application Security | 15% | Steady |
| Incident Response and Recovery | 14% | Steady |
| Cryptography | 9% | Efficient; learn the purposes, not the mathematics |

## Resources

Use the [official outline](https://www.isc2.org/certifications/sscp/sscp-certification-exam-outline) as the checklist, the [notes](./notes/01-security-concepts-and-practices.md) for explanation, and the [practice questions](../../../resources/practice-questions/isc2-sscp.md) to find gaps. Read each explanation, including the ones for questions you got right.
