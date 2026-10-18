# Service Layer

## Objective
Implement a service layer that orchestrates business logic, validations, and flow control without coupling to the transport layer.

## Business outcome
The application needs business logic separated from controllers so operational rules stay testable and consistent.

## Implemented solution
### 1) Complaint service contract
```python
class ComplaintService:
    def create_complaint(self, payload: dict) -> dict:
        self.validate_required_fields(payload)
        complaint = self._build_complaint(payload)
        self.repository.save(complaint)
        return {"complaint_id": complaint.complaint_id, "status": complaint.status}

    def escalate(self, complaint_id: str, reason: str, actor: str) -> None:
        complaint = self.repository.get(complaint_id)
        complaint.status = "escalated"
        complaint.assigned_to = actor
        self.repository.update(complaint, reason=reason)
```

### 2) Business responsibilities
- validate mandatory complaint fields
- allocate priority and ownership
- attach evidence and audit trail
- preserve case state through workflow transitions

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
