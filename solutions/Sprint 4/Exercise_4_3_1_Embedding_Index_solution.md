# Embedding Index

## Objective
Create a vector index and embedding approach that finds semantically relevant complaint and policy passages.

## Business outcome
The app needs a searchable vector index that can surface semantically related complaint and policy passages quickly.

## Implemented solution
### 1) Embedding strategy
```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("all-MiniLM-L6-v2")
vector = model.encode("customer reported unauthorised card transaction on the 8th of October")
```

### 2) Retrieval design
- index chunk vectors with metadata
- keep source id and document version inside each row
- filter by product, issue type, and effective date when possible

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
