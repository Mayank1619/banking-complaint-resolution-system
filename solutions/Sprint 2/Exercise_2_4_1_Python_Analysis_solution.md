# Python Analysis

## Objective
Use Python to validate, summarise, and explain the complaint dataset in a repeatable way so the team can draw evidence-based conclusions from the raw records.

## Business outcome
The complaint-management team needs an analysis script that can be rerun whenever the data changes, while keeping the logic transparent and reviewable by both business and technical stakeholders.

## Implemented solution
```python
import pandas as pd
from pathlib import Path

base = Path('data')
customers = pd.read_csv(base / 'customers.csv')
accounts = pd.read_csv(base / 'accounts.csv')
complaints = pd.read_csv(base / 'complaints.csv')
service_requests = pd.read_csv(base / 'service_requests.csv')

# Join the complaint facts to customer and account context
joined = complaints.merge(customers, on='customer_id', how='left')                    .merge(accounts, on='account_id', how='left')

# Basic volume summaries
summary = {
    'total_complaints': int(joined['complaint_id'].nunique()),
    'open_cases': int((joined['complaint_status'] == 'open').sum()),
    'resolved_cases': int((joined['complaint_status'] == 'resolved').sum()),
    'top_categories': joined['category'].value_counts().head(5).to_dict(),
    'top_channels': joined['complaint_channel'].value_counts().head(5).to_dict(),
}

print('Complaint summary:')
for k, v in summary.items():
    print(f' - {k}: {v}')

# Flag overdue complaints
joined['submitted_at'] = pd.to_datetime(joined['submitted_at'])
joined['resolution_due_at'] = pd.to_datetime(joined['resolution_due_at'])
joined['resolved_at'] = pd.to_datetime(joined['resolved_at'])
joined['overdue'] = joined['complaint_status'].ne('resolved') & (joined['resolution_due_at'] < pd.Timestamp.utcnow())
print('Overdue complaints:', int(joined['overdue'].sum()))
```

## Why this is a valid solution
This script does three practical things:
- loads the complaint data with clear source boundaries,
- joins the complaint to customer and account context,
- summarises the trends that matter to operational teams without hiding the raw data.

## Output the team should expect
A realistic analysis output would include:
- total complaint volume,
- number of open and resolved complaints,
- dominant complaint reason and channel,
- any complaints breaching service-level expectations.

## Acceptance criteria
- The script can run against the source data without manual editing.
- The summary metrics match the business questions being asked.
- The analysis is easy to review and explain to a non-technical reviewer.

## Handoff
This Python analysis is the bridge between raw data and the service-layer decisions that follow in the sprint.
