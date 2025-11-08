# Docker Deployment Guide

## Prerequisites

- Docker installed on your system
- Docker Compose (optional, but recommended)
- API keys for Pinecone and Google Gemini

## Option 1: Using Docker Compose (Recommended)

### 1. Build and Run

```bash
# Build the Docker image
docker-compose build

# Start the container
docker-compose up -d

# View logs
docker-compose logs -f

# Stop the container
docker-compose down
```

### 2. Access the Application

Open your browser and navigate to:
```
http://localhost:8080
```

## Option 2: Using Docker Commands

### 1. Build the Docker Image

```bash
docker build -t health-ai-chatbot .
```

### 2. Run the Container

```bash
docker run -d \
  --name health-ai-chatbot \
  -p 8080:8080 \
  -e PINECONE_API_KEY=your_pinecone_api_key \
  -e GOOGLE_API_KEY=your_google_api_key \
  health-ai-chatbot
```

### 3. Using .env file

```bash
docker run -d \
  --name health-ai-chatbot \
  -p 8080:8080 \
  --env-file .env \
  health-ai-chatbot
```

### 4. View Logs

```bash
docker logs -f health-ai-chatbot
```

### 5. Stop the Container

```bash
docker stop health-ai-chatbot
docker rm health-ai-chatbot
```

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
PINECONE_API_KEY=your_pinecone_api_key_here
GOOGLE_API_KEY=your_google_api_key_here
```

## Useful Docker Commands

### Check Container Status
```bash
docker ps
```

### Enter Container Shell
```bash
docker exec -it health-ai-chatbot /bin/bash
```

### View Container Resource Usage
```bash
docker stats health-ai-chatbot
```

### Rebuild After Changes
```bash
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

## Production Deployment

For production deployment, consider:

1. **Use a reverse proxy** (Nginx/Traefik) for SSL/TLS
2. **Set up proper logging** and monitoring
3. **Use Docker secrets** for sensitive data
4. **Configure resource limits**:

```yaml
services:
  medical-chatbot:
    # ... other config
    deploy:
      resources:
        limits:
          cpus: '2'
          memory: 4G
        reservations:
          cpus: '1'
          memory: 2G
```

## Troubleshooting

### Container fails to start
- Check logs: `docker logs health-ai-chatbot`
- Verify environment variables are set correctly
- Ensure port 8080 is not already in use

### Application not responding
- Check if container is running: `docker ps`
- Verify health check status: `docker inspect health-ai-chatbot`
- Check application logs for errors

### Out of memory errors
- Increase Docker memory allocation
- Add resource limits in docker-compose.yml

## Cloud Deployment

### Deploy to AWS ECS
```bash
# Tag and push to ECR
docker tag health-ai-chatbot:latest <account-id>.dkr.ecr.<region>.amazonaws.com/health-ai-chatbot:latest
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/health-ai-chatbot:latest
```

### Deploy to Google Cloud Run
```bash
# Tag and push to GCR
docker tag health-ai-chatbot:latest gcr.io/<project-id>/health-ai-chatbot:latest
docker push gcr.io/<project-id>/health-ai-chatbot:latest

# Deploy
gcloud run deploy health-ai-chatbot \
  --image gcr.io/<project-id>/health-ai-chatbot:latest \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --set-env-vars PINECONE_API_KEY=xxx,GOOGLE_API_KEY=xxx
```

### Deploy to Azure Container Instances
```bash
# Tag and push to ACR
docker tag health-ai-chatbot:latest <registry-name>.azurecr.io/health-ai-chatbot:latest
docker push <registry-name>.azurecr.io/health-ai-chatbot:latest

# Deploy
az container create \
  --resource-group <resource-group> \
  --name health-ai-chatbot \
  --image <registry-name>.azurecr.io/health-ai-chatbot:latest \
  --dns-name-label health-ai-chatbot \
  --ports 8080 \
  --environment-variables PINECONE_API_KEY=xxx GOOGLE_API_KEY=xxx
```
