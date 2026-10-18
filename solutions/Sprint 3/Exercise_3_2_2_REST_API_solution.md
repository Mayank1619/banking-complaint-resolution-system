# REST API

## Objective
Expose complaint workflow endpoints with clear request and response contracts, validation, and status handling.

## Business outcome
A reliable complaint API is needed so external systems and internal tools can create, retrieve, and update complaint records safely.

## Implemented solution
### 1) API routes
```python
@app.post("/complaints")
def submit_complaint(payload: ComplaintCreate):
    complaint = complaint_service.create_complaint(payload.model_dump())
    return complaint

@app.get("/complaints/{complaint_id}")
def get_complaint(complaint_id: str):
    return complaint_service.get_complaint(complaint_id)
```

### 2) Release behaviour
- create complaint returns 201 with a complaint id
- get returns status, evidence links, and priority metadata
- invalid payloads fail with a clear validation error payload

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
