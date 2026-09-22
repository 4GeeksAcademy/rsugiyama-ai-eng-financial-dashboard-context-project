# Security and Configuration Rules

## Nombre

Configuración segura por entorno.

## Alcance

Aplica a CORS, debugpy, autoreload, URLs de API, variables de entorno, Dockerfiles y despliegues.

## Justificación

`backend/app/main.py` permite todos los orígenes, métodos y headers. `backend/Dockerfile` expone debugpy en `0.0.0.0:5678` y ejecuta Uvicorn con `--reload`. El frontend usa `VITE_API_BASE_URL` y el proxy de `frontend/vite.config.ts` apunta a `http://backend:8000` dentro de Compose.

## Guía específica del proyecto

- Tratar CORS abierto, debugpy y autoreload como configuración exclusiva de desarrollo.
- Restringir orígenes CORS y desactivar debugpy y `--reload` en producción.
- No codificar URLs externas ni secretos en componentes o código fuente.
- Usar `VITE_API_BASE_URL` y `frontend/.env.example` para configurar un backend alternativo.
- Recordar que `backend:8000` funciona dentro de Docker Compose; en ejecución manual el backend está en `localhost:8000`.
- Mantener separados los modos de desarrollo y producción en Dockerfiles o mediante configuración explícita de entorno.
