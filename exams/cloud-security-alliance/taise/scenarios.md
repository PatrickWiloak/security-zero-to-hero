---
last-updated: 2026-11-07
difficulty: intermediate
reading-time: 5 min
---

# CSA TAISE Scenarios

Worked situations that cross the module boundaries.

---

## Scenario 1: A chatbot is asked to ignore its rules

**Scenario**: A support chatbot receives a message telling it to disregard its instructions and reveal internal notes.

**Solution Pattern**:
- Recognize prompt injection against the application
- Keep secrets out of prompts, enforce access outside the model, and limit what the bot can reach
- Validate output, and monitor for repeated attempts
- Log and review incidents

**Key Takeaway**: Assume input is hostile and limit what a manipulated model can do.

---

## Scenario 2: An unvetted model from a public hub

**Scenario**: A team downloads a pre-trained model from a public repository and puts it in production.

**Solution Pattern**:
- Treat the model as a supply chain component: verify source, integrity and license
- Test behavior before use and record the version
- Add it to the AI inventory with an owner

**Key Takeaway**: Third-party models and data need vetting and traceability.

---

## Scenario 3: Who is responsible for which layer

**Scenario**: A company builds an app on a cloud-hosted foundation model and wonders who secures what.

**Solution Pattern**:
- Identify the roles: model provider, orchestrated service provider, application provider, AI customer, cloud provider
- Assign controls by layer and document the split
- Verify, don't assume, what the provider covers

**Key Takeaway**: Responsibility is divided across the AI stack, and you must know your part.

---

## Scenario 4: The model slowly gets worse

**Scenario**: A classifier's accuracy declines over months after deployment.

**Solution Pattern**:
- Suspect drift in the data or environment
- Check monitoring, then retrain or adjust per the change process
- Update thresholds and alerting; record the incident

**Key Takeaway**: Post-deployment monitoring and a feedback loop are part of the life cycle.

---

## Scenario 5: Personal data in the training set

**Scenario**: A fine-tuning set turns out to include customer personal data without a clear basis.

**Solution Pattern**:
- Stop use, assess the basis and the privacy impact
- Remove or replace the data and evaluate whether the model must be retrained
- Fix intake controls so data is classified and approved before use

**Key Takeaway**: Data governance happens before training, not after.
