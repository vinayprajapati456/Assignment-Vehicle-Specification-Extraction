# 🚗 Vehicle Specification Extraction — RAG Pipeline (with OpenRouter)

This repository implements a complete **RAG (Retrieval-Augmented Generation)** pipeline to extract structured **vehicle specifications** (torque values, fluid capacities, part numbers, etc.) from automotive service manuals.

It uses:

### 🔍 Retrieval  
- **Sentence-Transformers** (local embeddings)  
- **FAISS** (vector similarity search)

### 🤖 Optional LLM Extraction (via OpenRouter)  
- Supports any OpenRouter model (GPT-4o-mini, Llama-3.1, Mixtral, etc.)  
- Produces clean structured JSON outputs

### 🔧 Offline Fallback (No API Required)  
- Regex-based heuristic extractor  
- Ensures the pipeline **always returns results**

---

## 🚀 Features

### ✅ Local (Free) Mode  
- Extract PDF text using PyMuPDF  
- Clean + chunk text  
- Embed with all-MiniLM-L6-v2  
- Build FAISS semantic index  
- Retrieve best-matching chunks  
- Extract specs using regex heuristics  

### 🤖 Enhanced Mode (with LLM)
Set your OpenRouter key:

```
export OPENROUTER_API_KEY="your_key_here"
```

You get:
- High-precision JSON extraction  
- Better component labeling  
- Improved accuracy  

### 🔄 Auto-Fallback  
If no key is found → automatically switches to regex mode.

---

# 📁 Repository Structure

```
spec_extraction/
│
├── notebooks/
│   └── spec_extraction_optionB_detailed.ipynb
│
├── src/
│   ├── pipeline.py
│   ├── utils.py
│   └── __init__.py
│
├── faiss_index/
│
├── requirements.txt
└── README.md
```

---

# 🛠 Installation

Clone:

```bash
git clone https://github.com/your-username/spec-extraction.git
cd spec-extraction
```

Install:

```bash
pip install -r requirements.txt
```

---

# 📓 Usage (Google Colab Recommended)

Open:

```
notebooks/spec_extraction_optionB_detailed.ipynb
```

Build FAISS index:

```python
model, index, meta = build_pipeline(PDF_PATH)
```

Run a query:

```python
query_pipeline("Torque for brake caliper bolts")
```

---

# 🤖 Enable OpenRouter for Better Extraction

```python
import os
os.environ["OPENROUTER_API_KEY"] = "your-key-here"
```

---

# 🔄 Fallback Logic

| Condition        | Extraction Mode      |
|------------------|-----------------------|
| API key present  | LLM JSON extraction   |
| API key missing  | Regex heuristic       |

---

# 📚 Notes

- `faiss_index/` is generated after running the notebook  
- Full implementation lives inside the notebook  
