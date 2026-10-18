# SQL Metrics

## Objective
Translate the complaint dataset into operational KPIs that help track resolution quality, case volume, and service pressure.

## Business outcome
The bank does not only need to count complaints; it needs to know whether the complaint handling process is healthy and where operational pain points are emerging.

## Implemented solution

### 1) Complaint volume by month
```sql
SELECT
    DATE_TRUNC('month', submitted_at) AS month_start,
    COUNT(*) AS complaint_total
FROM complaints
GROUP BY DATE_TRUNC('month', submitted_at)
ORDER BY month_start;
```

### 2) Resolution rate by category
```sql
SELECT
    cc.category_name,
    COUNT(*) AS total_cases,
    COUNT(CASE WHEN c.complaint_status = 'resolved' THEN 1 END) AS resolved_cases,
    ROUND(
        100.0 * COUNT(CASE WHEN c.complaint_status = 'resolved' THEN 1 END) / NULLIF(COUNT(*), 0),
        2
    ) AS resolution_rate_pct
FROM complaints c
JOIN complaint_categories cc
    ON c.category_id = cc.category_id
GROUP BY cc.category_name
ORDER BY resolution_rate_pct ASC;
```

### 3) Complaints that breach target resolution time
```sql
SELECT
    category_name,
    COUNT(*) AS at_risk_cases
FROM (
    SELECT
        cc.category_name,
        c.complaint_id,
        c.resolution_due_at,
        c.resolved_at
    FROM complaints c
    JOIN complaint_categories cc
        ON c.category_id = cc.category_id
    WHERE c.resolved_at IS NOT NULL
      AND c.resolved_at > c.resolution_due_at
) x
GROUP BY category_name
ORDER BY at_risk_cases DESC;
```

## Managerial interpretation
- Monthly complaint volume highlights workload trend and seasonal risk.
- Resolution-rate KPIs show which issue types are hard to close on time.
- Breach measures expose where service recovery or process changes are required.

## Acceptance criteria
- Metrics are simple to explain to a business audience.
- The KPIs are tied to the decisions teams need to make.
- The queries can be reused as dashboard building blocks.

## Handoff
These KPIs become the analytical foundation for the later Python analysis and the operational story for the Week 2 release.
