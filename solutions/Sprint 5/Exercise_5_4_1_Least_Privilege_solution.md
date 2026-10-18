# Least Privilege

## Objective
Apply least-privilege patterns so the agent can act on complaint data without unnecessary permissions.

## Business outcome
The system must restrict tool and data permissions so the agent acts only within approved boundaries.

## Implemented solution
### 1) Policy pattern
The agent should be allowed to read complaint status and account metadata but not to alter payment instructions or customer personal details without explicit approval.

```text
read: complaint, evidence, policy
write: case notes, status updates
approve: payment reversal, closure, transfer to specialist team
```

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
