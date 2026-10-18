# Personas Journeys

## Objective
Map the main personas and complaint journeys so the system matches real customer and operational behaviour.

## Business outcome
Customer and agent journeys must be explicit so the experience and escalation logic reflect reality instead of an abstract assumption.

## Implemented solution
### 1) Primary personas
- customer raising a complaint
- agent handling the intake and triage
- specialist investigating complex or financial-risk cases
- analyst reviewing patterns and escalations

### 2) Journey map
```text
Submit complaint -> classify issue -> attach evidence -> assign owner -> investigate -> customer update -> resolution -> closure
```

The journey is not complete until status, evidence, and next actions are recorded in the case record.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
