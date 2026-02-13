# RAG API

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![Python 3.11](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104.1-009688.svg)](https://fastapi.tiangolo.com)

AI-powered RAG (Retrieval-Augmented Generation) API for intelligent document retrieval and question answering. Built with FastAPI, ChromaDB, Ollama, and LangChain.

## 🚀 Features

- **Document Management**: Upload, store, and manage documents in a vector database
- **Intelligent Retrieval**: Semantic search using sentence transformers embeddings
- **Question Answering**: Context-aware responses powered by local LLMs via Ollama
- **RESTful API**: Clean and intuitive API endpoints built with FastAPI
- **Vector Storage**: Efficient document storage using ChromaDB
- **Docker Support**: Fully containerized application with Docker Compose
- **Production Ready**: Health checks, logging, and monitoring built-in

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Docker** (20.10+) and **Docker Compose** (2.0+)
- **Python** 3.11+ (for local development)
- **Git**

## 🛠️ Tech Stack

- **Framework**: FastAPI 0.104.1
- **Vector Database**: ChromaDB 0.4.14
- **LLM Integration**: Ollama 0.0.11
- **Embeddings**: Sentence Transformers 2.2.2
- **Orchestration**: LangChain 0.0.350
- **Web Server**: Uvicorn
- **Containerization**: Docker & Docker Compose

## 📦 Installation

### Using Docker (Recommended)

1. **Clone the repository**
```bash
git clone https://github.com/vteeparty/rag-api.git
cd rag-api
```

2. **Create environment file**
```bash
cp .env.example .env
```

3. **Configure environment variables** (optional)
Edit `.env` file to customize settings:
```env
ENVIRONMENT=production
OLLAMA_HOST=http://ollama:11434
OLLAMA_MODEL=tinyllama
CHROMA_DB_PATH=./chroma_db
```

4. **Start the application**
```bash
docker-compose up -d
```

5. **Verify installation**
```bash
# Check if services are running
docker-compose ps

# View logs
docker-compose logs -f
```

The API will be available at `http://localhost:8000`

### Local Development Setup

1. **Clone and navigate to the repository**
```bash
git clone https://github.com/vteeparty/rag-api.git
cd rag-api
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up Ollama**
```bash
# Install Ollama (visit https://ollama.ai for instructions)
# Pull the model
ollama pull tinyllama
```

5. **Create and configure .env file**
```bash
cp .env.example .env
# Edit .env with your local settings
```

6. **Run the application**
```bash
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

## 🚦 Quick Start

### 1. Check API Health
```bash
curl http://localhost:8000/health
```

### 2. Upload a Document
```bash
curl -X POST "http://localhost:8000/documents" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Your document content here",
    "metadata": {"source": "example.txt"}
  }'
```

### 3. Query the System
```bash
curl -X POST "http://localhost:8000/query" \
  -H "Content-Type: application/json" \
  -d '{
    "question": "What is this document about?",
    "max_results": 5
  }'
```

### 4. Access API Documentation
Open your browser and navigate to:
- **Interactive Docs**: http://localhost:8000/docs
- **Alternative Docs**: http://localhost:8000/redoc

## 📖 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/health` | Health check endpoint |
| POST | `/documents` | Upload and store a document |
| GET | `/documents` | List all documents |
| GET | `/documents/{id}` | Get specific document |
| DELETE | `/documents/{id}` | Delete a document |
| POST | `/query` | Query documents with a question |
| POST | `/embed` | Generate embeddings for text |

## 🔧 Configuration

### Environment Variables

Key configuration options in `.env`:

```env
# Application Settings
ENVIRONMENT=development          # development, staging, production
DEBUG=true                       # Enable debug mode
HOST=0.0.0.0                     # Server host
PORT=8000                        # Server port

# Ollama Configuration
OLLAMA_HOST=http://localhost:11434  # Ollama service URL
OLLAMA_MODEL=tinyllama               # Model to use (tinyllama, llama2, etc.)

# ChromaDB Configuration
CHROMA_DB_PATH=./chroma_db       # Path for vector database
COLLECTION_NAME=documents        # Collection name in ChromaDB

# Model Configuration
EMBEDDING_MODEL=all-MiniLM-L6-v2  # Sentence transformer model
MAX_DOCS_QUERY=5                  # Max documents to retrieve per query

# Logging
LOG_LEVEL=INFO                    # DEBUG, INFO, WARNING, ERROR
```

### Supported Ollama Models

You can use any model supported by Ollama:
- `tinyllama` (lightweight, fast)
- `llama2` (balanced)
- `mistral` (powerful)
- `codellama` (code-focused)

Pull a model:
```bash
docker-compose exec ollama ollama pull <model-name>
```

## 🧪 Testing

### Run Tests
```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Run specific test file
pytest tests/test_api.py
```

### Run Code Quality Checks
```bash
# Format code
black app/

# Lint code
flake8 app/

# Type checking
mypy app/
```

## 📁 Project Structure

```
rag-api/
│
├── app/                    # Application source code
│   ├── __init__.py
│   ├── main.py            # FastAPI application
│   ├── models/            # Pydantic models
│   ├── routers/           # API route handlers
│   ├── services/          # Business logic
│   └── utils/             # Utility functions
│
├── tests/                  # Test suite
│   ├── __init__.py
│   └── test_*.py
│
├── chroma_db/             # Vector database storage (created at runtime)
├── logs/                  # Application logs (created at runtime)
│
├── .env.example           # Example environment variables
├── .gitignore            # Git ignore rules
├── CONTRIBUTING.md       # Contribution guidelines
├── DEPLOYMENT.md         # Deployment instructions
├── Dockerfile            # Docker image definition
├── docker-compose.yml    # Docker Compose configuration
├── LICENSE               # MIT License
├── pytest.ini            # Pytest configuration
├── README.md             # This file
└── requirements.txt      # Python dependencies
```

## 🚀 Deployment

For detailed deployment instructions, see [DEPLOYMENT.md](DEPLOYMENT.md).

### Quick Deploy with Docker

```bash
# Production build
docker-compose -f docker-compose.yml up -d --build

# View logs
docker-compose logs -f rag-api

# Stop services
docker-compose down
```

### Kubernetes Deployment

Refer to [DEPLOYMENT.md](DEPLOYMENT.md) for Kubernetes manifests and Helm charts.

## 🐛 Troubleshooting

### Common Issues

**Issue**: Ollama service not starting
```bash
# Check Ollama logs
docker-compose logs ollama

# Restart Ollama service
docker-compose restart ollama
```

**Issue**: Database connection errors
```bash
# Clear ChromaDB data
rm -rf chroma_db/

# Restart services
docker-compose restart
```

**Issue**: Model not found
```bash
# Pull the model manually
docker-compose exec ollama ollama pull tinyllama
```

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [FastAPI](https://fastapi.tiangolo.com/) - Modern web framework
- [ChromaDB](https://www.trychroma.com/) - Vector database
- [Ollama](https://ollama.ai/) - Local LLM runtime
- [LangChain](https://python.langchain.com/) - LLM orchestration
- [Sentence Transformers](https://www.sbert.net/) - Embedding models

## 📞 Support

For questions, issues, or suggestions:
- **Issues**: [GitHub Issues](https://github.com/vteeparty/rag-api/issues)
- **Discussions**: [GitHub Discussions](https://github.com/vteeparty/rag-api/discussions)

## 🗺️ Roadmap

- [ ] Add support for PDF and document parsing
- [ ] Implement authentication and authorization
- [ ] Add streaming responses
- [ ] Support for multiple embedding models
- [ ] Web UI for document management
- [ ] Advanced search filters
- [ ] Multi-language support
- [ ] Performance monitoring dashboard

---

**Made with ❤️ by [vteeparty](https://github.com/vteeparty)**
