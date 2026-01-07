# Aria

**AI Reasoning Investigation Assistant**

An AI-powered IT Service Management platform with intelligent workflow orchestration, Kepner-Tregoe investigation methodology, and Bayesian reasoning.

## Quick Start

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (Docker Desktop on Windows/Mac)
- [Docker Compose](https://docs.docker.com/compose/install/) (included in Docker Desktop)
- **Local LLM** - [Ollama](https://ollama.ai/) with Qwen 2.5 7B recommended:
  ```bash
  ollama pull qwen2.5:7b
  ```

### Installation

```bash
# Clone the repository
git clone https://github.com/dx111ge/aria.git
cd aria

# Copy environment file
cp .env.example .env

# Start Aria
docker compose -f docker-compose.prod.yml up -d
```

**That's it!** All images are pre-built on Docker Hub - no build required.

- Frontend: http://localhost:3001
- Backend API: http://localhost:8001

### Stop Aria

```bash
docker compose -f docker-compose.prod.yml down
```

### Reset Data

```bash
docker compose -f docker-compose.prod.yml down -v
```

## Architecture

```
                    User Interaction
                          |
                          v
+----------------------------------------------------------+
|                    CHAT MODULE                            |
|         Primary interface - voice-ready                   |
+----------------------------------------------------------+
                          |
                          v
+----------------------------------------------------------+
|                    ORCHESTRATOR                           |
|    Coordinates workflow, manages conversation state       |
+----------------------------------------------------------+
                          |
                          v
+----------------------------------------------------------+
|               WORKFLOW BLUEPRINT                          |
|     Data-driven tree structure (nodes, edges, decisions)  |
+----------------------------------------------------------+
                          |
                          v
+----------------------------------------------------------+
|               BAYESIAN NETWORK                            |
|    Probabilistic reasoning for complex diagnostics        |
+----------------------------------------------------------+
```

## Features

### Admin Section
- **System Setup** - Configuration and settings
- **Tools & Integrations** - External system connections
- **People Management** - Users, teams, roles
- **Runbooks** - Operational procedures
- **K-T Investigation** - Investigation template management
- **Service Catalog** - Service request templates and workflows

### Personal Section
- **Intake** - Ticket submission and initial triage
- **Service Requests** - End-user service request portal

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | Next.js 15, React 19, TypeScript, Tailwind CSS, Zustand |
| **Backend** | Python 3.13, FastAPI, SQLAlchemy 2.0 (async), Socket.IO |
| **Database** | PostgreSQL 15 |
| **Cache** | Redis 7 |
| **AI/ML** | LangChain, pgmpy (Bayesian inference) |
| **Infrastructure** | Docker, Docker Compose |

## Configuration

Edit `.env` to customize:

| Variable | Default | Description |
|----------|---------|-------------|
| `FRONTEND_PORT` | 3001 | Frontend port |
| `BACKEND_PORT` | 8001 | Backend API port |
| `POSTGRES_PASSWORD` | aria_dev_password | Database password |
| `SECRET_KEY` | (dev key) | App secret - **change in production!** |
| `JWT_SECRET_KEY` | (dev key) | JWT secret - **change in production!** |
| `OLLAMA_BASE_URL` | host.docker.internal:11434 | Ollama API endpoint |
| `OLLAMA_MODEL` | qwen2.5:7b | LLM model to use |

## Development

For local development with hot reload:

```bash
# Use development compose file (builds from source)
docker compose up -d

# View logs
docker compose logs -f backend
docker compose logs -f frontend
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines.

## License

This project is licensed under the Business Source License 1.1 - see the [LICENSE](LICENSE) file for details.

**Free for production use** with up to 10 users. Converts to Apache 2.0 on 2030-01-01.
