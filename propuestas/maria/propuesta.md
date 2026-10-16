# Propuesta de mejora del diseño de software HomeCrop IoT

## 1. Introducción

HomeCrop IoT es un sistema orientado al monitoreo y control de cultivos mediante sensores y dispositivos de riego. Para mejorar su diseño, se propone implementar el patrón de diseño Observer (Observador) y una arquitectura basada en eventos.

Esta propuesta busca reducir el acoplamiento entre los componentes del sistema y permitir que diferentes módulos reaccionen a los cambios detectados sin depender directamente unos de otros.

## 2. Problema identificado

En un sistema de monitoreo agrícola, los sensores pueden generar información continuamente sobre variables como la humedad del suelo y la temperatura.

Si el módulo que obtiene estas mediciones también debe conocer directamente al sistema de riego, al panel de monitoreo y al módulo de notificaciones, se generan dependencias innecesarias.

Esto dificulta agregar nuevos componentes, modificar los existentes y mantener el software a medida que crecen sus funcionalidades.

## 3. Propuesta de solución

Se propone utilizar el patrón Observer para que los componentes interesados puedan suscribirse a los eventos generados por el sistema.

La arquitectura incluirá los siguientes componentes:

- **SensorService:** obtiene las mediciones de los sensores.
- **EventManager:** administra los eventos y las suscripciones de los componentes.
- **EventoMedicion:** representa una nueva medición disponible.
- **RiegoObserver:** evalúa las mediciones recibidas y solicita el riego cuando corresponda.
- **AlertaObserver:** genera alertas cuando las mediciones superan los límites configurados.
- **DashboardObserver:** actualiza la información que se presenta en el panel de monitoreo.

Cuando se obtiene una nueva medición, el sistema genera un evento. El administrador de eventos notifica a los componentes suscritos, y cada uno ejecuta su propia lógica de manera independiente.

## 4. Funcionamiento propuesto

1. El SensorService obtiene una medición de humedad o temperatura.
2. Se genera un EventoMedicion con los datos obtenidos.
3. El EventManager identifica los componentes suscritos al evento.
4. El RiegoObserver evalúa si las condiciones requieren activar el riego.
5. El AlertaObserver determina si es necesario generar una notificación.
6. El DashboardObserver actualiza la información del monitoreo.

Las decisiones de riego deben considerar las reglas de seguridad y los límites configurados para el cultivo.

## 5. Beneficios de la propuesta

- Menor acoplamiento entre los módulos.
- Facilidad para incorporar nuevos observadores.
- Mayor flexibilidad para modificar el comportamiento del sistema.
- Separación de las responsabilidades de monitoreo, riego y notificaciones.
- Posibilidad de probar cada componente de forma independiente.
- Mejor capacidad de adaptación ante nuevos requisitos.

## 6. Consideraciones de diseño

El administrador de eventos debe gestionar adecuadamente las suscripciones para evitar notificaciones duplicadas y permitir que los componentes dejen de recibir eventos cuando sea necesario.

También se deben contemplar errores en los observadores, límites de medición y mecanismos de seguridad para impedir activaciones de riego no autorizadas.

## 7. Conclusión

La aplicación del patrón Observer permite que HomeCrop IoT responda a los cambios de las mediciones mediante componentes independientes que reaccionan a eventos.

Esta propuesta mejora la flexibilidad y extensibilidad de la arquitectura, facilitando la incorporación de nuevas funciones sin necesidad de modificar directamente el módulo que obtiene las mediciones.