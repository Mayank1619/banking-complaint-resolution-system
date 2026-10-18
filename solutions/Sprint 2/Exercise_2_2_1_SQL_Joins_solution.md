# SQL Joins

## Objective
Join complaint, account, customer, and service data so that analysts can understand not just the complaint itself, but the customer and product context behind it.

## Business outcome
A complaint should not be treated as an isolated case. To investigate professionally, the analyst needs to answer: which customer, which products, which service request, and which operational team are involved?

## Implemented solution
```sql
SELECT
    c.complaint_id,
    concat(cs.first_name, ' ', cs.last_name) AS customer_name,
    a.account_type,
    a.product_name,
    cc.category_name,
    c.complaint_status,
    c.submitted_at,
    sr.request_type,
    sr.request_status,
    sr.assigned_team
FROM complaints c
JOIN customers cs
    ON c.customer_id = cs.customer_id
LEFT JOIN accounts a
    ON c.account_id = a.account_id
JOIN complaint_categories cc
    ON c.category_id = cc.category_id
LEFT JOIN service_requests sr
    ON c.complaint_id = sr.complaint_id
ORDER BY c.submitted_at DESC;
```

## Why this matters
This query creates a single investigation view that allows a complaint analyst to:
- see the customer and product involved,
- see the category and severity,
- identify the active service request and team ownership,
- understand the complaint context before making a response or escalation decision.

## Additional operational view
```sql
SELECT
    sr.assigned_team,
    COUNT(DISTINCT c.complaint_id) AS active_case_count,
    COUNT(DISTINCT CASE WHEN c.complaint_status = 'open' THEN c.complaint_id END) AS open_cases
FROM complaints c
LEFT JOIN service_requests sr
    ON c.complaint_id = sr.complaint_id
GROUP BY sr.assigned_team
ORDER BY active_case_count DESC;
```

## Acceptance criteria
- The output joins the complaint to the relevant customer and account context.
- Operational ownership is visible when service requests exist.
- Analysts can identify the next action without needing to inspect multiple raw datasets.

## Handoff
This investigation view becomes the basis for deeper metrics and the downstream reporting/triage logic used in the case system.
