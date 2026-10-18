# Repositories

## Objective
Set up a software structure that separates business logic, data access, API concerns, and analytics concerns so the team can continue building without creating tangled dependencies.

## Business outcome
A clean repository allows consultants and developers to work in parallel without breaking each other?s work or losing the audit trail for the project.

## Implemented solution
```text
banking-complaint-system/
??? app/
?   ??? api/
?   ?   ??? routes/
?   ?   ?   ??? complaints.py
?   ?   ?   ??? health.py
?   ?   ??? schemas/
?   ?       ??? complaint_schema.py
?   ?       ??? response_schema.py
?   ??? domain/
?   ?   ??? customer.py
?   ?   ??? account.py
?   ?   ??? complaint.py
?   ??? repositories/
?   ?   ??? complaint_repository.py
?   ?   ??? customer_repository.py
?   ?   ??? account_repository.py
?   ??? services/
?   ?   ??? complaint_service.py
?   ?   ??? triage_service.py
?   ?   ??? policy_service.py
?   ??? main.py
??? data/
?   ??? customers.csv
?   ??? accounts.csv
?   ??? complaints.csv
?   ??? service_requests.csv
??? tests/
?   ??? test_api.py
?   ??? test_services.py
?   ??? test_repository.py
??? notebooks/
?   ??? complaint_analysis.ipynb
??? README.md
??? requirements.txt
??? pyproject.toml
??? scripts/
    ??? seed_data.py
    ??? analyse_complaints.py
```

## Design responsibilities
- `app/api` handles transport and validation.
- `app/domain` owns complaint behaviour and business objects.
- `app/repositories` isolates persistence logic.
- `app/services` orchestrates workflow, triage, and exception handling.
- `data` contains source and synthetic datasets for analysis and testing.
- `tests` protects the operational behaviour required by the project.

## Acceptance criteria
- Each layer has a clear purpose and a single reason to change.
- A new developer can understand where to add logic without editing the wrong layer.
- The structure supports API work, SQL analysis, and later agent or retrieval work.

## Handoff
This repository design is the engineering baseline for the next sprint?s API, validation, and operational service work.
