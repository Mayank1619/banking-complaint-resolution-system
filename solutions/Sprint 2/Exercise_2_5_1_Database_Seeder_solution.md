# Database Seeder

## Objective
Generate realistic complaint data so the system can be tested with meaningful scenarios rather than empty or artificial records.

## Business outcome
An engineering team needs seeded complaint records that reflect realistic complaint channels, categories, customers, and service events so they can validate query logic and workflow quality.

## Implemented solution
```python
import random
from datetime import datetime, timedelta

customers = [
    {'customer_id': 1, 'first_name': 'Aisha', 'last_name': 'Patel'},
    {'customer_id': 2, 'first_name': 'Daniel', 'last_name': 'Moran'},
    {'customer_id': 3, 'first_name': 'Sofia', 'last_name': 'Nguyen'},
]

accounts = [
    {'account_id': 1001, 'customer_id': 1, 'account_type': 'Current Account', 'product_name': 'Everyday Plus'},
    {'account_id': 1002, 'customer_id': 2, 'account_type': 'Savings', 'product_name': 'Online Saver'},
    {'account_id': 1003, 'customer_id': 3, 'account_type': 'Credit Card', 'product_name': 'Travel Rewards'},
]

categories = ['fraud', 'payment_failed', 'unauthorised_transaction', 'service_delay', 'fees_and_charges']
channels = ['web', 'phone', 'branch', 'mobile_app']

records = []
for i in range(1, 51):
    customer = random.choice(customers)
    account = next(a for a in accounts if a['customer_id'] == customer['customer_id'])
    category = random.choice(categories)
    channel = random.choice(channels)
    submitted = datetime.utcnow() - timedelta(days=random.randint(1, 90))
    due = submitted + timedelta(days=random.randint(3, 20))
    records.append({
        'complaint_id': i,
        'customer_id': customer['customer_id'],
        'account_id': account['account_id'],
        'category': category,
        'complaint_channel': channel,
        'complaint_status': random.choice(['open', 'in_review', 'resolved']),
        'submitted_at': submitted.isoformat(),
        'resolution_due_at': due.isoformat(),
    })

print(records[:3])
```

## What this produces
The seeder creates a realistic volume of complaint data that reflects:
- multiple customer journeys,
- different complaint categories,
- different channels,
- varying resolution urgency and status.

## Acceptance criteria
- Seed data reflects realistic complaint patterns and operational variability.
- The output is easy to query and explain.
- The dataset supports testing SQL, Python analysis, and downstream triage logic.

## Handoff
This seeded data is the working evidence set used in the week 2 release and later retrieval and scoring exercises.
