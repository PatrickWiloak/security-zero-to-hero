# Microsoft Security, Compliance, and Identity Fundamentals (SC-900)

## Exam Overview

The Security, Compliance, and Identity Fundamentals certification validates foundational knowledge on security, compliance, and identity concepts and related cloud-based Microsoft solutions. This exam is intended for those looking to familiarize themselves with the fundamentals of security, compliance, and identity across cloud-based and related Microsoft services.

**Exam Details:**
- **Exam Code:** SC-900
- **Duration:** 60 minutes
- **Number of Questions:** 40-60 questions
- **Passing Score:** 700 out of 1000
- **Question Types:** Multiple choice, multiple select, drag and drop, hot area, case studies
- **Cost:** $99 USD
- **Prerequisites:** None (basic understanding of Microsoft 365 and Azure helpful)

## Exam Domains

These are the domains and weights in Microsoft's study guide, skills measured as of October 21, 2026 (source: **[📖 SC-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-900)**). Azure Active Directory is now Microsoft Entra ID throughout; older courses that still say "Azure AD" are teaching the same product under its old name.

> **Outline update, October 21, 2026.** Microsoft marked two skill groups as minor changes. Under *Describe function and identity types of Microsoft Entra ID*, the bullet now reads "types of identities, including workload identities" (the July 2026 wording said "including agent ID"). Under *Describe threat protection with Microsoft Defender XDR*, "Microsoft Defender Threat Intelligence (Defender TI)" became "Microsoft Threat Intelligence". Both are covered in [Outline additions: what the other notes miss](./notes/outline-additions-2026-10.md).

### 1. Describe the concepts of security, compliance, and identity (10-15%)
- **Security and compliance concepts:** shared responsibility model, defense in depth, Zero Trust, encryption and hashing, governance, risk, and compliance (GRC) concepts
- **Identity concepts:** identity as the primary security perimeter, authentication, authorization, identity providers, directory services and Active Directory, federation

### 2. Describe the capabilities of Microsoft Entra (25-30%)
- **Function and identity types of Microsoft Entra ID:** what Entra ID is, types of identities including workload identities, hybrid identity
- **Authentication capabilities:** authentication methods, multifactor authentication (MFA), password protection and management
- **Access management capabilities:** Conditional Access, Microsoft Entra roles and role-based access control (RBAC)
- **Identity protection and governance:** Microsoft Entra ID Governance, access reviews, Privileged Identity Management (PIM), Microsoft Entra ID Protection

### 3. Describe the capabilities of Microsoft security solutions (35-40%)
- **Core infrastructure security in Azure:** DDoS Protection, Azure Firewall, Web Application Firewall (WAF), network segmentation with virtual networks, network security groups (NSGs), Azure Bastion, Azure Key Vault
- **Security management in Azure:** Microsoft Defender for Cloud, cloud security posture management (CSPM), how policies, standards, and recommendations improve posture, cloud workload protection
- **Microsoft Sentinel:** SIEM and SOAR concepts, threat detection and mitigation in Sentinel
- **Threat protection with Microsoft Defender XDR:** Defender XDR services, Defender for Office 365, Defender for Endpoint, Defender for Cloud Apps, Defender for Identity, Defender Vulnerability Management, Microsoft Threat Intelligence, the Microsoft Defender portal

### 4. Describe the capabilities of Microsoft compliance solutions (20-25%)
- **Service Trust Portal and privacy:** Service Trust Portal offerings, Microsoft's privacy principles
- **Compliance management in Microsoft Purview:** the Purview portal, Compliance Manager, compliance score
- **Information protection, data lifecycle management, and data governance:** data classification, Content explorer and Activity explorer, sensitivity labels and label policies, data loss prevention (DLP), records management, retention policies and labels
- **Insider risk, eDiscovery, and audit:** insider risk management, eDiscovery, audit

Security solutions is the largest domain by a wide margin, so a third of your study time belongs there. Compliance dropped from the 25-30% band in older outlines to 20-25%.

## Notes

- [Security, compliance, and identity concepts](./notes/security-compliance-identity-concepts.md) - domain 1
- [Microsoft identity and access solutions](./notes/microsoft-identity-access-solutions.md) - domain 2
- [Microsoft security and compliance solutions](./notes/microsoft-security-compliance-solutions.md) - domains 3 and 4
- [Outline additions: what the other notes miss](./notes/outline-additions-2026-10.md) - workload identities, Microsoft Threat Intelligence, CSPM and Bastion, GRC, Service Trust Portal, Content and Activity explorer

## Study Tips

### Recommended Study Timeline: 4-6 weeks
1. **Week 1:** Security, compliance, and identity concepts
2. **Week 2:** Microsoft Entra ID and identity management
3. **Week 3:** Microsoft security solutions
4. **Week 4:** Compliance and information protection
5. **Week 5-6:** Practice tests and review

### Key Study Resources
- **Microsoft Learn Learning Paths:**
  - SC-900 part 1: Describe the concepts of security, compliance, and identity
  - SC-900 part 2: Describe the capabilities of Microsoft identity and access management solutions
  - SC-900 part 3: Describe the capabilities of Microsoft security solutions
  - SC-900 part 4: Describe the capabilities of Microsoft compliance solutions

### Hands-on Practice
- Explore the Microsoft Entra admin center
- Configure MFA and conditional access policies
- Set up Microsoft Defender for Cloud
- Use the Microsoft Purview portal
- Create sensitivity labels and DLP policies
- Review security and compliance dashboards

### Exam Strategy
- Understand the Zero Trust security model
- Know the difference between authentication and authorization
- Focus on capabilities rather than detailed configuration
- Understand compliance requirements and solutions
- Practice identifying appropriate tools for security scenarios

### Common Gotchas
- Distinguish between different Microsoft Defender products
- Understand Microsoft Entra ID vs on-premises Active Directory
- Know when to use different authentication methods
- Understand data classification and protection concepts
- Be familiar with compliance frameworks and regulations

## 📚 Comprehensive Study Resources

**👉 [Complete Azure Study Resources Guide](../../../.templates/resources-azure.md)**

For detailed information on courses, practice tests, hands-on labs, communities, and more, see our comprehensive Azure study resources guide which includes:
- Official Microsoft Learn paths (FREE)
- Top-rated video courses with specific instructors
- Practice test platforms with pricing and comparisons
- Hands-on lab environments and free tier details
- Community forums and study groups
- Essential tools and Azure CLI resources
- Pro tips and budget-friendly study strategies

### Quick Links (SC-900 Specific)
- **[SC-900 Official Exam Page](https://learn.microsoft.com/en-us/certifications/exams/sc-900/)** - Registration and exam details
- **[Microsoft Learn - SC-900 Learning Path](https://learn.microsoft.com/en-us/certifications/microsoft-365-fundamentals/)** - FREE official study path
- **[Azure Documentation](https://docs.microsoft.com/en-us/azure/)** - Complete Azure documentation
- **[Azure Free Account](https://azure.microsoft.com/en-us/free/)** - $200 free credit for hands-on practice

## Key Services Quick Reference

### Identity and Access Management
- **Microsoft Entra ID (formerly Azure Active Directory):** Cloud-based identity and access management
- **Microsoft Entra External ID:** External identity solutions (B2B collaboration and customer identities)
- **Microsoft Entra PIM:** Privileged identity management
- **Conditional Access:** Risk-based access policies

### Security Solutions
- **Microsoft Defender for Cloud:** Cloud security posture management
- **Microsoft Defender for Endpoint:** Endpoint detection and response
- **Microsoft Sentinel:** Cloud-native SIEM/SOAR solution
- **Azure Key Vault:** Secrets and key management

### Compliance Solutions
- **Microsoft Purview:** Unified data governance and compliance
- **Compliance Manager:** Compliance assessment and management
- **Information Protection:** Data classification and protection
- **eDiscovery:** Legal hold and content search

## Security Frameworks and Standards
- **NIST Cybersecurity Framework**
- **ISO 27001/27002**
- **SOC 1/2/3**
- **GDPR and other privacy regulations**
- **HIPAA, PCI DSS, FedRAMP**

Remember: This exam covers the breadth of Microsoft's security, compliance, and identity solutions. Focus on understanding when to use different services and their key capabilities rather than detailed technical implementation.