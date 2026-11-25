# Flujo de usuario

Pantallas y transiciones de cada rol, en Mermaid.

## Docente
```mermaid
flowchart TD
    A["Inicio"] --> B["Panel del docente"]
    B --> C["Listado de actividades"]
    C --> D["Crear actividad"]
    C --> E["Editar actividad"]
    D --> F{"5 preguntas y 3-4 opciones?"}
    E --> F
    F -->|"Si"| G["Guardar y publicar"]
    F -->|"No"| H["Mostrar errores"]
    H --> D
    B --> I["Seleccionar niño"]
    I --> J["Ver intentos y métricas"]
```

## Niño
```mermaid
flowchart LR
    A["Inicio"] --> B["Ingresar código de clase"]
    B --> C["Elegir alias de la clase"]
    C --> D["Elegir avatar"]
    D --> E{"Datos válidos?"}
    E -->|"Sí"| F["Listado de actividades"]
    E -->|"No"| B
    F --> G["Iniciar partida"]
    G --> H["Voltear primera carta"]
    H --> I["Voltear segunda carta"]
    I --> J{"Forma pareja?"}
    J -->|"Sí"| K["Permanecen descubiertas"]
    J -->|"No"| L["Indicar error y ocultar"]
    K --> M{"Completó 6 parejas?"}
    L --> M
    M -->|"No"| H
    M -->|"Sí"| N["Guardar intento"]
```
