# Reglas propuestas del proyecto

Estas reglas se basan en la estructura y el comportamiento actuales del repositorio.

## Arquitectura y dominio

### 1. Mantener una única fuente de verdad para los datos financieros

`frontend/src/lib/mock-data.ts` contiene datos mock, mientras que `backend/app/routes.py` genera los datos que consume actualmente `frontend/src/App.tsx`.

Los nuevos datos o cambios de dominio deben implementarse en una única fuente claramente definida. Los fixtures obsoletos deben eliminarse o marcarse explícitamente como datos de prueba.

### 2. Mantener alineados los contratos backend y frontend

Los modelos Pydantic están definidos en `backend/app/routes.py` y sus equivalentes TypeScript en `frontend/src/lib/financial-types.ts`.

Cualquier cambio en campos, enums o formatos de fecha debe actualizar ambos lados y sus tests.

### 3. Mantener coherente el período de datos

`_year_for_month()` en `backend/app/routes.py` depende de `date.today()`, mientras la interfaz muestra `2024 - Full Year` en `frontend/src/App.tsx`.

Los datos mock deben representar un intervalo anual explícito y la UI debe derivar el período de la misma fuente.

### 4. Reutilizar la capa de filtrado existente

`backend/app/routes.py` ya concentra filtros por fecha, categoría y tipo de operación en `filter_movements()`.

Los nuevos endpoints no deben duplicar filtros; deben reutilizar o extender esa función.

## Reproducibilidad y datos mock

### 5. Preservar la reproducibilidad de los mocks

Los endpoints llaman `generate_mock_movements(seed=42)` y los tests dependen de un resultado estable de 360 movimientos en `backend/tests/test_routes.py`.

No cambiar el seed ni la distribución sin actualizar explícitamente los tests y la documentación.

### 6. No modificar el generador global de aleatoriedad

`backend/app/routes.py` usa `random.seed(seed)`.

La generación futura debe usar una instancia local de `random.Random` para evitar efectos secundarios entre requests o funcionalidades.

### 7. Probar fechas reales de calendario

`_build_movement()` genera días entre 1 y 28, por lo que no cubre días 29, 30 ni 31.

Los tests de fechas deben incluir finales de mes y cambios de año antes de modificar la lógica temporal.

## Seguridad y configuración

### 8. Tratar CORS abierto y debugpy como configuración exclusiva de desarrollo

`backend/app/main.py` permite todos los orígenes, métodos y headers. Además, `backend/Dockerfile` expone debugpy en `0.0.0.0:5678` y ejecuta Uvicorn con `--reload`.

Las imágenes o configuraciones de producción deben restringir CORS y desactivar debugpy y autoreload.

### 9. Usar configuración de entorno para URLs externas

`frontend/src/App.tsx` usa `VITE_API_BASE_URL`, y `frontend/.env.example` documenta esa variable.

No codificar URLs del backend ni secretos en componentes o código fuente.

## Testing

### 10. Acompañar cambios de API con tests de contrato

`backend/tests/test_routes.py` cubre endpoints, filtros, orden y agregaciones.

Todo nuevo endpoint o parámetro debe tener al menos un test de respuesta y uno de comportamiento relevante.

### 11. Ejecutar validaciones específicas antes de integrar cambios

El frontend define `build`, `lint` y `test` en `frontend/package.json`, y el backend usa pytest.

Los cambios frontend deben validar TypeScript, lint y tests; los cambios backend deben ejecutar pytest.

### 12. No ignorar warnings de dependencias

Los tests actuales pasan, pero muestran warnings de compatibilidad entre `httpx` y Starlette.

Las actualizaciones de dependencias deben revisar esos warnings y evitar normalizarlos como salida esperada.

## DX y dependencias

### 13. Mantener instalaciones reproducibles

Existe `frontend/package-lock.json`, pero `frontend/Dockerfile` usa `npm install`; `backend/requirements.txt` no fija versiones.

Los builds deben usar `npm ci` cuando corresponda y dependencias Python versionadas o bloqueadas.

### 14. Documentar la diferencia entre Docker y ejecución local

`frontend/vite.config.ts` apunta el proxy a `http://backend:8000`, hostname válido dentro de Compose, mientras la ejecución local usa `localhost:8000`.

Toda instrucción de ejecución debe indicar explícitamente qué modo está describiendo.

## Frontend

### 15. Separar lógica financiera de la presentación

`frontend/src/lib/financial-utils.ts` contiene `computeKPIs()` y `computeMonthlyData()`.

Los nuevos cálculos deben permanecer en utilidades testeables, no dentro de los componentes JSX.

### 16. Preservar estados de carga y error

`frontend/src/App.tsx` ya maneja `loading` y `error`, aunque el error mostrado es genérico.

Los nuevos flujos de datos deben conservar esos estados y, cuando sea posible, diferenciar errores de red, HTTP y formato.

### 17. Conservar la estructura de componentes y accesibilidad

Los componentes están separados entre `dashboard` y `ui`, y `frontend/src/App.tsx` usa secciones semánticas con `aria-label`.

Los nuevos componentes deben respetar esa separación y mantener HTML semántico y etiquetas accesibles.

## Documentación y agentes

### 18. Mantener sincronizados README, configuración y comportamiento real

`README.es.md` y `README.md` documentan Docker, proxy y `.env.example`, pero la UI aún muestra un período fijo distinto del generado por el backend.

Toda modificación de ejecución, endpoints o períodos debe actualizar ambas documentaciones.

### 19. No asumir que existen reglas o memoria de agentes

`AGENTS.md` referencia `.agents/rules`, `.agents/skills` y `memory-bank`, pero esas carpetas no existen actualmente.

Los agentes deben comprobar su existencia antes de usarlas y no asumir que contienen convenciones adicionales.
