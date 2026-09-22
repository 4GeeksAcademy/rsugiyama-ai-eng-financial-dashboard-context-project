# Technology Stack

## Languages and frameworks

- TypeScript and React 19 for the frontend.
- Python and FastAPI for the backend API.
- Pydantic models in `backend/app/routes.py` for API response/domain contracts.
- Tailwind CSS through the Vite plugin for frontend styling.

## Frontend tooling and key dependencies

- Vite for development and production builds.
- Vitest for frontend tests.
- ESLint with TypeScript and React plugins.
- Recharts for financial charts.
- `lucide-react` for icons.
- `clsx`, `tailwind-merge`, and `class-variance-authority` for class composition and component variants.
- The `@/` import alias resolves to `frontend/src`.

## Backend and infrastructure

- Uvicorn serves the FastAPI application.
- Pytest and `pytest-cov` provide backend test tooling.
- `httpx` is used by the backend test client.
- `debugpy` is included for debugging.
- Docker Compose runs `frontend` on port `5173` and `backend` on port `8000`; backend debugging is exposed on port `5678`.
- The Vite development proxy sends `/api` requests to `http://backend:8000` inside Compose.

## Evidence

- Frontend scripts and dependencies: `frontend/package.json`
- Python dependencies: `backend/requirements.txt`
- Compose services, ports, and volumes: `docker-compose.yml`
- Vite plugins, alias, and proxy: `frontend/vite.config.ts`
- API server and middleware: `backend/app/main.py`
