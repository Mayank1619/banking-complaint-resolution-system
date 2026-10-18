# Database Schema

## Objective
Design a schema that can hold customer, account, complaint, evidence, and servicing data without losing traceability between a complaint and the operational actions that follow it.

## Business outcome
The bank needs an auditable complaint record that ties customer context, account activity, complaint events, and resolution decisions together in a way that supports analysis, investigations, and downstream RAG workflows.

## Implemented solution
The schema below is structured to support real operational and analytical use without over-normalising the data model.

```sql
CREATE TABLE customers (
    customer_id BIGINT PRIMARY KEY,
    first_name VARCHAR(80),
    last_name VARCHAR(80),
    date_of_birth DATE,
    email VARCHAR(255),
    phone VARCHAR(30),
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE accounts (
    account_id BIGINT PRIMARY KEY,
    customer_id BIGINT NOT NULL REFERENCES customers(customer_id),
    account_type VARCHAR(40) NOT NULL,
    product_name VARCHAR(100) NOT NULL,
    opened_at TIMESTAMP NOT NULL,
    status VARCHAR(30) NOT NULL,
    balance NUMERIC(12,2) DEFAULT 0
);

CREATE TABLE complaint_categories (
    category_id SMALLINT PRIMARY KEY,
    category_name VARCHAR(80) NOT NULL UNIQUE,
    severity_level VARCHAR(20) NOT NULL,
    policy_reference VARCHAR(200)
);

CREATE TABLE complaints (
    complaint_id BIGINT PRIMARY KEY,
    customer_id BIGINT NOT NULL REFERENCES customers(customer_id),
    account_id BIGINT REFERENCES accounts(account_id),
    category_id SMALLINT REFERENCES complaint_categories(category_id),
    complaint_channel VARCHAR(40) NOT NULL,
    complaint_source VARCHAR(80) NOT NULL,
    complaint_status VARCHAR(40) NOT NULL,
    complaint_summary TEXT NOT NULL,
    submitted_at TIMESTAMP NOT NULL,
    first_seen_at TIMESTAMP,
    resolution_due_at TIMESTAMP,
    resolved_at TIMESTAMP,
    root_cause VARCHAR(200),
    case_owner VARCHAR(120)
);

CREATE TABLE complaint_events (
    event_id BIGINT PRIMARY KEY,
    complaint_id BIGINT NOT NULL REFERENCES complaints(complaint_id),
    event_type VARCHAR(50) NOT NULL,
    event_timestamp TIMESTAMP NOT NULL,
    event_details JSONB,
    created_by VARCHAR(120)
);

CREATE TABLE complaint_evidence (
    evidence_id BIGINT PRIMARY KEY,
    complaint_id BIGINT NOT NULL REFERENCES complaints(complaint_id),
    evidence_type VARCHAR(50) NOT NULL,
    source_system VARCHAR(80),
    source_reference VARCHAR(200),
    captured_at TIMESTAMP NOT NULL,
    evidence_payload JSONB
);

CREATE TABLE service_requests (
    service_request_id BIGINT PRIMARY KEY,
    complaint_id BIGINT NOT NULL REFERENCES complaints(complaint_id),
    request_type VARCHAR(80) NOT NULL,
    request_status VARCHAR(30) NOT NULL,
    created_at TIMESTAMP NOT NULL,
    assigned_team VARCHAR(80),
    resolved_at TIMESTAMP
);

CREATE TABLE resolution_actions (
    resolution_action_id BIGINT PRIMARY KEY,
    complaint_id BIGINT NOT NULL REFERENCES complaints(complaint_id),
    action_type VARCHAR(80) NOT NULL,
    action_taken_by VARCHAR(120),
    action_timestamp TIMESTAMP NOT NULL,
    action_summary TEXT,
    customer_impact TEXT
);
```

## Why this design works
- `customers` and `accounts` keep the factual customer and product context separate from the complaint narrative.
- `complaints` is the core operational object and stores the complaint lifecycle across intake, review, and closure.
- `complaint_events` preserves the chronology so an investigation can explain what happened and when.
- `complaint_evidence` keeps attachments and extracted facts in a queryable structure for downstream policy checking and retrieval.
- `service_requests` and `resolution_actions` support operational follow-up and explainability.

## Acceptance criteria
- Every complaint is traceable to a customer and, if relevant, an account.
- Complaint status changes are retained as events rather than overwritten.
- Evidence and service actions are stored independently to support analysis and audits.
- The design can support both operational reporting and AI grounding queries.

## Handoff
This schema becomes the source of truth for the SQL exercises, Python analysis, and the downstream complaint service layer.
