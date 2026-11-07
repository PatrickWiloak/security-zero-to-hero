---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 4 min
---

# ISC2 SSCP Study Plan

Six weeks at 6-8 hours a week for someone with some IT or security operations experience. Study against the [official outline](https://www.isc2.org/certifications/sscp/sscp-certification-exam-outline) (effective October 1, 2025). Weights are close to even, so each week gets roughly equal time.

## Week 1: Security concepts and practices (Domain 1, 16%)

- [ ] Read `notes/01-security-concepts-and-practices.md`
- [ ] Sort ten example controls by type and by function
- [ ] Write the steps of a change request, including the security impact analysis
- [ ] Explain the sanitization choice for three kinds of retired media

## Week 2: Network and communications security (Domain 6, 16%)

- [ ] Read `notes/06-network-and-communications-security.md`
- [ ] Draw a segmented network with a DMZ and mark where each appliance sits
- [ ] List the common ports and the insecure protocol each secure one replaces
- [ ] Compare RADIUS and TACACS+, IDS and IPS, WPA-Personal and WPA-Enterprise

## Week 3: Access controls and risk (Domains 2 and 3, 15% each)

- [ ] Read notes 02 and 03
- [ ] Walk a joiner, mover and leaver through the identity life cycle
- [ ] Do three ALE calculations by hand
- [ ] Describe what a SIEM correlation rule for a brute-force-then-success pattern would look at

## Week 4: Systems and application security (Domain 7, 15%)

- [ ] Read `notes/07-systems-and-application-security.md`
- [ ] Match each malware type to its defining behaviour
- [ ] Explain COPE, BYOD and COBO and the control each needs
- [ ] State the shared responsibility split for IaaS, PaaS and SaaS

## Week 5: Incident response, recovery and cryptography (Domains 4 and 5, 14% and 9%)

- [ ] Read notes 04 and 05
- [ ] Put the incident response phases in order and say what ends each
- [ ] Order evidence by volatility
- [ ] Say which key signs, which verifies, which encrypts and which decrypts
- [ ] Read the [cloud incident response tabletop](../../../resources/hands-on-projects/cloud-incident-response-tabletop.md) and talk it through

## Week 6: Practice and review

- [ ] Work through the [practice questions](../../../resources/practice-questions/isc2-sscp.md); read every explanation
- [ ] Re-read the notes for any domain below 70%
- [ ] Work through the [scenarios](./scenarios.md)

## Readiness check

You are ready when you can explain, without notes, the difference between: IDS and IPS, RADIUS and TACACS+, DAC and MAC, RBAC and rule-based, RTO and RPO, differential and incremental backups, hash and digital signature, and encryption in transit and at rest.
