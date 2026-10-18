# State Model

## Objective
Model the lifecycle state transitions that track complaint progress through investigation, review, approval, and closure.

## Business outcome
The complaint lifecycle needs explicit state transitions so every agent and reviewer knows what action is valid next.

## Implemented solution
### 1) Lifecycle states
```text
new -> triaged -> in_review -> evidence_required -> escalated -> awaiting_approval -> resolved -> closed
```

Each state carries a clear owner, required evidence, and allowed next action. This prevents unstructured or inconsistent hand-offs across the graph.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
