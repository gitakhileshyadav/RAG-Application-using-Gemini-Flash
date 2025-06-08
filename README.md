# RAG Application using Gemini Flash

A Retrieval-Augmented Generation (RAG) application built with LangChain, Google's Gemini Flash, and Streamlit that allows users to ask questions about PDF documents and get AI-powered answers based on the document content.

## Features

- 📄 **PDF Document Processing**: Automatically loads and processes PDF documents
- 🔍 **Intelligent Chunking**: Splits documents into manageable chunks for better retrieval
- 🧠 **Vector Embeddings**: Uses Google's embedding model for semantic search
- 🚀 **Fast Retrieval**: FAISS vector store for efficient similarity search
- 💬 **Interactive Chat**: Streamlit-powered chat interface
- ⚡ **Powered by Gemini**: Uses Google's Gemini 2.0 Flash model for responses

## Prerequisites

- Python 3.8 or higher
- Google API Key (for Gemini Flash and embeddings)
- Ubuntu/Linux system (for installation instructions)

## Installation

### 1. System Dependencies
```bash
sudo apt update && sudo apt install -y python3 python3-pip python3-venv python3-dev build-essential sqlite3 libsqlite3-dev
```

### 2. Virtual Environment Setup
```bash
# Create virtual environment
python3 -m venv ai_project_env

# Activate virtual environment
source ai_project_env/bin/activate

# Upgrade pip
pip install --upgrade pip
```

### 3. Install Python Dependencies
```bash
# Install all required packages
pip install pysqlite3-binary python-dotenv streamlit sentence-transformers unstructured langchain langchain-community langchain-google-genai langchain-experimental langchainhub faiss-cpu pypdf
```

## Configuration

### 1. Environment Variables
Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

To get a Google API key:
1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create or select a project
3. Generate an API key
4. Copy the key to your `.env` file

### 2. PDF Document
Place your PDF document in the project root and name it `source_file.pdf`, or modify the filename in the code:

```python
loader = PyPDFLoader("your_document.pdf")
```

## Usage

### 1. Activate Virtual Environment
```bash
source ai_project_env/bin/activate
```

### 2. Run the Application
```bash
streamlit run app.py
```

### 3. Access the Application
Open your browser and navigate to `http://localhost:8501`

### 4. Ask Questions
Use the chat input at the bottom of the page to ask questions about your PDF document.

## Project Structure

```
rag-gemini/
├── ai_project_env/          # Virtual environment
├── app.py                   # Main application file
├── .env                     # Environment variables (create this)
├── my_paper.pdf            # Your PDF document
├── requirements.txt        # Python dependencies (optional)
└── README.md              # This file
```

## How It Works

1. **Document Loading**: PyPDFLoader extracts text from the PDF document
2. **Text Splitting**: RecursiveCharacterTextSplitter breaks the document into chunks
3. **Embeddings**: Google's embedding model converts text chunks into vectors
4. **Vector Storage**: FAISS stores and indexes the embeddings for fast retrieval
5. **Query Processing**: User questions are embedded and matched against document chunks
6. **Answer Generation**: Gemini Flash generates contextual answers based on retrieved chunks

## Customization

### Modify Chunk Size
```python
text_splitter = RecursiveCharacterTextSplitter(chunk_size=1500)  # Adjust chunk size
```

### Change Retrieval Parameters
```python
retriever = vectorstore.as_retriever(
    search_type="similarity", 
    search_kwargs={"k": 5}  # Adjust number of retrieved chunks
)
```

### Modify System Prompt
```python
system_prompt = (
    "Your custom system prompt here..."
    "{context}"
)
```

### Switch Gemini Model
```python
llm = ChatGoogleGenerativeAI(
    model="gemini-2.0-flash",  # or "gemini-pro"
    temperature=0.3,     # Adjust creativity
    max_tokens=1000      # Adjust response length
)
```

## Troubleshooting

### Common Issues

**1. SQLite3 Version Error**
The code includes a fix for SQLite3 version conflicts. If you still encounter issues:
```python
import sys
try:
    import pysqlite3 as sqlite3
    sys.modules['sqlite3'] = sqlite3
except ImportError:
    import sqlite3
```

**2. Google API Key Error**
- Ensure your `.env` file is in the project root
- Verify your API key is valid and has the necessary permissions
- Check that you've enabled the Gemini API in Google Cloud Console

**3. PDF Loading Error**
- Ensure your PDF file exists in the specified path
- Try with a different PDF if the current one is corrupted
- Install additional PDF processing libraries if needed:
```bash
pip install pymupdf  # Alternative PDF reader
```

**4. Memory Issues**
For large documents, consider:
- Reducing chunk size
- Limiting the number of retrieved chunks (k parameter)
- Using a more powerful machine

## Dependencies

### Core Libraries
- `langchain`: LLM application framework
- `langchain-community`: Community components
- `langchain-google-genai`: Google Gemini integration
- `streamlit`: Web application framework
- `faiss-cpu`: Vector similarity search
- `python-dotenv`: Environment variable management

### Supporting Libraries
- `pypdf`: PDF processing
- `sentence-transformers`: Text embeddings
- `pysqlite3-binary`: SQLite3 compatibility

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [LangChain](https://langchain.com/) for the RAG framework
- [Google AI](https://ai.google/) for Gemini Pro and embedding models
- [Streamlit](https://streamlit.io/) for the web interface
- [FAISS](https://github.com/facebookresearch/faiss) for vector search

## Support

If you encounter any issues or have questions:
1. Check the troubleshooting section above
2. Open an issue on GitHub
3. Refer to the [LangChain documentation](https://docs.langchain.com/)
4. Check [Google AI documentation](https://ai.google.dev/docs)

---
