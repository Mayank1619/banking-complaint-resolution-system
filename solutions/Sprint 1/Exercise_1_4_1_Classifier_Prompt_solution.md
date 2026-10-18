# Classifier Prompt Solution

## Objective
Implement a reliable complaint classification prompt that routes issues consistently and uses a structured output that downstream systems can trust.

## Example solution
Use a prompt that asks the model to classify the complaint into one of a fixed taxonomy such as:
- payment failure
- account access issue
- billing dispute
- service disruption
- fraud or suspicious activity
- policy interpretation

## Prompt pattern
You are a complaint triage assistant for a retail bank. Read the complaint text and classify it into one of the allowed categories. Return JSON only with these fields:
- complaint_type
- urgency
- confidence
- summary
- required_evidence
- recommended_next_step

## Business rules
- If the complaint is about money movement, check for account-level and transaction-level context.
- If there is risk or policy ambiguity, mark urgency as high and escalate for manual review.
- Do not make a final resolution decision without policy and evidence checks.

## Example output
```json
{
  "complaint_type": "billing dispute",
  "urgency": "medium",
  "confidence": 0.91,
  "summary": "Customer disputes a fee applied to an account after a failed transfer attempt.",
  "required_evidence": ["account history", "fee schedule", "transaction timeline"],
  "recommended_next_step": "review billing policy and account transaction ledger"
}
```

## Acceptance criteria
- The classifier returns valid structured JSON.
- Categories are limited to the approved taxonomy.
- High-risk cases are escalated appropriately.
- Output supports downstream review and operational routing.
