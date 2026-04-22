# Cargue-de-datos
Este proyecto se enfoca en el diseño y creación de diferentes programas batch que formaran parte de un aplicativo con el fin
de cargar datos masivos diarios

## Programa: Parametros.cbl
### Objetivo.
Crear parametros con el fin de controlar el cargue diarios en diferentes proyectos
```mermaid
flowchart TD
    A([INICIO]) --> B[Obtener fecha del sistema]
    B --> C[Mostrar fecha al usuario\n¿Desea ejecutar el proceso?]
    C --> D{Usuario responde}
    D -->|N| E[Mostrar: Proceso cancelado]
    E --> F([FIN])
    D -->|S| G[Abrir archivo PARAMETROS]
    G --> H{File Status = 00?}
    H -->|No| I[Mostrar: Error abriendo archivo]
    I --> F
    H -->|Sí| J[Buscar registro por fecha de hoy]
    J --> K{¿Existe registro?}
    K -->|Sí| L[Mostrar: Proceso ya fue ejecutado hoy]
    L --> F
    K -->|No| M[Llamar VALDTRNS]
    M --> N{Return Code = 0?}
    N -->|No| O[Mostrar: Error en VALDTRNS]
    O --> F
    N -->|Sí| P[Llamar APLICTRNS]
    P --> Q{Return Code = 0?}
    Q -->|No| R[Mostrar: Error en APLICTRNS]
    R --> F
    Q -->|Sí| S[Llamar GENREPORT]
    S --> T{Return Code = 0?}
    T -->|No| U[Mostrar: Error en GENREPORT]
    U --> F
    T -->|Sí| V[Llamar CONCILIA]
    V --> W{Return Code = 0?}
    W -->|No| X[Mostrar: Error en CONCILIA]
    X --> F
    W -->|Sí| Y[Grabar fecha en archivo PARAMETROS]
    Y --> Z[Mostrar: Proceso completado exitosamente]
    Z --> F
```
