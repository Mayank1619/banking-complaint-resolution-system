# Advanced SQL

## Objective
Use window functions and time-based calculations to understand the complaint lifecycle, identify trend shifts, and make the data useful for operational decision-making.

## Business outcome
A complaint team needs to see not just totals, but changes over time, overdue patterns, and risk shifted by category or channel.

## Implemented solution

### 1) Running complaint count by month
```sql
WITH monthly_counts AS (
    SELECT
        DATE_TRUNC('month', submitted_at) AS month_start,
        COUNT(*) AS monthly_total
    FROM complaints
    GROUP BY DATE_TRUNC('month', submitted_at)
)
SELECT
    month_start,
    monthly_total,
    SUM(monthly_total) OVER (ORDER BY month_start) AS running_total
FROM monthly_counts
ORDER BY month_start;
```

### 2) Compare current month with previous month by category
```sql
WITH monthly_category_counts AS (
    SELECT
        cc.category_name,
        DATE_TRUNC('month', c.submitted_at) AS month_start,
        COUNT(*) AS complaint_count
    FROM complaints c
    JOIN complaint_categories cc
        ON c.category_id = cc.category_id
    GROUP BY cc.category_name, DATE_TRUNC('month', c.submitted_at)
)
SELECT
    category_name,
    month_start,
    complaint_count,
    LAG(complaint_count) OVER (PARTITION BY category_name ORDER BY month_start) AS prior_month_count,
    complaint_count - LAG(complaint_count) OVER (PARTITION BY category_name ORDER BY month_start) AS month_over_month_delta
FROM monthly_category_counts
ORDER BY category_name, month_start;
```

### 3) Rank categories by complaint volume in each month
```sql
WITH monthly_category_counts AS (
    SELECT
        DATE_TRUNC('month', c.submitted_at) AS month_start,
        cc.category_name,
        COUNT(*) AS complaint_count
    FROM complaints c
    JOIN complaint_categories cc
        ON c.category_id = cc.category_id
    GROUP BY DATE_TRUNC('month', c.submitted_at), cc.category_name
)
SELECT
    month_start,
    category_name,
    complaint_count,
    RANK() OVER (PARTITION BY month_start ORDER BY complaint_count DESC) AS volume_rank
FROM monthly_category_counts
ORDER BY month_start, volume_rank;
```

## Interpretation
These queries help the team distinguish sustained risk from one-off spikes and separate category trends from short-term operational noise.

## Acceptance criteria
- Time-based patterns are visible and explainable.
- The results can be used for dashboarding and management reviews.
- The logic demonstrates a clear understanding of SQL window functions and trend analysis.

## Handoff
This is the advanced analytical layer that informs the Python analysis and the final release narrative.
