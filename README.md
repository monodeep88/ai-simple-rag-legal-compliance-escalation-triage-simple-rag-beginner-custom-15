# Legal Compliance Escalation Triage RAG Assistant

## Project Overview

Legal Compliance Escalation Triage RAG Assistant is a complete full-stack AI project for **Simple RAG** at **Beginner** difficulty. It includes a FastAPI backend, a React frontend, sample documents, vector search with ChromaDB support, source citations, timeline logs, structured run storage, Docker files, and tests.

The legal compliance domain involves adhering to laws, regulations, and internal policies. Escalation triage specifically focuses on the initial assessment of reported compliance issues, determining their severity, responsible department, and next steps. This project simplifies this process by providing quick access to relevant policy information.

Difficulty controls project complexity, architecture depth, AI model selection, and how advanced the generated codebase is.

- Architecture depth: minimal backend, simple folder structure, easy README, low-cost/free model
- Selected architecture: Compliance Knowledge Portal
- Template path: templates/simple-rag/compliance-knowledge-portal
- Generated stack: FastAPI backend, React UI, local vector fallback, simple tests
- README style: beginner-friendly setup and clear expected output

## Tech Stack

- Backend: Python, FastAPI, Pydantic, SQLAlchemy
- AI/RAG: LangChain-ready prompt layer, ChromaDB vector storage, local deterministic fallback model
- Workflow: Agent pipeline with planner, retrieval, tool, reasoning, and final answer steps
- Frontend: React and Vite
- Database: SQLite by default, PostgreSQL through Docker Compose
- Testing: pytest
- Difficulty: Beginner

## Generation Method

This project was generated with a template-based architecture engine. AI is used only for the blueprint, domain customization, sample data, prompts, and documentation. The codebase is produced from tested FastAPI/React/Docker templates rather than raw LLM source output.

## Why This Project Satisfies Simple RAG

This repository satisfies **Simple RAG** because it includes runnable implementation evidence, domain-specific workflow steps, validation gates, and portfolio documentation instead of only describing the idea.

## Project Type Satisfaction Map

This generated project satisfies **Simple RAG** through the runtime path below. The implementation is not only a README claim: the files listed after the diagram are generated in the repository and validated before GitHub push.

```text
[User]
  |
  | question / task details / tone / constraints
  v
[React Frontend]
  |
  | POST /api/ask
  v
[FastAPI Backend]
  |
  +--> [Vector Store / Sample Docs]
  |        |
  |        +-- retrieved context / cited sources
  |
  v
[Retriever]
  |
  v
[Citation Answer Builder]
  |
  v
[Final Answer Builder]
  |
  | answer + sources + timeline steps
  v
[React Frontend]
  |
  v
[User sees final output + agent timeline]
```

Runtime proof points:

- `frontend/src/App.jsx` renders the user workspace, starter prompts, answer panel, cited sources, and timeline.
- `backend/app/main.py` exposes `POST /api/ask` and returns the final answer, sources, timeline steps, and project type.
- `backend/app/services/pipeline.py` orchestrates the project-type flow: Retriever, Citation Answer Builder.
- `backend/app/services/vector_store.py` loads sample documents and retrieves relevant cited context.
- `backend/app/domain.py` contains the generated topic-specific workflow steps, business rules, tools, persona, and starter questions.
- `backend/app/db.py` stores each run so the generated app behaves like a real workflow tool instead of a static prompt demo.
- `backend/tests/test_project_contract.py` validates the API contract and project-type behavior.

Type-specific behavior:

- Flow style: User question -> load documents -> split chunks -> embed -> Chroma similarity search -> answer with citations.
- Visible output: final answer, cited sources, timeline steps, and project type.
- Validation gate: pytest, frontend build, Docker Compose config, and Docker build before repository upload.

## Folder Structure

```text
ai-simple-rag-legal-compliance-escalation-triage-simple-rag-beginner-custom-15/
  backend/
app/
  main.py
  config.py
  db.py
  schemas.py
  data/sample_docs/
  services/
text.py
vector_store.py
llm.py
tools.py
pipeline.py
tests/
  test_project_contract.py
requirements.txt
Dockerfile
  frontend/
src/
  App.jsx
  main.jsx
  styles.css
package.json
Dockerfile
  docker-compose.yml
  .env.example
  README.md
  ARCHITECTURE.md
  SYSTEM_DESIGN.md
  DATABASE_DESIGN.md
  API_DESIGN.md
  DFD_LEVEL_0.md
  DFD_LEVEL_1.md
  DFD_LEVEL_2.md
  ER_DIAGRAM.md
  SEQUENCE_DIAGRAMS.md
  SECURITY.md
  SCALABILITY.md
  TESTING_STRATEGY.md
  INTERVIEW_GUIDE.md
  WHY_THIS_PROJECT.md
  DEPLOYMENT.md
  docs/screenshots/app-preview.svg
```

## Environment Variables

```env
OPENAI_API_KEY=
OPENAI_MODEL=gpt-4o-mini
USE_CREWAI_RUNTIME=false
PINECONE_API_KEY=
PINECONE_INDEX_NAME=
DATABASE_URL=sqlite:///./app.db
ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000
VITE_API_URL=http://localhost:8000
```

The app runs without an OpenAI key by using a deterministic local answer model. Add `OPENAI_API_KEY` to use LangChain with OpenAI. For CrewAI projects, set `USE_CREWAI_RUNTIME=true` after installing dependencies to run the live CrewAI Agent/Task/Crew workflow; otherwise the app uses a deterministic CrewAI-shaped fallback.

For Pinecone projects, add `PINECONE_API_KEY` and `PINECONE_INDEX_NAME` to use a live Pinecone index. Without them, the repo still runs using local ChromaDB/local retrieval fallback.

## Installation

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

```bash
cd ../frontend
npm install
```

## Run Backend

```bash
cd backend
uvicorn app.main:app --reload --port 8000
```

## Run Frontend

```bash
cd frontend
npm run dev
```

## Run With Docker

```bash
docker compose up --build
```

## Example API Request

```bash
curl -X POST http://localhost:8000/api/ask ^
  -H "Content-Type: application/json" ^
  -d "{\"question\": \"What is the refund policy?\"}"
```

## Example User Question

```text
What should I do if a customer asks for a refund without an order id?
```

## Expected Output

The API returns:

- `answer`: a grounded answer generated from retrieved context
- `sources`: cited document chunks with similarity scores
- `steps`: planner, retriever, reasoning, tool-call, and final-answer timeline logs
- `project_type`: `Simple RAG`

## How The RAG/Agent Flow Works

User question -> load documents -> split chunks -> embed -> Chroma similarity search -> answer with citations.

## Project Documentation

- [System Design](SYSTEM_DESIGN.md)
- [Architecture](ARCHITECTURE.md)
- [Database Design](DATABASE_DESIGN.md)
- [API Design](API_DESIGN.md)
- [DFD Level 0](DFD_LEVEL_0.md)
- [DFD Level 1](DFD_LEVEL_1.md)
- [DFD Level 2](DFD_LEVEL_2.md)
- [ER Diagram](ER_DIAGRAM.md)
- [Sequence Diagrams](SEQUENCE_DIAGRAMS.md)
- [Deployment](DEPLOYMENT.md)
- [Security](SECURITY.md)
- [Scalability](SCALABILITY.md)
- [Testing Strategy](TESTING_STRATEGY.md)
- [Interview Guide](INTERVIEW_GUIDE.md)

## Project Planner Agent Workflow

User -> React Dashboard -> FastAPI -> Project Planner Agent -> Specialist Agents -> Generated Project -> Auto Testing -> GitHub Repository Creation -> Push Code -> Return GitHub URL

- **Architecture Agent**: Define app boundaries, data flow, runtime stack, and integration points. Outputs: For a beginner project, we'll prioritize simplicity and local execution where possible. We'll use open-source embedding models (e.g., `sentence-transformers`) and an in-memory or file-based vector database (e.g., `ChromaDB` or `FAISS` running locally) to reduce setup complexity. The LLM can be accessed via a free tier/developer key (e.g., OpenAI, Google Gemini) or a local small LLM (e.g., a quantized Llama-2 variant) if computational resources allow. Docker will containerize the backend and frontend for easy deployment. The focus is on understanding the core RAG pipeline, not on production-scale infrastructure..
- **Backend Agent**: Design FastAPI modules, service contracts, validation, and error handling. Outputs: {'api_service': 'FastAPI application defining REST endpoints for health checks, document upload (for future expansion), and the core RAG query.', 'rag_core': 'Python module containing the RAG orchestration logic: query embedding, vector database interaction, context retrieval, and LLM prompting.', 'document_processor': "Module for loading, chunking (e.g., using Langchain's TextSplitter), and embedding documents into the vector store.", 'embedding_service': "Wrapper around a chosen embedding model (e.g., HuggingFace's `sentence-transformers`).", 'vector_store_manager': 'Interface for interacting with the chosen vector database (e.g., `ChromaDB` client).'}.
- **Frontend Agent**: Design React screens, state flow, controls, and user feedback states. Outputs: {'search_input': 'Text input field for users to type their compliance-related questions.', 'response_display': 'Area to display the AI-generated answer.', 'loading_indicator': 'Visual feedback while the AI is processing the query.', 'source_document_links': 'Display links or references to the original document chunks used by the LLM (optional, but good for trust).', 'basic_styling': 'Clean, simple UI design for readability and ease of use.'}.
- **Database Agent**: Design persistence models, sample data, indexes, and audit records. Outputs: Run history; Source document metadata; Generated workflow audit records.
- **Testing Agent**: Define contract tests, smoke tests, and generated project validation. Outputs: {'unit_tests': 'Test individual components: chunking logic, embedding function, vector store retrieval, prompt construction.', 'integration_tests': 'Test the full RAG pipeline with known queries and expected answers against the sample document corpus. Verify that relevant documents are retrieved and LLM generates plausible answers.', 'rag_evaluation': 'Manual evaluation for relevance of retrieved chunks and faithfulness/accuracy of LLM generated responses. Test edge cases (e.g., out-of-scope questions, ambiguous queries).', 'frontend_tests': 'Basic UI tests for component rendering and user interaction (e.g., input field, button click).'}.
- **DevOps Agent**: Define environment variables, Docker workflow, and repository packaging. Outputs: Docker-ready project; Environment sample file; GitHub repository upload.
- **Reviewer Agent**: Review the generated plan for completeness, security, and portfolio quality. Outputs: **Step 1: Document Ingestion (Offline/Setup)**: Sample compliance documents are loaded, chunked into smaller passages, and converted into numerical embeddings.; **Step 2: Vector Database Population (Offline/Setup)**: These embeddings are stored in the vector database, indexed for efficient semantic search.; **Step 3: User Query (Online)**: A Junior Compliance Officer enters a question into the frontend (e.g., 'How do I report a conflict of interest?').; **Step 4: Query Embedding (Backend)**: The backend API receives the query and converts it into a vector embedding using the same embedding model.; **Step 5: Semantic Search (Backend + Vector DB)**: The query embedding is used to search the vector database for the most semantically similar document chunks.; **Step 6: Context Retrieval (Backend)**: The top N (e.g., 3-5) most relevant document chunks are retrieved..

## AI-Customized Domain Workflow

- **Step 1: Document Ingestion (Offline/Setup)**: Sample compliance documents are loaded, chunked into smaller passages, and converted into numerical embeddings.
- **Step 2: Vector Database Population (Offline/Setup)**: These embeddings are stored in the vector database, indexed for efficient semantic search.
- **Step 3: User Query (Online)**: A Junior Compliance Officer enters a question into the frontend (e.g., 'How do I report a conflict of interest?').
- **Step 4: Query Embedding (Backend)**: The backend API receives the query and converts it into a vector embedding using the same embedding model.
- **Step 5: Semantic Search (Backend + Vector DB)**: The query embedding is used to search the vector database for the most semantically similar document chunks.
- **Step 6: Context Retrieval (Backend)**: The top N (e.g., 3-5) most relevant document chunks are retrieved.
- **Step 7: Prompt Construction (Backend)**: These retrieved chunks are combined with the original user query and a system instruction into a concise prompt for the LLM.
- **Step 8: LLM Generation (Backend)**: The prompt is sent to the LLM, which generates a coherent and relevant answer based *only* on the provided context.

## Business Rules

- **Relevance First**: Answers must primarily rely on information retrieved from the provided compliance documents.
- **Conciseness**: Responses should be direct and to the point, avoiding unnecessary jargon.
- **Clarity**: Language used in responses should be easy for a JCO to understand.
- **Non-Discretionary**: The system should not offer legal advice or make subjective judgments; it only provides information based on policies.
- **Source Transparency (Recommended)**: If possible, indicate which document(s) or policy sections were used to formulate the answer.
- **Scope Limitation**: The system should acknowledge if a query is outside the scope of its knowledge base (i.e., no relevant documents found).

1. The backend loads sample documents from `backend/app/data/sample_docs`.
2. Documents are split into chunks.
3. Chunks are embedded and stored in ChromaDB when available, with a local fallback for development.
4. User questions are matched against relevant chunks.
5. Agent-specific steps run: planner, retriever, tool call, reasoning, reviewer, or graph nodes.
6. The final answer is returned with source citations and a timeline.

## Testing

```bash
cd backend
pytest
```

## Validation Gates Before GitHub Push

The SaaS validates generated projects before creating and pushing the GitHub repository:

- `pytest`
- `npm install`
- `npm run build`
- `docker compose config`
- `docker compose build`

## Portfolio Proof Files

- `WHY_THIS_PROJECT.md`: explains why this repo satisfies the selected project type.
- `SYSTEM_DESIGN.md`, `ARCHITECTURE.md`, and DFD files: document the design, runtime flow, data movement, and validation strategy.
- `DATABASE_DESIGN.md`, `ER_DIAGRAM.md`, and `API_DESIGN.md`: connect generated code to data and API contracts.
- `SECURITY.md`, `SCALABILITY.md`, and `TESTING_STRATEGY.md`: explain production hardening and quality checks.
- `INTERVIEW_GUIDE.md`: helps students explain the project in interviews.
- `DEPLOYMENT.md`: gives Render, Railway, Vercel, and Docker deployment options.
- `docs/screenshots/app-preview.svg`: generated UI preview image for README/profile use.

## Deployment

See `DEPLOYMENT.md` for Render, Railway, Vercel, and Docker deployment steps.
