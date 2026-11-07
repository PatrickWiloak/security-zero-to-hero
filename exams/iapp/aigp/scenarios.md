---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 6 min
---

# IAPP AIGP Scenarios

Worked situations, each targeting a distinction the blueprint leans on.

---

## Scenario 1: The tool nobody approved

**Scenario**: Several sales staff paste customer emails into a public chatbot to draft replies. Nobody in legal or security knew.

**Solution Pattern**:
- Inventory the AI in use, including shadow use
- Update the acceptable use and data protection policies for AI: what data may go where
- Offer an approved alternative, with training, so staff are not pushed back to the public tool
- Assess what has already left, with privacy and legal

**Key Takeaway**: Governance starts with an inventory and policy, then enables safe use. A ban alone moves the behavior out of sight.

---

## Scenario 2: Which tier is the CV screener?

**Scenario**: An HR vendor sells a tool that ranks job applicants. Your company wants to deploy it in the EU.

**Solution Pattern**:
- Employment, including recruitment and selection, is an Annex III area, so the tool is high-risk
- The vendor is the provider and carries Articles 9 to 17; you are the deployer under Article 26
- As deployer: use per instructions, assign trained human oversight, monitor, keep logs, inform workers
- Check nondiscrimination law obligations independently

**Key Takeaway**: Classify the use, identify your role, then list the obligations for that role.

---

## Scenario 3: A model that got worse

**Scenario**: A fraud model passed validation at launch. Six months later the false negative rate has climbed.

**Solution Pattern**:
- Suspect drift: fraud patterns change
- Check monitoring metrics and the retraining schedule
- Document as an incident, assess impact, decide whether to constrain or retrain
- Update the monitoring plan so the signal is caught sooner

**Key Takeaway**: Launch testing does not last. Monitoring and maintenance are governance duties.

---

## Scenario 4: Reading the vendor contract

**Scenario**: A vendor's draft says it may use customer prompts to improve its models and may update the model without notice.

**Solution Pattern**:
- Negotiate no training on your data, or an opt-out, and confidentiality terms
- Require change notification and documentation so you can re-assess
- Seek IP indemnity and incident notification, and exit and data return terms
- Escalate to legal and privacy before signing

**Key Takeaway**: Third-party risk is managed in the contract; the terms are your controls.

---

## Scenario 5: Switching it off

**Scenario**: A customer-service agent can issue refunds. After an odd batch of refunds, someone asks who can turn it off.

**Solution Pattern**:
- Name the owner who may deactivate it, and document the procedure
- Provide a fallback process so service continues
- Review the agent's permissions and add approval above a limit
- Test the switch-off periodically

**Key Takeaway**: A deactivation policy needs an owner, a fallback and a test.
