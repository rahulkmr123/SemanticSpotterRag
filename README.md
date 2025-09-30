# Semantic Spotter RAG

This project provides a clean Retrieval-Augmented Generation (RAG) workflow for answering questions about HDFC insurance policy documents. It consolidates the strongest ideas from two prior notebooks into a single, production-friendly implementation.

## Highlights
- Persistent vector store with Chroma (`./chroma_persistence`)
- OpenAI embeddings with in-memory caching to avoid recomputation
- Retriever tuned with MMR + score threshold
- Contextual compression using a cross-encoder reranker (`cross-encoder/ms-marco-MiniLM-L-2-v2`)
- Standard RAG prompt pipeline and modular chain composition

## Prerequisites
- Python 3.10+
- An OpenAI API key
- Insurance PDFs placed in `insuranceDoc/` (already prepared by setup)

Export your API key in the environment before running:
```bash
export OPENAI_API_KEY=your_key_here
```

## How to Run
1. Open the notebook:
   - `semantic_spotter_rag.ipynb`
2. Run cells top to bottom. The first cell installs pinned dependencies.
3. The notebook will:
   - Load PDFs from `insuranceDoc/`
   - Split into chunks
   - Build and persist a Chroma DB with cached embeddings
   - Configure a retriever (MMR + threshold + contextual compression)
   - Compose a RAG chain with a standard prompt
   - Execute example queries to mirror expected answers

## Folder Structure
- `insuranceDoc/`: Source PDFs for indexing
- `chroma_persistence/`: On-disk Chroma DB
- `semantic_spotter_rag.ipynb`: Main RAG notebook
- `README_semantic_spotter_rag.md`: This readme

## Notes
- If you change or add PDFs, delete `chroma_persistence/` to rebuild from scratch or call Chroma’s API to upsert.
- You can adjust chunk sizes, overlap, `top_k`, and `score_threshold` to tune retrieval.
- The example queries at the end emulate the reference notebook’s behavior without duplicating its code.
