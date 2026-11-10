# AGENTS.md
Contexto y convenciones del proyecto. Léalo antes de cambiar código.

## Proyecto
Plataforma web lúdica para niños. Curso: Ciencias; mecánica: Memoria de parejas. Roles docente y niño; el niño entra con código de clase y avatar, sin correo. Prototipo con inicio, `/salud`, `/api/proyecto`, `/docs` y PWA; aún sin modelos ni servicios.

## Stack y comandos
Python >= 3.11 (CI: 3.13), FastAPI, Jinja2, SQLModel, pytest/TestClient y Ruff. SQLite en desarrollo, PostgreSQL al publicar; CI en GitHub Actions y despliegue en Render.
- Instalar: `pip install -r requirements-dev.txt`
- Ejecutar: `uvicorn app.main:app --reload` (http://127.0.0.1:8000; API en `/docs`)
- Verificar en orden: `ruff check .` y `pytest -v`; CI también consulta `/salud`.
- Prueba puntual: `pytest tests/test_inicio.py::test_salud_responde_ok -v` o `pytest -k <nombre> -v`.
- Hooks: `pre-commit install` (Ruff y `pytest -q`).
- Entrega: copie `entregas/plantilla.md` a `entregas/semana-N.md` y ejecute `python entregar.py N`.

## Arquitectura
- `app/main.py` monta estáticos y routers; `app/rutas/` presenta HTML/API y delega reglas a `app/servicios/`; `app/modelos/` contiene tablas.
- `app/proyecto.py` es fuente única de aprendiz, curso, mecánica, versión y URL pública; no duplique esos datos.
- `/sw.js` debe servirse desde la raíz para controlar todo el sitio; PWA e iconos están en `app/static/`.
- Si cambia un recurso cacheado, actualice la versión de `CACHE` en `sw.js`. `pyproject.toml` configura pytest; no hace falta instalar el paquete.

## Documentación

- Mantenga alineados `README.md`, `specs/spec.md`, `specs/user-flow.md`, `specs/plan.md` y `specs/tasks.md`.
- Criterios observables de `specs/spec.md` deben tener cobertura en `tests/aceptacion/`; ADR nuevos parten de `specs/adr/0000-plantilla.md`.
- Guarde prompts como `prompts/semana-N-tema.md`, con objetivo, herramienta/modelo, prompt exacto y resultado.
- Lea `STATE.md` al iniciar y actualícelo al cerrar.

## Convenciones y entorno

- Use nombres claros en español; preserve la separación rutas → servicios → modelos y pruebe todo comportamiento modificado.
- Cambios pequeños, una tarea por rama. Siga `.github/skills/commit/SKILL.md`; commits Conventional Commits en español, propuestos para aprobación.
- Use secretos desde `.env` (basado en `.env.example`); nunca suba secretos, bases locales ni PDF de `entregas/`.
- No modifique pruebas para hacerlas pasar, no use datos personales reales y verifique paquetes en PyPI antes de agregarlos.
- Revise diferencias con `git diff --ignore-space-at-eol` por posibles finales CRLF. En Windows use `venv/Scripts/`; en Linux/WSL, `.venv`.
- `requirements-dev.txt` usa `httpx2` porque Starlette lo importa; no lo cambie por `httpx`.

## Lecciones aprendidas
Añada aquí una regla concreta cuando un error revele una lección; `entregar.py` lee esta sección.
