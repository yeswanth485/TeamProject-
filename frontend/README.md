# AegisCore — Frontend

This folder contains the **frontend** of the AegisCore AI Security Scanner platform.

## Files

| File | Description |
|------|-------------|
| `index.html` | Single-page application — contains all HTML, CSS, and JavaScript for the dashboard UI |
| `github_banner.png` | Visual banner asset used in the dashboard |

## How It Works

The frontend is a **single-file SPA** (Single Page Application) built with vanilla HTML, CSS, and JavaScript.

- It communicates with the backend via REST API calls (e.g., `fetch('/scan', ...)`)
- The backend (`server.py`) serves this `index.html` at the root `/` endpoint
- All scan results, patch status, pipeline controls, and terminal logs are driven from the backend API

## Running

The frontend is served automatically by the backend FastAPI server.
Start the backend and open `http://localhost:8000` in your browser.

> **Note:** To deploy the frontend separately (e.g., on Vercel/Netlify as a static site),
> you will need to update all API base URLs in `index.html` to point to your backend's deployed URL.
