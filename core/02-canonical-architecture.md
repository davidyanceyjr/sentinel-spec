# 2. Canonical Architecture

The system pipeline consists of four stages:

Parser  
Classifier  
Finding Engine  
Output Generator

### Finding Engine internal stages

rule evaluation  
temporal correlation  
evidence aggregation  
finding generation

## Normative Requirements

- `[CORE-ARCH-001]` All implementations MUST execute top-level pipeline stages in this order: Parser, Classifier, Finding Engine, Output Generator.

---
