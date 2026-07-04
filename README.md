# RAG AI PDF Chat App

Live app: https://ragai.buzz

## Overview

This repository contains a full-stack PDF question-answer application with:

- `client/` — Next.js frontend
- `server/` — Express backend for file upload and chat
- `worker.js` — background PDF processing using Redis / BullMQ
- Redis and Qdrant for queueing, embedding storage, and retrieval
- Nginx reverse proxy for production HTTPS and request routing
- `docker-compose.prod.yml` for production deployment

## Quick Start (Local)

1. Create a `.env` file in the repo root:

```env
OPENAI_API_KEY=your_openai_api_key
```

2. Run locally with Docker Compose:

```bash
docker compose up --build
```

3. Open the app:

- Frontend: `http://localhost:3000`
- Server health: `http://localhost:8000`

## Production Deployment (Live Server)

This project includes a production-ready reverse proxy setup using `docker-compose.prod.yml` and `nginx/nginx.conf`.

### 1. Clone the repository on your server

```bash
git clone <your-repo-url>
cd ragAI-pdf
```

### 2. Create a `.env` file on the server

```env
OPENAI_API_KEY=your_openai_api_key
QDRANT_COLLECTION_NAME=langchainjs-testing
```

### 3. Start production services

```bash
docker compose -f docker-compose.prod.yml up --build -d
```

### 4. Use the live site

- `http://<your-server-ip>`
- Configure DNS and HTTPS to use your domain

## Deployment Files

- `.env.example` — environment variable template
- `docker-compose.prod.yml` — production Compose setup
- `nginx/nginx.conf` — public reverse proxy rules

## Notes

- Keep `OPENAI_API_KEY` private.
- For local development, the frontend communicates with the API at `http://localhost:8000`.
- For production, Nginx proxies `/upload/pdf` and `/chat` to the backend and serves the client.
- Uploaded PDFs are saved in `server/uploads`.
- Embedding data is stored in the `qdrant_data` Docker volume.


