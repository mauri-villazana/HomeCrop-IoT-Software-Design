# Diseño original de HomeCrop IoT

## 1. Identificación de responsabilidades

HomeCrop IoT se encuentra actualmente en una etapa de diseño y prototipado, por lo que todavía no cuenta con una estructura definitiva de clases implementada.

Para realizar el análisis solicitado se toma como referencia un diseño inicial en el que una clase principal denominada `HomeCropSystem` concentra las funciones planteadas originalmente para el sistema.

## Clase principal: HomeCropSystem

La clase `HomeCropSystem` tendría la responsabilidad de coordinar el funcionamiento general del sistema HomeCrop IoT.

Sus principales responsabilidades serían las siguientes:

### Monitoreo de sensores

La clase se encargaría de obtener las mediciones generadas por los diferentes sensores del sistema:

- Humedad del suelo.
- Temperatura ambiental.
- Humedad ambiental.
- Nivel de agua disponible en el depósito.

Funciones asociadas:

- `leerHumedadSuelo()`
- `leerTemperatura()`
- `leerHumedadAmbiental()`
- `leerNivelAgua()`

### Evaluación de las condiciones de la planta

La clase analizaría principalmente la humedad del suelo para determinar si la planta necesita riego.

Función asociada:

- `evaluarNecesidadRiego()`

### Control del sistema de riego

Cuando la humedad del suelo se encuentre por debajo del nivel establecido, la clase sería responsable de activar la minibomba.

Cuando la humedad alcance nuevamente un nivel adecuado, también tendría que detener el riego.

Funciones asociadas:

- `activarBomba()`
- `detenerBomba()`

### Administración de las mediciones

La clase también tendría la responsabilidad de registrar las mediciones obtenidas por los sensores y conservar información como la fecha y hora de cada lectura.

Funciones asociadas:

- `guardarMedicion()`
- `consultarHistorial()`

### Gestión de alertas

El sistema deberá generar alertas cuando se detecten situaciones que requieran la atención del usuario, por ejemplo, cuando el nivel de agua del depósito sea bajo.

Función asociada:

- `generarAlerta()`

### Información para el usuario

La clase también proporcionaría la información necesaria para que el usuario pueda consultar el estado actual de la planta y los datos históricos mediante un dashboard.

Función asociada:

- `obtenerEstadoActual()`

## Resumen de responsabilidades

En el diseño inicial, la clase `HomeCropSystem` concentra las siguientes responsabilidades:

1. Leer los sensores.
2. Analizar las condiciones de la planta.
3. Determinar cuándo es necesario realizar el riego.
4. Controlar la minibomba.
5. Registrar las mediciones.
6. Consultar información histórica.
7. Generar alertas.
8. Proporcionar información al dashboard.

Esta estructura será utilizada como punto de partida para analizar posteriormente los problemas que pueden presentarse cuando una sola clase concentra demasiadas responsabilidades.
