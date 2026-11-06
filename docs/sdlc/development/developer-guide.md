# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `ce1d22f` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
Calculator is a generated two-app repository from the Quorq AI SDLC platform: a Vite + React 19 single-page frontend whose screens were approved by design review and currently render seeded sample data, and a FastAPI 0.115 backend scaffold that has no approved architecture yet, so it exposes only a health check. The backend uses SQLAlchemy with a SQLite file by default (switchable to Postgres via DATABASE_URL) and a docker-compose file provisions a Postgres 16 database for local use.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm/Vite, React 19, TypeScript 5.6)
- Python 3.12
- pip
- Docker and Docker Compose (optional, for the Postgres service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository
2. cd frontend && npm install
3. cd backend && pip install -r requirements.txt
4. (optional) docker compose up -d db   # starts Postgres 16 if you want to use it instead of the default SQLite file
5. (optional) copy .env.example to .env and set values such as DATABASE_URL or ALLOWED_ORIGINS
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA (run inside frontend/) |
| backend dev | `uvicorn app.main:app --reload` | Starts the FastAPI backend with auto-reload (run inside backend/); creates SQLite tables on startup |
| db | `docker compose up -d db` | Starts a Postgres 16 container with user/db 'app' for local development |
| frontend preview | `npm run preview` | Serves the production build locally (used by Playwright e2e against a built app) |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `frontend/` | React 19 + Vite SPA; approved screens running on seeded data |
| `frontend/src` | App source: main.tsx entrypoint, lib/ (api client, UI/icon vocabulary, navigation), index.css (brand tokens) |
| `frontend/e2e` | Playwright acceptance tests |
| `backend/` | FastAPI service scaffold |
| `backend/app` | Application package: main.py (entrypoint, CORS, /health), database.py (engine/session), models.py (SQLAlchemy models, empty), schemas.py (Pydantic schemas, StubResponse), routers/ (per-component routers, currently empty) |
| `backend/tests` | Pytest suite (conftest.py, test_health.py) |
| `.devcontainer/` | VS Code devcontainer configuration |
| `.quorq/` | Platform metadata (handoff.json) |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend: one router per architecture component that owns endpoints; every generated route starts as a stub returning a typed StubResponse until implemented
- Backend models subclass the shared SQLAlchemy Base in app/database.py; models.py is imported in main.py before create_all so tables register
- Pydantic schemas live in app/schemas.py, one pair per entity
- Backend config via environment variables (DATABASE_URL, ALLOWED_ORIGINS) read with os.getenv and sensible local defaults
- Frontend screens live under src/screens/ (one module per approved screen), with App.tsx as the navigation shell; src/lib/ui.tsx and src/lib/icons.tsx define the shared component/icon vocabulary
- Frontend API access is centralized in src/lib/api.ts (apiFetch) with bearer-token auth via a session token or shared secret; screens do not yet call it, they use seeded data
- Linting/formatting enforced via ESLint + Prettier (frontend) and ruff (backend)
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| frontend unit tests | `npm test` | Runs Vitest component tests colocated with components (frontend/) |
| frontend lint | `npm run lint` | Runs ESLint over the frontend app; CI/platform gate |
| frontend format check | `npm run format:check` | Checks Prettier formatting |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit (not run by npm run build) |
| frontend e2e | `npm run test:e2e` | Runs Playwright acceptance tests from e2e/; requires npm run test:e2e:install first, boots backend+frontend locally unless E2E_BASE_URL is set |
| backend tests | `pytest` | Runs the backend pytest suite (backend/tests) |
| backend lint | `ruff check .` | Lints the backend Python code |
| backend format | `ruff format .` | Formats the backend Python code |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend fetch calls to the backend fail with a CORS error | Set ALLOWED_ORIGINS (comma-separated) on the backend to include the frontend origin; in dev, http://localhost:5173 and http://127.0.0.1:5173 are allowed by default |
| `pytest` from backend/ fails with 'cannot import app' | Run pytest from the backend/ directory where pytest.ini sets pythonpath = . |
| Playwright e2e tests fail to start the backend | The webServer command expects a backend/.venv with dependencies installed (.venv/bin/python -m uvicorn ...); create and populate that venv, or set E2E_BASE_URL to point at an already-running deployment |
| Backend has no data after restart / wrong database | By default DATABASE_URL defaults to sqlite:///./app.db; set DATABASE_URL to point at the Postgres instance started via docker compose up -d db if persistent/shared storage is wanted |
<!-- sdlc:auto:end troubleshooting -->
