# Retrieval Service

## Objective
Build a retrieval service that returns the best supporting context for a complaint question or investigation.

## Business outcome
The system requires a retrieval layer that returns the right evidence based on relevance, freshness, and source quality.

## Implemented solution
### 1) Retrieval function
```python
def retrieve_context(question: str, product: str, top_k: int = 5):
    query_vector = embed(question)
    matches = index.search(query_vector, product=product, top_k=top_k)
    return [m for m in matches if m.score >= 0.55]
```

This retrieval service is used to build grounded answers for fact-based questions and policy lookup tasks.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
