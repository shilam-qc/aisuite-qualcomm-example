# Playground Notebook

This notebook (`playground.ipynb`) demonstrates a simple retrieval-augmented
generation (RAG) workflow using OpenAI-compatible APIs and ChromaDB. It is
intended for experimentation and learning, showing how to ingest text
data, query a vector store, and generate responses with a language model.

## Requirements

- Python 3.8+
- Packages listed below (install with pip):
  ```bash
  pip install openai chromadb dotenv
  ```
- An Imagine Cloud (OpenAI-compatible) API key and endpoint. The notebook uses
  the `INFERENCE_CLOUD_API_KEY` value to authenticate.

## Notebook Structure

1. **Setup**
   - Install dependencies (first cell).
   - Import necessary modules: `os`, `openai`, `chromadb`, `dotenv`, etc.
   - Load environment variables (API key and endpoint).

2. **Client Initialization**
   - Create an `OpenAI` client pointing to the Cirrascale Imagery SDK endpoint.
   - Instantiate a persistent ChromaDB client specifying the database path.
   - Define the collection name used for indexing.

3. **Embedding Function**
   - Configure an `OpenAIEmbeddingFunction` that wraps the external model
     (`BAAI/bge-large-en-v1.5`) for generating embeddings.

4. **Indexing Data**
   - `index()` function builds or retrieves the Chroma collection.
   - A hard-coded list of Emirates baggage policy rules is added only once.
   - Each rule is stored as a separate document with an associated ID.

5. **Retrieval**
   - `retrieve(query)` queries the collection for the top-3 relevant
     documents using the same embedding function.
   - Returns concatenated text or a message if nothing is found.

6. **Generation**
   - `generate(query)` composes a system/user prompt including retrieved
     context and sends it to the `Llama-3.1-8B` chat model via the OpenAI
     client.
   - Outputs the model's natural language answer.

7. **Example Usage**
   - The final cells run `index()` to populate the store, then execute two
     sample queries about baggage size and weight, printing the questions
     along with the model responses.

## Running the Notebook

1. Clone this repository and open the notebook in VS Code or Jupyter.
2. Set the `INFERENCE_CLOUD_API_KEY` environment variable before launching
   (e.g., add to a `.env` file or export in the shell).
3. Execute the cells sequentially, starting at the top.

The notebook is suitable for exploring basic RAG patterns, modifying the
text data, or swapping models/embedding functions.

## Notes

- The notebook uses a simplified domain (baggage policy) for illustrative
  purposes; you can replace the hard-coded rules with your own dataset.
- The API endpoint and embedding/model names may need adjustment if the
  services evolve.
- The provided code does not include error handling or batching; it is meant
  for experimentation rather than production use.
