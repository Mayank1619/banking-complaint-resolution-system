# Retrieval Decision

## Objective
Decide when to use structured SQL, policy retrieval, or synthetic reasoning so the complaint workflow is based on evidence rather than guesswork.

## Business outcome
A complaint support assistant should answer questions with the right source of truth: fact tables for operational metrics, retrieval for policy and procedure, and human review where the answer affects customer remediation.

## Implemented solution
The appropriate pattern depends on the question type:

### Use SQL when the answer is factual and auditable
- Count of complaints in the last 30 days
- Open unresolved cases by category
- default response timing by customer segment

```sql
SELECT
    complaint_channel,
    COUNT(*) AS complaint_count
FROM complaints
WHERE submitted_at >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY complaint_channel
ORDER BY complaint_count DESC;
```

### Use retrieval when the answer depends on policy or procedural guidance
Examples:
- what policy applies to unauthorised card activity,
- where to escalate a repeated complaint,
- which evidence should be reviewed before a closure decision is made.

### Use a hybrid pattern for production-grade support
1. query the complaint and account facts
2. retrieve the relevant policy or procedure
3. assemble the answer with source citations
4. route risky or high-impact cases to human approval

## Decision framework
- if the data exists in the database, query it directly,
- if the answer requires explanatory guidance, retrieve the policy or document,
- if the response affects financial remediation or legal obligations, require human verification before closure.

## Acceptance criteria
- The system chooses the evidence source that matches the question.
- Unsupported answers are rejected or clearly labelled as low confidence.
- Human review remains available for sensitive decisions.

## Handoff
This retrieval decision model becomes the backbone for the later grounded-answer and agent workflows.
