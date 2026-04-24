# AegisCore — AI-Powered Security Scanner

AegisCore is a self-healing security platform that automatically detects vulnerabilities (SQL Injection, XSS, Eval/Exec Injection) in code and web applications, and generates AI-powered patches.

---

## Project Structure

```
Yeswanth-Project--main/
├── frontend/                  ← All UI files (HTML, CSS, JS)
│   ├── index.html             # Single-page dashboard application
│   ├── github_banner.png      # Visual banner asset
│   └── README.md              # Frontend documentation
│
├── backend/                   ← All server & engine files (Python)
│   ├── server.py              # FastAPI server — all API routes
│   ├── main.py                # CLI tool (scan / patch / review / dashboard)
│   ├── seed_data.py           # Database seed script
│   ├── debug_db.py            # DB debugging utility
│   ├── requirements.txt       # Python dependencies
│   ├── Dockerfile             # Docker image config
│   ├── docker-compose.yml     # Docker Compose config
│   ├── runtime.txt            # Python version for deployment
│   ├── vercel.json            # Vercel deployment config
│   ├── scan_engine/           # Core vulnerability scanning engine
│   │   ├── core.py            # Main scan orchestrator
│   │   ├── auth.py            # Role-based access control
│   │   ├── analytics.py       # Analytics & reporting
│   │   ├── audit.py           # Audit log service
│   │   ├── visualization.py   # Terminal dashboard
│   │   ├── intel/             # CVE intelligence & DB lifecycle
│   │   ├── patching/          # AI patch generator & validator
│   │   └── scanners/          # Bandit & Semgrep scanner integrations
│   └── test_data/             # Sample vulnerable Python files
│
└── README.md                  ← You are here
```

---

## Quick Start

### 1. Run the Backend

```bash
cd backend
pip install -r requirements.txt
uvicorn server:app --reload --port 8000
```

### 2. Open the Frontend

The frontend (`frontend/index.html`) is **automatically served** by the backend at:

```
http://localhost:8000
```

### 3. CLI Usage

```bash
cd backend
python main.py scan --path ./test_data
python main.py patch --id VULN-12345
python main.py review
python main.py dashboard
```

### 4. Docker

```bash
cd backend
docker-compose up --build
```

---

## Tech Stack

| Layer    | Technology |
|----------|-----------|
| Frontend | HTML5, Vanilla CSS, Vanilla JavaScript (SPA) |
| Backend  | Python, FastAPI, Uvicorn |
| Database | SQLite (dev) / PostgreSQL (prod) |
| AI Engine| Google Gemini / OpenAI (with offline fallback) |
| CI/CD    | GitHub Webhooks, Docker, Vercel/Render |

---

## Key Features

- 🔍 **Multi-source scanning** — Local files, GitHub repos, live websites
- 🤖 **AI patch generation** — LLM-powered or deterministic offline fallback
- ✅ **Automated validation** — Regex + AST-based patch correctness check
- 📊 **Live dashboard** — Real-time terminal logs, risk scores, pipeline status
- 🔐 **Role-based access** — ADMIN / DEVELOPER / VIEWER roles
- 🔗 **GitHub webhook** — Auto-trigger scans on every push event
