# Graph Routing

## Objective
Route tasks across the agent graph based on complaint type, urgency, and evidence availability.

## Business outcome
The case engine needs routing rules that select the right agent for the current complaint and context.

## Implemented solution
### 1) Routing logic
```python
if complaint.issue_type in {"fraud", "unauthorised_transaction"}:
    route_to = "evidence_agent"
elif complaint.severity == "high":
    route_to = "resolution_agent"
else:
    route_to = "intake_agent"
```

Routing should be deterministic, explainable, and tied to evidence quality rather than vague heuristics.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
