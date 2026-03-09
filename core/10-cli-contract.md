# 10. CLI Contract

Required flags:

--input  
--output  
--rules  

Optional flags:

--max-evidence  
--verbose  
--format  

## Normative Requirements

- `[CLI-001]` CLI MUST exit with a non-zero status code when parser processing fails.
- `[CLI-002]` Warnings MUST NOT terminate execution.
- `[CLI-003]` CLI invocations MUST require `--input`, `--output`, and `--rules`.

---
