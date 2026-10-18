# Agent Spec

## Objective
Define the investigation agent specification and the business outcomes it needs to support for complaint handling.

## Business outcome
The business needs a defined investigation agent that can reason about complaint evidence, actions, and policy obligations.

## Implemented solution
### 1) Agent objective
The investigation agent should identify the missing fact, gather evidence, and propose the next operational step with clear traceability.

```text
Case in -> collect facts -> reason over policy -> decide on next action -> summarise findings -> request approval if needed
```

### 2) Trust guardrails
- do not make arbitrary decisions without evidence
- respect the policy and operational boundary
- surface uncertainty clearly
- escalate sensitive actions to a human reviewer

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
