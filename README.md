# Notes Chatbot 🤖

A personal AI-powered knowledge base chatbot built with **RAG (Retrieval-Augmented Generation)**. Ask questions about your own notes and get intelligent, context-aware answers — powered by **Google Gemini** and **LangChain**.

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-2.x-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![LangChain](https://img.shields.io/badge/LangChain-RAG-1C3C3C?style=for-the-badge)](https://www.langchain.com)
[![Gemini](https://img.shields.io/badge/Google_Gemini-Flash-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev)
[![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📌 What is this?

**Notes Chatbot** is a local RAG system that turns your `.txt` notes into a searchable, conversational knowledge base. Instead of Ctrl+F-ing through files, you can **ask natural language questions** and get precise, markdown-formatted answers drawn directly from your notes.

- 🔍 **Semantic search** over your personal notes using FAISS vector store
- 🧠 **Google Gemini 1.5 Flash** as the reasoning LLM
- 💬 **Chat interface** served locally via Flask
- 📝 **Markdown rendering** for clean, formatted responses

---

## 🗂️ Project Structure

```
Notes_Chatbot/
├── App2.py              ← Main Flask app + RAG pipeline
├── index.html           ← Chat frontend (served from Flask)
├── index.faiss          ← Pre-built FAISS vector index
├── index.pkl            ← LangChain docstore (paired with FAISS)
├── Leave Rules.txt      ← Sample notes file
├── ideas.txt            ← Sample notes file
├── tasks.txt            ← Sample notes file
└── README.md
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| **Web Framework** | Flask |
| **LLM** | Google Gemini 1.5 Flash (`gemini-1.5-flash-latest`) |
| **Embeddings** | Google Generative AI Embeddings (`embedding-001`) |
| **Vector Store** | FAISS (`faiss-cpu`) |
| **RAG Pipeline** | LangChain (`langchain`, `langchain-community`, `langchain-core`) |
| **Text Rendering** | `markdown` (Python) |
| **Document Loading** | `DirectoryLoader` (`.txt` files) |

---

## ⚙️ How it Works

```
Your .txt notes
     │
     ▼
DirectoryLoader → RecursiveCharacterTextSplitter (chunk_size=1000, overlap=200)
     │
     ▼
Google Embedding-001 → FAISS Vector Store (saved locally)
     │
     ▼
User Question → Retriever → Top-K relevant chunks
     │
     ▼
Gemini 1.5 Flash → Markdown-formatted answer
     │
     ▼
Flask Web UI → Rendered HTML response
```

---

## 🚀 Setup & Running

### Prerequisites
- Python 3.8+
- A [Google AI API Key](https://aistudio.google.com/app/apikey)

### Step 1 — Clone the repository
```bash
git clone https://github.com/SnehaTanwar006/Notes_Chatbot.git
cd Notes_Chatbot
```

### Step 2 — Create & activate a virtual environment
```bash
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
```

### Step 3 — Install dependencies
```bash
pip install -r requirements.txt
```

### Step 4 — Add your Google API Key
In `App2.py`, find this line and replace with your actual key:
```python
os.environ["GOOGLE_API_KEY"] = "your-actual-api-key-here"
```
> 💡 **Tip:** For better security, set it as an environment variable: `export GOOGLE_API_KEY=your-key`

### Step 5 — Add your notes
Create a `notes/` folder and drop in your `.txt` files:
```bash
mkdir notes
# Then add your .txt files into notes/
```
> The chatbot will automatically build a new vector index from your notes on first run.

### Step 6 — Run the app
```bash
python App2.py
```

### Step 7 — Open in browser
Visit `http://localhost:5000` and start asking questions about your notes!

---

## 💬 Usage Example

**Your notes contain:** `"Project deadline is July 15. Team meeting every Monday at 10 AM."`

**You ask:** `"When is the project due?"`

**Bot answers:** *"Based on your notes, the project deadline is **July 15**. The team also meets every Monday at 10 AM."

---

## 📦 Dependencies (`requirements.txt`)

```
flask
langchain
langchain-community
langchain-google-genai
langchain-core
faiss-cpu
markdown
google-generativeai
```

---

## 🔒 Security Note
Never hardcode API keys in production. Use environment variables or a `.env` file (add `.env` to `.gitignore`).

---

## 📄 License
MIT — see [LICENSE](LICENSE).

---
*Built with ❤️ by [Sneha Tanwar](https://github.com/SnehaTanwar006)*
