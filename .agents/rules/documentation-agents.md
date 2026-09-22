# Documentation and Agent Rules

## Nombre

Documentación operativa y contexto para agentes.

## Alcance

Aplica a `README.md`, `README.es.md`, `AGENTS.md`, `.agents`, `memory-bank` y cualquier cambio que afecte la ejecución o las convenciones del repositorio.

## Justificación

`README.md` y `README.es.md` documentan Docker, el proxy y `frontend/.env.example`. `AGENTS.md` referencia `.agents/rules`, `.agents/skills` y `memory-bank`; la estructura de reglas propuesta se implementa en `.agents/rules`.

## Guía específica del proyecto

- Mantener sincronizados `README.md`, `README.es.md`, Docker Compose y el comportamiento real.
- Documentar cambios en comandos, endpoints, variables de entorno o períodos de datos en ambos README.
- Antes de actuar, comprobar si existen `.agents/rules`, `.agents/skills` y `memory-bank`; no asumir que contienen archivos.
- Consultar las reglas relevantes por área antes de modificar código.
- Referenciar rutas reales del repositorio y distinguir claramente entre configuración Docker y ejecución local.
- No introducir secretos, credenciales ni archivos `.env` en el control de versiones.
