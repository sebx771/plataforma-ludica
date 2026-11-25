# Especificación

## Contexto

La plataforma ofrece actividades educativas de Ciencias para niños de primaria. El prototipo permite que un docente consulte y mantenga actividades de memoria y que un niño las resuelva mediante código de clase, alias y avatar.

El curso asignado es **Ciencia** y la mecánica asignada es **Memoria de parejas**. Las respuestas obligatorias están documentadas en `specs/respuestas-cliente-memoria-parejas.md`; prevalecen sobre dudas o supuestos previos.

## Historias de usuario

### H1. El docente gestiona las actividades del curso

Como docente, quiero crear, consultar y modificar actividades de Ciencias, para que el niño encuentre contenido válido y organizado.

**Criterios de aceptación**

- Dado que el docente abre el panel de actividades, cuando la base contiene actividades, entonces puede verlas por nombre o listado.
- Dado que el docente crea o modifica una actividad, cuando guarda una actividad válida, entonces queda disponible para el niño.
- Dado que una actividad tiene menos de 5 preguntas o una pregunta no cumple 3–4 opciones y una sola respuesta correcta, entonces el sistema rechaza el guardado y muestra el error.

### H2. La plataforma inicia con contenido del curso

Como usuario nuevo, quiero que la aplicación cargue contenido de ejemplo al estar vacía, para poder probar el flujo completo sin configuración manual.

**Criterios de aceptación**

- Dado que la base de datos está vacía al iniciar, entonces se crea una clase de ejemplo, 3 actividades de Ciencias y 3 niños ficticios.
- Dado que cada actividad inicial existe, entonces contiene exactamente 5 preguntas.
- Dado que existen datos previos, entonces el arranque no duplica ni reemplaza el contenido inicial.
- Dado que una pregunta inicial existe, entonces tiene entre 3 y 4 opciones y una sola respuesta correcta.

### H3. El niño entra con el código de la clase, su alias y un avatar

Como niño, quiero elegir el código de clase, mi alias y mi avatar, para comenzar una actividad sin crear una cuenta con correo.

**Criterios de aceptación**

- Dado un código válido, entonces el sistema muestra únicamente los alias pertenecientes a esa clase.
- Dado un alias válido de la clase y uno de los 6 avatares permitidos (`colibri`, `tortuga`, `delfin`, `jaguar`, `buho`, `rana`), entonces permite iniciar una sesión de juego.
- Dado un código, alias o avatar inválido, entonces rechaza el ingreso sin crear progreso.

### H4. El niño resuelve una actividad y sabe de inmediato si acertó

Como niño, quiero recibir retroalimentación al descubrir cartas, para saber si encontré una pareja correcta durante la partida.

**Criterios de aceptación**

- Dado que el niño voltea dos cartas, entonces el sistema indica de inmediato si forman la pareja asociada a una pregunta.
- Dado que las cartas forman pareja, entonces permanecen descubiertas.
- Dado que las cartas no forman pareja, entonces se vuelven a ocultar después de mostrar la indicación.
- Dado que el niño completa las 6 parejas, entonces se crea un intento con aciertos, total de preguntas, duración y fecha.

### H5. La plataforma aplica la regla de Memoria de parejas

Como niño, quiero jugar siguiendo las reglas acordadas para Ciencias, para reforzar las parejas que me generan más dificultad.

**Criterios de aceptación**

- Dado una actividad válida, entonces la partida contiene 12 cartas: 6 enunciados y sus 6 respuestas correctas.
- Dado que el niño voltea una carta sin completar una pareja, entonces el contador de fallos de esa pareja aumenta en 1.
- Dado que descubre una pareja al primer intento de esa pareja, entonces su contador disminuye en 1, sin bajar de 0.
- Dada una siguiente partida, entonces usa las 6 parejas con mayor contador de fallos del niño.
- Dado un empate en fallos, entonces selecciona las parejas más antiguas según su orden de creación.

### H6. El docente consulta el progreso de cada niño

Como docente, quiero consultar el progreso individual, para orientar el acompañamiento sin identificar a los niños con datos personales.

**Criterios de aceptación**

- Dado que existen intentos de un niño, entonces el docente puede consultar sus aciertos, totales y porcentaje de aciertos.
- Dado que existen intentos repetidos de una actividad, entonces las actividades completadas se cuentan una sola vez por niño.
- Dado el historial de intentos de un niño, entonces el tiempo de juego mostrado es la suma de sus duraciones en segundos.
- Dado que no existen intentos, entonces el progreso se presenta con valores en cero y sin datos ficticios.

## Requisitos funcionales

| Código | Requisito | Historia |
| --- | --- | --- |
| RF1 | Mantener actividades con mínimo 5 preguntas y estructura válida. | H1 |
| RF2 | Crear datos iniciales solo cuando la base esté vacía. | H2 |
| RF3 | Permitir entrada por código de clase, alias y avatar. | H3 |
| RF4 | Crear un intento al completar una partida. | H4 |
| RF5 | Calcular aciertos y retroalimentación inmediata. | H4, H5 |
| RF6 | Mantener contadores de fallos por niño y pareja. | H5 |
| RF7 | Seleccionar la siguiente partida por prioridad de fallos y antigüedad. | H5 |
| RF8 | Mostrar progreso individual y métricas acumuladas. | H6 |
| RF9 | Cada intento guarda aciertos, total, duración y fecha. | H4 |

## Requisitos no funcionales

| Código | Requisito | Cómo se verifica |
| --- | --- | --- |
| RNF1 | La aplicación no requiere correo para el acceso del niño. | Probar H3 con datos válidos e inválidos. |
| RNF2 | El prototipo conserva los datos entre reinicios. | Reiniciar la app y consultar datos existentes. |
| RNF3 | La PWA usa `/sw.js` desde la raíz y permite instalación. | Ejecutar las pruebas de manifiesto y service worker. |
| RNF4 | Los errores de validación son claros y accionables. | Revisar respuestas HTTP y mensajes de interfaz. |

## Casos límite

- Actividad con menos de 5 preguntas: rechazar.
- Pregunta con menos de 3 o más de 4 opciones: rechazar.
- Pregunta sin respuesta correcta o con varias correctas: rechazar.
- Código de clase inexistente: rechazar.
- Alias inexistente o perteneciente a otra clase: rechazar.
- Avatar distinto de los 6 valores permitidos: rechazar.
- Base no vacía al arrancar: no ejecutar semillas.
- Niño sin intentos: porcentaje y métricas en cero.
- Empate de contadores: seleccionar por orden de creación.
- Partida abandonada: no crea intento ni modifica las métricas.

## Fuera de alcance

- Recuperación de contraseña y cuentas personales.
- Sincronización fuera de línea posterior al MVP.
- Personalización libre de preguntas por el docente.
- Uso de datos personales reales de menores.
- Límites de tiempo o intentos por partida.

## Criterios de terminado

- Las 6 historias tienen criterios de aceptación medibles.
- Los criterios se cubren con pruebas automatizadas o pruebas manuales registradas.
- El arranque no genera datos duplicados.
- Los cálculos de porcentaje, tiempo y completados cumplen las reglas del Anexo A.
- La documentación funcional y técnica describen las mismas entidades y rutas.

## Dudas abiertas

| Duda | Respuesta del cliente |
| --- | --- |
| ¿Puede un docente eliminar una actividad? | Pendiente de confirmación; no se asume para el MVP. |
| ¿Puede personalizar las 6 parejas de una actividad? | No; el prototipo usa contenido curado. |
| ¿Se conserva el mejor resultado al repetir una actividad? | Pendiente de confirmación; cada ejecución completa genera un intento. |
