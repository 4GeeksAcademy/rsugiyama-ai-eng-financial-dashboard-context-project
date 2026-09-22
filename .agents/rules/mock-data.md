# Mock Data Rules

## Nombre

Datos mock reproducibles y períodos financieros coherentes.

## Alcance

Aplica a la generación de movimientos, fechas, seeds, agregaciones y tests que dependan de datos mock.

## Justificación

Los endpoints llaman `generate_mock_movements(seed=42)` en `backend/app/routes.py`, y `backend/tests/test_routes.py` espera 360 movimientos ordenados. La generación actual usa `date.today()` y días del 1 al 28, mientras la UI muestra un período fijo en `frontend/src/App.tsx`.

## Guía específica del proyecto

- Preservar `seed=42` y actualizar tests y documentación si cambia la distribución de datos.
- Preferir `random.Random(seed)` local en vez de `random.seed(seed)`, para no modificar el generador global.
- Representar un período anual explícito y coherente; no combinar meses de años distintos por depender accidentalmente de la fecha actual.
- Mantener sincronizados el período generado por el backend y el período mostrado por la UI.
- Probar días 29, 30 y 31, finales de mes y cambios de año cuando se modifique la lógica temporal.
- No asumir que los mocks representan persistencia real: actualmente no existe base de datos.
