# OpenWebUI Development Setup

Quick reference for running OpenWebUI in development mode.

## Prerequisites

- Python 3.11 or higher
- Node.js (any recent version)
- uv (Python package manager)

## Running the Application

### 1. Start Backend (Terminal 1)

```bash
cd /Users/sjanjua/Code/IS/PrivateGPT
STATIC_DIR="/Users/sjanjua/Code/IS/PrivateGPT/backend/open_webui/static" CORS_ALLOW_ORIGIN="http://localhost:5173;http://localhost:8080" PORT=8080 uv run uvicorn open_webui.main:app --port 8080 --host 0.0.0.0 --forwarded-allow-ips '*' --reload
```

Backend will be available at: **http://localhost:8080**

### 2. Start Frontend (Terminal 2)

```bash
cd /Users/sjanjua/Code/IS/PrivateGPT
npm run dev
```

Frontend will be available at: **http://localhost:5173**

## Access the Application

Open your browser and navigate to: **http://localhost:5173**

## First Time Setup (Already Done)

If you need to set up from scratch:

```bash
# Backend dependencies
uv sync

# Frontend dependencies
npm install --legacy-peer-deps --engine-strict=false
```

## Common Issues & Solutions

### Issue: Backend dependency conflict
**Solution:** Already fixed in `pyproject.toml` (psycopg2-binary versions aligned)

### Issue: Frontend @tiptap version mismatch
**Solution:** Already fixed in `package.json` (all @tiptap packages at v3.x)

### Issue: Missing y-protocols
**Solution:** Already installed via `npm install y-protocols --legacy-peer-deps --engine-strict=false`

### Issue: Node.js version too new
**Solution:** Use flags `--legacy-peer-deps --engine-strict=false` when installing

## Development Notes

- Both servers support hot-reload (changes auto-reflect)
- Backend uses SQLite database (stored in `backend/data/`)
- Frontend uses Vite for fast development builds
- The syntax warning in `backend/open_webui/env.py` has been fixed

## Quick Start Script

For even faster startup, you can run both in the background:

```bash
# Start backend in background
cd /Users/sjanjua/Code/IS/PrivateGPT
CORS_ALLOW_ORIGIN="http://localhost:5173;http://localhost:8080" PORT=8080 uv run uvicorn open_webui.main:app --port 8080 --host 0.0.0.0 --forwarded-allow-ips '*' --reload &

# Start frontend in background
npm run dev &
```

To stop all background processes:
```bash
pkill -f "uvicorn open_webui.main:app"
pkill -f "vite dev"
```
