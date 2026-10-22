# Microsoft Security Operations Analyst Associate (SC-200)

## Exam Overview

The Microsoft Security Operations Analyst Associate (SC-200) certification validates the skills required to collaborate with organizational stakeholders to secure IT systems. The role mitigates threats by using Microsoft Sentinel, Microsoft Defender XDR, Microsoft Defender for Cloud, and third-party security products. Security operations analysts investigate, respond to, and hunt for threats using these tools and recommend improvements to security posture.

**Exam Details:**
- **Exam Code:** SC-200
- **Duration:** 100 minutes
- **Number of Questions:** 40 to 60 questions
- **Question Types:** Multiple choice, multiple response, drag and drop, case studies, hot area, build list, active screen
- **Passing Score:** 700 out of 1000
- **Cost:** $165 USD (varies by region)
- **Languages:** English, Japanese, Chinese (Simplified), Korean, German, French, Spanish, Portuguese (Brazil)
- **Delivery:** Pearson VUE testing center or online proctoring
- **Validity:** 1 year (renewable free via online assessment on Microsoft Learn)
- **Prerequisites:** None required. Recommended: foundational understanding of Microsoft 365, Azure services, and Windows/Linux operating systems.

## Exam Domains

Domains and weights from Microsoft's study guide, skills measured as of October 21, 2026 (source: **[📖 SC-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-200)**). The outline has three domains; courses that show four ("Configure protections and detections" as its own domain) teach the pre-2026 outline.

> **Outline update, October 21, 2026 (minor).** The change log lists one change: the ingestion bullet now reads "Configure collection of Azure activity logs by using Azure Policy and resource diagnostic settings" (previously "Azure activities"). The capabilities the 2026 outline names that older material lacks (Sentinel data lake tiers, KQL jobs, summary rules, Sentinel graph, the Sentinel MCP server, attack disruption, case management, Security Copilot, SOC optimization, WEF, Graph activity logs) are taught in [notes 07](notes/07-sentinel-platform-and-agentic-soc.md).

### Domain 1: Manage a security operations environment (40 to 45%)
- Configure automation for Microsoft Defender XDR and Microsoft Sentinel: notifications, alert tuning and suppression, Defender for Endpoint advanced features, rules, custom data collection, ASR rules, automated investigation and response, automatic attack disruption, device groups and automation levels, Sentinel automation rules and playbooks
- Configure the Microsoft Sentinel SIEM and platform: roles, data retention across the Analytics, Data lake, and XDR tiers, workbooks, SOC optimization
- Ingest data: choosing connectors, Windows Security Events via AMA with data collection rules, Windows Event Forwarding, Syslog and CEF via AMA, Azure activity logs through Azure Policy and diagnostic settings, threat indicators, custom log tables
- Configure detections: custom detection rules from Advanced Hunting, Sentinel analytics rules (scheduled, NRT, threat intelligence, machine learning), MITRE ATT&CK coverage, anomalies

### Domain 2: Respond to security incidents (35 to 40%)
- Respond in Microsoft Defender XDR: Defender for Office 365 (including attack disruption), Purview, Defender for Cloud workload protections, Defender for Cloud Apps, Entra ID compromised identities, Defender for Identity, Sentinel, agentic AI investigation with Security Copilot, multi-stage and lateral movement attacks, case management
- Respond in Microsoft Defender for Endpoint: device timelines, live response and investigation packages, evidence and entity investigation, incidents from automatic attack disruption
- Investigate Microsoft 365 activities: Purview Audit, Content search in eDiscovery, Microsoft Graph activity logs

### Domain 3: Perform threat hunting (20 to 25%)
- Detect threats with Defender XDR: choosing the right table, KQL, Advanced Hunting queries, threat analytics, hunting graphs and blast radius, Sentinel graph relationships
- Detect threats with the Microsoft Sentinel platform: hunting queries, KQL jobs in the data lake, summary rule tables, notebooks including the Sentinel MCP server

### How the notes map to the domains

| Domain | Notes |
|--------|-------|
| 1. Manage a security operations environment | [02](notes/02-microsoft-sentinel-fundamentals.md), [06](notes/06-defender-for-cloud-and-endpoint.md), [07](notes/07-sentinel-platform-and-agentic-soc.md) |
| 2. Respond to security incidents | [01](notes/01-microsoft-defender-xdr.md), [04](notes/04-incident-investigation-and-response.md), [07](notes/07-sentinel-platform-and-agentic-soc.md) |
| 3. Perform threat hunting | [03](notes/03-kql-for-security.md), [05](notes/05-threat-hunting.md), [07](notes/07-sentinel-platform-and-agentic-soc.md) |

## Study Materials

### Notes
- [01 - Microsoft Defender XDR](notes/01-microsoft-defender-xdr.md) - Unified portal, workloads, incident correlation
- [02 - Microsoft Sentinel Fundamentals](notes/02-microsoft-sentinel-fundamentals.md) - SIEM/SOAR architecture, workspace design
- [03 - KQL for Security](notes/03-kql-for-security.md) - Query language for hunting and analytics
- [04 - Incident Investigation and Response](notes/04-incident-investigation-and-response.md) - Triage workflow, automation
- [05 - Threat Hunting](notes/05-threat-hunting.md) - Proactive hunting techniques and queries
- [06 - Defender for Cloud and Endpoint](notes/06-defender-for-cloud-and-endpoint.md) - CSPM, CWPP, EDR
- [07 - Sentinel platform and agentic SOC](notes/07-sentinel-platform-and-agentic-soc.md) - data lake tiers, KQL jobs, summary rules, Sentinel graph, MCP, attack disruption, cases, Security Copilot

### Study Resources
- [Fact Sheet](fact-sheet.md) - Quick reference with key facts and doc links
- [Practice Plan](practice-plan.md) - Structured 6 to 8 week study schedule
- [Scenarios](scenarios.md) - Real-world SOC scenario-based practice
- [Strategy](strategy.md) - Exam day strategy and tips

## Official Resources

- **Microsoft SC-200 Certification Page:** https://learn.microsoft.com/en-us/credentials/certifications/security-operations-analyst/
- **SC-200 Study Guide (official):** https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-200
- **Microsoft Learn SC-200 Learning Path:** https://learn.microsoft.com/en-us/training/courses/sc-200t00
- **Microsoft Sentinel Documentation:** https://learn.microsoft.com/en-us/azure/sentinel/
- **Microsoft Defender XDR Documentation:** https://learn.microsoft.com/en-us/defender-xdr/
- **Microsoft Defender for Cloud Documentation:** https://learn.microsoft.com/en-us/azure/defender-for-cloud/

## Recommended Training

### Video Courses
1. **Microsoft Learn SC-200 Learning Path** - Free official modules
2. **John Savill SC-200 Study Cram** (YouTube) - Free comprehensive review
3. **Pluralsight SC-200 Path** - Paid structured video training
4. **Tim Warner SC-200** (O'Reilly/Pluralsight) - Detailed walkthroughs

### Practice and Labs
1. **Microsoft Applied Skills assessments** - Free hands-on Sentinel and Defender assessments
2. **Microsoft Sentinel Training Lab** - GitHub-hosted lab deployment
3. **MeasureUp SC-200 Practice Test** - Official Microsoft practice provider
4. **Whizlabs SC-200 Practice** - Additional practice question bank

### Books and References
1. **Microsoft Sentinel in Action** (Packt) by Richard Diver, Gary Bushey
2. **Microsoft Defender for Cloud book** (Packt)
3. **The Definitive Guide to KQL** by Mark Morowczynski, Rod Trent

## Next Steps After Certification

### Career Paths
- SOC Analyst (Tier 1/2/3)
- Security Operations Engineer
- Incident Responder
- Threat Hunter
- Microsoft Security Consultant
- Detection Engineer

### Related Microsoft Certifications
- **SC-100** - Microsoft Cybersecurity Architect Expert
- **AZ-500** - Azure Security Engineer Associate
- **SC-300** - Identity and Access Administrator Associate
- **SC-400** - Information Protection Administrator Associate
- **MS-500** - Microsoft 365 Security Administrator

---

**Good luck with your SC-200 certification!** Strong KQL skills and hands-on time in a Sentinel workspace are the two highest-leverage investments you can make for this exam.
