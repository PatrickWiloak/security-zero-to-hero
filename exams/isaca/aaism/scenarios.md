---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 6 min
---

# ISACA AAISM Scenarios

Worked situations, each targeting a distinction the outline leans on.

---

## Scenario 1: The chatbot that read the wiki

**Scenario**: An internal assistant answers staff questions from a document store. A user from sales receives a paragraph from a confidential HR file.

**Solution Pattern**:
- Contain: restrict the assistant's retrieval scope or disable it for the affected index
- Root cause: retrieval ignored the user's access rights, so enforce permission filtering at retrieval time
- Check logs for other exposures, assess notification duties with legal and privacy
- Add the case to monitoring and the incident record

**Key Takeaway**: Retrieval-augmented systems inherit the data's access rules. Authorization must be enforced where the data is fetched, not assumed.

---

## Scenario 2: A pasted web page changes behavior

**Scenario**: A summarization tool reads web pages. A page contains hidden text telling the tool to send the user's mailbox contents to an address. The tool has mail access.

**Solution Pattern**:
- This is indirect prompt injection into a tool with excess agency
- Reduce the tool's permissions, require human approval for sending data out, and separate untrusted content from instructions
- Validate and constrain outputs before they reach other systems
- Test with red-team scenarios and monitor for unusual tool calls

**Key Takeaway**: Limit what the system can do, because you cannot fully control what it reads.

---

## Scenario 3: The vendor model update

**Scenario**: A vendor silently updates its model. Output quality changes and a downstream control stops working.

**Solution Pattern**:
- Require change notification and version pinning in the contract
- Re-validate on your own test set after any update
- Keep a rollback path and monitor key quality metrics
- Include the dependency in business continuity planning

**Key Takeaway**: Embed requirements in the contract and verify after every change.

---

## Scenario 4: Threshold for acceptable error

**Scenario**: A fraud model team says 95% accuracy is "good". Management asks how security decides if that is acceptable.

**Solution Pattern**:
- Tie the threshold to business impact of false positives and false negatives
- Set it with the risk owner, record it in the risk appetite and treat gaps with controls
- Review when conditions change

**Key Takeaway**: Thresholds come from risk appetite, not from the model team's convenience.

---

## Scenario 5: Training data from an unknown source

**Scenario**: A team fine-tunes a model on a downloaded dataset of unknown origin.

**Solution Pattern**:
- Pause: verify provenance and license, scan for sensitive data and obvious manipulation
- Record lineage, and test the resulting model for unexpected behavior
- Treat the dataset as a supply chain component with an owner

**Key Takeaway**: Data is a supply chain input and can be poisoned or unlawful.
