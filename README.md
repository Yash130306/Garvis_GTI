# 🤖 GARVIS — Offline / Ollama Edition

**GARVIS (GAIL AI Retrieval & Information System)** is an AI-powered enterprise information retrieval and HR assistance system developed as part of a **Summer Internship Project at GAIL (India) Limited**.

This branch (`gail-official`) is the **offline/local-inference version of GARVIS**, designed to run LLM workloads locally using **Ollama** instead of relying on a cloud-hosted LLM API.

## 🎯 Purpose of This Branch

Enterprise environments may require sensitive organizational information to remain within local infrastructure.

This implementation explores a privacy-oriented architecture where:

- LLM inference can run locally through Ollama
- Employee and organizational information remains locally stored
- PostgreSQL handles structured enterprise information
- RAG enables retrieval from employee documents and PDFs
- Semantic embeddings support intelligent information retrieval
- OCR enables processing of scanned documents

## 🧠 Core Capabilities

- Natural-language employee queries
- Employee profile retrieval
- Team and company-wide queries
- Event-related queries
- PDF and resume processing
- Structured metadata extraction
- Retrieval-Augmented Generation (RAG)
- Semantic embeddings
- PostgreSQL-backed structured storage
- OCR fallback for scanned PDFs
- Local LLM inference using Ollama

## 🏗️ Architecture

```text
User Query
    │
    ▼
GARVIS Interface
    │
    ▼
Local LLM — Ollama
    │
    ├──────────────┐
    ▼              ▼
PostgreSQL      RAG / Documents
Structured      PDFs + Embeddings
Data               │
    │              │
    └──────┬───────┘
           ▼
    Local LLM Synthesis
           │
           ▼
      Final Response
```

## 🛠️ Technology Stack

- Python
- Ollama
- LangChain
- Sentence Transformers
- PostgreSQL
- SQLAlchemy
- Streamlit
- FastAPI
- pdfplumber
- PyPDF2
- Tesseract OCR
- pdf2image

## 📂 Data Processing

GARVIS can process employee information from structured records as well as unstructured documents.

PDF documents are first processed using digital text extraction. Scanned documents can fall back to OCR. Extracted information can then be transformed into embeddings and stored alongside structured employee information for retrieval.

## 🚀 Installation

```bash
git clone -b gail-official https://github.com/Yash130306/Garvis_GTI.git
cd Garvis_GTI

python3 -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt
```

Install and configure **Ollama** with the local model expected by the project before running the application.

Configure your local PostgreSQL database as required by the project.

## 🌿 Other Branches

- `main` — Primary GARVIS implementation using Groq-hosted LLM inference
- `gail-official` — Offline/local Ollama implementation
- `v1` — Earlier development version

## 🔐 Data Privacy

The repository primarily contains **synthetic/sample employee and organizational data** for demonstration and testing.

A limited number of contributor resumes may be used as test documents with the respective contributors' permission.

No confidential GAIL employee database or production organizational dataset is intended to be included in this public repository.

## 👥 Contributors

Developed collaboratively during the GAIL internship project by:

- **Yash Malhotra**
- **Aditya Bhardwaj**
- **Harsh**

Original Git commit history has been preserved to accurately represent project contributions.

## 🏢 Internship Project

Developed as part of a summer internship at **GAIL (India) Limited**, exploring Generative AI, RAG, semantic search, document intelligence, and locally hosted LLMs for enterprise information retrieval.

## ⚠️ Disclaimer

This repository represents a prototype/internship implementation and is **not an official production system of GAIL (India) Limited**.
