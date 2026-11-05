# AGENTS.md

Contexto y convenciones del proyecto para los agentes de IA. Léalo antes de realizar cambios.

## Proyecto

Plataforma web lúdica de cursos para niños. Curso: Ciencia. Mecánica: Memoria de Parejas.
Roles: docente y niño. El niño entra con código de clase y avatar, sin correo.

## Stack

- Python 3.11 o superior, FastAPI, plantillas Jinja2
- SQLModel con SQLite en desarrollo y PostgreSQL al publicar
- pytest con TestClient, Ruff
- GitHub Actions para el CI y Render para el despliegue

## Comandos

- Instalar: `pip install -r requirements-dev.txt`
- Ejecutar: `uvicorn app.main:app --reload`
- Pruebas: `pytest -v`
- Estilo: `ruff check .`

## Estructura

- `app/rutas/`: reciben la petición y llaman a los servicios; sin regla de negocio
- `app/servicios/`: regla de negocio, con pruebas propias
- `app/modelos/`: tablas de SQLModel
- `app/templates/`: vistas HTML con Jinja2; `app/static/`: estilos, JavaScript y recursos de la PWA
- `tests/`: pruebas; `tests/aceptacion/`: criterios de la especificación

## Documentación y plantillas del repositorio

Mantenga la documentación alineada con el código. Si un cambio modifica el comportamiento, los requisitos, la arquitectura o el flujo de usuario, actualice también los documentos relacionados.

- `README.md`: presentación del proyecto, instrucciones para instalar, ejecutar y verificar, y mapa de carpetas. Manténgalo como punto de entrada actualizado.
- `specs/spec.md`: contexto del producto, historias, requisitos y criterios de aceptación. Describa resultados observables, no detalles de implementación.
- `specs/user-flow.md`: pantallas y transiciones para los roles docente y niño. Actualice los diagramas cuando cambie la navegación.
- `specs/plan.md`: arquitectura, modelo de datos y contrato de API. Registre decisiones importantes por separado en `specs/adr/`, usando `specs/adr/0000-plantilla.md`.
- `specs/tasks.md`: tareas pequeñas vinculadas a una historia y a su prueba; mantenga actualizado su estado y las referencias a issues cuando correspondan.
- `tests/aceptacion/README.md`: indica cómo las pruebas de aceptación verifican los criterios de `specs/spec.md`. Las pruebas deben conservar esa trazabilidad.
- `prompts/README.md`: formato para guardar prompts relevantes. Cada registro debe incluir objetivo, herramienta y modelo, prompt exacto y resultado; use el nombre `semana-N-tema.md`.
- `entregas/plantilla.md`: cópiela como `entregas/semana-N.md` y complete sus secciones antes de generar la entrega con `python entregar.py N`.
- `app/templates/`: son plantillas de interfaz Jinja2, no documentos de especificación. Mantenga el HTML accesible y coherente con los requisitos y flujos documentados.

## Convenciones

- Nombres en español, claros y completos.
- Mantenga las reglas de negocio en servicios y las rutas enfocadas en recibir peticiones y delegar.
- Cambios pequeños, una tarea por rama; agregue o actualice pruebas para el comportamiento modificado.
- No duplique información: use el documento correspondiente como fuente y enlace o haga referencia desde los demás cuando sea necesario.

## Qué no hacer

- No escribir claves ni contraseñas en el código: se leen de variables de entorno.
- No instalar dependencias sin verificar que existen en pypi.org.
- No modificar ni borrar pruebas para que pasen.
- No usar datos personales reales.

## Lecciones aprendidas

Cada vez que el agente se equivoque, escriba aquí la regla que evita repetir el error.
