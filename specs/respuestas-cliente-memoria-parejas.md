# Respuestas del cliente: Memoria de parejas

Estas respuestas son obligatorias y prevalecen sobre los supuestos de specs/dudas-encargo.md.

## Para todas las mecánicas

- **Actividad:** grupo de preguntas del curso, con un mínimo de 5. Cada pregunta tiene un enunciado, de 3 a 4 opciones y una sola respuesta correcta.
- **Intento:** registro que se crea cuando un niño termina una actividad completa. Guarda los aciertos, el total de preguntas, la duración en segundos y la fecha.
- **Porcentaje de aciertos:** aciertos dividido por el total de preguntas, multiplicado por 100.
- **Contenido inicial:** al iniciar, la aplicación carga una clase de ejemplo, 3 actividades de 5 preguntas del curso y 3 niños ficticios, solo si la base de datos está vacía.
- **Entrada del niño:** el niño escribe el código de la clase, elige su alias en la lista de niños de esa clase y elige uno de los 6 avatares.
- **Métricas del docente:** el tiempo de juego es la suma de la duración de los intentos; las actividades completadas se cuentan sin repetir.

## Avatares

Los 6 avatares se identifican con estos valores, que se guardan en el campo avatar: colibri, tortuga, delfin, jaguar, buho y rana.

## Regla de la mecánica Memoria de parejas

- Cada pregunta es una pareja: el enunciado y la respuesta correcta son las dos cartas.
- El tablero tiene 6 parejas, es decir, 12 cartas.
- Cada pareja tiene un contador de fallos por niño. Suma 1 cada vez que se voltea una de sus cartas sin formar la pareja. Resta 1, sin bajar de 0, cada vez que se descubre al primer intento.
- La siguiente partida usa las 6 parejas con más fallos. Si hay empate, se toman en el orden en que se crearon.
