# Chunking Experiment

## Objective
Compare chunking strategies so retrieved context is both relevant and compact enough for production-grade answers.

## Business outcome
The retrieval pipeline needs controlled chunk sizes so context is rich enough to answer well and compact enough to remain efficient.

## Implemented solution
### 1) Chunk experiment
The team should compare 200-word chunks, 400-word chunks, and overlap-based chunking for policy documents and customer communication transcripts.

```text
Small chunks: better retrieval precision, weaker holistic context
Large chunks: better narrative context, more noise
Overlap chunks: strong balance for sequential policy reasoning
```

The recommended baseline is 300-500 word chunks with 50-word overlap for policy material.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
