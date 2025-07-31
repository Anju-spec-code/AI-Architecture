# 🚀 Unified AI Architecture Diagram

```mermaid
flowchart TD
    U[End Users] --> GW[API Gateway]
    GW --> LB[Load Balancer]
    LB --> S1[LLM Service 1]
    LB --> S2[LLM Service 2]
    S1 --> DB[(Vector Store)]
    S2 --> OBS[Observability Layer]
    OBS --> AL[Alerts & Metrics Dashboard]
    
    %% RAG Workflow
    U --> Q[User Query]
    Q --> E[Embedding Generator]
    E --> VS[(Vector Database)]
    VS --> R[Retriever]
    R --> C[Context + Query]
    C --> LLM[LLM Model]
    LLM --> A[Answer with Sources]
    
    %% Edge Deployment
    DS[Data Source - Sensors, Cameras] --> PP[Pre-processing]
    PP --> TM[Trained AI Model]
    TM --> QM[Quantization & Optimization]
    QM --> ED[Edge Device Deployment]
    ED --> INF[Real-time Inference]
    INF --> CL[Cloud Feedback Loop]
    
    A --> CL
    ED --> OBS
