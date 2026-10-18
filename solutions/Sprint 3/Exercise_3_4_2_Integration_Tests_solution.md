# Integration Tests

## Objective
Exercise the end-to-end API and service flow with integration tests that confirm the complaint journey works as designed.

## Business outcome
The complaint service must be validated end-to-end to confirm API and service behaviour work together under realistic conditions.

## Implemented solution
### 1) End-to-end scenario
```text
POST /complaints -> 201 created
GET /complaints/{id} -> includes status and evidence links
POST /complaints/{id}/escalate -> status changes to escalated
```

These integration checks confirm the API, repository, and service layer behave consistently in a realistic workflow.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
