# Fact Extraction Solution

## Objective
Extract the most important complaint details into structured fields that can power triage, investigation, and final resolution workflows.

## Example extracted fields
- customer_id
- product_type
- issue_category
- transaction_reference
- amount
- date_of_incident
- channel_used
- account_status
- supporting_documents
- customer_impact

## Example output
```json
{
  "customer_id": "CUST-10492",
  "product_type": "current_account",
  "issue_category": "payment_failed",
  "amount": 425.00,
  "date_of_incident": "2026-10-04",
  "channel_used": "mobile_app",
  "customer_impact": "unable to complete debit card payment",
  "supporting_documents": ["transaction screenshot", "statement excerpt"]
}
```

## Implementation guidance
- Normalise dates, amounts, and account references before saving.
- Prefer structured confidence values for uncertain fields.
- Flag any missing critical fields for human review.
- Keep an evidence trail for all extracted attributes.

## Acceptance criteria
- Required facts are extracted consistently.
- Output is compatible with downstream routing and risk review.
- Uncertain or incomplete extraction is flagged instead of guessed.
