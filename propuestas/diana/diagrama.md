# Diagrama de arquitectura propuesta - HomeCrop IoT

## Diseño basado en los principios SOLID

El siguiente diagrama representa la arquitectura propuesta para HomeCrop IoT. Se utilizan clases especializadas e interfaces para separar responsabilidades, reducir el acoplamiento y facilitar la extensión del sistema.

```mermaid
classDiagram
direction TB

class HomeCropController {
    +solicitarLecturas()
    +solicitarRiego()
    +consultarEstado()
}

class SensorService {
    +obtenerMediciones()
}

class RiegoService {
    +evaluarNecesidadRiego()
    +activarRiego()
    +detenerRiego()
}

class MedicionRepository {
    +guardarMedicion()
    +consultarHistorial()
}

class NotificacionService {
    +generarAlerta()
    +enviarNotificacion()
}

class DashboardService {
    +obtenerEstadoActual()
    +obtenerHistorial()
}

class ISensor {
    <<interface>>
    +leerMedicion()
}

class SensorHumedad {
    +leerMedicion()
}

class SensorTemperatura {
    +leerMedicion()
}

class IControlRiego {
    <<interface>>
    +activar()
    +detener()
}

class ControlBomba {
    +activar()
    +detener()
}

class IMedicionRepository {
    <<interface>>
    +guardarMedicion()
    +consultarHistorial()
}

class RepositorioBaseDatos {
    +guardarMedicion()
    +consultarHistorial()
}

class INotificador {
    <<interface>>
    +enviar()
}

class NotificadorCorreo {
    +enviar()
}

class NotificadorApp {
    +enviar()
}

HomeCropController --> SensorService : solicita mediciones
HomeCropController --> RiegoService : coordina el riego
HomeCropController --> DashboardService : consulta información

SensorService --> ISensor : utiliza
ISensor <|.. SensorHumedad : implementa
ISensor <|.. SensorTemperatura : implementa

RiegoService --> IControlRiego : utiliza
IControlRiego <|.. ControlBomba : implementa

SensorService --> IMedicionRepository : registra mediciones
DashboardService --> IMedicionRepository : consulta datos
IMedicionRepository <|.. RepositorioBaseDatos : implementa

NotificacionService --> INotificador : utiliza
INotificador <|.. NotificadorCorreo : implementa
INotificador <|.. NotificadorApp : implementa

HomeCropController --> NotificacionService : solicita alertas