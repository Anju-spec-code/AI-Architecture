<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Context Engineering Architecture</title>
<style>
  :root{--border:#e5e7eb;--text:#0f172a}
  body{margin:0;font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,sans-serif;color:var(--text)}
  .wrap{max-width:1200px;margin:24px auto;padding:0 16px}
  h1,h2{margin:0 0 12px}
  .card{border:1px solid var(--border);border-radius:12px;padding:12px;margin:16px 0;overflow:auto;background:#fff}
  .note{font-size:12px;color:#475569;margin-top:6px}
</style>
</head>
<body>
<div class="wrap">
  <h1>Context Engineering Architecture</h1>
  <div class="note">Legend: <b>Solid</b> arrows = primary flow · <b>Dashed</b> arrows = feedback/policy paths</div>

  <h2>System Map</h2>
  <div class="card">
<pre class="mermaid">
flowchart LR
  %% Styles
  classDef lane fill:#ffffff,stroke:#94a3b8,rx:8,ry:8;
  classDef box  fill:#f8fafc,stroke:#334155,rx:6,ry:6;
  classDef accent fill:#eef6ff,stroke:#1f4d8f,rx:6,ry:6;

  subgraph S[Sources]:::lane
    S1[Enterprise Data]:::box
    S2[SaaS & Docs]:::box
    S3[Logs & Streams]:::box
    S4[Domain Assets]:::box
    S5[Identity & Entitlements]:::accent
  end

  subgraph I[Ingestion & Governance]:::lane
    I1[Connectors & CDC]:::box
    I2[Pre-Proc & Chunking<br/>Embedding Registry & Versioning]:::box
    I3[Governance<br/>Contracts • PII • RBAC/ABAC • Retention/Legal Hold]:::box
    I4[Quality & Lineage]:::box
    I5[Policy-as-Code (OPA/Cedar)]:::accent
  end

  subgraph X[Storage & Indexing]:::lane
    X1[Storage<br/>Lakehouse/Object • Shared DocID]:::box
    X2[Vector & Graph]:::box
    X3[Search Indexes<br/>BM25 • Hybrid]:::box
    X4[Semantic Cache<br/>Scoped keys: tenant/role/region/policy]:::box
    X5[Index Freshness Jobs<br/>Re-embed queue • &lt;15m SLO]:::box
  end

  subgraph C[Context Engineering]:::lane
    C1[Query Understanding]:::box
    C2[Planner & Retrieval<br/>ABAC pre-filter • Deny-by-default • Re-rank]:::accent
    C3[Context Builder<br/>Dedup • Packs • Citations]:::box
    C4[Freshness & Drift]:::box
    C5[Session Memory (TTL)]:::box
  end

  subgraph O[Orchestration & Trust]:::lane
    O1[LLM Router & Tools<br/>Region routing • Tool limits • Secrets • Prompt/Output cache]:::accent
    O2[Guardrails & Policy<br/>Safety • Firewall • JSON validators • Safe fallback]:::accent
    O3[Observability<br/>Tracing • Evidence • Budgets/SLOs]:::box
    O4[Feedback & Learning<br/>Golden set • Offline eval • Canary gate]:::box
    O5[Delivery<br/>APIs • Auth/Quotas]:::box
  end

  %% Primary ingest
  S1 --> I1
  S2 --> I1
  S3 --> I1
  S4 --> I1
  I1 --> I2
  I2 --> X1
  I2 --> X2
  I2 --> X3
  I2 --> X4
  I3 -.-> I5
  I4 -.-> I5
  S5 --> I5

  %% Retrieval
  X1 --> C1
  X2 --> C2
  X3 --> C2
  X4 --> C4
  S5 -.-> C2
  I5 -.-> C2
  C1 --> C2 --> C3 --> O1
  C4 -.-> X5
  C5 --> O1

  %% Orchestration & feedback
  O1 --> O2 --> O5
  O3 -.-> I5
  O4 -.-> X5
  O4 -.-> C3
</pre>
  </div>

  <h2>Runtime Path</h2>
  <div class="card">
<pre class="mermaid">
%%{init: {
  "theme": "neutral",
  "sequence": {
    "useMaxWidth": true,
    "mirrorActors": false,
    "rightAngles": true,
    "actorMargin": 20,
    "messageMargin": 12,
    "noteMargin": 10,
    "bottomMarginAdj": 6,
    "showSequenceNumbers": true
  }
}}%%
sequenceDiagram
  autonumber
  actor U as User
  participant R as Router/Tools
  participant Q as Query Understanding
  participant P as Planner & Retrieval
  participant IDX as Indexes<br/>(Vector/Keyword)
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
  G-->>R: Validate (PII / schema / safety)
  R-->>U: Response

  Note over O: Trace id, candidates (hashed), policy decisions,<br/>grounding%, latency/cost
  R-->>O: Spans / metrics
  P-->>O: Retrieval metrics
  L-->>O: Generation metrics

  U-->>F: Rating / clicks
  F-->>IDX: Re-embed / Invalidate
  F-->>R: Canary gate on regressions
</pre>
  </div>

  <div class="note">Tip: this page renders on GitHub Pages and in README previews (Mermaid enabled).</div>
</div>

<!-- Mermaid (CDN) -->
<script type="module">
  import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs";
  mermaid.initialize({ startOnLoad: true, theme: "neutral" });
</script>
</body>
</html>
