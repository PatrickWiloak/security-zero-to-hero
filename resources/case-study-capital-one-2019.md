---
last-updated: 2026-10-22
difficulty: intermediate
reading-time: 14 min
---

# Case Study: Capital One, 2019

> A misconfigured web application firewall let an outsider obtain the temporary credentials of an over-permissioned IAM role, and that role could read a large share of the bank's S3 data. About 106 million people in the US and Canada were affected. This page covers what is on the public record, why it happened, and which controls would have prevented or caught it. It is written for defenders; it contains no attack instructions.

---

## Why this case matters

Capital One was not a cloud laggard. It was one of the first large US banks to commit to public cloud and had invested heavily in security. That is exactly why the case is so useful: it shows how a single application-layer weakness combines with a broad identity permission to turn a small mistake into a very large breach. The same two-step pattern (a server can be tricked into making requests, and the server's identity can read too much) still appears in cloud incidents today.

---

## What happened (public record)

The facts below come from Capital One's own disclosure, the US Department of Justice case against the individual responsible, and the Office of the Comptroller of the Currency (OCC) enforcement action.

- **The access.** According to Capital One, the unauthorized access occurred on **22 and 23 March 2019**. The criminal complaint describes access to Capital One data stored with its cloud provider between March and July 2019.
- **The data.** The data was mainly from credit card applications submitted between 2005 and early 2019. Capital One reported about **100 million people in the US and about 6 million in Canada** affected, including about **140,000 US Social Security numbers**, about **80,000 linked bank account numbers** of secured card customers and about **1 million Canadian Social Insurance Numbers**. Capital One said no credit card numbers or log-in credentials were compromised.
- **The discovery.** Capital One did not detect the intrusion itself. On **17 July 2019**, someone emailed its responsible disclosure address saying that Capital One data appeared to be posted on GitHub. Capital One confirmed the issue on **19 July 2019** and announced it on **29 July 2019**, the same day the FBI arrested the suspect.
- **The person responsible.** A former employee of the cloud provider, who had built a tool to scan for misconfigured cloud accounts. DOJ said she accessed data from more than 30 organizations, not only Capital One, and also used compromised servers to mine cryptocurrency. A jury convicted her in **June 2022** of wire fraud and computer intrusion charges; in **October 2022** she was sentenced to time served and five years of probation.
- **The penalties.** In **August 2020** the OCC fined Capital One **$80 million**, finding that the bank had failed to establish effective risk assessment before moving significant IT operations to the public cloud and had failed to correct weaknesses in a timely way. Capital One also settled consumer class action litigation for **$190 million**.

**[📖 Information on the Capital One cyber incident](https://www.capitalone.com/digital/facts2019/)** - Capital One's own summary of dates, data and response.
**[📖 OCC assesses $80 million civil money penalty against Capital One](https://occ.gov/news-issuances/news-releases/2020/nr-occ-2020-101.html)** - the regulator's findings on cloud risk management.
**[📖 United States v. Paige Thompson](https://www.justice.gov/usao-wdwa/united-states-v-paige-thompson)** - DOJ case page with charging documents and press releases.

---

## How the intrusion worked, at the level defenders need

Public court filings and Capital One's statements describe a "configuration vulnerability" in a web application firewall running on a cloud server. At the level that matters for defence, three conditions lined up:

1. **A server could be made to send requests on an outsider's behalf.** This class of flaw is called **server-side request forgery (SSRF)**: an application or proxy accepts a destination from the request and fetches it, so an outsider can make the server talk to places only the server should reach. See [OWASP Top 10 explained](../learn/concepts/owasp-top-10-explained.md), where SSRF is its own category in the 2021 list.
2. **One of the places only the server should reach handed out credentials.** Every EC2 instance can query the instance metadata service (IMDS) for the temporary credentials of the IAM role attached to it. In 2019 the original version, IMDSv1, answered any simple request from the instance. If a server can be tricked into fetching a URL, it can be tricked into fetching its own role credentials.
3. **The role could read far more than a firewall needs.** According to the complaint, the firewall's role could list and read data in a large number of S3 buckets. A WAF has no business need to read customer application data.

Each condition alone is survivable. Together they turned one misconfiguration into a breach of about 106 million records. That is the core lesson.

---

## Root causes

### 1. Over-permissioned IAM role (the biggest factor)

The firewall's role had permissions to list and read storage that held sensitive customer data. Least privilege would have scoped the role to exactly what a WAF needs (writing its own logs, reading its own configuration) and nothing else. This is the single control that would have shrunk the incident from "100 million records" to "an attacker obtained credentials that could do almost nothing". See [Least privilege explained](../learn/concepts/least-privilege-explained.md).

### 2. Application-layer misconfiguration enabling SSRF

The WAF configuration allowed requests to be relayed to internal destinations. Network egress from a reverse proxy should be limited to the backends it serves; it should never be able to reach the metadata endpoint or arbitrary hosts.

### 3. Credential delivery that trusted any local request

IMDSv1 did not distinguish between a request made deliberately by software on the instance and one relayed through a vulnerable application. AWS responded in **November 2019** with **IMDSv2**, which requires a session token obtained with a PUT request carrying a custom header, and sets a default hop limit that blocks most relayed requests. Most SSRF flaws can only issue simple GET requests, so IMDSv2 defeats them. **[📖 Use IMDSv2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html)** - configuring instances to require session tokens.

### 4. Detection gaps on the cloud control plane

The role's credentials were used from outside Capital One's environment to list and copy large amounts of data, and the intrusion was found through an outside tip months later. Signals that could have fired include: an instance role's credentials used from an IP outside the account's own infrastructure, a role that normally makes a handful of API calls suddenly listing many buckets, and an unusual volume of object reads. The OCC's findings specifically cite weaknesses in network security controls, data loss prevention and alerting.

### 5. Governance of the cloud migration

The OCC's central finding was about governance, not a single setting: risk assessment before the migration and the bank's internal audit function did not identify and fix these weaknesses in time. Controls existed on paper but were not effective in practice.

---

## What would have stopped or detected it

The value of a case study is in mapping each failure to a control you can check in your own environment today.

| Failure | Preventive control | Detective control |
|---|---|---|
| WAF could relay requests internally | Restrict proxy egress to known backends; validate and allow-list destinations in any feature that fetches URLs | WAF and proxy logs reviewed for requests to internal or link-local addresses |
| Metadata service handed out credentials to relayed requests | Require IMDSv2 on every instance (enforce with an SCP or account default); set hop limit to 1 where containers are not used | AWS Config rule or CSPM finding for instances allowing IMDSv1 |
| Role could read customer data | Least-privilege role scoped to the WAF's own resources; S3 bucket policies that only allow named roles; permission boundaries | IAM Access Analyzer unused access and external access findings; regular review of what each role can reach |
| Credentials used from outside the account | VPC endpoints with endpoint policies; bucket policies requiring access via the organization's VPC endpoints or network (`aws:SourceVpce`, `aws:PrincipalOrgID`, data perimeter conditions) | GuardDuty finding for instance credentials used from an external IP |
| Large-scale data copy went unnoticed | Encrypt sensitive data with KMS keys whose key policy does not grant the WAF role decrypt rights | S3 data events in CloudTrail; anomaly detection on object read volume per principal; DLP and Macie on sensitive buckets |
| Weaknesses not found by risk and audit functions | Cloud security architecture review before migration; independent testing of cloud controls | Continuous CSPM posture reporting to risk committees |

Two items in that table deserve more detail.

**Data perimeter controls.** AWS now publishes a "data perimeter" approach: guardrails that ensure only trusted identities access trusted resources from expected networks. A bucket policy that denies access unless the request comes through the company's own VPC endpoints means stolen role credentials used from the internet are refused, even if the role's IAM policy allows the read. **[📖 Building a data perimeter on AWS](https://docs.aws.amazon.com/whitepapers/latest/building-a-data-perimeter-on-aws/building-a-data-perimeter-on-aws.html)** - identity, resource and network perimeter controls.

**Credential exfiltration detection.** GuardDuty has a finding type for EC2 instance credentials being used from outside AWS or from another account. **[📖 GuardDuty IAM finding types](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types-iam.html)** - including `InstanceCredentialExfiltration`.

---

## The same pattern on Azure and GCP

The lesson is not AWS-specific. Every cloud has a local metadata endpoint that gives workloads credentials:

- **Azure** exposes managed identity tokens through the Instance Metadata Service and requires a `Metadata: true` header, which blocks the simplest SSRF requests. The defence is still the same: scope the managed identity tightly and restrict egress.
- **GCP** requires a `Metadata-Flavor: Google` header on metadata requests. Attached service accounts should have narrow roles, and the default Compute Engine service account (historically granted broad Editor rights) should not be used for workloads.

Across all three, the durable control is least privilege on the workload identity. Header requirements and IMDSv2 reduce the chance of credential theft; least privilege limits the damage when theft happens anyway.

---

## Defender's checklist

Use this list against your own estate. Each item maps to a root cause above.

- [ ] Every EC2 instance requires IMDSv2; new instances default to it at the account level
- [ ] No reverse proxy, WAF or URL-fetching feature can reach link-local or internal addresses it does not serve
- [ ] Every workload role, managed identity and service account is scoped to its own resources; no infrastructure component can read customer data
- [ ] IAM Access Analyzer (or the Azure and GCP equivalents) run with findings reviewed
- [ ] Sensitive buckets restrict access to named principals and expected networks (data perimeter)
- [ ] KMS key policies on sensitive data grant decrypt only to the services that need it
- [ ] S3 data events or equivalent object-level logging enabled for sensitive stores
- [ ] GuardDuty (or equivalent) enabled in every account and region, with credential exfiltration findings routed to on-call
- [ ] Alerts on unusual data access volume per principal
- [ ] A responsible disclosure channel that is monitored and triaged quickly
- [ ] Cloud control effectiveness tested independently, not only documented

---

## Cert mapping

| Cert | What this case tests |
|---|---|
| [CCSP](../exams/isc2/ccsp/) | Cloud data security, IAM in IaaS, shared responsibility |
| [CCSK](../exams/cloud-security-alliance/ccsk/) | IAM, infrastructure security, data security in cloud |
| [AWS Security Specialty](../exams/aws/specialty/security-scs-c02/) | IMDSv2, IAM policy evaluation, GuardDuty, S3 bucket policies, data perimeters |
| [Security+](../exams/comptia/security-plus/) | Least privilege, SSRF, misconfiguration as a vulnerability class |
| [CISSP](../exams/isc2/cissp/) | Security governance, risk assessment before major change, audit |

---

## Discussion questions

1. Which single control in the table above would have reduced the impact most? Why that one rather than IMDSv2?
2. Your WAF vendor's appliance needs an IAM role. Write down, in plain English, the exact permissions it should have.
3. How would you prove to an auditor that no instance in your organization accepts IMDSv1 requests?
4. The intrusion was found through an outside tip. What would your own first alert have been, and how long after the first API call would it fire?
5. The OCC's finding was about governance. What should a board-level risk committee have been shown before the migration?

---

## Related

- [Least privilege explained](../learn/concepts/least-privilege-explained.md) and [IAM explained](../learn/concepts/iam-explained.md)
- [OWASP Top 10 explained](../learn/concepts/owasp-top-10-explained.md) - SSRF and misconfiguration
- [CSPM and CNAPP explained](../learn/concepts/cspm-and-cnapp-explained.md) - catching misconfigurations continuously
- [Data loss prevention explained](../learn/concepts/data-loss-prevention-explained.md)
- [Centralized security logging and SIEM pipeline](./architecture-patterns/centralized-security-logging-siem.md) - getting data access logs to where detections run
- [Secrets and PKI platform](./architecture-patterns/secrets-and-pki-platform.md) - workload identity done well
- Other case studies: [SolarWinds 2020](./case-study-solarwinds-2020.md), [Log4Shell 2021](./case-study-log4shell-2021.md), [MOVEit 2023](./case-study-moveit-2023.md), [Snowflake customers 2024](./case-study-snowflake-customer-breaches-2024.md)
