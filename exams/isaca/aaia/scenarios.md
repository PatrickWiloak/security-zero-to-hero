---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 6 min
---

# ISACA AAIA Scenarios

Worked situations, each targeting a distinction the outline leans on.

---

## Scenario 1: Nobody owns the model

**Scenario**: During an audit of a credit decision model, the data science team says the business owns it, the business says IT owns it, and no one reviews its performance.

**Solution Pattern**:
- Finding: ownership of AI-related risk, controls and decisions is undefined
- Cause: no governance charter or accountability assignment
- Recommendation: define a model owner, a review cycle and escalation, documented in policy
- Management responds with an action plan and date

**Key Takeaway**: Missing ownership is a governance finding and often explains other control gaps.

---

## Scenario 2: The model changed on Friday

**Scenario**: A model was retrained and released with no record of who approved it or what was tested.

**Solution Pattern**:
- Evaluate the change management program as applied to AI: approval, testing, rollback, versioning
- Sample recent changes and compare to the process
- Report the exception and the risk: unvalidated changes can alter decisions
- Recommend change control that covers model, data and configuration

**Key Takeaway**: Model retraining is a change; it needs the same discipline as code.

---

## Scenario 3: Testing the fairness claim

**Scenario**: Management says its hiring screener is unbiased and offers a vendor letter.

**Solution Pattern**:
- Treat the letter as an assertion, not sufficient evidence
- Request the test design, data and results, or perform your own analysis on outcomes by group
- Evaluate data input requirements (appropriateness, bias, privacy)
- Report the method and limits of your analysis

**Key Takeaway**: Seek independent, direct evidence, and assess data appropriateness as well as outputs.

---

## Scenario 4: Using AI in the audit

**Scenario**: The audit team wants to use a generative tool to summarize client documents.

**Solution Pattern**:
- Evaluate impact, opportunity and risk of AI inside the audit process
- Confirm confidentiality of client data, accuracy checking and reviewer sign-off
- Document how outputs were verified
- Do not treat the tool's summary as evidence without verification

**Key Takeaway**: AI can speed audits but the auditor remains responsible for the evidence and conclusions.

---

## Scenario 5: Incident, but no AI playbook

**Scenario**: A chatbot gave customers wrong refund terms for two days. Incident management had no AI procedure.

**Solution Pattern**:
- Evaluate the problem and incident management programs for AI
- Identify gaps: detection, classification, escalation, communication, root cause
- Recommend AI-specific procedures and evidence retention
- Follow up on remediation

**Key Takeaway**: AI incidents need defined handling, including preservation of prompts, outputs and versions.
