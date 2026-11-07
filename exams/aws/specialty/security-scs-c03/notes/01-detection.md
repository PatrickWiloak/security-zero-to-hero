---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
applies-to: AWS docs as read 2026-11-07
---

# 01 - Detection

**Domain 1: Detection (16%)** - SCS-C03 tasks 1.1 to 1.3.

Detection answers one question: if something bad happens in this account, how do you find out, and how fast? The exam splits it into deciding what to watch (1.1), collecting the evidence (1.2) and fixing the pipeline when it breaks (1.3).

---

## 1.1 Design and implement monitoring and alerting

Start with the workload: what must be observed, and what does an anomaly look like for it? Then pick services by what they detect.

**Amazon GuardDuty** is the managed threat detection service. AWS describes it as continuously monitoring and analysing data sources and logs, using threat intelligence feeds and machine learning. When you enable it in an account, it ingests the foundational sources automatically: CloudTrail management events, VPC flow logs and DNS logs, with no agents and no log configuration on your side. On top of that you enable protection plans for more sources: S3 protection, EKS audit log monitoring, Runtime Monitoring (EKS, EC2, ECS and Fargate), Malware Protection for EC2, S3 and AWS Backup, RDS login activity, Lambda network activity and AI protection for Bedrock and SageMaker AI workloads. Extended Threat Detection correlates multi-stage attacks across sources and time into attack sequence findings. For many accounts use AWS Organizations with a delegated administrator, so new accounts are enrolled automatically.

```bash
# Enable GuardDuty in the current account and Region
aws guardduty create-detector --enable --region us-east-1
```

**AWS Security Hub** (the CSPM capability) gives one view of posture. It runs checks against standards such as AWS Foundational Security Best Practices, CIS, PCI DSS and NIST, and receives findings from GuardDuty, Inspector, Macie and partner products. Most control checks depend on AWS Config: you must enable Config and record resources, or the controls produce no findings. Security Hub only sees findings generated after it is enabled and only in the Region where it is enabled, and CIS compliance needs it in all Regions, so use cross-Region aggregation to a single aggregation Region. Automation rules change or suppress findings, and EventBridge routes them to responders. Findings are normalised so tools can consume them; the C03 guide removed ASFF as a topic, so know the idea and that OCSF is the schema to know (below).

**Amazon Macie** finds sensitive data in S3. **Amazon Inspector** finds vulnerabilities and unintended network exposure (domain 3). **AWS Config** records resource configuration and evaluates rules; **conformance packs** bundle rules and remediation actions as a YAML template deployable to an account or an organization.

```bash
aws configservice put-conformance-pack \
  --conformance-pack-name operational-best-practices \
  --template-s3-uri s3://example-config-templates/operational-best-practices.yaml
```

Skill 1.1.3 asks about aggregating events: use delegated administrator accounts for GuardDuty, Security Hub and Inspector, aggregator Regions, and Security Lake (next section) for a data lake. **Systems Manager State Manager** keeps resources in a desired state and runs recurring assessments.

Build metrics, alarms and dashboards for anomalies with CloudWatch. A metric filter on a log group turns a pattern, such as console logins without MFA or root account use, into a metric that can raise an alarm. Route alarms to Amazon SNS or EventBridge, and decide who is paged.

## 1.2 Design and implement logging

Decide sources, then storage, then analysis.

**AWS CloudTrail** records API activity. Management events are on by default in the 90-day event history for each account; for retention and organization-wide coverage create a trail. An **organization trail** logs events for the management account and all member accounts; only the management account or a delegated administrator can create it, and member accounts can see it but cannot delete it, stop logging or change what it logs. Organization trails created in the console are multi-Region. Logs go to one S3 bucket organised by organization and account ID, and by default only the management account can read them, so plan access for your security tooling.

```bash
aws cloudtrail create-trail \
  --name org-trail \
  --s3-bucket-name example-org-trail-bucket \
  --is-organization-trail \
  --is-multi-region-trail \
  --enable-log-file-validation
aws cloudtrail start-logging --name org-trail
```

**Log file validation** produces signed digest files so you can prove logs were not altered; check them with `aws cloudtrail validate-logs --trail-arn ARN --start-time TIME`. Data events (S3 object level, Lambda invocations) are off by default and must be selected, at a cost. **CloudTrail Lake** and **Insights** add querying and anomaly detection.

Other sources matter by threat: **VPC Flow Logs** (and transit gateway flow logs) for network metadata, **Route 53 Resolver query logs** for DNS (spotting malware domains), **ELB and CloudFront access logs**, **AWS WAF logs**, **S3 server access logs**, **CloudWatch Logs** agent for operating system and application logs. Use a dedicated logging account whose bucket denies deletion, with Object Lock and KMS encryption (domain 5), so a compromised workload account cannot erase its own tracks.

**Amazon Security Lake** centralises security data into a data lake in your account. It converts ingested data into Apache Parquet and the Open Cybersecurity Schema Framework (OCSF), backed by S3 buckets you own, and collects from CloudTrail, EKS audit logs, Route 53 resolver logs, Security Hub findings, VPC Flow Logs and WAF logs plus custom sources. Subscribers read the data; rollup Regions consolidate for residency. This is the answer when the question asks for normalised, multi-source, third-party-consumable logs.

For analysis: **CloudWatch Logs Insights** queries log groups, **Amazon Athena** queries logs in S3 with SQL, **OpenSearch Service** and **Managed Grafana** support search, correlation and dashboards, and **Lambda** parses or enriches events in flight. Match tool to need: ad hoc SQL over a lake is Athena; interactive search with dashboards is OpenSearch.

## 1.3 Troubleshoot monitoring, logging and alerting

Troubleshooting questions give a symptom and ask for the missing piece. Work the pipeline from source to destination.

- **No logs from a Lambda function**: its execution role lacks permission to write to CloudWatch Logs.
- **No CloudWatch agent data on an instance**: the agent is not installed or its configuration file is wrong, or the instance profile lacks the CloudWatch permissions.
- **CloudTrail not delivering**: the S3 bucket policy does not allow the CloudTrail service principal, or the KMS key policy does not let CloudTrail encrypt. For organization trails, CloudTrail creates the trail in member accounts even if validation fails, so check `get-trail-status` for delivery errors.
- **API Gateway or CloudFront logging gaps**: logging not enabled on the stage or distribution, or the logging role or bucket is missing.
- **Alarm never fires**: the metric filter pattern does not match, the alarm treats missing data wrongly, or the SNS topic policy blocks the publisher.
- **Findings missing in Security Hub**: it was enabled after the findings occurred, Config is not recording, or you are looking in a different Region than the aggregation Region.

---

## Key terms

- **GuardDuty foundational data sources** - the sources GuardDuty ingests automatically on enablement: CloudTrail management events, VPC flow logs and DNS logs
- **Extended Threat Detection** - the GuardDuty capability that correlates events across sources and time into multi-stage attack sequence findings
- **Security Hub CSPM** - the service that checks resources against security standards and aggregates findings from AWS services and partners
- **Cross-Region aggregation** - collecting findings from linked Regions into a single aggregation Region
- **Conformance pack** - a collection of AWS Config rules and remediation actions deployed as a single entity to an account or organization
- **Organization trail** - a CloudTrail trail that logs events for the management account and all member accounts
- **Log file validation** - CloudTrail digest files that let you verify logs were not modified after delivery
- **Data events** - high-volume CloudTrail events for resource operations such as S3 object access and Lambda invocation, off by default
- **VPC Flow Logs** - records of IP traffic metadata to and from network interfaces in a VPC
- **Amazon Security Lake** - a managed security data lake that stores normalised OCSF data in S3 buckets you own
- **OCSF** - the Open Cybersecurity Schema Framework, an open schema for security events
- **CloudWatch metric filter** - a pattern that turns matching log events into a CloudWatch metric
- **CloudWatch Logs Insights** - an interactive query tool for log groups

---

## Related

- [Notes 02: incident response](./02-incident-response.md)
- [Centralized logging and alerting project](../../../../../resources/hands-on-projects/centralized-logging-and-alerting.md)
- [Detection and response topic](../../../../../topics/detection-and-response.md)
- **[📖 What is Amazon GuardDuty?](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)** - data sources, protection plans, multi-account management
- **[📖 What is AWS Security Hub CSPM?](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)** - standards, controls, aggregation and automation
- **[📖 Creating a trail for an organization](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-trail-organization.html)** - organization trail behaviour and permissions
- **[📖 Conformance packs for AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/conformance-packs.html)** - rule and remediation bundles
- **[📖 What is Amazon Security Lake?](https://docs.aws.amazon.com/security-lake/latest/userguide/what-is-security-lake.html)** - OCSF, Parquet, subscribers and rollup Regions
