flowchart LR
  %% Layout
  %% Solid arrows = primary flow; dashed arrows = feedback/policy
  %% GitHub supports Mermaid out of the box.

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
    I3[Governance<br/>Contracts • PII • RBAC/ABAC]:::box
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
    O1[LLM Router & Tools<br/>Region routing • Tool limits • Secrets]:::accent
    O2[Guardrails & Policy<br/>Safety • Firewall • JSON validators]:::accent
    O3[Observability<br/>Tracing • Evidence • SLOs]:::box
    O4[Feedback & Learning<br/>Golden set • Offline eval • Canary]:::box
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
