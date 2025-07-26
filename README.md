#  Bengali-English RAG Pipeline using Ollama and LangChain

This project implements a **Retrieval-Augmented Generation (RAG)** system that allows you to ask questions in **Bengali or English** based on content extracted from PDF files. It uses **LangChain**, **ChromaDB**, and **Ollama** running a local **Qwen2.5 LLM**.

---

##  Setup Guide

###  Requirements

- Python 3.10+
- Ollama installed
- Model `Qwen2.5` pulled via Ollama

##  Setup Guide

### Tools, Libraries, Packages
- Ollama ( Local LLM runner )
- Qwen2.5	(Multilingual LLM for generation)
- LangChain	(RAG pipeline)
- PyPDFLoader	(PDF content extraction)
- Sentence-Transformers	(Embedding model)
- Chroma	(Vector database)
- PromptTemplate	(Controlled LLM prompt design)

```bash
sudo apt-get install -y curl
curl -fsSL https://ollama.ai/install.sh | sh
pip install ollama
pip install langchain langchain-community langchain-ollama pypdf sentence-transformers chromadb


