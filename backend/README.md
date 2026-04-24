# AegisCore — Backend

This folder contains the **backend** of the AegisCore AI Security Scanner platform.

## Tech Stack

- **Framework:** FastAPI (Python)
- **Database:** SQLite (local) / PostgreSQL (production via `DATABASE_URL` env var)
- **Server:** Uvicorn / Gunicorn
- **Deployment:** Docker / Render / Railway

## File Structure

```
backend/
├── server.py              # Main FastAPI app — all API routes & pipeline logic
├── main.py                # CLI entry point (scan, patch, review, dashboard commands)
├── seed_data.py           # Database seeder with sample vulnerability data
├── debug_db.py            # DB debugging utility
├── requirements.txt       # Python dependencies
├── Dockerfile             # Docker build config
├── docker-compose.yml     # Docker Compose config
├── runtime.txt            # Python runtime version (for Render/Heroku)
├── vercel.json            # Vercel deployment config
├── .gitignore             # Git ignore rules
├── scan_engine/           # Core scanning engine module
│   ├── __init__.py
│   ├── core.py            # ScanEngine orchestrator
│   ├── auth.py            # Role-based access control
│   ├── analytics.py       # Analytics & reporting
│   ├── alerts.py          # Alert system
│   ├── audit.py           # Audit log service
│   ├── health.py          # Health check utilities
│   ├── infrastructure.py  # Infrastructure scanning
│   ├── visualization.py   # Terminal dashboard visualizer
│   ├── models.py          # Shared Pydantic models
│   ├── intel/             # Vulnerability intelligence & database
│   │   ├── db.py          # SQLModel DB session
│   │   ├── models.py      # Vulnerability data models
│   │   ├── lifecycle.py   # State transition manager
│   │   └── enrichment.py  # CVE enrichment service
│   ├── patching/          # AI-powered patch generation
│   │   ├── generator.py   # Patch generator
│   │   ├── validator.py   # Patch validation
│   │   ├── ai_service.py  # LLM integration
│   │   ├── prompt_engine.py # Prompt builder
│   │   ├── risk_assessor.py # Risk scoring
│   │   ├── feedback.py    # Feedback loop
│   │   └── models.py      # Patch data models
│   └── scanners/          # Language-specific scanners
│       ├── base.py        # Base scanner class
│       ├── bandit_scanner.py  # Python static analysis (Bandit)
│       └── semgrep_scanner.py # Multi-language scanner (Semgrep)
└── test_data/             # Sample vulnerable code for testing
    ├── vuln_code.py
    ├── vulnerable.py
    └── test_vuln.py
```

## Setup & Run

### Local (without Docker)

```bash
cd backend
pip install -r requirements.txt
uvicorn server:app --reload --port 8000
```

### With Docker

```bash
cd backend
docker-compose up --build
```

### CLI Usage

```bash
python main.py scan --path ./test_data
python main.py patch --id VULN-12345
python main.py review
python main.py dashboard
python main.py export-audit
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | SQLite (local file) |
| `LLM_API_KEY` | OpenAI/Gemini API key for AI patching | None (uses offline mode) |
| `GITHUB_TOKEN` | GitHub API token for repo scanning | None (guest limits) |
| `REQUIRE_AUTH` | Enable API key authentication | `False` |
| `AEGIS_API_KEY` | API key for enterprise auth | `enterprise-demo-key-2026` |
