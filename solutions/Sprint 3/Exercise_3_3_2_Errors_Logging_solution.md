# Errors Logging

## Objective
Add structured error handling and logging so operational failures are visible, actionable, and consistent.

## Business outcome
Support teams need traceable operational logs and structured errors to debug and resolve failures quickly.

## Implemented solution
### 1) Error handling
```python
from fastapi import HTTPException

def validate_case_status(status: str):
    allowed = {"new", "in_review", "escalated", "resolved"}
    if status not in allowed:
        raise HTTPException(status_code=400, detail="unsupported_case_status")
```

### 2) Logging strategy
- log request id, case id, actor, and business action
- emit structured JSON log entries for audit and monitoring
- separate operational logs from customer-facing exceptions

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
