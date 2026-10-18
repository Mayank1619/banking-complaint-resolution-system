# Classifier Prompt and Triage Logic

## Objective
Build a reliable mechanism for identifying complaint type, urgency, and required next action from raw customer text.

## Business problem
The bank needs a prompt-based triage mechanism that can interpret customer complaints consistently and route them to the correct team without depending on manual, inconsistent classification.

## Requirements gathered
- Define the allowed complaint categories and classification rules.
- Design a structured output with category, urgency, evidence needed, and next action.
- Capture rejection, ambiguity, and escalation paths for low-confidence cases.
- Validate the logic against realistic complaint examples.

## Key outputs to produce
- Stakeholder and scope overview
- Functional requirements and constraints
- Quality gates and edge cases
- Acceptance criteria tied to the sprint objective
- Clear handoff notes for downstream work

## Success metrics
- Complaint classification is more consistent across samples.
- High-risk cases are identified earlier and reviewed appropriately.
- Support teams have a structured and explainable decision trail.
- The prompt output is ready for downstream routing and investigation.

## Handoff
The classifier output feeds the routing, investigation, and AI workflow so the complaint process can move from intake to action with less ambiguity.

## Completion status
Completed as the actual solution for this exercise in the banking complaint-resolution programme.
