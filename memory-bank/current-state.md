# Current State

## Working capabilities

- The frontend has a dashboard shell with KPI cards and two financial charts.
- The frontend fetches `/api/metrics`, computes presentation aggregates, and handles loading and API error states.
- The backend exposes health and metrics routes, including date/category/operation filters and B2B/B2C views.
- Backend tests cover health, full-year mock generation, chronological ordering, date boundaries, filters, and B2B/B2C responses.
- Frontend tests cover KPI calculations, monthly aggregation across years, and formatters.
- Frontend validation last observed in this workspace: `npm run build`, `npm run lint`, and `npm test` passed; Vitest reported 5 passing tests. The build emitted existing Node deprecation and chunk-size warnings.

## Known gaps and risks

- `frontend/src/App.tsx` displays the hard-coded period `2024 - Full Year`, while `backend/app/routes.py` derives generated movement years from the current date. The displayed period can become inaccurate over time.
- `backend/app/main.py` enables unrestricted CORS (`allow_origins`, methods, and headers set to `*`), which is suitable for development but unsafe as a production default.
- `docker-compose.yml` exposes debugpy on `5678`; production deployment should disable or restrict it.
- `backend/requirements.txt` does not pin dependency versions, reducing reproducibility.
- `generate_mock_movements()` uses the global `random` module and `random.seed()`, which can create shared state between requests.
- `_build_movement()` only generates days 1 through 28, so dates 29-31 are not represented by the mock data.
- The Vite proxy targets the Compose hostname `backend`; local execution outside Compose needs a compatible API base/proxy configuration.

## Next priorities

1. Derive the displayed dashboard period from API data instead of hard-coding it.
2. Separate development and production configuration for CORS, debugpy, reload behavior, and dependency locking.
3. Replace global random seeding with a local seeded random generator while preserving the existing deterministic fixture contract.
4. Expand date-generation and date-boundary tests before changing calendar logic.
5. Keep frontend/backend contract tests aligned when API models or filters change.

## Evidence

- Frontend behavior: `frontend/src/App.tsx`
- Backend behavior and mock generation: `backend/app/routes.py`
- CORS configuration: `backend/app/main.py`
- Compose ports and services: `docker-compose.yml`
- Backend coverage: `backend/tests/test_routes.py`
- Frontend calculation coverage: `frontend/src/lib/financial-utils.test.ts`
- Dependency and script definitions: `frontend/package.json`, `backend/requirements.txt`
