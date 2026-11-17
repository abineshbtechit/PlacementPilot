# 🏗️ PlacementPilot: Microservice Production Architecture Guide

> **Architecture Style:** Polyglot Event-Driven / RESTful Microservices Architecture  
> **Tech Stack:**  
> - **Backend Services:** FastAPI + LangGraph + Ollama (`llama3.2:3b` on NVIDIA RTX 2050 4GB VRAM)  
> - **Vector Database Service:** In-process / Serverless ChromaDB Microservice with `nomic-embed-text`  
> - **State & Memory Database:** MongoDB Cluster (Inspected via MongoDB Compass)  
> - **Frontend Application:** Next.js 14 (App Router) + Tailwind CSS + Monaco Editor + Streamlit Gateway  
> - **Infrastructure & Orchestration:** Docker Compose + Microservice Service Mesh

---

## 📂 1. Microservices Root Directory Layout

```
agentic WorkFlow/
│
├── backend/                              # All Backend Microservices & Shared Logic
│   ├── services/                         # Independent Domain Microservices
│   │   ├── orchestrator/                 # CORE SERVICE: LangGraph Multi-Agent State Machine (Port 8000)
│   │   │   ├── Dockerfile
│   │   │   ├── requirements.txt
│   │   │   ├── main.py                   # FastAPI Application Entry Point
│   │   │   ├── agents/                   # The 9 LangGraph Autonomous Agents
│   │   │   │   ├── __init__.py
│   │   │   │   ├── resume_profiler.py    # Agent 1: Resume Extraction & Normalization
│   │   │   │   ├── company_scout.py      # Agent 2: Company Hiring Round Intelligence
│   │   │   │   ├── strategy_planner.py   # Agent 3: Adaptive Spaced-Repetition Planner
│   │   │   │   ├── rag_retriever.py      # Agent 4: Semantic Query Builder & Chroma Client
│   │   │   │   ├── retrieval_grader.py   # Agent 5: Corrective RAG (CRAG) Validator
│   │   │   │   ├── multi_generator.py    # Agent 6: 4-Track Daily Challenge Synthesizer
│   │   │   │   ├── game_master.py        # Agent 7: Chat-to-Game Extractor & Boss Fights
│   │   │   │   ├── quality_critic.py     # Agent 8: 14-Day Anti-Repetition Guardrail
│   │   │   │   └── evaluator_mentor.py   # Agent 9: Code Complexity Grader & XP Engine
│   │   │   ├── workflow/                 # LangGraph Graph Definition
│   │   │   │   ├── state.py              # TypedDict LangGraph Schema
│   │   │   │   ├── nodes.py              # Agent Execution Nodes
│   │   │   │   ├── edges.py              # Conditional Routing & Reflection Loops
│   │   │   │   └── graph.py              # Compiled LangGraph Workflow
│   │   │   └── api/                      # REST Endpoints (/session/start, /chat/trigger-game)
│   │   │
│   │   ├── profiler/                     # Microservice 2: Resume Ingestion & OCR (Port 8001)
│   │   │   ├── Dockerfile
│   │   │   ├── main.py
│   │   │   ├── parser.py                 # PyMuPDF & LlamaParse extraction
│   │   │   └── api/                      # POST /resume/upload & /resume/skills
│   │   │
│   │   ├── rag_retriever/                # Microservice 3: ChromaDB Vector Query Engine (Port 8002)
│   │   │   ├── Dockerfile
│   │   │   ├── main.py
│   │   │   ├── indexer.py                # Automated indexing pipeline for company question banks
│   │   │   ├── embeddings.py             # nomic-embed-text wrapper
│   │   │   └── api/                      # POST /rag/retrieve & /rag/index
│   │   │
│   │   ├── game_engine/                  # Microservice 4: Gamified Battleground & Timers (Port 8003)
│   │   │   ├── Dockerfile
│   │   │   ├── main.py
│   │   │   ├── boss_fight.py             # Company Boss Battle State Engine
│   │   │   ├── sudden_death.py           # 60-second rapid MCQ timer & multiplier
│   │   │   └── api/                      # WS /ws/game & POST /game/submit
│   │   │
│   │   └── evaluator/                    # Microservice 5: Code Sandbox & Static Analyzer (Port 8004)
│   │       ├── Dockerfile
│   │       ├── main.py
│   │       ├── code_sandbox.py           # Isolated Python/C++/JS AST Complexity Analyzer
│   │       └── api/                      # POST /evaluate/code & /evaluate/quiz
│   │
│   └── shared/                           # Shared Library across Microservices
│       ├── __init__.py
│       ├── models/                       # Common Pydantic & Domain DTOs
│       │   ├── candidate.py              # Candidate Profile Schema
│       │   ├── session.py                # Daily Session & 4-Track DTOs
│       │   └── game.py                   # Game Arena & Score Event Models
│       └── utils/
│           ├── hardware.py               # GPU Memory Monitor for RTX 2050 (4GB VRAM)
│           └── logger.py                 # Structured JSON Logging
│
├── frontend/                             # Presentation Tier
│   ├── package.json
│   ├── tailwind.config.js
│   ├── next.config.js
│   ├── public/                           # Company Icons (Google, Amazon, Meta, Uber, etc.)
│   └── src/
│       ├── app/                          # Next.js 14 App Router
│       │   ├── layout.tsx
│       │   ├── page.tsx                  # Placement Arena Dashboard
│       │   ├── resume/page.tsx           # Resume Upload & Profile Scanner
│       │   ├── daily-tracks/page.tsx     # The 4 Daily Challenge Tabs
│       │   └── boss-battle/page.tsx      # Target Company Boss Fights
│       ├── components/
│       │   ├── battleground/             # Monaco Code Editor, Test Case Runner
│       │   ├── chat_arena/               # Live Chat with Chat-to-Game Popup Modal
│       │   └── analytics/                # Skill Radar, XP Streaks, Mistake Review
│       └── lib/
│           ├── api_client.ts             # Typed Axios / Fetch Client to Backend Gateway
│           └── sockets.ts                # WebSocket client for 60-Second Sudden Death
│
├── database/                             # Persistence & Schema Definitions
│   ├── mongo/                            # MongoDB Service Configuration
│   │   ├── Dockerfile
│   │   ├── mongod.conf                   # MongoDB Local Config
│   │   └── init-scripts/                 # Seed Scripts for Collections
│   │       ├── 01_candidates.js
│   │       ├── 02_daily_sessions.js
│   │       ├── 03_mistake_vault.js
│   │       └── 04_mastery_metrics.js
│   ├── chroma/                           # ChromaDB Vector Store Persistence
│   │   ├── data/                         # Local Persistent Vector Embeddings
│   │   └── vault_seed/                   # Raw Knowledge Markdown/JSON Archives
│   │       ├── cs_fundamentals/          # OS, DBMS, Computer Networks
│   │       ├── dsa_patterns/             # LeetCode Curated Patterns
│   │       └── company_vault/            # Google, Amazon, Microsoft, Uber
│   └── compass_configs/                  # MongoDB Compass connection profiles & saved queries
│
├── infra/                                # Deployment, Containerization & Networking
│   ├── docker/
│   │   ├── docker-compose.yml            # Complete Multi-Container Local Stack
│   │   └── docker-compose.override.yml   # GPU Device Passthrough for RTX 2050
│   └── k8s/                              # Kubernetes Manifests for Scale (Optional)
│
├── Cross-Verification-PlacementPilot-vs-ChatGPT.md
├── Interactive-Gamified-Platform-Spec.md
├── README.md
└── PROJECT-STRUCTURE.md
```

---

## ⚡ 2. Microservice Port & API Topology

| Service | Port | Protocol | Primary Responsibility | Data Dependency |
| :--- | :--- | :--- | :--- | :--- |
| **Frontend (Next.js)** | `3000` | HTTP / WS | User UI, Monaco Editor, Boss Fight, Radar Charts | Backend Gateway |
| **API Gateway / Orchestrator** | `8000` | HTTP | LangGraph Multi-Agent Orchestration & Reflection | All Microservices + MongoDB |
| **Resume Profiler Service** | `8001` | HTTP | PDF Parsing, Entity Extraction, Skill Normalization | Local Llama 3.2 3B |
| **RAG Retriever Service** | `8002` | HTTP | ChromaDB Semantic Vector Search & Chunker | `nomic-embed-text` |
| **Gamified Battle Service** | `8003` | HTTP / WS | 60-Sec Sudden Death Timer, Boss Battle State, Multipliers | Redis / Memory |
| **Code Evaluator Service** | `8004` | HTTP | AST Code Complexity Checker, Test Case Validator | Isolated Subprocess Sandbox |
| **MongoDB Service** | `27017` | TCP | Candidate profiles, session logs, `mistake_vault` | **MongoDB Compass** |
| **Ollama Inference Engine** | `11434` | HTTP | `llama3.2:3b` (num_gpu 99) on RTX 2050 GPU | NVIDIA Driver 592.82 |

---

## 🐳 3. `docker-compose.yml` Specification

```yaml
version: '3.8'

services:
  # 1. MongoDB Long-Term Memory (Inspected via MongoDB Compass)
  mongo:
    image: mongo:7.0
    container_name: placementpilot_mongo
    ports:
      - "27017:27017"
    volumes:
      - ./database/mongo/data:/data/db
      - ./database/mongo/init-scripts:/docker-entrypoint-initdb.d
    restart: always

  # 2. Vector DB Service (ChromaDB)
  chroma:
    image: chromadb/chroma:0.5.5
    container_name: placementpilot_chroma
    ports:
      - "8002:8000"
    volumes:
      - ./database/chroma/data:/chroma/chroma
    environment:
      - IS_PERSISTENT=TRUE

  # 3. Core LangGraph Multi-Agent Orchestrator
  orchestrator:
    build:
      context: ./backend/services/orchestrator
    container_name: placementpilot_orchestrator
    ports:
      - "8000:8000"
    environment:
      - MONGO_URI=mongodb://mongo:27017/placement_pilot
      - CHROMA_HOST=chroma
      - CHROMA_PORT=8000
      - OLLAMA_HOST=http://host.docker.internal:11434
    depends_on:
      - mongo
      - chroma

  # 4. Frontend Next.js Client
  frontend:
    build:
      context: ./frontend
    container_name: placementpilot_frontend
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://localhost:8000
    depends_on:
      - orchestrator
```

---

## 🧭 4. MongoDB Compass Inspection Endpoints

Open **MongoDB Compass** and connect to:
```
mongodb://localhost:27017
```
Database: `placement_pilot`
- **`candidates`**: Inspect profiles populated by the Profiler Microservice.
- **`daily_sessions`**: Inspect active 4-track challenges synthesized by the Orchestrator.
- **`mistake_vault`**: Inspect diagnostic errors logged by the Evaluator Service.
- **`mastery_metrics`**: Watch player XP and topic mastery levels climb live.
