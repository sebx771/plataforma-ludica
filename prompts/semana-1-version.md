## Objetivo
Agregar `GET /api/version` para devolver la versión configurada en `app/proyecto.py` y cubrir el contrato con una prueba.

## Herramienta y modelo
Copilot SDK en VS Code; modelo Auto(gpt 6 Luna).

## Prompt
```markdown
## Rol
Actúa como desarrollador backend con experiencia en FastAPI y pruebas con pytest.

## Objetivo
Agregar `GET /api/version` para devolver la versión definida en `app/proyecto.py`.
La respuesta debe ser un objeto JSON con el campo `version`.

## Contexto
Lee `AGENTS.md`, `app/proyecto.py`, `app/main.py` y `tests/test_inicio.py`.

## Restricciones
Mantén la arquitectura existente y usa FastAPI, SQLModel y pytest.
No modifiques las pruebas existentes; agrega una prueba para el nuevo endpoint.
No cambies la versión definida en `app/proyecto.py`.

## Formato de salida
Antes de escribir código, muestra el plan con las rutas completas de los archivos que vas a modificar y espera mi aprobación.

## Ejemplo
`GET /api/version` devuelve `{"version": "0.1.0"}`.

## Criterio de éxito
`ruff check .` no reporta errores y las pruebas de `tests/test_inicio.py` pasan.
Si después de 3 intentos no se cumple, detente y explica el problema.
```

## Resultado
Se agregó el endpoint y la prueba en `tests/test_inicio.py`, y se documentó el contrato en `specs/plan.md`.
Ruff pasó y las siete pruebas de `tests/test_inicio.py` pasaron.
No fue necesario corregir el resultado.
