# 🚀 Unified AI Architecture Diagram (Enterprise-Grade)

This diagram represents a production-ready, enterprise-scale AI architecture with governance, observability, retraining, and compliance layers—ideal for real-world deployments in regulated environments.

```mermaid
flowchart TD
    %% ========================
    %% USER ENTRY POINTS
    %% ========================
    A[End Users] -->|Sends Request| B[User Query]
    A --> C[API Gateway]

    %% ========================
    %% DATA INGESTION AND QUERY FLOW
    %% ========================
    B --> D[Embedding Generator]
    D --> E[(Vector Database)]
    E --> F[Retriever]
    F --> G[Context + Query]
    G --> H[LLM Model]
    H --> I[Answer with Sources]

    %% ========================
    %% DATA SOURCE AND MODEL TRAINING
    %% ========================
    J[Data Source - Sensors, Cameras] --> K[Pre-processing]
    K --> L[Data Validation & Lineage]
    L --> M[Trained AI Model]
    M --> N[Quantization & Optimization]
    N --> O[Edge Device Deployment]
    O --> P[Real-time Inference]

    %% ========================
    %% API GATEWAY TO MODEL SERVICES
    %% ========================
    C --> Q[Load Balancer]
    Q --> R[LLM Service 1]
    Q --> S[LLM Service 2]
    R --> T[(Vector Store)]
    S --> U[Observability Layer]
    U --> V[Alerts & Metrics Dashboard]

    %% ========================
    %% SECURITY AND GOVERNANCE LAYER
    %% ========================
    subgraph SEC[Governance, Security & Compliance Layer]
    L
    M
    N
    H
    end

    %% ========================
    %% FEEDBACK LOOP AND RETRAINING
    %% ========================
    I --> W[Cloud Feedback Loop]
    P --> W
    W --> X[Model Registry]
    X --> Y[Auto-Retraining Pipeline]
    Y --> M

    %% ========================
    %% EXPLAINABILITY AND HUMAN REVIEW
    %% ========================
    I --> Z[Explainability & Human Approval Gateway]
    Z --> A
