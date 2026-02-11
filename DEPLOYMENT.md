# Deployment Guide

## Local Deployment

### Prerequisites
- Python 3.9+
- Ollama installed

### Steps

1. **Clone and setup**
   ```bash
   git clone https://github.com/vteeparty/rag-api.git
   cd rag-api
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

2. **Start Ollama**
   ```bash
   ollama pull tinyllama
   ollama serve
   ```

3. **Run application**
   ```bash
   python -m uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

## Docker Deployment

### Build and Run

```bash
# Build image
docker build -t rag-api:latest .

# Run container
docker run -p 8000:8000 \
  -e OLLAMA_HOST=http://host.docker.internal:11434 \
  rag-api:latest
```

### Docker Compose

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## Kubernetes Deployment

See `k8s/deployment.yaml` for Kubernetes manifests.

```bash
kubectl apply -f k8s/deployment.yaml
kubectl port-forward svc/rag-api 8000:8000
```

## Production Checklist

- [ ] Set `ENVIRONMENT=production`
- [ ] Configure proper logging
- [ ] Set up monitoring and alerting
- [ ] Use strong secrets management
- [ ] Enable CORS only for trusted origins
- [ ] Set up rate limiting
- [ ] Configure backup strategy for ChromaDB
- [ ] Test failover procedures
