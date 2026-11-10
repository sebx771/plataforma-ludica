## Endpoint de versión
1. **Objetivo:** agregar `GET /api/version` para devolver la versión configurada en `app/proyecto.py` y cubrirlo con una prueba.
2. **Herramienta y modelo:** Copilot SDK en VS Code; modelo Auto(gpt 6 Luna).
3. **Prompt:**
   > Lee AGENTS.md. Agrega el endpoint GET /api/version, que devuelva la versión definida en app/proyecto.py, con su prueba en tests/test_inicio.py. Antes de escribir código, explícame qué archivos vas a modificar y espera mi aprobación.

4. **Resultado:** se agregó el endpoint y la prueba en `tests/test_inicio.py`, y se documentó el contrato en `specs/plan.md`. Ruff pasó y las siete pruebas de `tests/test_inicio.py` pasaron. No fue necesario corregir el resultado.
