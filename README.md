#  Bengali-English RAG Pipeline using Ollama and LangChain

This project implements a **Retrieval-Augmented Generation (RAG)** system that allows you to ask questions in **Bengali or English** based on content extracted from PDF files. It uses **LangChain**, **ChromaDB**, and **Ollama** running a local **Qwen2.5 LLM**.

---

##  Setup Guide

###  Requirements

- Python 3.10+
- Ollama installed
- Model `Qwen2.5` pulled via Ollama

###  Installation

```bash
sudo apt-get install -y curl
curl -fsSL https://ollama.ai/install.sh | sh
pip install ollama
pip install langchain langchain-community langchain-ollama pypdf sentence-transformers chromadb
```

###  Model Setup

```bash
ollama pull Qwen2.5
```

---

##  Tools, Libraries, Packages

| Tool | Purpose |
|------|---------|
| `Ollama` | Local LLM runner |
| `Qwen2.5` | Multilingual LLM for generation |
| `LangChain` | RAG pipeline |
| `PyPDFLoader` | PDF content extraction |
| `Sentence-Transformers` | Embedding model |
| `Chroma` | Vector database |
| `PromptTemplate` | Controlled LLM prompt design |

---

##  Sample Queries and Outputs

###  Input PDF:
> A Bengali literature PDF with biographical details.

###  Sample Query (Bengali):
```
অনুপমের ভাষায় সুপুরুষ কাকে বলা হয়েছে?
```
###  Output:
> সুপুরুষ বলতে তিনি বুঝিয়েছেন সেই ব্যক্তি যে মনের দিক থেকে সুন্দর, চরিত্রবান ও আত্মবিশ্বাসী।

---

###  Sample Query (English):
```
What was Kalyani’s real age during marriage?
```
###  Output:
> At the time of marriage, Kalyani's actual age was around 16, as mentioned in the context.

---

##  API Documentation (If applicable)

Currently, no API is implemented. This project runs as a Jupyter Notebook. A future version may expose an API using FastAPI or Flask.

---

##  Evaluation Matrix (Optional)

| Metric | Description |
|--------|-------------|
| Retrieval Accuracy | How many retrieved chunks were relevant |
| Response Correctness | Manual rating of final answers |
| Query Language Support | Bengali & English |
| Latency | Time from query to response |

---



###  1. What method or library did you use to extract the text, and why?

Used: `LangChain` + `PyPDFLoader`

**Why**: PyPDFLoader is robust and preserves the text on each page. It integrates easily with LangChain and avoids layout-breaking issues.

**Challenge**: As it is a Bangla textbook, initially I was extracting the PDF, but the content could not be read properly. I feel it has inconsistent font encodings. This resulted in slight misformatting in Unicode.

---

###  2. What chunking strategy did you choose?

Used: `RecursiveCharacterTextSplitter` with `chunk_size=1000`, `chunk_overlap=200`

Character-based chunking preserves structure without breaking paragraphs. Overlap ensures continuity for retrieval. It works well for semantic search, especially in multilingual documents.

---

###  3. What embedding model did you use and why?

Used: `sentence-transformers/distiluse-base-multilingual-cased-v1`

**Why**:
- Multilingual: Supports Bengali and English
- Lightweight: Fast for local inference
- Good semantic quality for question-answer tasks

It maps semantically similar sentences to nearby points in vector space.

---

###  4. How are you comparing the query with stored chunks?

Used: Cosine similarity via `Chroma` vector store

It's simple, fast, and effective for semantic vectors. Chroma supports persistence and fast retrieval out of the box.

---

###  5. How do you ensure meaningful comparisons?

- The query is embedded using the same model as the document chunks.
- Prompt explicitly limits the LLM to use only the context (`Answer ONLY from the provided context`).
- If the query is vague, the system may return irrelevant chunks. The LLM is prompted to respond with “I don’t know” if the context is insufficient.

---

###  6. Are the results relevant? If not, what can be improved?

**Mostly yes**, especially when the question is specific.

**To improve this model**:
- Use better OCR/text cleaning for low-quality PDFs
- Test other embedding models
- Tune chunk size and overlap per document type
- There is scope for fine-tuning with advanced models
- Add a reranking step using an LLM to score the relevance of retrieved chunks before answering.
- Models like E5/BGE models are trained specifically for semantic retrieval and QA tasks can be used



---

##  Author

- Badrun Nahar Luna

