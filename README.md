---

# Persian News RAG (Lite Baseline)

This repository contains a lightweight baseline implementation of a **Retrieval-Augmented Generation (RAG)** system for **Persian news data**.
The goal of this project is to explore and compare different retrieval strategies on Persian text and evaluate their effectiveness in a simple RAG pipeline.

The project is intentionally kept simple and notebook-based, focusing more on **retrieval quality** rather than heavy generative models.

---

## Project Overview

The pipeline follows the standard RAG structure:

1. **Data preparation and chunking**
2. **Building retrieval models**
3. **Answer generation based on retrieved chunks**
4. **Manual evaluation and comparison of retrieval methods**

Three retrieval approaches are implemented and compared:

* **Semantic retrieval** using SentenceTransformer embeddings and FAISS
* **Lexical retrieval** using BM25
* **Hybrid retrieval** combining semantic and lexical results (RRF-style fusion)

---

## Repository Structure

```
.
├── 01_prepare_data.ipynb
├── 02_build_rag_baseline.ipynb
├── 03_evaluate_and_report.ipynb
├── evaluation/
│   └── results.jsonl
└── README.md
```

### Notebooks

* **01_prepare_data.ipynb**
  Loads the dataset, removes empty texts, applies basic preprocessing, samples a balanced subset of data, and chunks the texts based on fixed settings.

* **02_build_rag_baseline.ipynb**
  Builds semantic, lexical, and hybrid retrieval models.
  Creates FAISS indexes, BM25 retrievers, and defines retrieval and answer-generation functions.

* **03_evaluate_and_report.ipynb**
  Defines evaluation questions, runs all retrieval modes, performs manual evaluation, and summarizes the results.

---

## Retrieval Methods

* **Semantic**
  Uses dense embeddings to capture the overall meaning of the text. Performs well when exact keywords are not shared.

* **BM25 (Lexical)**
  Relies on word overlap between the query and documents. Works well for keyword-heavy queries.

* **Hybrid**
  Combines both approaches to benefit from semantic similarity and keyword matching.
  In practice, this approach showed the most stable and reliable performance.

---

## Evaluation

* 15 news-related questions were manually designed.
* Each question was answered using all three retrieval methods.
* Evaluation was performed **manually**, based on answer relevance and usefulness.
* Results are stored in `evaluation/results.jsonl`.

Based on the evaluation, the hybrid approach generally produced more acceptable answers compared to using semantic or lexical retrieval alone.

---

## Notes and Limitations

* Answer generation is currently done by **concatenating retrieved chunks**, without using a large language model.
* The focus of this project is on **retrieval quality**, not fluent text generation.
* Evaluation is subjective and human-based due to the open-ended nature of news questions.

---

## Possible Improvements

* Using stronger or Persian-specific embedding models
* Improving the chunking strategy (e.g. paragraph-based chunking)
* Adding a generative model to rewrite or summarize retrieved chunks
* Introducing automatic or semi-automatic evaluation metrics

---

## Requirements

Main libraries used in this project include:

* sentence-transformers
* faiss-cpu
* rank-bm25
* pandas
* numpy
* scikit-learn

---

## Final Note

This project is meant as a **clear and minimal baseline** for experimenting with RAG systems on Persian text and can serve as a starting point for more advanced implementations.

---.
