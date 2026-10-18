# Grounded Answers

## Objective
Generate grounded responses using retrieved evidence rather than unsupported model guesses.

## Business outcome
The complaint assistant must answer with evidence and clear citations so users trust the conclusion.

## Implemented solution
### 1) Answering pattern
```text
1. identify the user question
2. retrieve the strongest evidence
3. structure the answer with a clear summary and citation list
4. state uncertainty when evidence is incomplete or conflicting
```

A good grounded answer explicitly names the evidence and ties it to the complaint context instead of producing unsupported general advice.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
