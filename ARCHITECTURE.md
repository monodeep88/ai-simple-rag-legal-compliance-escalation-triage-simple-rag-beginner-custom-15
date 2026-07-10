# Architecture

  ## Architecture Overview

  **Legal Compliance Escalation Triage RAG Assistant** uses a React frontend, FastAPI backend, SQL persistence, retrieval-aware pipeline, and optional LLM provider. The architecture is intentionally small enough for students to run locally but structured enough to explain in interviews.

  - Selected architecture: Compliance Knowledge Portal
  - Template path: templates/simple-rag/compliance-knowledge-portal
  - Blueprint note: For a beginner project, we'll prioritize simplicity and local execution where possible. We'll use open-source embedding models (e.g., `sentence-transformers`) and an in-memory or file-based vector database (e.g., `ChromaDB` or `FAISS` running locally) to reduce setup complexity. The LLM can be accessed via a free tier/developer key (e.g., OpenAI, Google Gemini) or a local small LLM (e.g., a quantized Llama-2 variant) if computational resources allow. Docker will containerize the backend and frontend for easy deployment. The focus is on understanding the core RAG pipeline, not on production-scale infrastructure.

  ## System Architecture Diagram

  ```mermaid
  flowchart LR
USER[User] --> UI[React Frontend]
UI --> API[FastAPI API]
API --> PIPE[Simple RAG Pipeline]
PIPE --> VECTOR[(Vector store)]
VECTOR --> PIPE
PIPE --> SERVICE[Service workflow]
SERVICE --> REVIEW[Validation and synthesis]
PIPE --> DB[(Run Log Database)]
REVIEW --> OUT[Legal Compliance Escalation Triage RAG Assistant Answer]
OUT --> UI
  ```

  ## Component Responsibilities

  - Frontend layer: captures questions, shows answers, sources, and timeline.
  - Backend layer: validates requests, exposes API routes, handles errors.
  - AI/LLM layer: optional provider call with local deterministic fallback.
  - RAG/vector layer: retrieves relevant chunks when the project type needs retrieval.
  - Database layer: stores run logs and explainability evidence.
  - Background worker layer: recommended production upgrade for long tasks.
  - External services: optional OpenAI/Pinecone or deployment provider.

  ## Implementation Map

  - `backend/app/main.py`: FastAPI app, API routes, and request contract.
  - `backend/app/services/pipeline.py`: project workflow, retrieval, timeline, fallback handling, and answer synthesis.
  - `backend/app/domain.py`: domain profile, workflow steps, rules, starter questions, and tool catalog.
  - `backend/app/models.py`: SQL run-log model used for portfolio and debugging evidence.
  - `frontend/src/App.jsx`: learner-facing workspace and generated project UI.
  - `docs/PROJECT_DESIGN.md`: full problem statement, DFDs, database schema, APIs, and interview explanation.

  ## Component Diagram

  ```mermaid
  flowchart TB
UI[React App] --> CLIENT[API Client]
CLIENT --> ROUTE[FastAPI Routes]
ROUTE --> PIPELINE[Pipeline Service]
PIPELINE --> SEARCH[Vector/Search Service]
PIPELINE --> LLM[LLM/Fallback Service]
PIPELINE --> TOOLS[Tools and Domain Rules]
PIPELINE --> STORE[(SQL Run Logs)]
  ```

  ## Request Lifecycle

  ```mermaid
  sequenceDiagram
participant U as User
participant UI as React UI
participant API as FastAPI
participant P as Pipeline
participant S as Search
participant DB as Database
U->>UI: Submit question
UI->>API: POST /api/ask
API->>P: Validate and run workflow
P->>S: Retrieve context
S-->>P: Relevant chunks
P->>DB: Store run log
P-->>API: Answer, sources, timeline
API-->>UI: JSON response
UI-->>U: Render result
  ```

  ## Error Flow

  Provider or retrieval failures should return a friendly fallback response, preserve request context, and store a timeline step explaining the fallback mode without exposing secrets.

  ## Observability

  Track request latency, retrieval count, fallback mode, validation errors, and provider availability.

  ## Deployment Topology

  React can be served from Vercel/Nginx, FastAPI from Render/Railway/Docker, PostgreSQL as managed storage, and Chroma/Pinecone as a separate vector service for production datasets.
