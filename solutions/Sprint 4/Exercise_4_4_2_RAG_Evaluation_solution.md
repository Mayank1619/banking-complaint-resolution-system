# RAG Evaluation

## Objective
Evaluate answer quality, retrieval relevance, and compliance against a clear checklist.

## Business outcome
The team needs objective quality checks to ensure answers are grounded, relevant, and consistent.

## Implemented solution
### 1) Evaluation checks
- retrieval relevance score
- groundedness and citation presence
- factual consistency with known policy text
- answer usefulness for the complaint handler

```text
pass if citation coverage >= 80% and no unsupported claim is present
```

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
