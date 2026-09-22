# Frontend and Dependency Rules

## Nombre

Experiencia de desarrollo y consistencia del frontend.

## Alcance

Aplica a React, TypeScript, componentes, estados de carga/error, instalación de dependencias y builds.

## Justificación

`frontend/src/App.tsx` maneja estados `loading` y `error`, usa `VITE_API_BASE_URL` y contiene secciones con `aria-label`. El proyecto organiza componentes en `dashboard` y `ui`, tiene `frontend/package-lock.json`, pero `frontend/Dockerfile` ejecuta `npm install`.

## Guía específica del proyecto

- Conservar estados de carga, error y éxito en todo flujo que consuma la API.
- Separar errores técnicos de los mensajes visibles para el usuario y conservar suficiente detalle para depuración.
- Mantener HTML semántico, `aria-label` y accesibilidad en nuevas vistas.
- Usar `npm ci` en builds reproducibles cuando exista `package-lock.json`.
- Fijar o bloquear versiones de dependencias Python en `backend/requirements.txt` o mediante un mecanismo equivalente.
- No crear una segunda fuente de datos mock en el frontend sin documentar su propósito.
