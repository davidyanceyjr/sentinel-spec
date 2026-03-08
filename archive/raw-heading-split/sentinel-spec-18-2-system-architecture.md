# 2. System Architecture

This section reconciles the architectural descriptions from the core spec and the pipeline spec.

## 2.1 Canonical V1 Processing Model

The canonical V1 architecture is:

```text
Input Stream
      │
      ▼
Stream Reader
      │
      ▼
Format Decoder (Parser)
      │
      ▼
Raw Record
      │
      ▼
Record Normalizer
      │
      ▼
Canonical Event
      │
      ▼
Event Classifier
      │
      ▼
Classified Event
      │
      ▼
Finding Engine
      │
      ▼
Findings
      │
      ▼
Output Renderer
```

For section-level shorthand elsewhere in this specification, the same architecture may be referred to as:

```text
Parser
Classifier
Finding Engine
Output Generator
```

## 2.2 Reconciliation Rule

The following stages from the core spec are treated as internal responsibilities of the Finding Engine and are not separate top-level pipeline stages in V1:

- Rule engine
- Evidence correlation
- Finding generation

The Finding Engine therefore performs:

- rule evaluation
- temporal correlation
- evidence aggregation
- finding generation

## 2.3 Stage Boundary Interpretation

The parser remains responsible only for decoding input and emitting parsed records.

Normalization remains responsible only for converting raw records into canonical events.

Classification remains responsible only for assigning stable event classes and bounded context.

The Finding Engine consumes classified events and emits immutable findings.

Output rendering remains responsible only for report and JSON generation and must not reinterpret rule logic.

## 2.4 Source Material Retained for Reference

The original pipeline specification text is retained below for reference.

