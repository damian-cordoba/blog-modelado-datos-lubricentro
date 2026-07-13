# Diseñando la base de datos de mi sistema de gestión: consistencia, claves y pagos diferidos

## Contexto

Como parte del desarrollo de un sistema de gestión para un lubricentro, tuve que diseñar y crear una base de datos desde cero. El sistema debía registrar clientes, proveedores, productos, ventas y gastos, y sobre esos datos se generan análisis de forma automática. Por eso, la calidad del modelo de datos no era un detalle técnico menor: cualquier error en el diseño se trasladaba directamente a los reportes y análisis del negocio.

## Problema

El principal desafío fue el modelado de los datos. Necesitaba garantizar la consistencia de la información para evitar registros duplicados de clientes, proveedores, productos, ventas y gastos, algo que al principio ocurría con frecuencia y distorsionaba los análisis.

Además, me costaba definir correctamente las claves primarias (PK) y foráneas (FK) para relacionar las tablas sin generar redundancia. A esto se sumaba una complejidad propia del negocio: el sistema debía permitir el control de pagos diferidos y mantener un historial de costos de los productos, lo que no podía resolverse con las tablas principales y exigía diseñar tablas auxiliares.

## Acciones (Post-Mortem)

Para resolver el problema apliqué un análisis de causa raíz: los duplicados y las inconsistencias no eran fallas aisladas, eran consecuencia de un modelo que no estaba correctamente normalizado.

A partir de ese diagnóstico:

- Rediseñé el modelo identificando las entidades principales (clientes, proveedores, productos, ventas, gastos) y definiendo una clave primaria única para cada una.
- Establecí las claves foráneas necesarias para relacionar las tablas, asegurando la integridad referencial y evitando que un mismo dato se cargara en más de un lugar.
- Incorporé restricciones y validaciones para impedir la carga de registros duplicados.
- Diseñé tablas auxiliares específicas: una tabla de **detalle de pagos** para controlar los pagos diferidos de cada venta, y una tabla de **historial de costos** para registrar la evolución del costo de cada producto en el tiempo.

## Aprendizajes

Esta experiencia me permitió comprender que un buen modelo de datos no consiste solamente en crear tablas que "funcionen", sino en organizar la información de manera que se reduzca la redundancia, se mantenga la integridad y el modelo pueda crecer con el negocio.

Aprendí la importancia de definir correctamente las claves primarias y foráneas antes de cargar datos, porque corregir un modelo con información ya cargada es mucho más costoso. También entendí el valor de las tablas auxiliares: separar el detalle de pagos y el historial de costos de las tablas principales me permitió resolver necesidades reales del negocio sin romper la estructura del modelo.

## Evidencia de control de versiones

Este blog fue desarrollado utilizando GitHub. Durante su elaboración se realizaron distintos commits para registrar las modificaciones y mantener un historial de cambios del proyecto.

## Reflexión sobre feedback radicalmente sincero

El feedback recibido durante mi formación fue clave para destrabar este desafío. En lugar de limitarme a "hacer que funcione", los comentarios sobre mis primeros diseños me obligaron a repensar el modelo desde su lógica: qué representa cada tabla, cómo se relacionan los datos y qué pasa cuando el sistema crece. Aceptar que mi primer diseño tenía fallas estructurales no fue cómodo, pero fue lo que me permitió mejorarlo de verdad. Esta experiencia fortaleció mi mentalidad de crecimiento: hoy entiendo los errores de diseño como parte natural del proceso de aprendizaje.

## Conclusión

Diseñar la base de datos del sistema de gestión me enseñó que aprender tecnologías y conceptos nuevos requiere tiempo, práctica y disposición para recibir feedback. Más allá del resultado técnico, considero que desarrollar una mentalidad de crecimiento es fundamental para seguir avanzando en mi formación como profesional de Data Science / Data Analytics.
