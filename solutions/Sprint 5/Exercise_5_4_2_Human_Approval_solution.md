# Human Approval

## Objective
Add human approval checkpoints for sensitive or high-impact actions before they are executed.

## Business outcome
Sensitive or financially material actions require a human review checkpoint before execution.

## Implemented solution
### 1) Approval policy
For sensitive actions, the agent must package a summary, evidence, expected impact, and human decision request.

```text
action: refund approval
evidence: complaint summary, policy reference, account status
reviewer: specialist operator
risk: financial and customer impact
```
The operator either approves, rejects, or requests more evidence.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
