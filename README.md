# SIRAG

A configurable self-improving RAG system combining hybrid retrieval, cross-encoder reranking, evidence-grounded generation, NLI-based faithfulness evaluation, and persistent feedback-driven memory.

SIRAG combines hybrid information retrieval, LLM-based query enhancement, evidence-grounded generation, NLI-based faithfulness evaluation, and persistent feedback-driven memory.

**The system improves through retrieval and memory mechanisms without fine-tuning or modifying the underlying LLM weights.**

## Architecture

```text
Official Mihon Documentation
          |
          v
   Website Crawling
          |
          v
 Heading-Aware Chunking
          |
          v
  Hybrid Retrieval
   |           |
 FAISS        BM25
   |           |
   +-----+-----+
         |
         v
  Reciprocal Rank Fusion
         |
         v
 Cross-Encoder Reranking
         |
         v
  Retrieval Quality Gate
         |
         v
  Gemma 4 E4B-it
         |
         v
  NLI Faithfulness Check
         |
         v
  Evidence-Grounded Answer
         |
         v
 SQLite Feedback Memory
```

## Key Features

- **Hybrid Retrieval:** Combines dense FAISS vector search and BM25 keyword retrieval using Reciprocal Rank Fusion.
- **Cross-Encoder Reranking:** Reorders retrieved documents based on query-document relevance.
- **HyDE:** Generates hypothetical documents to improve semantic retrieval.
- **Query Rewriting:** Reformulates questions for improved document retrieval.
- **Retrieval Gating:** Uses retrieval relevance and NLI signals to identify weak evidence and abstain when necessary.
- **Faithfulness Evaluation:** Evaluates individual answer claims against retrieved evidence using Natural Language Inference.
- **Gap-Targeted Retrieval:** Performs additional retrieval when generated claims lack sufficient evidence.
- **Persistent Memory:** Stores previous interactions, verified answers, corrections and feedback using SQLite.
- **Verified Question Aliases:** Adds positively reviewed questions as additional retrieval keys.
- **Lesson Distillation:** Converts feedback into reusable instructions for future queries.

## Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| LLM | Google Gemma 4 E4B-it |
| Embeddings | Sentence Transformers |
| Vector Database | FAISS |
| Keyword Retrieval | BM25 |
| Reranking | Cross-Encoder |
| Faithfulness Evaluation | DeBERTa NLI |
| Database | SQLite |
| Deep Learning | PyTorch |
| Document Processing | BeautifulSoup, Trafilatura |

## Self-Improvement Mechanism

SIRAG does not fine-tune the underlying language model.

Instead, it uses persistent memory and feedback-driven retrieval improvements:

1. Stores previous questions and answers.
2. Uses positive feedback and corrections to identify reusable answers.
3. Creates question aliases pointing to relevant documentation chunks.
4. Distills feedback into lessons.
5. Retrieves relevant memories and lessons during future queries.
6. Uses negative feedback to help avoid reusing known bad answers.

## Model Configuration

- Generator: `google/gemma-4-E4B-it`
- Embedding model: `sentence-transformers/all-MiniLM-L6-v2`
- Reranker: `cross-encoder/ms-marco-MiniLM-L-6-v2`
- NLI model: `cross-encoder/nli-deberta-v3-base`
- Generator quantization: 8-bit

## Running the Project

The current implementation is provided as a Jupyter notebook and is designed for a Kaggle GPU environment.

1. Clone the repository.
2. Open `sirag.ipynb` in Kaggle.
3. Accept the Gemma model license on Hugging Face.
4. Add a Kaggle secret named `HF_TOKEN`.
5. Enable GPU acceleration.
6. Execute the notebook cells in order.

## Limitations

- No language-model weight updates or fine-tuning.
- Faithfulness evaluation estimates evidence support, not factual correctness.
- Documentation caching can result in stale information.
- Feedback-based memory can introduce incorrect information if feedback is unreliable.
- Multiple LLM inference passes can increase response latency.
- The current implementation is text-only.

## Future Improvements

- Build a dedicated web interface.
- Add automated retrieval and answer-quality benchmarks.
- Implement memory validation and management.
- Improve document freshness and incremental indexing.
- Add support for multiple documentation sources.

## Project Status

Research and development prototype.

## License

[Choose and add an appropriate license before publishing.]
