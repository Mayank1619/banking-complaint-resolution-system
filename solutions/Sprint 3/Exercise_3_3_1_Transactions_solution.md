# Transactions

## Objective
Handle complaint and account updates safely with transactional guarantees for service operations.

## Business outcome
Financial and customer-impacting actions must be rolled back consistently when processing fails or is interrupted.

## Implemented solution
### 1) Transaction pattern
```python
from sqlalchemy.orm import Session

def create_case_with_evidence(session: Session, complaint_data: dict, evidence: list[dict]):
    with session.begin():
        complaint = Complaint(**complaint_data)
        session.add(complaint)
        session.flush()
        for item in evidence:
            session.add(Evidence(complaint_id=complaint.complaint_id, **item))
    return complaint
```

The transaction boundary ensures the complaint and evidence are stored together or not at all.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
