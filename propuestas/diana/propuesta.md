# Propuesta de mejora del diseño de software - Diana

## 1. Objetivo

Proponer una mejora en la arquitectura del software de HomeCrop IoT con el propósito de reducir el acoplamiento entre componentes, facilitar las pruebas y permitir que el sistema pueda incorporar nuevas funcionalidades sin requerir modificaciones innecesarias .

La propuesta parte del problema identificado en el diseño original, donde la clase `HomeCropSystem` concentra responsabilidades relacionadas con sensores, control de riego, almacenamiento, alertas y consulta de información.

Para mejorar esta estructura, se propone organizar el sistema mediante interfaces, clases especializadas y dependencias orientadas a abstracciones.

## 2. Problemas identificados en el diseño original

La concentración de diferentes funcionalidades en la clase `HomeCropSystem` puede ocasionar los siguientes problemas:

- **Responsabilidades múltiples:** una misma clase se encarga de operaciones que deberían estar separadas.
- **Alto acoplamiento:** los cambios en una funcionalidad pueden afectar otras operaciones del sistema.
- **Dificultad para extender el software:** incorporar nuevos tipos de sensores o mecanismos de notificación puede requerir modificar código existente.
- **Pruebas complicadas:** la dependencia directa entre componentes dificulta probar cada funcionalidad de forma aislada.
- **Dependencia de implementaciones concretas:** si las clases dependen directamente de dispositivos o mecanismos específicos, reemplazarlos puede requerir cambios en varias partes del sistema.

## 3. Estructura propuesta

Se propone reorganizar el sistema mediante componentes especializados y contratos definidos por interfaces.

### 3.1. HomeCropController

Será el punto de coordinación entre las solicitudes del usuario y los servicios del sistema.

Responsabilidades:

- Recibir solicitudes relacionadas con el monitoreo y el riego.
- Coordinar la ejecución de los servicios correspondientes.
- Entregar los resultados de las operaciones.

El controlador no realizará directamente la lectura de sensores, el almacenamiento de mediciones ni el envío de notificaciones.

### 3.2. SensorService

Se encargará de obtener las mediciones de los sensores instalados en el sistema.

Funciones principales:

- `leerHumedadSuelo()`
- `leerTemperatura()`
- `leerHumedadAmbiental()`
- `leerNivelAgua()`

Su implementación deberá utilizar una abstracción para permitir incorporar diferentes tipos de sensores.

### 3.3. RiegoService

Se encargará de evaluar las condiciones necesarias para el riego y coordinar el control de la bomba.

Funciones principales:

- `evaluarNecesidadRiego()`
- `activarBomba()`
- `detenerBomba()`

La lógica de decisión del riego deberá mantenerse separada de los detalles específicos del dispositivo que activa la bomba.

### 3.4. MedicionRepository

Gestionará el almacenamiento y la consulta de las mediciones generadas por el sistema.

Funciones principales:

- `guardarMedicion()`
- `consultarHistorial()`

Se propone definir una interfaz para el repositorio, de modo que la implementación del almacenamiento pueda cambiar sin afectar directamente los servicios que utilizan las mediciones.

### 3.5. NotificacionService

Se encargará de comunicar alertas cuando se detecten condiciones que requieran atención.

Funciones principales:

- `generarAlerta()`
- `enviarNotificacion()`

Su diseño permitirá incorporar diferentes medios de notificación mediante implementaciones compatibles con una misma interfaz.

### 3.6. DashboardService

Se encargará de preparar la información actual e histórica que necesita consultar el usuario.

Funciones principales:

- `obtenerEstadoActual()`
- `obtenerHistorial()`

Este componente utilizará los servicios y repositorios correspondientes sin encargarse directamente de leer los sensores ni de controlar la bomba.

## 4. Aplicación de los principios SOLID

### 4.1. S - Principio de responsabilidad única

Cada clase debe tener una responsabilidad principal bien definida.

En la propuesta, `SensorService` obtiene mediciones, `RiegoService` coordina el riego, `MedicionRepository` gestiona los datos y `NotificacionService` se encarga de las alertas.

De esta manera, los cambios relacionados con una funcionalidad se concentran en el componente correspondiente.

### 4.2. O - Principio abierto/cerrado

El software debe permitir agregar nuevas funcionalidades sin modificar innecesariamente el código existente.

Por ejemplo, si se necesita incorporar un nuevo tipo de sensor, se podrá crear una nueva implementación compatible con la interfaz de lectura de sensores.

Así, el sistema podrá ampliar sus capacidades sin tener que modificar toda la lógica de monitoreo.

### 4.3. L - Principio de sustitución de Liskov

Las implementaciones de una abstracción deben poder sustituirse entre sí sin alterar el comportamiento esperado del sistema.

Por ejemplo, diferentes implementaciones de sensores podrán utilizarse mediante una misma interfaz, siempre que cumplan el contrato establecido para obtener mediciones.

Esto permitirá reemplazar una implementación por otra compatible sin cambiar el funcionamiento esperado de los servicios que la utilizan.

### 4.4. I - Principio de segregación de interfaces

Es preferible definir interfaces pequeñas y específicas en lugar de una interfaz general que obligue a implementar operaciones innecesarias.

Por ejemplo, se pueden definir interfaces independientes para leer sensores, controlar el riego, almacenar mediciones y enviar notificaciones.

De esta manera, cada componente implementará únicamente las operaciones que necesita y se evitarán dependencias innecesarias.

### 4.5. D - Principio de inversión de dependencias

Los componentes de alto nivel deben depender de abstracciones y no directamente de implementaciones concretas.

Por ejemplo, `RiegoService` podrá depender de una interfaz para controlar la bomba, mientras que `MedicionRepository` podrá implementarse mediante diferentes mecanismos de almacenamiento.

Esto facilitará sustituir dispositivos o tecnologías sin modificar la lógica principal del sistema.

## 5. Beneficios esperados

La aplicación de los principios SOLID permitirá:

- Mejorar la organización y comprensión del código.
- Reducir el acoplamiento entre los componentes.
- Facilitar las pruebas unitarias.
- Incorporar nuevos sensores y mecanismos de notificación.
- Sustituir implementaciones sin afectar innecesariamente otras clases.
- Facilitar el mantenimiento y la detección de errores.
- Preparar el sistema para futuras ampliaciones.

## 6. Conclusión

La propuesta busca mejorar el diseño de HomeCrop IoT mediante una estructura modular basada en los principios SOLID.

A diferencia de una organización que únicamente separa funcionalidades, esta propuesta también establece criterios para definir las responsabilidades de las clases, diseñar interfaces y administrar las dependencias entre componentes.

Su aplicación permitirá desarrollar un sistema más flexible, mantenible y preparado para incorporar nuevas tecnologías y funcionalidades en el futuro.