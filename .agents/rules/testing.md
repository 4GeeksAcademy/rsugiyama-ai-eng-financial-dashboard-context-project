# Testing Rules

## Nombre

Pruebas de comportamiento y contratos financieros.

## Alcance

Aplica a cambios de backend, frontend, endpoints, filtros, cálculos financieros y dependencias de test.

## Justificación

`backend/tests/test_routes.py` cubre salud, filtros, orden, facets, resúmenes, categorías, comparación, alertas y vistas B2B/B2C. El frontend define `test`, `build` y `lint` en `frontend/package.json`. Los tests actuales pasan, aunque muestran warnings de compatibilidad entre `httpx` y Starlette.

## Guía específica del proyecto

- Añadir tests de respuesta y comportamiento para cada endpoint o parámetro nuevo.
- Mantener tests de orden cronológico y filtros combinados.
- Cubrir cálculos financieros en `frontend/src/lib/financial-utils.test.ts` cuando cambie `financial-utils.ts`.
- Ejecutar `pytest` para cambios de backend.
- Ejecutar `npm test`, `npm run build` y `npm run lint` para cambios de frontend.
- Investigar warnings de dependencias; no tratarlos como salida normal sin documentar la decisión.
- Añadir pruebas de contrato cuando se modifiquen modelos Pydantic o tipos TypeScript.
