# 7. Rule Definition Model

## Normative Requirements

- `[CORE-RULE-001]` All rules MUST include these top-level fields: `rule_id`, `description`, `severity`, `confidence`, `trigger_conditions`, `context_fields`, and `evidence_fields`.
- `[CORE-RULE-002]` Top-level fields outside the required rule structure MUST NOT appear; optional extension data MAY appear only under a top-level `extensions` object.

```
rule_id
description
severity
confidence
trigger_conditions
context_fields
evidence_fields
extensions (optional)
```

### Confidence Enum

low  
medium  
high

Values outside this enum are invalid.

---
