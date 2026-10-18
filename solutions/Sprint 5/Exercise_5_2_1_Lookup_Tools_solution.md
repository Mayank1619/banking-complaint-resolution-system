# Lookup Tools

## Objective
Implement the lookup tools that let the agent check customer, account, policy, and case evidence efficiently.

## Business outcome
The agent needs efficient lookups against customer, account, and policy data to gather facts before making recommendations.

## Implemented solution
### 1) Example implementation
```python
def lookup_customer(customer_id: str):
    customer = db.customers.get(customer_id)
    if not customer:
        return {"status": "not_found"}
    return {
        "customer_id": customer.customer_id,
        "segment": customer.segment,
        "account_ids": customer.account_ids,
    }
```

The tool returns only the fields needed to understand the complaint and decide on next action.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
