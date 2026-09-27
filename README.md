# AI Document Assistant

A Python application for asking questions about PDF documents using Retrieval-Augmented Generation (RAG).

The app extracts text from uploaded PDFs, stores searchable embeddings, and retrieves relevant passages to help an AI model answer questions.

## Features

- Upload PDF documents individually.
- Ask questions across ingested documents.
- Choose how many text chunks to retrieve.
- Display answers with retrieved source filenames.
- Inspect ingestion and question-answering workflows in Inngest.

## How It Works

### Document ingestion
1. A user uploads a PDF through Streamlit.
2. Inngest triggers the ingestion workflow.
3. LlamaIndex extracts text and splits it into overlapping chunks.
4. OpenAI converts the chunks into numerical embeddings.
5. Qdrant stores the embeddings alongside the text and source filename.

### Answer generation
1. A user submits a question.
2. OpenAI creates an embedding for the question.
3. Qdrant retrieves similar document chunks.
4. GPT-4o-mini receives the question and retrieved text.
5. Streamlit displays the answer and source filenames.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application and workflow logic |
| Streamlit | PDF upload and question-answering interface |
| FastAPI and Uvicorn | Serve the backend and Inngest endpoint |
| Inngest | Coordinate and monitor background workflows |
| LlamaIndex | Extract PDF text and split it into chunks |
| OpenAI | Generate embeddings and answers |
| Qdrant | Store vectors and perform similarity search |
| Docker | Run Qdrant and the Inngest development server locally |
| uv | Manage Python dependencies and the virtual environment |

The embedding model is `text-embedding-3-large`, using 3,072-dimensional vectors.

## Project Files

- `streamlit_app.py`: User interface, uploads, and workflow requests.
- `main.py`: FastAPI application and Inngest workflows.
- `data_loader.py`: PDF extraction, text splitting, and embeddings.
- `vector_db.py`: Qdrant collection, storage, and search operations.
- `custom_types.py`: Structured workflow data models.
- `pyproject.toml` and `uv.lock`: Dependencies and locked versions.

## Local Development Requirements

- Python 3.13 and uv.
- Docker Desktop running Qdrant and an Inngest development server.
- An OpenAI API key with available API credits.
- A local `.env` file containing `OPENAI_API_KEY` and `INNGEST_DEV=1`.

The Streamlit interface runs at http://localhost:8501.
The Inngest dashboard runs at http://localhost:8288.

API keys, uploaded documents, virtual environments, and local database files should remain outside Git.

## Current Limitations

- The interface accepts one PDF per upload.
- Questions search the shared document collection.
- No OCR workflow is implemented for scanned PDFs.
- Sources show filenames rather than page-level citations.
- Answers may contain mistakes and should be checked against the documents.
- This is a local learning project; authentication and production hardening are not implemented.

## Acknowledgements

Based on Tech With Tim’s “How to Build a Production-Ready RAG AI Agent in Python” tutorial.

Tutorial: https://www.youtube.com/watch?v=AUQJ9eeP-Ls

Original repository: https://github.com/techwithtim/ProductionGradeRAGPythonApp

This repository documents my learning and development of the tutorial project.
