# Fact Extraction

## Objective
Specify the extraction rules that pull the important facts out of unread complaint text and structure them for downstream use.

## Business outcome
Operational teams need the critical facts from each complaint pulled into a structured form so downstream analysis and decisioning are reliable.

## Implemented solution
### 1) Extraction rules
Parse complaint text to gather:
- customer id or account id
- product and channel
- dates, amounts, and transaction references
- issue description and supporting evidence paths
- customer impact and urgency indicators

```python
extracted = {
    "customer_id": "C-184220",
    "account_id": "A-90234",
    "product": "credit_card",
    "complaint_type": "unauthorised_transaction",
    "amount": 320.50,
    "reported_at": "2026-10-08T14:15:00Z",
}
```

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
