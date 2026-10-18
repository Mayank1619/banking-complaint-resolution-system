# Classifier Prompt

## Objective
Define the complaint classification logic and the prompt structure that separates issue types consistently.

## Business outcome
The bank needs a repeatable way to classify complaint types at scale so routing and prioritisation are consistent.

## Implemented solution
### 1) Prompt design
```python
system_prompt = """
You are a complaint triage classifier for a UK retail bank.
Classify the complaint into one of: card payment, fraud, account access,
credit reporting, service quality, charges, or other.
Return JSON with keys: complaint_type, severity, confidence, rationale.
"""
```

### 2) Rule base
- fraud and unauthorised transactions are high severity by default
- repeated complaints indicate elevated risk
- missing customer identifiers reduce confidence and trigger verification
- service-delay complaints are routed to operations rather than fraud teams

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
