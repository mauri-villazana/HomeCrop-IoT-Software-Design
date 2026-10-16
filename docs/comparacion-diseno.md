# Comparación del diseño de HomeCrop IoT

## Diseño original

El diseño original se representa mediante una sola clase, `HomeCropSystem`, que concentra las diferentes responsabilidades del sistema.

Entre ellas se encuentran:

- Lectura de sensores.
- Evaluación de la necesidad de riego.
- Control de la minibomba.
- Registro de mediciones.
- Consulta de históricos.
- Generación de alertas.
- Obtención de información para el dashboard.

Esta organización facilita representar inicialmente el funcionamiento del sistema, pero puede generar dificultades conforme el proyecto crezca.

## Diseño mejorado - Propuesta de Mauricio

La propuesta de mejora separa las responsabilidades en clases especializadas:

- `SensorService`
- `RiegoService`
- `MedicionRepository`
- `NotificacionService`
- `DashboardService`
- `HomeCropController`

`HomeCropController` funciona como coordinador y delega cada operación al componente especializado correspondiente.

## Comparación

| Aspecto | Diseño original | Diseño mejorado |
|---|---|---|
| Número de responsabilidades por clase | Muchas en `HomeCropSystem` | Responsabilidades distribuidas |
| Mantenimiento | Los cambios afectan una clase central | Los cambios pueden concentrarse en un componente |
| Pruebas | Varias funciones están agrupadas | Los componentes pueden probarse con mayor independencia |
| Reutilización | Funciones concentradas en una clase | Servicios especializados reutilizables |
| Crecimiento | La clase principal aumenta de complejidad | Se pueden agregar nuevos componentes |
| Organización | Centralizada | Modular y especializada |

## Resultado

El diseño mejorado conserva las funcionalidades planteadas originalmente para HomeCrop IoT, pero reorganiza la estructura del software para facilitar su mantenimiento y evolución.
