# AI Agent with MCP Integration

> **⚠️ Note:** Docker setup is available but not recommended. Follow manual setup below.

## 📋 Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (installed and running)
- [LM Studio](https://lmstudio.ai/) (with model downloaded and server started)
- Node.js and npm
- Python 3.8+

## 🚀 Quick Start

### 1. Environment Setup

Create `.env` in the `todo-list` directory:

```bash
# PostgreSQL Settings
POSTGRES_USER=appuser
POSTGRES_PASSWORD=a-strong-password
POSTGRES_DB=todo_db

# Docker Host IP
DOCKER_HOST_IP=host.docker.internal
LIVEKIT_API_KEY=devkey
LIVEKIT_API_SECRET=secret
```

### 2. Start Services

Run these commands in **separate terminals**:

**Terminal 1: LiveKit server**
```bash
livekit-server --dev
```

**Terminal 2: Infrastructure (database)**
```bash
docker compose -f compose.infra.yml up --build
```

**Terminal 3: Backend API**
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 4: Frontend**
```bash
cd frontend
npm install
npm run dev
```

### 3. Access Application

Open browser: http://localhost:5173

## 🛠️ Technology Stack

| Component | Technology |
|-----------|------------|
| **Backend** | Python/FastAPI |
| **Frontend** | React/TypeScript/Vite |
| **Database** | PostgreSQL |
| **Real-Time** | WebRTC with LiveKit |
| **AI** | LM Studio |
| **Containers** | Docker/Docker Compose |

## 🔧 Development Commands

### Database migrations
```bash
alembic revision --autogenerate -m "Create initial todo_lists and todo_items tables"
alembic upgrade head
```

### Docker operations
```bash
# Start with dev overrides
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up --build

# Stop and remove
docker-compose -f docker-compose.yml -f docker-compose.dev.yml down
```

### Audio conversion (macOS)
```bash
say -o speech.aiff "Create a new list called shopping"
ffmpeg -i speech.aiff -acodec libmp3lame -q:a 2 input.mp3
rm speech.aiff
```

---

## 📚 Legacy Version

Previous voice API implementation: [echo-voiceapi](https://github.com/fady17/echo-voiceapi/)