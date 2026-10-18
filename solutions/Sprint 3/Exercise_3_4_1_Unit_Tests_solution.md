# Unit Tests

## Objective
Write unit tests that validate the business rules and edge cases behind complaint creation and workflow logic.

## Business outcome
The service rules need automated checks so risk, validation, and edge-case behaviour remain stable as the system evolves.

## Implemented solution
### 1) Example test
```python
def test_priority_rises_for_repeated_complaints():
    complaint = create_complaint({"customer_id": "C1", "issue_type": "card", "repeat": True})
    assert complaint.priority == "high"
```

### 2) Coverage objectives
- validation rules for required fields
- status transitions and escalation logic
- edge cases such as duplicate evidence and missing metadata

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
