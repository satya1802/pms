# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `c0cfdac` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
PMS ("Simple people management system") is a generated scaffold with two independent apps in one repo. The frontend is an approved Vite + React 19 SPA whose screens render seeded sample data and have not yet been wired to a real API. The backend is a FastAPI 0.115 service that, because no architecture was approved yet, only exposes a `/health` liveness check; its routers, models and schemas are scaffolded (SQLAlchemy models file, Pydantic `StubResponse` schema, empty routers package) ready to be filled in. The backend defaults to a local SQLite file so it runs with no external database, but can point at PostgreSQL (the approved database, also runnable via the repo's docker-compose) through the `DATABASE_URL` env var.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm/Vite/React 19, per frontend/package.json)
- Python 3.12 (per backend/Dockerfile)
- pip
- Docker and Docker Compose (optional, for the PostgreSQL service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository
2. cd backend && pip install -r requirements.txt
3. (optional) cd .. && docker compose up -d   # starts PostgreSQL 16 on localhost:5432 if you want a real database instead of the default SQLite file
4. cd backend && uvicorn app.main:app --reload   # starts the API on http://localhost:8000
5. In a new terminal: cd frontend && npm install
6. npm run dev   # starts the Vite dev server, by default on http://localhost:5173
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| backend dev | `cd backend && uvicorn app.main:app --reload` | Runs the FastAPI app with auto-reload; serves /health and the OpenAPI docs |
| backend db (optional) | `docker compose up -d` | Starts the PostgreSQL 16 container defined in docker-compose.yml for use via DATABASE_URL |
| frontend dev | `cd frontend && npm run dev` | Starts the Vite dev server for the React SPA |
| frontend build | `cd frontend && npm run build` | Bundles the app with Vite (does not typecheck) |
| frontend preview | `cd frontend && npm run preview` | Serves the production build locally |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend` | FastAPI service: app package, routers, models, schemas, tests, Dockerfile, requirements |
| `backend/app` | App code: main.py entrypoint, database.py (engine/session), models.py (SQLAlchemy), schemas.py (Pydantic), routers/ package |
| `backend/tests` | Pytest tests (currently the health check test) |
| `frontend` | Vite + React 19 SPA: approved UI screens running on seeded sample data |
| `frontend/src` | App source: main.tsx entrypoint, App shell, lib/ utilities (api client, UI components, icons, navigation), index.css |
| `frontend/e2e` | Playwright acceptance tests run against the built/served app or a deployed URL |
| `.quorq` | Platform handoff metadata (handoff.json) for the Quorq AI SDLC platform |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend routes are generated one router per architecture component, one route per spec'd endpoint; unimplemented routes return the typed Pydantic StubResponse placeholder so the service stays startable with a complete OpenAPI document
- SQLAlchemy models inherit from the shared Base in app/database.py; app/main.py imports app.models before calling Base.metadata.create_all so tables register first (no migrations yet)
- Backend DB connection is driven by the DATABASE_URL env var, defaulting to a local SQLite file (sqlite:///./app.db) so the service runs without a database server
- CORS allowed origins come from the ALLOWED_ORIGINS env var (comma-separated), defaulting to the local Vite dev server origins
- Frontend screens currently render seeded sample data and are not yet wired to the backend; frontend/src/lib/api.ts (apiFetch, API_BASE_URL, API_SECRET_KEY) is the intended integration seam, driven by VITE_API_BASE_URL and VITE_API_SECRET_KEY
- Frontend uses a `@/` path alias for `src/` (configured in both tsconfig.json and vite.config.ts)
- Frontend code style enforced via ESLint (flat config) and Prettier; backend via ruff (ruff.toml)
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend tests | `cd backend && pytest` | Runs pytest (pythonpath=. configured in pytest.ini); currently covers the /health endpoint |
| backend lint | `cd backend && ruff check .` | Lints the backend Python code |
| backend format | `cd backend && ruff format .` | Formats the backend Python code |
| frontend unit tests | `cd frontend && npm run test` | Runs Vitest component tests located beside their components |
| frontend lint | `cd frontend && npm run lint` | Runs ESLint over the whole frontend app (CI gate) |
| frontend typecheck | `cd frontend && npm run typecheck` | Runs tsc --noEmit (not run by npm run build) |
| frontend e2e install | `cd frontend && npm run test:e2e:install` | Installs the Chromium browser needed by Playwright |
| frontend e2e | `cd frontend && npm run test:e2e` | Runs Playwright acceptance tests from e2e/; without E2E_BASE_URL it builds/serves the frontend and boots the backend from backend/.venv locally |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend calls to the backend are blocked by CORS | Set the ALLOWED_ORIGINS env var on the backend to include the frontend's origin (defaults to http://localhost:5173 and http://127.0.0.1:5173 in dev) |
| `npm run build` succeeds but the app has type errors | Run `npm run typecheck` (tsc --noEmit) separately; `vite build` does not typecheck |
| `pytest` fails with `ModuleNotFoundError: app` | Run pytest from the backend/ directory; pytest.ini sets pythonpath=. relative to that directory |
| Playwright e2e run fails to start the backend | Its webServer command expects a Python venv at backend/.venv with dependencies installed; create it and install backend/requirements.txt there before running npm run test:e2e, or set E2E_BASE_URL to point at an already-running deployment instead |
| Backend data isn't persisting across runs in a real deployment | The default SQLite file (app.db) is for local scaffolding only; set DATABASE_URL to point at PostgreSQL (e.g. the one started via docker compose up -d) before it holds real data, and add migrations since the scaffold only auto-creates tables |
<!-- sdlc:auto:end troubleshooting -->
