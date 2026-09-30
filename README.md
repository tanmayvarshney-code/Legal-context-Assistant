# ⚖️ Legal RAG Assistant

A **Retrieval-Augmented Generation (RAG)** based legal document assistant that allows users to upload legal PDF documents and ask questions using natural language.

The application extracts text from uploaded PDFs, splits the content into chunks, generates embeddings using **Azure OpenAI**, stores them in a **FAISS vector database**, retrieves relevant document sections, and generates contextual responses through an AI assistant.

---

## 🚀 Features

- Upload and process legal PDF documents
- Extract text from PDFs using **PyMuPDF**
- Split documents into manageable text chunks
- Generate vector embeddings using **Azure OpenAI**
- Store and retrieve embeddings using **FAISS**
- Perform semantic similarity search
- Generate document-grounded answers using **RAG**
- Interactive web interface built with **Streamlit**
- AI agent integration using **AutoGen**
- Retrieve the most relevant legal context for user queries

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core programming language |
| **Streamlit** | Interactive web interface |
| **LangChain** | Document processing and RAG pipeline |
| **Azure OpenAI** | Embeddings and AI response generation |
| **FAISS** | Vector database and similarity search |
| **AutoGen** | AI agent orchestration |
| **PyMuPDF** | PDF text extraction |
| **Python-dotenv** | Environment variable management |

---

## 📁 Project Structure

```text
legal-rag-assistant/
│
├── app.py
├── main_chat.py
├── rag_index_builder.py
├── tools.py
├── requirements.txt
├── README.md
├── .gitignore
├── .env.example
│
└── docs/
    └── sample_rental_agreement.pdf
```

> The `.env` file and generated `rag_faiss_store/` directory are excluded from GitHub using `.gitignore`.

---

## 🧠 How It Works

The application follows a **Retrieval-Augmented Generation (RAG)** pipeline:

```text
              ┌──────────────────────┐
              │     PDF Upload       │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │   Text Extraction    │
              │      PyMuPDF         │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │    Text Chunking     │
              │      LangChain       │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │ Azure OpenAI         │
              │ Embeddings           │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │  FAISS Vector Store  │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │ Semantic Similarity  │
              │       Search         │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │ Relevant Document    │
              │       Context        │
              └──────────┬───────────┘
                         ↓
              ┌──────────────────────┐
              │   AI Agent Response  │
              └──────────────────────┘
```

### RAG Workflow

1. The user uploads a legal PDF document.
2. **PyMuPDF** extracts text from the uploaded PDF.
3. LangChain's `RecursiveCharacterTextSplitter` divides the extracted text into smaller chunks.
4. **Azure OpenAI Embeddings** convert the chunks into vector representations.
5. **FAISS** stores the generated vectors.
6. The user enters a legal question.
7. FAISS performs a similarity search to retrieve the most relevant document chunks.
8. The retrieved legal context is provided to the AI assistant.
9. The assistant generates a contextual response based on the retrieved document information.

---

## ⚙️ Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/tanmayvarshney-code/Legal-context-Assistant.git
```

Navigate to the project directory:

```bash
cd Legal-context-Assistant
```

---

### 2. Create a Virtual Environment

```bash
python -m venv myenv
```

### 3. Activate the Virtual Environment

#### Windows

```bash
myenv\Scripts\activate
```

#### macOS/Linux

```bash
source myenv/bin/activate
```

---

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

The project uses packages including:

- `openai`
- `langchain`
- `langchain_community`
- `langchain_openai`
- `faiss-cpu`
- `autogen`
- `pymupdf`
- `tiktoken`
- `python-dotenv`
- `streamlit`

---

## 🔐 Environment Variables

Create a `.env` file in the root directory of the project.

```env
AZURE_OPENAI_API_KEY=your_azure_openai_api_key
AZURE_OPENAI_ENDPOINT=your_azure_openai_endpoint
AZURE_OPENAI_API_VERSION=your_api_version
AZURE_OPENAI_EMBEDDING_DEPLOYMENT=text-embedding-3-small
AZURE_OPENAI_CHAT_DEPLOYMENT=your_chat_deployment
```

> ⚠️ **Never upload your real `.env` file, API keys, or credentials to GitHub.**

A `.env.example` file can be included in the repository to show the required variables without exposing credentials.

---

## ▶️ Run the Application

Make sure the virtual environment is activated.

Then run:

```bash
streamlit run app.py
```

Streamlit will display a local URL, usually:

```text
http://localhost:8501
```

Open it in your browser to use the application.

---

## 💬 Example Usage

### Upload

Upload a legal PDF such as a rental agreement.

### Ask Questions

For example:

```text
Are pets allowed in the property?
```

or:

```text
What are the conditions for terminating the agreement?
```

The application searches the uploaded document for relevant information and generates a contextual response.

---

## 🔍 Vector Search

The application uses **FAISS similarity search** to retrieve the most relevant document chunks.

The retrieval pipeline searches for the top relevant chunks before providing context to the AI assistant.

```python
docs = db.similarity_search(query, k=3)
```

This helps the model answer questions using information retrieved from the uploaded document instead of relying only on the language model.

---

## 📸 Project UI

### Legal RAG Assistant

<img width="934" alt="Legal RAG Assistant UI" src="https://github.com/user-attachments/assets/3eabb1ac-625c-4ee0-97fb-b6e3d970538d" />

The Streamlit interface allows users to:

- Upload a legal PDF
- Build the FAISS vector index
- Enter legal questions
- Receive AI-generated contextual responses
- View the agent conversation history

---

## 🔒 Security

Sensitive configuration values are stored using environment variables.

The following files/directories should not be committed:

```gitignore
.env
myenv/
.venv/
rag_faiss_store/
__pycache__/
```

Never hard-code API keys directly into the source code.

---

## 🔮 Future Improvements

Potential improvements include:

- Support for multiple PDF documents
- Conversation memory for follow-up questions
- Source citations with page numbers
- Improved document metadata handling
- Support for DOCX and TXT documents
- Hybrid keyword + vector search
- Reranking retrieved documents
- Improved error handling
- Cloud deployment
- User authentication

---

## ⚠️ Disclaimer

This project is intended for **educational and demonstration purposes only**.

The responses generated by the application should **not be considered professional legal advice**. Users should consult a qualified legal professional for legal guidance.

---

## 👨‍💻 Author

**Tanmay Varshney**

- [GitHub](https://github.com/tanmayvarshney-code)
- [LinkedIn](https://www.linkedin.com/in/tanmay-varshney-785746332)

---

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.