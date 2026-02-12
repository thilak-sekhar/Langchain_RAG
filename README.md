# Enterprise Knowledge RAG Assistant

A **production-style Retrieval-Augmented Generation (RAG) system** built using **LangChain, Pinecone, Ollama, and Streamlit**, enhanced with **RAGAS-based automated evaluation**.

The system answers user queries **strictly grounded in ingested documents**, demonstrating clean architecture, incremental ingestion, measurable evaluation, and real-world usability.

This project is intentionally designed as a **maintainable AI system**, not a chatbot demo.

---

## 🔍 Key Features

- Incremental PDF ingestion (no Pinecone index reset)
- Vector-based semantic search using Pinecone
- Retrieval-Augmented Generation (RAG) with LangChain
- Local LLM inference via Ollama (offline capable)
- RAGAS-based automated evaluation pipeline
- Faithfulness & hallucination detection
- Transparent source attribution
- Streamlit-based interactive UI
- Modular, production-aligned architecture
- CLI and UI execution modes
- Vendor-independent evaluation design

---

## 🧠 Architecture Overview

```
Streamlit UI
↓
System Entrypoint (main.py)
↓
RAG Chain (LangChain)
↓
Retriever + Prompt + LLM (Ollama)
↓
Pinecone Vector Store
↓
RAGAS Evaluation Module
```

### Design Principles

- UI is a thin client (no business logic)
- All orchestration flows through `main.py`
- RAG logic is isolated and reusable
- Evaluation is decoupled from inference
- Data ingestion is incremental and safe
- Evaluation is measurable and auditable

---

## 📊 RAG Evaluation with RAGAS

This project integrates **RAGAS (Retrieval-Augmented Generation Assessment Suite)** to objectively evaluate answer quality and grounding.

Unlike prototype systems that rely on visual inspection, this assistant includes **automated quality scoring**.

### 🧠 Metrics Used

- **Faithfulness** – Are generated answers strictly supported by retrieved documents?
- **Context Precision** – Were the retrieved chunks actually useful?
- **Context Recall** – Did retrieval capture all necessary information?
- **Answer Relevancy** – Does the answer directly address the user query?

These metrics help detect:

- Hallucinations
- Retrieval noise
- Weak prompt design
- Incomplete grounding
- Over-generation beyond evidence

---

### 🔬 Evaluation Flow

```
User Query
↓
Retriever (Pinecone)
↓
Top-k Chunks
↓
LLM (Ollama)
↓
Generated Answer
↓
RAGAS Evaluation
   ├── Evaluator LLM
   └── Embedding Model
↓
Quantitative Quality Scores
```

The evaluation module can be used for:

- Offline validation
- Regression testing
- Retrieval tuning
- Prompt optimization
- Hallucination monitoring

---

### ⚙️ Evaluator Configuration

The system supports two modes:

#### 1️⃣ Fully Local Evaluation
- Evaluator LLM: Ollama (LLaMA-based model)
- Embeddings: HuggingFace sentence-transformers
- No external API dependency

#### 2️⃣ High-Precision Evaluation (Optional)
- Evaluator LLM: GPT-4-class model
- Recommended for strict hallucination detection and benchmarking

This decoupled architecture allows:
- Cost-efficient local inference
- Stronger evaluation when needed
- Vendor-independent quality monitoring

---

### 📈 Example Evaluation Output

```json
{
  "faithfulness": 0.78,
  "context_precision": 0.64,
  "context_recall": 0.71,
  "answer_relevancy": 0.88
}
```

These scores provide measurable insight instead of subjective judgment.

---

## 📂 Project Structure

```
enterprise-rag-assistant/
│
├── app/
│   ├── chains/          # RAG chain logic
│   ├── config/          # Configurations
│   ├── embeddings/      # Embedding logic
│   ├── ingestion/       # PDF loading, chunking, ingestion
│   ├── retriever/       # Pinecone retriever
│   ├── evaluation/      # RAGAS evaluation module
│   ├── ui/              # Streamlit UI
│   ├── utils/           # Logger and helpers
│   └── main.py          # System entrypoint
│
├── data/
│   └── pdf/
│       └── langchain_deep_dive.pdf
│
├── requirements.txt
├── README.md
└── .gitignore
```

---

## 📘 Demo Data

The repository includes a **5+ page LangChain deep-dive PDF** to demonstrate:

- Chunking quality
- Cross-section retrieval
- Concept-level grounding
- Hallucination resistance
- Evaluation scoring behavior

File:

```
data/pdf/langchain_deep_dive.pdf
```

---

## 🖥️ Offline / Local LLM Setup (Ollama + Nomic + LLaMA)

This project supports **fully offline execution** after model setup.

### 🔧 Components Used

- **Ollama** – Local LLM runtime
- **LLaMA-based model** – Answer generation
- **nomic-embed-text** – Embedding model
- **Pinecone** – Vector database
- **HuggingFace embeddings** – Evaluation embeddings

---

## 🧠 Offline Execution Capabilities

After initial model pull, no internet is required for:

- Query answering
- Embedding generation
- Retrieval
- Evaluation (local mode)
- Streamlit UI interaction

All inference runs locally.

---

## 🚀 Getting Started

### 1️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 2️⃣ Ingest Documents

```bash
python app/ingestion/ingest_pipeline.py
```

This appends documents to the Pinecone index safely.

---

### 3️⃣ Run Streamlit UI

```bash
streamlit run app/ui/streamlit_app.py
```

---

### 4️⃣ Run CLI Mode

```bash
python app/main.py
```

---

## 🧪 Example Demo Queries

Use these to validate behavior:

- What is LangChain and why is it used in production systems?
- Explain how LangChain supports Retrieval-Augmented Generation.
- What are agents in LangChain?
- What are best practices for using LangChain in production?

Out-of-scope test:

- What is quantum teleportation over blockchain?

(Expected: refusal or low-confidence grounded response)

---

## 🛠 Key Design Decisions

- Precision-first retrieval to reduce hallucinations
- Strict grounding in retrieved documents
- Incremental ingestion for production safety
- UI separated from orchestration logic
- No direct LLM calls from UI
- Evaluation decoupled from inference
- Measurable performance via RAGAS

---

## 📌 Use Cases

- Enterprise document Q&A
- Internal knowledge assistants
- Policy and compliance exploration
- Technical documentation search
- Analyst and developer productivity tools
- AI system quality benchmarking

---

## 📈 Future Enhancements

- Automated evaluation logging
- Historical metric tracking
- CI-based regression testing with RAGAS
- FastAPI service layer
- Dockerized deployment
- Metadata-based filtering
- Multi-document evaluation benchmarking

---

## 👤 Author

Built as a **production-grade RAG system** with emphasis on:

**architecture, correctness, grounding, and measurable evaluation** — not shortcuts.

This project reflects real-world applied AI engineering practices rather than demo-oriented experimentation.
