<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Context Engineering Architecture</title>
  <style>
    body { margin: 0; font-family: system-ui, -apple-system, Segoe UI, Roboto, sans-serif; background:#fff; }
    .wrap { max-width: 1200px; margin: 24px auto; padding: 0 16px; }
    h1 { font-size: 20px; margin: 0 0 12px; }
    svg { width: 100%; height: auto; border: 1px solid #eee; border-radius: 12px; }
    .box { transition: fill 120ms ease, stroke 120ms ease; }
    .box:hover { fill: #eef6ff; stroke: #1f4d8f; }
    .arrow { stroke: #333; stroke-width: 2; marker-end: url(#arrowhead); transition: stroke-width 120ms ease; }
    .arrow:hover { stroke-width: 4; }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>Context Engineering Architecture</h1>

    <!-- Inline SVG (safe for GitHub Pages and local viewing) -->
    <svg width="1200" height="800" xmlns="http://www.w3.org/2000/svg">

      <!-- Styles inside SVG for portability -->
      <style>
        .box { fill: #f8f9fa; stroke: #333; stroke-width: 1.5; rx: 10; ry: 10; }
        .title { font: bold 16px sans-serif; fill: #222; }
        .text  { font: 14px sans-serif; fill: #333; }
      </style>

      <!-- Arrow Marker Definition -->
      <defs>
        <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="10" refY="3.5" orient="auto">
          <polygon points="0 0, 10 3.5, 0 7" fill="#333"/>
        </marker>
      </defs>

      <!-- LAYER 1: DATA SOURCES -->
      <rect x="30" y="40" width="250" height="160" class="box"/>
      <text x="50" y="70" class="title">Data &amp; Context Sources</text>
      <text x="50" y="100" class="text">CRM, Orders, KB, Policies</text>
      <text x="50" y="120" class="text">Chat Logs, Product Catalog</text>

      <!-- LAYER 2: INGESTION -->
      <rect x="320" y="40" width="250" height="160" class="box"/>
      <text x="340" y="70" class="title">Ingestion &amp; Processing</text>
      <text x="340" y="100" class="text">Connectors, ETL, Chunking</text>
      <text x="340" y="120" class="text">Metadata Enrichment</text>

      <!-- LAYER 3: STORAGE -->
      <rect x="610" y="40" width="250" height="160" class="box"/>
      <text x="630" y="70" class="title">Storage &amp; Indexing</text>
      <text x="630" y="100" class="text">Vector DB, Hybrid Search</text>
      <text x="630" y="120" class="text">Structured DB</text>

      <!-- LAYER 4: CONTEXT ENGINEERING -->
      <rect x="900" y="40" width="270" height="200" class="box"/>
      <text x="920" y="70" class="title">Context Engineering</text>
      <text x="920" y="100" class="text">Query Understanding</text>
      <text x="920" y="120" class="text">Multi-source Retrieval</text>
      <text x="920" y="140" class="text">Ranking, Filtering</text>
      <text x="920" y="160" class="text">Context Envelope</text>

      <!-- LAYER 5: LLM ORCHESTRATION -->
      <rect x="320" y="260" width="400" height="160" class="box"/>
      <text x="340" y="290" class="title">LLM Orchestration Layer</text>
      <text x="340" y="320" class="text">RAG Pipeline, Guardrails</text>
      <text x="340" y="340" class="text">Agentic Workflow</text>

      <!-- LAYER 6: FEEDBACK -->
      <rect x="760" y="260" width="280" height="160" class="box"/>
      <text x="780" y="290" class="title">Feedback &amp; Learning</text>
      <text x="780" y="320" class="text">User Ratings</text>
      <text x="780" y="340" class="text">Context Quality Scoring</text>

      <!-- LAYER 7: OBSERVABILITY -->
      <rect x="30" y="260" width="260" height="160" class="box"/>
      <text x="50" y="290" class="title">Observability &amp; Trust</text>
      <text x="50" y="320" class="text">Tracing, Explainability</text>
      <text x="50" y="340" class="text">Security, RBAC</text>

      <!-- Arrows -->
      <line x1="280" y1="120" x2="320" y2="120" class="arrow"><title>Sources → Ingestion</title></line>
      <line x1="570" y1="120" x2="610" y2="120" class="arrow"><title>Ingestion → Storage</title></line>
      <line x1="860" y1="120" x2="900" y2="120" class="arrow"><title>Storage → Context Engineering</title></line>
      <line x1="1030" y1="240" x2="900" y2="260" class="arrow"><title>Context → Orchestration</title></line>
      <line x1="690" y1="200" x2="690" y2="260" class="arrow"><title>Storage → Orchestration</title></line>
      <line x1="280" y1="340" x2="320" y2="340" class="arrow"><title>Observability → Orchestration</title></line>
      <line x1="720" y1="340" x2="760" y2="340" class="arrow"><title>Orchestration → Feedback</title></line>
    </svg>
  </div>
</body>
</html>
