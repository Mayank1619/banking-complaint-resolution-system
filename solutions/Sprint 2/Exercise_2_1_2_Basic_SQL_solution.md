# SQL and Data Query Solution

## Objective
Provide the business-facing SQL logic needed to validate complaint data, produce operational metrics, and support downstream investigation.

## Example queries
```sql
SELECT category, COUNT(*) AS complaints
FROM complaints
GROUP BY category
ORDER BY complaints DESC;
```

```sql
SELECT c.customer_id, c.complaint_id, a.account_id, a.balance
FROM complaints c
JOIN accounts a ON a.customer_id = c.customer_id
WHERE c.status = 'open';
```

```sql
SELECT
  DATE(created_at) AS day,
  COUNT(*) AS total_complaints,
  SUM(CASE WHEN severity = 'high' THEN 1 ELSE 0 END) AS high_severity
FROM complaints
GROUP BY DATE(created_at)
ORDER BY day;
```

## Business value
- Helps analysts spot complaint hotspots.
- Supports SLA and risk monitoring.
- Helps validate the health of the complaint pipeline.

## Acceptance criteria
- Queries return the correct population of complaints, customers, and evidence.
- Metrics are stable and explainable to business stakeholders.
- The SQL is readable and suitable for operational dashboards.
