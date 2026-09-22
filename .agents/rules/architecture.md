# Architecture Rules

## Nombre

Arquitectura y contratos del dashboard financiero.

## Alcance

Aplica a cambios en `backend/app`, `frontend/src`, endpoints HTTP, modelos financieros y organización de componentes.

## Justificación

El backend define modelos Pydantic en `backend/app/routes.py`, mientras el frontend mantiene sus equivalentes en `frontend/src/lib/financial-types.ts`. Además, el filtrado compartido ya está centralizado en `filter_movements()` y los componentes están separados entre `dashboard` y `ui`.

## Guía específica del proyecto

- Mantener alineados los modelos Pydantic y los tipos TypeScript cuando cambien campos, enums o fechas.
- Reutilizar o extender `filter_movements()` en lugar de duplicar filtros en cada endpoint.
- Mantener la lógica financiera fuera del JSX y usar utilidades testeables.
- Tratar `backend/app/routes.py` como la fuente actual de datos de la aplicación; `frontend/src/lib/mock-data.ts` solo debe conservarse si se usa explícitamente como fixture o prototipo.
- Usar el alias `@/` para imports del frontend, según `frontend/tsconfig.app.json` y `frontend/vite.config.ts`.
- Preservar la separación entre componentes de `dashboard` y componentes reutilizables de `ui`.
