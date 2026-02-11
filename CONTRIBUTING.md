# Contributing to Legendary AI DevOps RAG API

Thank you for your interest in contributing! Here's how you can help:

## Development Setup

```bash
# Clone repository
git clone https://github.com/vteeparty/rag-api.git
cd rag-api

# Create virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install dependencies
pip install -r requirements.txt

# Start Ollama
ollama serve

# In another terminal, run app
python -m uvicorn app.main:app --reload
```

## Code Style

- Follow PEP 8
- Use type hints
- Run `black app` and `flake8 app` before committing

## Testing

```bash
pytest --cov=app
```

## Pull Request Process

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing`)
5. Open Pull Request

## Report Issues

Use [GitHub Issues](https://github.com/vteeparty/rag-api/issues) to report bugs.
