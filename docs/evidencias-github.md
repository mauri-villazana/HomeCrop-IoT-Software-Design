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

- Desarrollo de una propuesta individual de mejora.
- Aplicación de principios SOLID al diseño de HomeCrop IoT.
- Elaboración de un diagrama de clases de la arquitectura propuesta.
- Registro de sus cambios mediante commits individuales.

### Propuesta desarrollada

La propuesta de Diana reorganiza el sistema aplicando principios SOLID con el objetivo de separar responsabilidades, reducir dependencias y facilitar futuras modificaciones.

### Pull Request

Pull Request #2: `Propuesta de mejora del diseño de software - Diana`

La propuesta fue desarrollada en la rama `propuesta-diana` e integrada posteriormente a `main`.

---

## Maria Elizabeth Martinez Galvan

### Rama utilizada

`propuesta-maria`

### Aportaciones realizadas

- Desarrollo de una propuesta individual de mejora.
- Aplicación del patrón Observer.
- Propuesta de una arquitectura basada en eventos.
- Elaboración del diagrama de clases utilizando Mermaid.
- Registro de sus cambios mediante commits individuales.

### Propuesta desarrollada

La propuesta de Maria utiliza el patrón Observer y una arquitectura basada en eventos para permitir que diferentes componentes reaccionen ante cambios del sistema sin depender fuertemente unos de otros.

### Pull Request

Pull Request #3: `Propuesta de mejora del diseño de software - Maria`

Los archivos y commits de la propuesta fueron desarrollados por la cuenta de Maria y posteriormente integrados a `main`.

---

## Resumen de las propuestas

| Integrante | Enfoque principal |
|---|---|
| Mauricio | Separación de responsabilidades mediante servicios especializados y controlador |
| Diana | Aplicación de principios SOLID |
| Maria | Patrón Observer y arquitectura basada en eventos |

Las tres propuestas presentan diferentes formas de mejorar la organización del software de HomeCrop IoT y facilitar su mantenimiento y evolución.
