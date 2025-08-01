
## Runtime Path
```mermaid
sequenceDiagram
  autonumber
  actor U as User
  participant R as Router/Tools
  participant Q as Query Understanding
  participant P as Planner & Retrieval
  participant IDX as Indexes (Vector/Keyword)
  participant CB as Context Builder
  participant L as LLM
  participant G as Guardrails
  participant O as Observability
  participant F as Feedback/Evals

  U->>R: Request
  R->>Q: Detect intent & language
  Q->>P: Task + entities
  P->>P: ABAC pre-filter (deny-by-default)
  P->>IDX: Fan-out search (hybrid)
  IDX-->>P: Candidates (+scores)
  P->>CB: Top-k after re-rank
  CB->>L: Prompt + grounded context
  L-->>G: Draft answer
  G-->>R: Validate (PII/schema/safety)
  R-->>U: Response

  par Telemetry
    Note over O: Trace id, candidates (hashed), policy decisions,<br/>grounding%, latency/cost
    R-)O: Spans/metrics
    P-)O: Retrieval metrics
    L-)O: Generation metrics
  end

  U-->>F: Rating/clicks
  F-)IDX: Re-embed / Invalidate
  F-)R: Canary gate on regressions
