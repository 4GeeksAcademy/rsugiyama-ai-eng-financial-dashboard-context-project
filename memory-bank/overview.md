# Product Overview

## Verified purpose

Financial Metrics Dashboard: a web dashboard that presents financial movements as KPIs and monthly charts. The repository README describes it as a React + TypeScript frontend backed by FastAPI.

## Main user flow

1. The frontend requests `GET /api/metrics`.
2. `frontend/src/App.tsx` computes KPIs and monthly aggregates with `computeKPIs()` and `computeMonthlyData()`.
3. The dashboard renders a header, KPI row, income/outcome chart, and profit-percentage chart.
4. Loading and API error states are rendered in the dashboard.

## Evidence

- Product description and local URLs: `README.md`
- Frontend composition and API request: `frontend/src/App.tsx`
- Financial API models, generation, filtering, and aggregation: `backend/app/routes.py`
- API application setup: `backend/app/main.py`
- Frontend financial calculations: `frontend/src/lib/financial-utils.ts`
