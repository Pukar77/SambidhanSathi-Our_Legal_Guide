SambidhanSathi - Nepal Constitution AI Advisor

An AI legal advisor for the Constitution of Nepal. It ingests a PDF of the Constitution into Qdrant, then provides a Streamlit chat UI that answers questions using retrieval-augmented generation (RAG) with Google Gemini.

## Features

- PDF ingestion and cleaning with PyMuPDF
- Article-level chunking with Part and Article metadata
- Vector search in Qdrant
- Streamlit chat UI with grounded, citation-aware responses

## Project Structure

```
app.py                      # Streamlit UI
main.py                     # PDF ingestion pipeline
requirements.txt
data/                       # Source PDF (see Setup)
qdrant_db/                  # Local Qdrant data (if using local storage)
src/
  pdf_loader.py             # PDF reading and cleaning
  text_splitter.py          # Part/Article chunking
  vector_store.py           # Qdrant + embeddings
```

## Prerequisites

- Python 3.9+ (recommended)
- Qdrant running locally on port 6333
- A Google Gemini API key

## Setup

1. Create and activate a virtual environment (optional but recommended).
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Add your API key to a `.env` file in the project root:
   ```bash
   GEMINI_API_KEY=your_api_key_here
   ```
4. Place the Constitution PDF at:
   ```
   data/Nepal_Law.pdf
   ```

## Run Qdrant

Use a local Qdrant instance. For example (Docker):

```bash
docker run -p 6333:6333 qdrant/qdrant
```

## Ingest the PDF

Run the ingestion pipeline to build the vector store:

```bash
python main.py
```

This will:

- Load and clean the PDF
- Split text by Part and Article
- Generate embeddings
- Upsert into the Qdrant collection

## Start the App

```bash
streamlit run app.py
```

Open the URL shown in the terminal to use the chat UI.

## Environment Variables

- `GEMINI_API_KEY` (required): Google Gemini API key
- `DOCUMENT_TITLE` (optional): Defaults to "The Constitution of Nepal"
- `QDRANT_COLLECTION` (optional): Defaults to `nepal_constitution_v1`

## Notes

- The app answers strictly based on retrieved constitutional text. If relevant context is not found, it will say so.
- Qdrant must be running before ingestion and before using the app.

## Troubleshooting

- If the app cannot connect to Gemini, verify `GEMINI_API_KEY` and network access.
- If ingestion fails, check that `data/Nepal_Law.pdf` exists and Qdrant is reachable.

## License

Add a license if you plan to distribute this project.
