# Especificación de requerimientos

Traduce los temas y las brechas en veintidós requerimientos —dieciséis funcionales y seis no funcionales—, cada uno con su origen, su prioridad MoSCoW y su criterio de aceptación. Delimita además el alcance de la solución: qué entra, qué queda fuera y con qué razón.

## 1. Alcance de la solución

La solución es una herramienta de línea de comandos que genera proyectos backend a partir de plantillas y permite incorporar y actualizar módulos reutilizables a lo largo del ciclo de vida de esos proyectos.

**Naturaleza de la solución**

Se implementa como CLI únicamente, sin componentes de servidor. El catálogo de plantillas y módulos se resuelve de forma declarativa mediante un manifiesto versionado, y la distribución se apoya en el registro de paquetes existente en la organización.

Esta decisión responde a la brecha B-03: las soluciones que ofrecen catálogo gobernado exigen desplegar y operar una plataforma, costo desproporcionado para el contexto, y al tema T-14, que fija el umbral de uso en un comando.

**Dentro del alcance**

- Generación de proyectos backend sobre Node.js y TypeScript, con NestJS como framework de referencia.
- Incorporación de módulos transversales a proyectos nuevos y a proyectos ya en curso.
- Propagación de cambios de un módulo hacia los proyectos que lo consumen.
- Generación automática de documentación de API bajo el estándar OpenAPI.
- Catálogo declarativo de plantillas y módulos, con versión y distribución sobre el registro de paquetes de la organización.
- Configuración externalizada en los proyectos generados.

**Fuera del alcance**

- Despliegue, infraestructura y automatización de entrega continua.
- Aplicaciones serverless. La herramienta se orienta a servicios backend con servidor propio. **Revisado el 2026-11-09:** lo que queda fuera son las aplicaciones **sin API HTTP expuesta**. Un producto cuyo host invoca una función por ruta pertenece a la familia, porque cumple la condición mínima de pertenencia; lo que no tiene es servidor propio, que era la razón de esta exclusión y no la condición. El anteproyecto no excluye serverless, así que esto corrige un estrechamiento del propio proyecto.
- Implementación de funcionalidades específicas de negocio.
- Lenguajes o ecosistemas distintos de Node.js y TypeScript.
- Componentes de servidor propios, incluido cualquier portal o servicio de catálogo alojado.

**Consideración sobre otros frameworks**

El diseño no debe atarse a NestJS. Aunque es el framework del contexto de aplicación y el que se soportará en esta fase, la herramienta debe admitir la incorporación posterior de otros frameworks backend no serverless. Es una condición de diseño, no una capacidad a implementar en esta fase.

**Consideración sobre la inteligencia artificial**

El análisis registró la inteligencia artificial como tema emergente, con la conclusión de reservar el determinismo para la generación de estructura y la asistencia para el contenido. No se especifica como requerimiento de la herramienta. Su eventual aplicación pertenece al proceso de construcción de la solución y no al comportamiento especificado.

## 2. Criterios de priorización

Se adopta la escala MoSCoW.

| Nivel | Significado | Criterio de asignación |
| :---- | :---- | :---- |
| M - Must have | Imprescindible | Responde a una de las tres brechas identificadas, o sin él la solución no resuelve el problema levantado |
| S - Should have | Importante | Responde a una necesidad documentada, pero la solución sigue siendo válida sin él en esta fase |
| C - Could have | Deseable | Aporta valor comprobado y puede quedar fuera si el alcance lo exige |
| W - Won't have | Excluido de esta fase | Reconocido como valioso, pero explícitamente diferido |

## 3. Requerimientos funcionales

**Generación de proyectos**

| ID | Requerimiento | Prioridad | Origen | Criterio de aceptación |
| :---- | :---- | :---- | :---- | :---- |
| RF-01 | La herramienta debe generar un proyecto backend ejecutable a partir de una plantilla | M | T-01, T-02 | El proyecto generado arranca sin errores inmediatamente después de la generación, sin edición previa de archivos |
| RF-02 | La herramienta debe parametrizar la generación mediante valores proporcionados por el usuario, aplicables al contenido, los nombres de archivo y la estructura | M | T-01, T-02, T-11 | Dos ejecuciones con parámetros distintos producen proyectos con nombres, rutas y contenido acordes a lo indicado |
| RF-03 | El proyecto generado debe incorporar de origen la estructura modular, las convenciones del marco de referencia y el entorno de análisis de código y de ejecución de pruebas ya configurado | M | T-07, T-08 | El proyecto generado permite ejecutar el análisis de código y el comando de pruebas sin configuración previa. No incluye pruebas escritas, que corresponden a la lógica de negocio |
| RF-04 | El proyecto generado debe producir su documentación de API bajo el estándar OpenAPI de forma automática | S | T-07, T-08 | La documentación queda disponible sin configuración adicional y refleja los endpoints del proyecto generado |
| RF-05 | La herramienta debe producir el mismo resultado ante la misma entrada, de forma determinista | M | T-06 | Dos ejecuciones con parámetros idénticos, por usuarios distintos, producen estructuras equivalentes |

**Composición de módulos**

| ID | Requerimiento | Prioridad | Origen | Criterio de aceptación |
| :---- | :---- | :---- | :---- | :---- |
| RF-06 | La herramienta debe incorporar un módulo transversal a un proyecto ya existente, sin que el usuario edite manualmente archivos del proyecto | M | T-04, T-09, B-01 | Ejecutado el comando sobre un proyecto en curso, el módulo queda integrado y el proyecto sigue ejecutándose |
| RF-07 | La incorporación de un módulo debe modificar los archivos del proyecto que deban referenciarlo, sin sobrescribir código propio del desarrollador | M | T-04, T-09, B-01 | Tras incorporar un módulo, el código previo del proyecto permanece intacto y las referencias necesarias quedan registradas |
| RF-08 | La herramienta debe permitir consultar qué módulos están disponibles y cuáles están incorporados en un proyecto | S | T-04, T-09, T-15 | El comando de consulta lista los módulos del catálogo y los presentes en el proyecto con su versión |
| RF-09 | El catálogo debe disponer de al menos un módulo transversal construido conforme al marco de referencia, que permita validar la composición y la actualización | S | T-04, T-09 | Existe un módulo funcional en el catálogo, incorporable y actualizable sobre un proyecto real. Las demás capacidades identificadas en el análisis quedan como catálogo a construir posteriormente |

**Actualización y propagación**

| ID | Requerimiento | Prioridad | Origen | Criterio de aceptación |
| :---- | :---- | :---- | :---- | :---- |
| RF-10 | El proyecto debe registrar qué módulos tiene incorporados y en qué versión | M | T-05, B-02 | Existe en el proyecto un registro consultable con el módulo y su versión |
| RF-11 | La herramienta debe actualizar un módulo incorporado a una versión posterior, sin intervención manual sobre el proyecto | M | T-05, B-02 | Publicada una versión nueva de un módulo, el comando de actualización la aplica y el proyecto sigue ejecutándose |
| RF-12 | La herramienta debe informar si un proyecto tiene módulos desactualizados respecto del catálogo | M | T-06 | El comando de verificación identifica los módulos con versión inferior a la vigente |
| RF-13 | La actualización de un módulo debe preservar el código propio del proyecto que lo consume | M |  T-10 | Modificado el código del proyecto que usa un módulo y actualizado este módulo, las modificaciones del desarrollador permanecen intactas. El tratamiento de las modificaciones sobre el módulo mismo depende de si el marco lo define como inmutable o editable |

**Catálogo y distribución**

| ID | Requerimiento | Prioridad | Origen | Criterio de aceptación |
| :---- | :---- | :---- | :---- | :---- |
| RF-14 | El catálogo de plantillas y módulos debe definirse de forma declarativa y versionada, sin requerir componentes de servidor | M | T-15, B-03 | El catálogo se declara en un artefacto versionado y la herramienta opera sin infraestructura adicional |
| RF-15 | Los módulos y plantillas deben distribuirse mediante el registro de paquetes existente en la organización | M | T-12 | La herramienta obtiene módulos y plantillas del registro sin canal propio de distribución |
| RF-16 | El catálogo debe registrar la propiedad de cada módulo y las condiciones para incorporar uno nuevo | S | T-15 | Cada entrada del catálogo declara su responsable, y existe un procedimiento documentado de incorporación |

## 4. Requerimientos no funcionales

| ID | Requerimiento | Atributo | Prioridad | Origen | Criterio de aceptación |
| :---- | :---- | :---- | :---- | :---- | :---- |
| RNF-01 | Las operaciones de la herramienta deben ejecutarse con un comando cada una | Usabilidad | M | T-14 | Cada operación de la herramienta se completa con la ejecución de un único comando |
| RNF-02 | El código generado debe ser modificable sin que ello impida seguir usando la herramienta sobre el proyecto | Adaptabilidad | M | T-10 | Modificado el proyecto generado, los comandos de incorporación y actualización siguen operando |
| RNF-03 | Lo generado debe poder someterse a análisis estático de código, incluidos aspectos de seguridad | Verificabilidad | S | T-13 | El proyecto generado se analiza con las herramientas de la organización sin adaptación previa |
| RNF-04 | La herramienta debe poder someterse a auditoría de dependencias y vulnerabilidades, con resultado consultable | Verificabilidad | S | T-13 | La auditoría se ejecuta sobre la herramienta y su resultado puede presentarse a las áreas técnicas y de riesgo |
| RNF-05 | El proyecto generado no debe contener valores fijos susceptibles de cambio, en particular direcciones de servicios y parámetros de negocio | Configurabilidad | M | T-11 | La revisión del proyecto generado confirma que endpoints y parámetros residen fuera del código |
| RNF-06 | La herramienta y sus módulos deben evolucionar por versiones, admitiendo la convivencia de versiones distintas entre proyectos | Evolución | M | T-12 | Dos proyectos operan simultáneamente con versiones distintas de un mismo módulo |
