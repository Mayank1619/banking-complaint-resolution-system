# Basic SQL

## Objective
Use SQL to answer the most important business questions from the complaint dataset: what is the volume, what is the pattern, and where is the risk or friction?

## Business outcome
The bank needs a repeatable way to understand complaint volume, severity, and operational pressure before building automated triage or deeper analytics.

## Implemented solution

### 1) Count complaints by channel and category
```sql
SELECT
    c.complaint_channel,
    cc.category_name,
    COUNT(*) AS complaint_count
FROM complaints c
JOIN complaint_categories cc
    ON c.category_id = cc.category_id
GROUP BY c.complaint_channel, cc.category_name
ORDER BY complaint_count DESC;
```

### 2) Count complaints still unresolved after SLA
```sql
SELECT
    COUNT(*) AS overdue_complaints
FROM complaints
WHERE complaint_status NOT IN ('resolved', 'closed')
  AND resolution_due_at < CURRENT_DATE;
```

### 3) Identify the most common complaint themes by customer segment
```sql
SELECT
    CASE
        WHEN a.account_type = 'Current Account' THEN 'Retail'
        WHEN a.account_type = 'Business' THEN 'SME'
        ELSE 'Other'
    END AS customer_segment,
    cc.category_name,
    COUNT(*) AS complaint_count
FROM complaints c
JOIN accounts a
    ON c.account_id = a.account_id
JOIN complaint_categories cc
    ON c.category_id = cc.category_id
GROUP BY 1, 2
ORDER BY 1, complaint_count DESC;
```

## Interpretation
- This provides a daily operational view of complaint mix and load.
- The overdue complaint query highlights where the bank is breaching internal service levels.
- Segmenting by account type helps identify which customer groups are experiencing recurring issues.

## Acceptance criteria
- Queries return concrete values for the business questions they are meant to answer.
- Results are grouped by useful operational dimensions such as channel, category, and customer segment.
- The SQL is simple enough to review and explain to non-technical stakeholders.

## Handoff
This SQL output becomes the baseline metric layer for the later SQL join and metrics exercises.
