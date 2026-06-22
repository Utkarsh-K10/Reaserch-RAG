# Multi-Domain Hybrid RAG Assistant

[![Live Demo](https://img.shields.io/badge/Demo-Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](YOUR_STREAMLIT_APP_URL)
[![Python Version](https://img.shields.io/badge/Python-3.10%2B-green?style=flat-square&logo=python)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-black?style=flat-square)](LICENSE)
An end-to-end, production-ready Retrieval-Augmented Generation (RAG) pipeline engineered to perform high-precision, isolated document retrieval across multiple scientific research domains and distinct academic topics. 
The system implements a **Dynamic Hybrid Search (Dense Semantic + Sparse Lexical)** mechanism to handle both abstract contextual queries and exact technical terminology.

## 🚀 System Architecture

The application bypasses the strict limits of single-index cloud resources by implementing a virtual multi-index architecture leveraging isolated database namespaces. 

    
                                  +-------------------------+
                                  |   Input PDF Documents   |
                                  +------------+------------+
                                               |
                                               v
                                  +-------------------------+
                                  | Recursive Text Chunking |
                                  +------------+------------+
                                               |
                                               v
                     +-------------------------+-------------------------+
                     |                                                   |
                     v                                                   v
        +-------------------------+                         +-------------------------+
        |  Gemini Embeddings API  |                         |   Local BM25 Encoder    |
        |  (text-embedding-004)   |                         |  (Lexical Tokenization) |
        +------------+------------+                         +------------+------------+
                     |                                                   |
                     v                                                   v
        +-------------------------+                         +-------------------------+
        |   Dense Feature Vector  |                         |   Sparse Token Vector   |
        +------------+------------+                         +------------+------------+
                     |                                                   |
                     +-------------------------+-------------------------+
                                               |
                                               v
                                  +-------------------------+
                                  |  Pinecone Vector DB     |
                                  |  (Isolated Namespaces)  |
                                  +------------+------------+
                                               |
                                               v
                                  +-------------------------+
                                  | Hybrid Convex Fusion    |
                                  |  (Dynamic Alpha Blend)  |
                                  +------------+------------+
                                               |
                                               v
                                  +-------------------------+
                                  |    Gemini 1.5 Flash     |
                                  | (System Context Guard)  |
                                  +------------+------------+
                                               |
                                               v
                                  +-------------------------+
                                  |  Streamlit State UI     |
                                  +-------------------------+
                                  

### Key Architectural Highlights
* **Isolated Multi-Tenancy:** Uses **Pinecone Namespaces** to segment multi-domain documents (e.g., Technical Manuals vs. HR Policies) within a single infrastructure footprint, ensuring zero cross-domain data leakage.
* **Dynamic Hybrid Retrieval:** Generates **Dense Vectors** via Gemini `text-embedding-004` alongside **Sparse Vectors** derived from a locally fitted `BM25Encoder`. Queries are executed simultaneously against both vector footprints.
* **Deterministic Alpha Blending:** Integrates an adjustable convex scaling factor ($\alpha$) allowing runtime optimization between lexical matching (exact syntax/error codes) and semantic matching (intent/synonyms).
* **Deterministic Guardrails:** Implements specific system formatting instructions at the LLM integration layer (`gemini-1.5-flash`) to strictly suppress hallucinations and force fallback bounds when context is missing.

---

## 🛠️ Tech Stack & Infrastructure

* **Language:** Python 3.10+
* **Vector Database:** Pinecone (Serverless / Starter Core)
* **LLM & Embeddings:** Google Gemini API (`gemini-1.5-flash`, `text-embedding-004`)
* **Orchestration & UI:** Streamlit (State-managed session history)
* **Lexical Indexing:** `pinecone-text` utilities (Local text corpus serialization)

---

## 💻 Local Installation & Setup

1. **Clone the Repository:**
```bash
git clone https://github.com/Utkarsh-K10/Reaserch-RAG.git
cd Reaserch-RAG
```

2. **Establish Environment Isolation:**
```bash
python -bin venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

```


3. **Install Core Dependencies:**
```bash
pip install -r requirements.txt

```


4. **Configure Environment Secret Arrays:**
Create a `.env` file in the root root directory:
```env
GEMINI_API_KEY="your_google_gemini_api_key"
PINECONE_API_KEY="your_pinecone_api_key"

```


5. **Execute the Application Server:**
```bash
streamlit run app.py

```



---

## ⚙️ Production Deployment Portfolio

This pipeline is fully containerized and deployed natively using a secure cloud stack:

* **Host Platform:** Hugging Face Spaces / Streamlit Community Cloud
* **Secret Isolation:** Environment encryption via cloud platform keystores (`os.getenv`)
* **State Preservation:** Uses Streamlit session context objects to persist conversations without maintaining a costly database state layer.

---

## 💡 Production Trade-offs & Engineering Choices

* **Why Namespaces over Multiple Indexes?** To optimized infrastructure utility on budget constraints. Namespaces provide clean $\mathcal{O}(1)$ isolation profiles within a single physical index partition.
* **Why Flash over Pro?** `gemini-1.5-flash` was selected for its superior sub-second inference latency profiles and high token throughput efficiency, making it highly optimal for production RAG context completion.
* **Persistent BM25 Serialization:** The lexical analyzer caches state locally using `.dump()`/`.load()` routines to maintain statistical relevance rankings across arbitrary container recycles.

---

## 📬 Contact & Professional Profile

I am an engineer focused on scalable backend system architectures, clean data pipelining, and generative AI integration frameworks.

* **LinkedIn:** (https://www.linkedin.com/in/utk10/)
* **Email:** `utkarshkushwah9@gmail.com`
