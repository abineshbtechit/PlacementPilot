# 🚀 PlacementPilot: Autonomous Resume-Adaptive Agentic RAG Placement Coach

> **Architecture:** Polyglot Microservices Architecture  
> **Backend Tier:** FastAPI + LangGraph Multi-Agent Workflows  
> **Frontend Tier:** Next.js 14 (App Router) + Tailwind CSS + Monaco Editor + Streamlit  
> **Database Tier:** MongoDB (Long-Term Memory via Compass) + ChromaDB (Local Vector Store)  
> **Inference Tier:** Local `llama3.2:3b` (num_gpu 99) on NVIDIA RTX 2050 (4 GB VRAM) via Ollama

---

## 🏛️ Microservice Architecture & Directory Separation

The repository is organized into distinct, isolated microservice domains:

```
agentic WorkFlow/
├── backend/                      # Microservices Tier
│   ├── services/
│   │   ├── orchestrator/         # Port 8000: LangGraph Core, 9 Agents, Reflection Loops
│   │   ├── profiler/             # Port 8001: Resume PDF OCR & Skill Normalization
│   │   ├── rag_retriever/        # Port 8002: ChromaDB Semantic Query Engine
│   │   ├── game_engine/          # Port 8003: 60-Sec Sudden Death & Company Boss Battles
│   │   └── evaluator/            # Port 8004: AST Complexity Checker & Code Sandbox
│   └── shared/                   # Common Pydantic Models & GPU Utils
│
├── frontend/                     # Presentation Tier
│   ├── src/app/                  # Next.js 14 Interactive Battleground
│   ├── src/components/           # Monaco Editor, Chat-to-Game Modal, Skill Radar
│   └── public/                   # Company Icons (Google, Amazon, Meta, Uber)
│
├── database/                     # Persistence Tier
│   ├── mongo/                    # MongoDB Docker Config & Initial Seed Collections
│   ├── chroma/                   # ChromaDB Vector Storage & Company Archives
│   └── compass_configs/          # MongoDB Compass inspection queries
│
└── infra/                        # Infrastructure Tier
    └── docker/                   # docker-compose.yml local orchestration
```

---

## 🛠️ Microservice Roles & Technology Mapping

| Microservice / Layer | Role | Tech Stack & Operational Details |
| :--- | :--- | :--- |
| **`backend/services/orchestrator`** | **Multi-Agent Engine** | **LangGraph + LangChain** (Port 8000). Manages state handoffs, Corrective RAG (CRAG) loops, 14-day anti-repetition guardrails, and quality gates across all 9 agents. |
| **`backend/services/profiler`** | **Resume Parser** | **FastAPI + PyMuPDF** (Port 8001). Extracts candidate skills, frameworks, and project architectures into normalized JSON. |
| **`backend/services/rag_retriever`** | **Vector Search Service** | **ChromaDB + `nomic-embed-text`** (Port 8002). Embeds and retrieves past interview questions from Google, Amazon, and GATE archives. |
| **`backend/services/game_engine`** | **Gamified Battleground** | **FastAPI + WebSockets** (Port 8003). Powers the **Chat-to-Game** loop, 60-second sudden death trivia, and company boss fights. |
| **`backend/services/evaluator`** | **Submission Grader** | **Python AST Sandbox** (Port 8004). Analyzes time/space complexity, evaluates test cases, awards XP, and updates the mistake vault. |
| **`frontend`** | **Interactive UI** | **Next.js 14 + Tailwind CSS + Monaco** (Port 3000). Sleek cyber gamer UI with interactive code editors, live timers, and skill radar charts. |
| **`database/mongo`** | **State & Memory** | **MongoDB** (Port 27017). Inspected live via **MongoDB Compass**. Stores candidate profiles, daily challenge logs, mistake vaults, and player XP. |
| **`database/chroma`** | **Vector Storage** | **ChromaDB**. In-process vector store housing company interview archives. |
| **Local LLM Engine** | **Inference Runtime** | **`llama3.2:3b` via Ollama**. Offloads 100% of layers to your **NVIDIA RTX 2050 (4 GB VRAM)** for private, offline inference at 25–35 tokens/sec. |

---

## 🧭 Database Inspection via MongoDB Compass

Connect to `mongodb://localhost:27017` in **MongoDB Compass**:
- Database: `placement_pilot`
  - `candidates`: Parsed resume entities, target roles, and candidate stack.
  - `daily_sessions`: Daily 4-track challenge sets and test outcomes.
  - `mistake_vault`: Failure logs used by the Strategy Planner for spaced repetition.
  - `mastery_metrics`: Dynamic XP, current streak, and topic mastery radar scores.

---

## 🚀 Running the Microservices Locally

### 1. Start Persistence & Backend Services
```powershell
cd "infra\docker"
docker-compose up -d
```

### 2. Verify Database in MongoDB Compass
Open **MongoDB Compass**, connect to `mongodb://localhost:27017`, and observe collections seeding automatically.

### 3. Start Frontend Client
```powershell
cd "frontend"
npm install
npm run dev
```
Visit `http://localhost:3000` to start your daily placement preparation battle!
