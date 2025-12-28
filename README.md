# Sanskrit CPU-Based Retrieval-Augmented Generation (RAG) System

This project implements a **Retrieval-Augmented Generation (RAG) system** designed to process Sanskrit narrative texts and generate query-based responses using a **CPU-only inference pipeline**. The system ingests uploaded Sanskrit documents, embeds them, retrieves semantically relevant chunks, and generates responses using a lightweight LLM — all without requiring GPU acceleration.

---

## Project Objective

The primary goal of this project is to:

- Build a functional CPU-optimized RAG pipeline
- Support Sanskrit document retrieval & question answering
- Ensure efficient vector similarity search on CPU
- Evaluate latency & retrieval quality under hardware constraints

---

## Dataset Description

The system ingests Sanskrit narrative texts from `Rag-docs.docx`, containing moral and satirical stories including:

- **Mūrkha-bhṛtyasya** — The Foolish Servant satire  
- **Caturasya Kālidāsasya** — Clever Kalidasa court tale  
- **Vṛddhāyāḥ Cāturyam** — Old woman & “Ghantakarna Demon” myth  
- **Devabhakta** — God helps those who help themselves (udyam)

Approximate corpus size: **~9000 characters**

The stories are chunked and indexed for semantic retrieval.

---

## System Architecture

The RAG pipeline consists of three core modules:

1. Document Ingestion & Preprocessing  
2. Vector Retriever (FAISS — CPU)  
3. Response Generator (TinyLlama-1.1B-Chat)

### Component Selection

- **Document Loader** — `python-docx`
- **Embedding Model** — `sentence-transformers/paraphrase-multilingual-mpnet-base-v2`
- **Vector Database** — **FAISS (CPU)**
- **LLM** — **TinyLlama-1.1B-Chat-v1.0 (float32)**

Optimized for compute-constrained environments.

---

## Preprocessing Pipeline

1. Regex-based text normalization  
2. Chunking into **500-character segments**
3. **50-character overlap** to preserve boundary context

This ensures complete narrative segments remain intact during retrieval.

---

## Retrieval & Inference Workflow

1. User query is embedded using multilingual MPNet
2. Top-k relevant chunks retrieved from FAISS
3. Chunks passed as context to TinyLlama generator
4. Response produced with grounded context

---

## Performance Evaluation (CPU-Only)

Latency observations:

- Fastest response — **~59.92s**
- Slowest response — **~150.48s**
- Average latency — **~109s / query**

### Retrieval Quality

- Relevant chunks retrieved accurately for context-specific queries

### Generation Limitations

- Limited Devanagari Sanskrit fluency
- Occasional transliteration / English mixing in outputs

---

## Current Limitations

- High inference latency from 1.1B parameter LLM on CPU
- Sanskrit text generation quality varies
- Intended for experimentation / research use

---

## Future Enhancements

- Indic-LLM fine-tuning for Sanskrit
- Model quantization (GGUF)
- Faster CPU embedding models
- Optional GPU fallback mode
- Interactive web UI

---

## Conclusion

This project demonstrates that a functional Sanskrit RAG pipeline:

- Can operate fully on **CPU hardware**
- Provides reliable document retrieval via FAISS
- Suffers latency + linguistic constraints due to model size

Further optimization & Indic-language alignment are recommended for production deployment.

---

## Author

**Krish Kumar**  
Lovely Professional University  
Machine Learning & AI Specialization
