# APUOPE-RE: LLM-Powered Teaching Assistant

This application serves as an interactive teaching assistant for Requirements Engineering (RE) courses. It utilizes **Retrieval-Augmented Generation (RAG)** to provide context-aware answers, quizzes, and assignments based specifically on uploaded course PDF materials rather than general knowledge.

## System Overview

Unlike a standard monolithic LLM approach where a model relies solely on its training data, this project implements a RAG architecture. When a user uploads a course document, the system indexes the content into a vector store. Subsequent user queries (such as generating a quiz or explaining a concept) trigger a semantic search against this index.

The application retrieves the specific text chunks relevant to the user's request and feeds them into OpenAI's models (GPT-4/GPT-4o) as context. This ensures that the generated content aligns strictly with the provided lecture materials and reduces hallucinations.

## Key Components

### Core RAG Engine
The backend logic is handled primarily in `rag_engine.py`. This module manages the lifecycle of document processing:
*   **Ingestion:** PDFs are split into chunks of approximately 500 words to ensure optimal context window usage.
*   **Vectorization:** Each chunk is converted into embeddings using the `text-embedding-ada-002` model.
*   **Storage:** Vectors are cached locally using pickle files with MD5-hashed filenames to prevent redundant processing.
*   **Retrieval:** When a query is received, the engine calculates cosine similarity to find the top matching chunks before generating a response.

### Application Modules
The user-facing functionality is organized into specific components found in the `components/` directory:
*   **Assessment Tools:** `quizzes.py` and `assignment.py` generate scenario-based questions and coding tasks. These modules use the RAG engine to find specific topics within the PDFs to build questions around.
*   **Learning Aids:** `conceptual_examples.py` and `lecture_summaries.py` help students review material by extracting key points and generating illustrative examples.
*   **Student Tracking:** The dashboard and progress tracking modules monitor user interaction and quiz performance.

## Installation

1.  **Clone the repository**

2.  **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Environment Setup**
    Create a `.env` file in the root directory and add your OpenAI API key:
    ```
    OPENAI_API_KEY=your_key_here
    ```

4.  **Run the application**
    ```bash
    streamlit run app.py
    ```

## Configuration

You can tune the performance of the RAG retrieval in `rag_engine.py`. The `chunk_size` (default: 500 words) determines the granularity of the context, while `top_k` (default: 3-5) controls how many distinct text segments are fed to the LLM during generation.

The application uses SQLite (`lecture_summaries.db`) for data persistence regarding user progress and cached summaries. If you need to reset the application state, run `python clear_database.py`.

## Project Structure

```text
RAG/
├── app.py                    # Main Streamlit entry point
├── rag_engine.py             # Embedding, retrieval, and generation logic
├── quiz_handler.py           # Quiz logic and scoring
├── pdf_extractor.py          # PDF text parsing
├── relevance_check.py        # Validates if content matches the query
├── auth.py                   # User authentication
├── db.py                     # Database interactions
├── file_storage.py           # File I/O utilities
├── style.css                 # Custom UI styling
├── components/               # UI Modules
│   ├── assignment.py
│   ├── conceptual_examples.py
│   ├── dashboard.py
│   ├── feedback.py
│   ├── lecture_summaries.py
│   ├── progress_tracking.py
│   └── quizzes.py
├── vector_store/             # Local cache for embeddings
└── tests/                    # Unit tests

## Running Tests

To run the comprehensive testing framework:

```bash
# Full test suite (90 tests, ~15-30 minutes)
python run_tests.py

# Limited testing (e.g., 5 tests for validation)
python run_tests.py --limit 5

# Generate statistics from existing results
python quick_stats.py
```
