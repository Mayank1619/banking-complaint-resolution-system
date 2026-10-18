# Database Schema Solution

## Objective
Design a scalable schema for the complaint-resolution system that captures customer data, account activity, complaint records, and investigation evidence.

## Core tables
```sql
CREATE TABLE customers (
  customer_id BIGINT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  segment VARCHAR(50),
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE accounts (
  account_id BIGINT PRIMARY KEY,
  customer_id BIGINT NOT NULL REFERENCES customers(customer_id),
  account_type VARCHAR(20) NOT NULL,
  status VARCHAR(20) NOT NULL,
  balance DECIMAL(18,2) NOT NULL DEFAULT 0,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE complaints (
  complaint_id BIGINT PRIMARY KEY,
  customer_id BIGINT NOT NULL REFERENCES customers(customer_id),
  account_id BIGINT REFERENCES accounts(account_id),
  category VARCHAR(50) NOT NULL,
  severity VARCHAR(20) NOT NULL,
  status VARCHAR(30) NOT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE evidence (
  evidence_id BIGINT PRIMARY KEY,
  complaint_id BIGINT NOT NULL REFERENCES complaints(complaint_id),
  evidence_type VARCHAR(50) NOT NULL,
  source VARCHAR(255),
  content TEXT,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

## Design notes
- Keep customer and account records separate to support multi-account scenarios.
- Make complaint status and category queryable for dashboards and routing.
- Use foreign keys to enforce data integrity.
- Store evidence references rather than large blobs where possible.

## Acceptance criteria
- The schema supports customer, account, complaint, and evidence lifecycle tracking.
- Data can be queried for operational, reporting, and investigation needs.
- The model is extensible for policy and agent workflows.
