---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 12 min
applies-to: AWS docs as read 2026-11-07
---

# 02 - Incident response

**Domain 2: Incident Response (14%)** - SCS-C03 tasks 2.1 and 2.2.

In C02 incident response shared a domain with threat detection. In C03 it stands alone and adds a new skill, validating findings (2.2.3). The recurring pattern: prepare so that responders already have access, tools and runbooks; contain with the least blast radius; preserve evidence; then find the root cause.

---

## 2.1 Design and test an incident response plan

**Plans and runbooks** turn a finding into a sequence: who is told, what is checked, what is contained. Systems Manager Automation documents and OpsCenter hold runbooks; Step Functions orchestrate multi-step workflows; Lambda performs single steps. Write one runbook per common finding type (exposed access key, compromised instance, public bucket) and keep them in version control.

**Preparation** is mostly account design (see domain 6):

- A separate **security (forensics) account** where responders can reach copies of evidence, with access prepared in advance through roles that need no new provisioning during the incident.
- **Minimise blast radius**: workloads in separate accounts, narrow roles, no long-term keys, so one compromise cannot spread.
- Tools already deployed: GuardDuty, Security Hub, Detective, logging centralised and immutable.
- **AWS Shield Advanced** configured for resources exposed to denial of service, with its response team contact prepared.

```bash
# Route high-severity GuardDuty findings to a response target
aws events put-rule --name guardduty-high-severity \
  --event-pattern '{"source":["aws.guardduty"],"detail-type":["GuardDuty Finding"],"detail":{"severity":[{"numeric":[">=",7]}]}}'
```

GuardDuty creates an EventBridge event when a finding changes, which is the standard hook for automated response. Security Hub custom actions are the manual equivalent: an analyst picks a finding and chooses an action that runs a response.

**Automated remediation** fits well for low-risk, high-certainty cases: isolate an instance by swapping its security group to a quarantine group, disable an exposed access key, block a public bucket, or capture a forensic snapshot. Automating destructive actions without a human check risks outages, so build in approvals for production-critical resources. The exam guide names the Automated Forensics Orchestrator for Amazon EC2, Step Functions, Systems Manager and Application Recovery Controller as options.

**Testing** the plan is its own skill: tabletop exercises, game days, and **AWS Fault Injection Service** to introduce controlled failures, with Resilience Hub assessing resilience. A plan that has never run will fail at the first real incident. See the repo's [cloud incident response tabletop](../../../../../resources/hands-on-projects/cloud-incident-response-tabletop.md).

## 2.2 Respond to security events

Follow a loop: validate, scope, contain, eradicate, recover, learn.

**Capture and store forensic artifacts.** Snapshot EBS volumes of affected instances and share the snapshot to the forensics account; capture memory if your tooling allows; preserve relevant logs (CloudTrail, flow logs, application logs) in the immutable logging bucket. Hash and record what you collect. Do not terminate a compromised instance before capturing, unless the risk of continued damage outweighs the evidence loss.

**Search and correlate logs** across applications and services: Athena over CloudTrail and flow logs, CloudWatch Logs Insights, OpenSearch, or Security Lake. Correlate by principal, access key, source IP and time.

**Validate findings** (new in C03). A finding is a hypothesis. Check that the activity is not expected (a known scanner, a deployment), assess scope and impact (which resources, which accounts, which data) and determine severity. Corroborate GuardDuty findings with CloudTrail and with Detective's investigation.

**Contain, eradicate, recover**:

- **Compromised IAM credentials**: deactivate the access key, rotate secrets, attach a deny-all policy to the role or user and revoke active sessions (for roles, add an inline policy that denies actions for tokens issued before a time, which is how the console's "revoke active sessions" works). Review everything the credential did with CloudTrail.
- **Compromised instance**: isolate by swapping in a restrictive security group (security groups only allow, so use one with no rules, or only forensic access; already-tracked connections can persist, see network containment below), snapshot, then rebuild from a known-good image instead of cleaning.
- **Exposed data**: block public access, rotate any secrets inside, determine what was accessed using data events and S3 server access logs, and involve legal for notification duties.
- **Network containment** can also use network ACL deny rules for a source address, since network ACLs are stateless and take effect on existing flows, whereas removing a security group rule does not cut an already established tracked connection.
- **Recover** from backups (AWS Backup) after confirming they predate the compromise.

**Root cause analysis.** Amazon Detective collects log data from AWS resources and uses machine learning, statistical analysis and graph theory to build visualisations that help you analyse, investigate and identify the root cause of findings or suspicious activity. It complements GuardDuty (which detects) and Security Hub (which aggregates). Document the timeline and the control gap, and feed fixes back into preparation.

---

## Key terms

- **Runbook** - a documented, repeatable sequence of steps for responding to a defined type of event
- **Automated Forensics Orchestrator** - an AWS solution that automates forensic evidence capture for compromised EC2 instances
- **Blast radius** - the set of resources an incident or mistake can affect
- **Forensics account** - an isolated account where responders analyse copies of evidence
- **EventBridge rule** - a rule that matches events, such as GuardDuty findings, and routes them to targets
- **Security Hub custom action** - an analyst-triggered action that sends selected findings to an automated response
- **AWS Fault Injection Service** - a service for running controlled fault experiments to test resilience and response
- **Amazon Detective** - a service that builds interactive visualisations from log data to investigate the root cause of findings
- **Containment** - limiting the spread of an incident, for example by isolating an instance with a quarantine security group
- **Quarantine security group** - a security group with no inbound or outbound rules used to isolate a compromised instance
- **AWS Shield Advanced** - a paid DDoS protection tier with enhanced detection and response support

---

## Related

- [Notes 01: detection](./01-detection.md)
- [Notes 04: identity and access management](./04-identity-and-access-management.md) for credential response
- **[📖 What is Amazon GuardDuty?](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)** - EventBridge notification of findings, Detective integration
- **[📖 SCS-C03 exam guide, Domain 2](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03-domain2.html)** - the task statements and skills
