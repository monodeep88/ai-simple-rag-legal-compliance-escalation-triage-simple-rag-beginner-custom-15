# Generation Notes

Mode: ai

Model: gemini / gemini-2.5-flash

Fallback reason: OpenAI limit reached. Automatically switched to Gemini.

Architecture: Compliance Knowledge Portal

Template path: templates/simple-rag/compliance-knowledge-portal

Short description:

A beginner-friendly RAG system to help compliance officers quickly triage legal compliance escalation inquiries based on internal policy documents.

Architecture notes:

- For a beginner project, we'll prioritize simplicity and local execution where possible. We'll use open-source embedding models (e.g., `sentence-transformers`) and an in-memory or file-based vector database (e.g., `ChromaDB` or `FAISS` running locally) to reduce setup complexity. The LLM can be accessed via a free tier/developer key (e.g., OpenAI, Google Gemini) or a local small LLM (e.g., a quantized Llama-2 variant) if computational resources allow. Docker will containerize the backend and frontend for easy deployment. The focus is on understanding the core RAG pipeline, not on production-scale infrastructure.

Project planner agent workflow:

- Architecture Agent: Define app boundaries, data flow, runtime stack, and integration points. Outputs: For a beginner project, we'll prioritize simplicity and local execution where possible. We'll use open-source embedding models (e.g., `sentence-transformers`) and an in-memory or file-based vector database (e.g., `ChromaDB` or `FAISS` running locally) to reduce setup complexity. The LLM can be accessed via a free tier/developer key (e.g., OpenAI, Google Gemini) or a local small LLM (e.g., a quantized Llama-2 variant) if computational resources allow. Docker will containerize the backend and frontend for easy deployment. The focus is on understanding the core RAG pipeline, not on production-scale infrastructure.
- Backend Agent: Design FastAPI modules, service contracts, validation, and error handling. Outputs: {'api_service': 'FastAPI application defining REST endpoints for health checks, document upload (for future expansion), and the core RAG query.', 'rag_core': 'Python module containing the RAG orchestration logic: query embedding, vector database interaction, context retrieval, and LLM prompting.', 'document_processor': "Module for loading, chunking (e.g., using Langchain's TextSplitter), and embedding documents into the vector store.", 'embedding_service': "Wrapper around a chosen embedding model (e.g., HuggingFace's `sentence-transformers`).", 'vector_store_manager': 'Interface for interacting with the chosen vector database (e.g., `ChromaDB` client).'}
- Frontend Agent: Design React screens, state flow, controls, and user feedback states. Outputs: {'search_input': 'Text input field for users to type their compliance-related questions.', 'response_display': 'Area to display the AI-generated answer.', 'loading_indicator': 'Visual feedback while the AI is processing the query.', 'source_document_links': 'Display links or references to the original document chunks used by the LLM (optional, but good for trust).', 'basic_styling': 'Clean, simple UI design for readability and ease of use.'}
- Database Agent: Design persistence models, sample data, indexes, and audit records. Outputs: Run history; Source document metadata; Generated workflow audit records
- Testing Agent: Define contract tests, smoke tests, and generated project validation. Outputs: {'unit_tests': 'Test individual components: chunking logic, embedding function, vector store retrieval, prompt construction.', 'integration_tests': 'Test the full RAG pipeline with known queries and expected answers against the sample document corpus. Verify that relevant documents are retrieved and LLM generates plausible answers.', 'rag_evaluation': 'Manual evaluation for relevance of retrieved chunks and faithfulness/accuracy of LLM generated responses. Test edge cases (e.g., out-of-scope questions, ambiguous queries).', 'frontend_tests': 'Basic UI tests for component rendering and user interaction (e.g., input field, button click).'}
- DevOps Agent: Define environment variables, Docker workflow, and repository packaging. Outputs: Docker-ready project; Environment sample file; GitHub repository upload
- Reviewer Agent: Review the generated plan for completeness, security, and portfolio quality. Outputs: **Step 1: Document Ingestion (Offline/Setup)**: Sample compliance documents are loaded, chunked into smaller passages, and converted into numerical embeddings.; **Step 2: Vector Database Population (Offline/Setup)**: These embeddings are stored in the vector database, indexed for efficient semantic search.; **Step 3: User Query (Online)**: A Junior Compliance Officer enters a question into the frontend (e.g., 'How do I report a conflict of interest?').; **Step 4: Query Embedding (Backend)**: The backend API receives the query and converts it into a vector embedding using the same embedding model.; **Step 5: Semantic Search (Backend + Vector DB)**: The query embedding is used to search the vector database for the most semantically similar document chunks.; **Step 6: Context Retrieval (Backend)**: The top N (e.g., 3-5) most relevant document chunks are retrieved.
