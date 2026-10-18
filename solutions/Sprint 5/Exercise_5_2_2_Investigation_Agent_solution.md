# Investigation Agent

## Objective
Build the investigation agent that can gather facts, explain actions, and reason over complaint evidence.

## Business outcome
The investigation workflow needs a single decisioning agent capable of planning and summarising case findings.

## Implemented solution
### 1) Agent workflow
```text
read complaint -> extract facts -> look up context -> query policy -> assess risk -> draft action plan -> request approval if required
```

### 2) Output format
- summary of facts found
- policies or evidence referenced
- recommended next action
- risk or confidence level

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
