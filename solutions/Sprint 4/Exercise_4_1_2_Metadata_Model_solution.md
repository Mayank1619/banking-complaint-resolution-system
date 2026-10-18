# Metadata Model

## Objective
Create a metadata model that links complaint evidence, policies, and source documents so retrieval is accurate and auditable.

## Business outcome
Reliable retrieval depends on a clear metadata model linking source documents to issues, categories, and complaint context.

## Implemented solution
### 1) Metadata schema
```python
metadata = {
    "document_id": "pol-01234",
    "source_type": "policy",
    "product": "credit_card",
    "issue_type": "unauthorised_transaction",
    "region": "UK",
    "effective_from": "2025-01-01",
    "version": "v2.3",
    "confidence": 0.96,
}
```

Metadata ensures the retrieval system can distinguish factually authoritative policy content from raw operational notes.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
