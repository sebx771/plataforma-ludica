# STATE.md

Estado del proyecto. Léalo al iniciar cada sesión de trabajo y actualícelo al cerrarla.

## Estado actual

Plantilla creada y desplegada. La página de inicio, la PWA y `/docs` están disponibles. Los endpoints `/salud`, `/api/version` y `/api/proyecto` están en funcionamiento; este último devuelve los datos de identificación del proyecto (aprendiz, curso, mecánica y versión), definidos en `app/proyecto.py`. El prompt, objetivo, herramienta/modelo y resultado están registrados en `prompts/README.md`.

## Decisiones

| Fecha | Decisión | Motivo |
| --- | --- | --- |
| 2026-11-10 | Agregar el endpoint `/api/proyecto` para consultar los datos de identificación del proyecto. | Exponer aprendiz, curso, mecánica y versión desde la API. |

## Siguiente paso

Mantener la documentación y las pruebas alineadas al incorporar nuevos endpoints.
