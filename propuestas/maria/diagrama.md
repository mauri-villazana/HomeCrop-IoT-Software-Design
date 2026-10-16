# Diagrama de clases — HomeCrop IoT
## Patrón Observer y arquitectura basada en eventos

```mermaid
classDiagram
    class SensorService {
        +obtenerMedicion()
        +publicarMedicion()
    }

    class EventManager {
        -observadores
        +suscribir()
        +cancelarSuscripcion()
        +publicarEvento()
        +notificar()
    }

    class EventoMedicion {
        +humedad
        +temperatura
        +fechaHora
    }

    class Observer {
        <<interface>>
        +actualizar(evento)
    }

    class RiegoObserver {
        +actualizar(evento)
        +evaluarCondiciones()
        +solicitarRiego()
    }

    class AlertaObserver {
        +actualizar(evento)
        +evaluarLimites()
        +generarAlerta()
    }

    class DashboardObserver {
        +actualizar(evento)
        +actualizarPanel()
    }

    class ControlRiego {
        +activarRiego()
        +desactivarRiego()
    }

    SensorService --> EventManager : publica mediciones
    EventManager --> EventoMedicion : distribuye
    EventManager o-- Observer : administra suscripciones
    Observer <|.. RiegoObserver
    Observer <|.. AlertaObserver
    Observer <|.. DashboardObserver
    RiegoObserver --> ControlRiego : solicita acciones


```

## Descripción del diagrama

- **SensorService:** obtiene los datos de los sensores.
- **EventManager:** administra las suscripciones y distribuye los eventos.
- **EventoMedicion:** contiene la información de cada medición.
- **Observer:** define el contrato común para los componentes que reciben eventos.
- **RiegoObserver:** evalúa las condiciones para solicitar el riego.
- **AlertaObserver:** detecta condiciones que requieren una alerta.
- **DashboardObserver:** actualiza la información mostrada en el panel.
- **ControlRiego:** ejecuta las acciones de riego autorizadas por el sistema.