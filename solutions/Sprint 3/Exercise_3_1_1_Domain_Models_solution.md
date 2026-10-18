# Domain Models

## Objective
Design the complaint domain model so the service layer, API, and analytics teams all interpret the same business entities.

## Business outcome
The system needs a stable domain vocabulary so service logic, APIs, and analytics all speak the same language.

## Implemented solution
### 1) Entity model
```python
from dataclasses import dataclass, field
from datetime import datetime
from typing import Optional

@dataclass
class Customer:
    customer_id: str
    first_name: str
    last_name: str
    email: str
    segment: str

@dataclass
class Account:
    account_id: str
    customer_id: str
    product_type: str
    status: str

@dataclass
class Complaint:
    complaint_id: str
    customer_id: str
    account_id: Optional[str]
    complaint_type: str
    status: str
    priority: str
    created_at: datetime
    assigned_to: Optional[str] = None
```

### 2) Design decision
The complaint model keeps customer context and operational status in the same record so service and analytics logic can remain simple and auditable.

## Acceptance criteria
- The solution is specific, testable, and aligned to the complaint-resolution journey.
- The implementation is evidence-driven and built to be reviewed by both technical and business stakeholders.
- The output includes clear downstream handoff notes for the next stage of work.

## Handoff
This solution is the working artefact for the next sprint or technical phase and should be retained as the canonical implementation narrative for this exercise.
