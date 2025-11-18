# ICF Automation RAG Tool

An experimental prototype that generates **country-specific informed consent form (ICF) drafts** from long clinical trial protocols using **Retrieval-Augmented Generation (RAG)**.

> ⚠️ This repository uses **only synthetic, fake data** and is intended for educational and prototyping purposes. It is **not** a production or regulatory-approved system.

---

## 🔍 What it does

- Ingests a (toy) clinical trial protocol (`data/sample_protocol.pdf`)
- Extracts and chunks relevant sections (e.g. risks, procedures, visits)
- Uses embeddings + vector search (FAISS or similar) to retrieve protocol snippets
- Combines protocol snippets with an ICF template + simple "country rules"
- Generates draft ICF sections via an LLM (locally or via API)
- Shows results in a simple UI (Streamlit demo)

---

## 🧠 Architecture

**Pipeline:**

1. **Ingestion** – load protocol + template
2. **Parsing** – basic rule/marker-based extraction (e.g. headings, keywords)
3. **Chunking & Embedding** – create text chunks, embed in a vector index
4. **Retrieval** – for each ICF section, pull relevant protocol chunks
5. **Generation** – call an LLM with a controlled prompt
6. **Assembly** – combine all generated sections into a draft ICF

See `docs/examples.md` for example prompts and outputs.

---

## 🧰 Tech Stack

- Python
- Streamlit (UI)
- FAISS or sentence-transformers (embeddings & retrieval)
- PyPDF2 / pdfplumber (protocol parsing)
- Any LLM backend (OpenAI, local model, etc. – abstracted)

---

## 🚀 Getting Started

```bash
git clone https://github.com/<your-username>/icf-automation-rag.git
cd icf-automation-rag

python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate on Windows

pip install -r requirements.txt
streamlit run app/main.py
