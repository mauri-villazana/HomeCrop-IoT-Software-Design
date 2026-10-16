# Evidencias de colaboración en GitHub

Este documento registra las aportaciones individuales realizadas por los integrantes del equipo durante la actividad de análisis y mejora del diseño de software de HomeCrop IoT.

## Mauricio De Jesus Villazana

### Rama utilizada

`propuesta-mauricio`

### Aportaciones realizadas

- Identificación de responsabilidades del diseño original.
- Elaboración del diagrama del diseño original.
- Análisis de los problemas del diseño inicial.
- Desarrollo de una propuesta individual basada en separación de responsabilidades.
- Elaboración del diagrama de clases de la propuesta.
- Justificación de los beneficios de la solución.

### Propuesta desarrollada

La propuesta divide las responsabilidades de `HomeCropSystem` mediante clases especializadas:

- `SensorService`
- `RiegoService`
- `MedicionRepository`
- `NotificacionService`
- `DashboardService`
- `HomeCropController`

La idea principal es que cada clase tenga una responsabilidad específica y que `HomeCropController` coordine los diferentes componentes.

### Pull Request

Pull Request #1: `Propuesta de mejora individual - Mauricio`

La propuesta fue desarrollada inicialmente en la rama `propuesta-mauricio` y posteriormente integrada a `main`.

---

## Diana Valeria Ramirez Gonzalez

### Rama utilizada

`propuesta-diana`

### Aportaciones realizadas

- Desarrollo de una propuesta individual de mejora basada en los principios SOLID.
- Análisis de los problemas del diseño original relacionados con responsabilidades múltiples, acoplamiento y dependencias.
- Separación del sistema en clases especializadas.
- Incorporación de interfaces para sensores, control de riego, almacenamiento y notificaciones.
- Elaboración del diagrama de clases de la arquitectura propuesta.
- Registro de sus cambios mediante commits individuales.

### Propuesta desarrollada

La propuesta de Diana reorganiza HomeCrop IoT aplicando los cinco principios SOLID.

El diseño mantiene componentes especializados como:

- `HomeCropController`
- `SensorService`
- `RiegoService`
- `MedicionRepository`
- `NotificacionService`
- `DashboardService`

La principal diferencia de esta propuesta es el uso de abstracciones e interfaces como:

- `ISensor`
- `IControlRiego`
- `IMedicionRepository`
- `INotificador`

Estas interfaces permiten utilizar diferentes implementaciones sin modificar directamente la lógica principal del sistema.

Por ejemplo, distintos sensores pueden implementar `ISensor`, mientras que diferentes mecanismos de notificación, como correo o aplicación, pueden implementar `INotificador`.

Con esta organización se busca reducir el acoplamiento, facilitar las pruebas, permitir la sustitución de componentes y preparar el sistema para futuras ampliaciones.

### Pull Request

Pull Request #2: `Propuesta de mejora del diseño de software - Diana`

La propuesta fue desarrollada en la rama `propuesta-diana` y posteriormente integrada a `main`.

---

## Maria Elizabeth Martinez Galvan

### Rama utilizada

`propuesta-maria`

### Aportaciones realizadas

- Desarrollo de una propuesta individual basada en el patrón Observer.
- Diseño de una arquitectura orientada a eventos.
- Separación de los componentes encargados del monitoreo, riego, alertas y dashboard.
- Incorporación de un administrador de eventos para gestionar suscripciones y notificaciones.
- Elaboración del diagrama de clases mediante Mermaid.
- Registro de sus cambios mediante commits individuales.

### Propuesta desarrollada

La propuesta de Maria utiliza el patrón de diseño Observer y una arquitectura basada en eventos.

Los principales componentes son:

- `SensorService`
- `EventManager`
- `EventoMedicion`
- `Observer`
- `RiegoObserver`
- `AlertaObserver`
- `DashboardObserver`
- `ControlRiego`

En esta propuesta, `SensorService` obtiene las mediciones y genera eventos mediante `EventManager`.

Los diferentes observadores se suscriben a esos eventos y reaccionan de forma independiente:

- `RiegoObserver` evalúa si es necesario realizar el riego.
- `AlertaObserver` determina si debe generarse una alerta.
- `DashboardObserver` actualiza la información mostrada al usuario.

Esta estructura busca reducir el acoplamiento, ya que el componente encargado de obtener las mediciones no necesita conocer directamente todos los módulos que utilizarán la información.

También facilita incorporar nuevos observadores en el futuro sin modificar directamente el módulo que genera las mediciones.

### Pull Request

Pull Request #3: `Propuesta de mejora del diseño de software - Maria`

La propuesta fue desarrollada en la rama `propuesta-maria` mediante los commits correspondientes y posteriormente integrada a `main`.

## Resumen de las propuestas individuales

| Integrante | Enfoque principal | Característica distintiva |
|---|---|---|
| Mauricio | Servicios especializados y controlador | Divide las responsabilidades en servicios coordinados por `HomeCropController` |
| Diana | Principios SOLID | Utiliza interfaces y dependencias hacia abstracciones para facilitar sustitución y extensión |
| Maria | Observer y arquitectura basada en eventos | Los componentes reaccionan de forma independiente a eventos distribuidos por `EventManager` |

Las tres propuestas buscan resolver el problema de concentración de responsabilidades presente en el diseño inicial de `HomeCropSystem`, pero utilizan enfoques diferentes para organizar y relacionar los componentes.
