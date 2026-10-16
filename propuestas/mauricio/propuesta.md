# Propuesta de mejora - Mauricio

## Objetivo

La propuesta busca mejorar la estructura del software de HomeCrop IoT mediante la separación de responsabilidades en clases especializadas.

En el diseño original, una sola clase denominada `HomeCropSystem` concentra funciones relacionadas con sensores, control de riego, almacenamiento, alertas y consulta de información.

Esta concentración puede dificultar el mantenimiento, las pruebas y futuras modificaciones del sistema.

## Estructura propuesta

Se propone dividir las responsabilidades en las siguientes clases:

### SensorService

Responsable de obtener la información generada por los sensores.

Funciones principales:

- `leerHumedadSuelo()`
- `leerTemperatura()`
- `leerHumedadAmbiental()`
- `leerNivelAgua()`

### RiegoService

Responsable de evaluar las condiciones de humedad y controlar el sistema de riego.

Funciones principales:

- `evaluarNecesidadRiego()`
- `activarBomba()`
- `detenerBomba()`

### MedicionRepository

Responsable de almacenar y consultar las mediciones generadas por el sistema.

Funciones principales:

- `guardarMedicion()`
- `consultarHistorial()`

### NotificacionService

Responsable de generar alertas y notificaciones cuando exista una condición que requiera la atención del usuario.

Funciones principales:

- `generarAlerta()`
- `enviarNotificacion()`

### DashboardService

Responsable de proporcionar al usuario la información actual e histórica del sistema.

Funciones principales:

- `obtenerEstadoActual()`
- `obtenerHistorial()`

### HomeCropController

Responsable de coordinar la comunicación entre las diferentes clases del sistema.

Esta clase no realiza directamente todas las funciones, sino que utiliza los servicios especializados cuando necesita leer sensores, realizar un riego, guardar información o generar una alerta.

## Justificación de la propuesta

Separar las responsabilidades permite que cada clase tenga un propósito específico.

Por ejemplo, los cambios relacionados con sensores se realizarían en `SensorService`, mientras que las modificaciones del sistema de riego se concentrarían en `RiegoService`.

De esta manera, los componentes tienen menor dependencia entre sí y el código puede ser más fácil de comprender, mantener y probar.

Además, esta organización facilita agregar nuevas funcionalidades en el futuro sin modificar una única clase central que contenga toda la lógica del sistema.
