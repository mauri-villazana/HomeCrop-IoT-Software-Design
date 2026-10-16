# Análisis de problemas de diseño

## 2. Problemas identificados en el diseño original

En el diseño inicial de HomeCrop IoT se representa una clase principal denominada `HomeCropSystem`, la cual concentra diferentes responsabilidades del sistema.

Entre estas responsabilidades se encuentran la lectura de sensores, la evaluación de las condiciones de la planta, el control del riego, el almacenamiento de mediciones, la consulta de información histórica, la generación de alertas y la entrega de información para el dashboard.

Aunque esta estructura permite representar de manera sencilla el funcionamiento general del sistema, concentrar todas estas responsabilidades en una sola clase puede ocasionar diferentes problemas durante el desarrollo y mantenimiento del software.

### Dificultad de mantenimiento

Una clase que contiene funciones pertenecientes a diferentes áreas del sistema puede crecer rápidamente conforme se agreguen nuevas funcionalidades.

Por ejemplo, un cambio en la lectura de sensores, en la lógica de riego o en el almacenamiento de datos obligaría a modificar la misma clase.

Esto puede hacer que el código sea más difícil de comprender y mantener.

### Dependencia entre responsabilidades

Al encontrarse diferentes funciones dentro de una misma clase, las responsabilidades quedan fuertemente relacionadas entre sí.

Un cambio realizado en una parte del sistema podría afectar accidentalmente otras funciones que no deberían depender directamente de ese cambio.

Por ejemplo, modificar la lógica de almacenamiento de datos no debería afectar el control de la minibomba.

### Dificultad para realizar pruebas

Cuando una sola clase contiene muchas responsabilidades, las pruebas pueden volverse más complicadas.

Para probar únicamente la lógica de riego, por ejemplo, podrían estar involucradas también funciones relacionadas con sensores, almacenamiento o notificaciones.

Separar estas responsabilidades permitiría probar cada componente de manera más independiente.

### Posible duplicación de código

Conforme el proyecto crezca, algunas funciones podrían comenzar a repetirse en diferentes partes del sistema si no existe una separación clara de responsabilidades.

Por ejemplo, la consulta o preparación de mediciones podría terminar implementándose tanto para el dashboard como para otros módulos futuros.

Una estructura especializada facilita reutilizar las funciones existentes.

### Dificultad para incorporar nuevas funcionalidades

HomeCrop IoT contempla posibles mejoras futuras, como análisis de datos e Inteligencia Artificial.

Si toda la lógica permanece concentrada en `HomeCropSystem`, agregar nuevas funcionalidades podría hacer que la clase aumente todavía más su tamaño y complejidad.

Una estructura dividida en componentes especializados permite incorporar nuevas funciones sin modificar innecesariamente otras partes del sistema.

## Conclusión del análisis

El principal problema del diseño inicial no es el funcionamiento de HomeCrop IoT, sino la concentración de responsabilidades diferentes dentro de una sola clase.

Por esta razón, se considera conveniente dividir el sistema en clases más pequeñas y especializadas, de manera que cada componente tenga una función clara y pueda modificarse, probarse y mantenerse con mayor independencia.
