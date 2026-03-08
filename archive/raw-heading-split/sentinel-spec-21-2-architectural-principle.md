# 2. Architectural Principle

The analyzer is an **offline, deterministic, one-shot processing
pipeline**.

``` text
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

Each stage has a narrow contract and a single primary responsibility.

------------------------------------------------------------------------

