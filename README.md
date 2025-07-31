# AI Observability Architecture

```mermaid
flowchart LR
    U[End Users] --> GW[API Gateway]
    GW --> L[Load Balancer]
    L --> S1[LLM Service 1]
    L --> S2[LLM Service 2]
    S1 --> DB[(Vector Store)]
    S2 --> OBS[Observability Layer]
    OBS --> AL[Alerts & Metrics Dashboard]

3. Scroll down → **Commit changes**.

✅ GitHub will now render this **architecture diagram directly in your repo**.

---

# **5️⃣ Add Images (Optional)**

If you create diagrams in Excalidraw or Draw.io:
1. Click **Add file → Upload files** in your repo.
2. Drag and drop `.png` or `.svg` images.
3. In README.md, link them:

```markdown
![AI Architecture](diagram.png)
