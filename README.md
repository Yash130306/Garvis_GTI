# 🤖 GARVIS — GAIL AI Retrieval & Information System

**GARVIS** is an AI-powered enterprise information retrieval and HR assistance system developed as part of a **Summer Internship Project at GAIL (India) Limited**.

The system provides a conversational interface for retrieving structured and unstructured organizational information. It combines **Large Language Models (LLMs), Retrieval-Augmented Generation (RAG), PostgreSQL, document processing, OCR, and semantic embeddings** to allow users to query employee profiles, teams, projects, and organizational events using natural language.

---

## 🎯 Project Objective

Enterprise information is often distributed across structured databases, resumes, documents, reports, and event records.

GARVIS was designed to provide a unified conversational layer over these different information sources.

Instead of manually searching through databases and documents, users can ask questions in natural language such as:

- "Tell me about employee X."
- "Which department does X work in?"
- "What technologies has X worked with?"
- "Show employees working with Python."
- "What events are scheduled?"
- "Give me details about a particular company event."

GARVIS interprets the query, retrieves relevant structured and unstructured information, and generates a concise response.

---

## ✨ Key Features

### 👤 Employee Intelligence

- Natural-language employee search
- Employee profile retrieval
- Department and position filtering
- Project and technology-stack queries
- Structured employee metadata
- Resume/document-based information retrieval

### 🧠 AI-Powered Query Understanding

GARVIS uses an LLM-based entity extraction layer to identify relevant information from user queries, including:

- Employee name
- Department
- Position
- Project phase
- Technology stack

The extracted entities are then used to dynamically query the underlying data sources.

### 📄 Document Intelligence & RAG

GARVIS processes employee documents and PDFs to retrieve information that may not exist in the structured database.

The ingestion pipeline supports:

- PDF text extraction
- Table extraction
- OCR fallback for scanned documents
- Semantic embeddings
- Vector-based document storage
- LLM-assisted response synthesis

### 🏢 Structured + Unstructured Retrieval

GARVIS combines two forms of organizational knowledge:

**Structured Data**
- Employee records
- Departments
- Positions
- Contact information
- Structured project metadata

**Unstructured Data**
- Resumes
- PDFs
- Employee documents
- Project descriptions
- Additional metadata

This hybrid approach enables more complete responses than using either SQL or document retrieval alone.

### 📅 Event Intelligence

The architecture also supports organizational event information including:

- Event name
- Date
- Status
- Location
- Organiser
- Chief guest
- Attendance/scale
- Event description

### ⚙️ Employee Data Management

The application provides functionality for:

- Employee ingestion
- Structured metadata extraction
- PDF/document ingestion
- Embedding generation
- Employee deletion

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │     User Query       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Streamlit Portal   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ LLM Entity Extractor │
                    │   Groq / Llama 3.1   │
                    └──────────┬───────────┘
                               │
                ┌──────────────┴──────────────┐
                ▼                             ▼
       ┌─────────────────┐          ┌─────────────────┐
       │   PostgreSQL    │          │ Document / RAG  │
       │ Structured Data │          │  Vector Store   │
       └────────┬────────┘          └────────┬────────┘
                │                            │
                └─────────────┬──────────────┘
                              ▼
                   ┌──────────────────────┐
                   │  Response Synthesis  │
                   │    Groq / Llama      │
                   └──────────┬───────────┘
                              ▼
                   ┌──────────────────────┐
                   │    Final Response    │
                   └──────────────────────┘
```

---

## 📥 Data Ingestion Pipeline

```text
Employee Folder
      │
      ├── info.txt
      ├── metadata.txt
      └── Resume / PDF
             │
             ▼
     Document Extraction
             │
       ┌─────┴─────┐
       ▼           ▼
  pdfplumber    Tesseract OCR
                 (fallback)
       │           │
       └─────┬─────┘
             ▼
       Extracted Text
             │
             ▼
       Groq LLM Parser
             │
             ▼
       Structured JSON
             │
      ┌──────┴────────┐
      ▼               ▼
 PostgreSQL       Embeddings
 Structured       Generation
   Tables              │
                       ▼
                 Vector Storage
```

---

## 🛠️ Technology Stack

### AI / LLM
- Groq API
- Llama 3.1
- LangChain
- Sentence Transformers
- Ollama (offline branch)

### Backend & Data
- Python
- PostgreSQL
- SQLAlchemy
- FastAPI
- Pydantic

### Document Processing
- pdfplumber
- PyPDF2
- Tesseract OCR
- pdf2image

### Interface
- Streamlit
- Frontend web application

---

## 📂 Repository Structure

```text
Garvis_GTI/
│
├── data/                 # Sample employee datasets/documents
├── events/               # Sample organizational event data
├── frontend/             # Frontend application
│
├── app.py
├── main.py               # Main Streamlit application
├── config.py             # Model/database configuration
├── ingest.py             # Employee/document ingestion pipeline
├── query_single.py       # Individual employee queries
├── query_overall.py      # Team/company-wide queries
├── query_events.py       # Event-related queries
│
├── requirements.txt
└── README.md
```

---

## 🌿 Repository Branches

### `main`

Primary implementation using **Groq-hosted LLM inference**.

### `gail-official`

Offline-oriented implementation using **Ollama**, designed for environments where organizational information should be processed using locally hosted models.

### `v1`

Earlier development/version branch retained for project history and reference.

---

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/Yash130306/Garvis_GTI.git
cd Garvis_GTI
```

### 2. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
DATABASE_URL=postgresql+psycopg2://username:password@localhost:5432/GTI_2
```

> Never commit your `.env` file or API credentials to version control.

### 5. Configure PostgreSQL

Create/configure the PostgreSQL database required by the application and ensure `DATABASE_URL` points to the correct local database.

### 6. Run the application

```bash
streamlit run main.py
```

---

## 🔐 Data Privacy & Security

This repository is intended as an internship project and demonstration implementation.

The employee profiles and organizational records included for demonstration/testing are primarily **synthetic/sample data**.

A limited number of contributor resumes may be included as project test documents with the respective contributors' permission.

**No confidential GAIL employee database or production organizational dataset is intended to be included in this public repository.**

Sensitive configuration including API keys and database credentials must be provided through environment variables and is excluded from version control using `.gitignore`.

---

## 👥 Project Contributors

Developed collaboratively during the GAIL internship project by:

- **Yash Malhotra**
- **Aditya Bhardwaj**
- **Harsh**

The Git commit history has been preserved to accurately reflect the original contributions and development history of the project.

---

## 🏢 Internship Project

Developed as part of a summer internship at **GAIL (India) Limited**.

The project explores the application of **Generative AI, Retrieval-Augmented Generation, semantic search, document intelligence, and natural-language interfaces** for enterprise information retrieval.

---

## ⚠️ Disclaimer

This repository represents a prototype/internship implementation and is not an official production system of GAIL (India) Limited.

The project is intended for educational, research, demonstration, and internship-evaluation purposes.
