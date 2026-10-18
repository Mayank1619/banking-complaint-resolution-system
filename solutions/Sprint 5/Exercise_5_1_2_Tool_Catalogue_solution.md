# Tool Catalogue

## Objective
Catalogue the tools the agent can use so the workflows are explicit, bounded, and auditable.

## Business outcome
The agent needs a bounded tool set so actions are predictable, auditable, and easier to govern.

## Implemented solution
### 1) Tool inventory
- lookup_customer(customer_id)
- lookup_account(account_id)
- lookup_case(complaint_id)
- get_policy(product, issue_type)
- search_evidence(complaint_id)
- update_case_status(complaint_id, status)

Each tool should have a clear contract, parameter validation, and permission boundary.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
