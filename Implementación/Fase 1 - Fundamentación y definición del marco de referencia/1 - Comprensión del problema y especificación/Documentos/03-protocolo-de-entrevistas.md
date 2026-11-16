# Protocolo de entrevistas y guiones por rol

Fija el método de las entrevistas y los seis guiones por rol. El método es una entrevista semiestructurada de diseño mixto: conversación abierta y, al cierre, un conjunto reducido de ítems cerrados que producen datos agregables. Esos ítems son los que la Fase 4 vuelve a preguntar para tener un antes y un después con la misma escala.

## 1. Tipo de entrevista

Entrevista semiestructurada con diseño mixto. Cada entrevista tiene dos partes:

- **Preguntas abiertas:** Capturan el proceso actual, los puntos de dolor y el criterio del entrevistado.
- **Preguntas cerradas:** Un conjunto reducido de ítems cerrados que el entrevistado responde en los minutos finales. Producen datos agregables que complementan las respuestas abiertas.

## 2. Población

- **Desarrolladores internos:** 2
- **Desarrolladores externos:** 3
- **Tester:** 1
- **Líder Técnico:** 1
- **Líderes de Producto:** 1
- **Arquitectura:** 1

## 3. Cobertura

Se relaciona cada guión con la información que debe cerrar. Garantiza que ningún vacío quede sin fuente y que ninguna pregunta exista sin propósito.

| Información a cerrar | Guion responsable |
| :---- | :---- |
| Desagregación del proceso de arranque por actividad y tiempos | Desarrolladores internos, externos |
| Puntos de dolor del arranque | Desarrolladores internos, externos |
| Proceso e incidencia de integración de módulos a lo largo del ciclo de vida | Desarrolladores internos, externos |
| Costo de propagación cuando un módulo o servicio cambia | Desarrolladores internos, Líder Técnico |
| Criterio sobre qué debería y qué no debería estandarizarse | Desarrolladores internos, Líder Técnico |
| Consistencia externa de APIs e interfaces | Tester |
| Heterogeneidad entre productos desde la perspectiva de cliente | Tester |
| Visión consolidada de la divergencia entre proyectos | Líder Técnico |
| Consideraciones para el modelo de gobernanza del catálogo | Líder Técnico |
| Impacto del tiempo de arranque e integración sobre la planeación | Líderes de Producto |
| Condiciones de diseño de un módulo de integración y organización de dominios | Arquitectura |
| Contraste sobre qué problemas son generales de la industria | Desarrolladores externos |

**Parte 2 - Guiones por rol**

**Introduccion**

Este proyecto es un trabajo de grado de maestría que busca desarrollar una herramienta para agilizar el desarrollo de proyectos backend. La idea es atender dos momentos: el arranque de un proyecto nuevo, que hoy suele consumir bastante tiempo en configuración antes de escribir la primera línea de negocio, y la integración de funcionalidades comunes que se repiten entre proyectos (como autenticación, notificaciones o el consumo de servicios compartidos) que hoy se suelen resolver copiando de un proyecto a otro.

Lo que investigo en esta etapa es cómo se hace ese trabajo hoy, qué cuesta, qué duele y qué condiciones debería cumplir una solución para que realmente ayude y no se quede sin usar. No vengo con la herramienta hecha a que la valides: vengo a entender el problema desde tu experiencia y tu rol.

Por eso me interesa tu punto de vista concreto: lo que ves, lo que vives y lo que esperarías. No hay respuestas correctas ni incorrectas.

## 4. Guiones por rol

Seis guiones, con las preguntas abiertas y los ítems cerrados que cada uno cierra. La tabla de
cobertura de la §3 dice qué información cierra cada uno.

### 4.1 Desarrolladores internos

**Parte A - Preguntas abiertas**

- ¿En qué proyectos trabajas actualmente y desde hace cuánto?
- ¿Cómo describirías tu participación típica en el ciclo de vida de un producto?

**Flujo de arranque**

- Piensa en el último proyecto backend que iniciaste o viste iniciar. ¿Cómo fue ese arranque, paso a paso, desde que se decide crear el servicio hasta que corre sin error?
- ¿Qué parte de ese arranque consume más tiempo y por qué?
- ¿Qué se configura manualmente cada vez que se arranca un proyecto?
- ¿Qué suele descubrirse tarde, ya avanzado el proyecto, que hubiera convenido resolver al inicio?
- ¿Cuántas personas intervienen en el arranque y qué pasa con el resto del equipo mientras tanto?
- ¿Pregunta sobre adaptación de BIAN o estandares?

**Flujo de integración de módulos**

- Cuando un producto ya en curso necesita una funcionalidad que otro proyecto ya tiene ¿cómo se incorpora hoy?
- ¿Qué tan seguido ocurre eso durante la vida de un producto?
- ¿Qué pasa cuando una de esas funcionalidades compartidas cambia después de haberse copiado a varios proyectos?
- Cuéntame un caso concreto en que un cambio obligó a tocar varios proyectos. ¿Qué implicó?
- ¿Qué es lo más frágil o costoso de reutilizar código entre proyectos hoy?

**Criterio de estandarización**

- Desde tu experiencia, ¿qué del arranque y de la reutilización tendría sentido estandarizar?
- ¿Qué no debería estandarizarse, o qué se perdería si se hiciera?
- Desde tu rol, ¿qué esperarías de una herramienta que apoyara estos dos flujos?

**Parte B - Preguntas cerradas**

- Dificultad percibida del arranque de un proyecto hoy. 1-5
- Tiempo aproximado de un arranque hasta que el proyecto corre. horas / días
- Frecuencia con que se reutiliza código por copia entre proyectos. 1-5
- Costo percibido de propagar un cambio de una funcionalidad compartida. 1-5
- Grado de divergencia que percibes entre los proyectos del equipo. 1-5
- Utilidad esperada de una herramienta que automatice arranque e integración. 1-5

### 4.2 Desarrolladores externos

**Parte A - Preguntas abiertas**

**Arranque**

- En tu experiencia, ¿cómo suele iniciarse un proyecto backend nuevo en los equipos donde has trabajado?
- ¿Cuánto tiempo suele tomar dejar un proyecto listo para escribir lógica de negocio, y qué lo consume?
- ¿Qué se configura una y otra vez en cada proyecto nuevo?
- ¿Has visto formas de reducir ese costo de arranque? ¿Cuáles funcionaron y cuáles no?

**Reutilización de funcionalidades**

- ¿Cómo se reutilizan las funcionalidades comunes (autenticación, logging, integraciones) entre proyectos en tu experiencia?
- ¿Qué problemas has visto cuando esas funcionalidades compartidas cambian?
- ¿Has trabajado con librerías internas, plantillas o generadores para esto? ¿Qué tal resultó?


**Criterio**

- ¿Qué de un proyecto backend crees que vale la pena estandarizar y qué no?
- Desde tu experiencia, ¿qué debería tener una herramienta que genere proyectos e integre módulos reutilizables para que realmente se use y no se abandone?

**Parte B - Preguntas cerradas**

- Dificultad típica del arranque de un proyecto backend. 1-5
- Tiempo típico de arranque hasta escribir lógica. horas / días
- Frecuencia de reutilización. 1-5
- Costo típico de propagar cambios de funcionalidades compartidas. 1-5

### 4.3 Tester

**Parte A - Preguntas abiertas**

- Pruebas productos de ambas células. Cuando pasas de probar un producto a otro, ¿empiezas de cero cada vez o hay cosas que puedes dar por sentadas? ¿Qué cambia entre uno y otro?
- Cuando pruebas las APIs de distintos productos, ¿se comportan de forma parecida o cada una tiene su propia lógica? Dame ejemplos de en qué difieren.
- Las respuestas de éxito y de error, ¿tienen una forma predecible entre productos o cada uno responde a su manera? ¿Cuánto te cuesta eso al probar?
- ¿Cómo es la documentación de las APIs que pruebas? ¿La usas, está completa, es igual entre productos, confías en ella?
- Cuando algo falla, ¿qué tan fácil es para ti entender qué pasó desde afuera, sin ver el código? ¿Qué te ayudaría?
- ¿Qué parte de tu trabajo se vuelve lenta o repetitiva precisamente porque los productos no se parecen entre sí?
- Si todos los productos salieran con el mismo contrato de API, los mismos formatos de respuesta y error, y la misma documentación, ¿qué cambiaría en tu forma de probar?
- Desde tu rol, ¿qué deberían tener en común, sí o sí, todos los productos que genere una herramienta como esta, para que probarlos fuera predecible?

**Parte B - Preguntas cerradas**

- Consistencia actual del contrato de las APIs entre productos. 1-5
- Consistencia actual de respuestas y errores entre productos. 1-5
- Calidad y homogeneidad de la documentación de APIs. 1-5
- Facilidad de diagnosticar una falla desde fuera hoy. 1-5
- Impacto que tendría una salida homogénea sobre tu trabajo de prueba. 1-5

### 4.4 Líder Técnico

**Parte A - Preguntas abiertas**

- Como rol con visión sobre todos los productos, ¿cómo describirías las diferencias estructurales entre ellos?
- ¿Qué se configura manualmente cada vez que se arranca un proyecto?
- ¿Qué suele descubrirse tarde, ya avanzado el proyecto, que hubiera convenido resolver al inicio?
- ¿Cuántas personas intervienen en el arranque y qué pasa con el resto del equipo mientras tanto?
- ¿A qué atribuyes esas diferencias?
- ¿Qué consecuencias tienen esas diferencias en el día a día del equipo?
- ¿Qué del arranque de proyectos y de la reutilización de funcionalidades consideras que debería estandarizarse?
- ¿Qué riesgos ves en estandarizar? ¿Qué debería quedar a criterio de cada equipo?
- Si existiera un catálogo compartido de plantillas y módulos, ¿quién debería mantenerlo y bajo qué reglas debería incorporarse o cambiarse algo?
- ¿Qué haría que un esfuerzo de estandarización perdurará en lugar de quedar desactualizado?
- Desde tu rol, ¿qué esperarías de una herramienta que apoye estos dos flujos?

**Parte B - Preguntas cerradas**

- Grado de divergencia estructural entre los productos. 1-5
- Impacto de esa divergencia sobre el trabajo del equipo. 1-5
- Conveniencia de estandarizar el arranque. 1-5
- Conveniencia de estandarizar la reutilización de módulos. 1-5
- Importancia de un rol que mantenga el catálogo para que perdure. 1-5

### 4.5 Líderes de Producto

**Parte A - Preguntas abiertas**

- Cual es el proceso regular de como nace un nuevo proyecto y en qué punto se empieza a incluir al equipo técnico?
- Cuando defines un producto nuevo con el equipo técnico, ¿cómo se traduce el arranque en tu planeación? ¿Es tiempo que ya das por perdido antes de ver la funcionalidad?
- En tu experiencia, ¿cuánto pasa entre que un proyecto empieza y entrega su primer valor de negocio visible? ¿Qué se lleva ese tiempo?
- Durante la vida de un producto, ¿con qué frecuencia el equipo tiene que incorporar algo que otro producto ya resolvió? ¿Cómo te enteras y cómo lo planeas?
- Cuando esa reincorporación aparece a mitad de camino, ¿qué le hace a tu cronograma?
- Si sumas el tiempo que el equipo dedicó a montar bases y reintegrar cosas comunes, ¿qué funcionalidad de negocio se queda sin hacer por eso?
- ¿Has tenido que ajustar un compromiso o una fecha por costos de arranque o de integración que no eran de negocio? Cuéntame.
- Desde tu rol, ¿qué esperarías de una herramienta que quitara ese costo, y qué te haría desconfiar de que funcione?

**Parte B - Preguntas cerradas**

- Impacto del tiempo de arranque sobre tu planeación. 1-5
- Frecuencia con que un producto requiere integrar funcionalidades ya existentes en otros. 1-5
- Impacto de esa integración sobre el cronograma cuando aparece a mitad de camino. 1-5
- Frecuencia de funcionalidades de negocio que se sacrifican por estos impactos. 1-5
- Valor esperado de reducir los tiempos de arranque e integración. 1-5

### 4.6 Arquitectura

Las preguntas van dirigidas a la función de arquitectura, que responde desde su rol y su experiencia profesional y no desde definiciones internas de ninguna organización.

**Parte A - Preguntas abiertas**

**Sobre iniciar proyectos**

- Cuando inician nuevos proyectos en diferentes equipos ¿qué de tu área es lo que más a menudo queda mal resuelto, mal configurado o directamente olvidado? Si una herramienta lo dejara bien resuelto desde el inicio, ¿qué debería garantizar exactamente?

**Sobre integrar funciones compartidas**

- El punto más reutilizado entre proyectos es la integración con servicios y capacidades compartidas. Desde tu función, ¿qué debe cumplir un módulo compartido para incorporarse a muchos proyectos sin volverse un riesgo común a todos ellos?
- Esos módulos compartidos evolucionan y cambian con el tiempo. ¿Cómo debería gestionarse ese cambio para que actualizar un módulo en muchos proyectos no se convierta en un problema de tu área?

**Sobre lo replicable y el riesgo**

- Cuando una herramienta genera muchos proyectos desde una misma base, una buena decisión se propaga sola, pero un error también. Desde tu función, ¿cuál es el error más peligroso que podría quedar embebido y replicado, y por qué sería difícil de revertir una vez propagado?
- ¿Qué debería quedar fijo e impuesto en esa base común, y qué debería quedar configurable por cada equipo? ¿Dónde pondrías la línea desde tu área?
- ¿Qué del arranque de proyectos y de la reutilización de funcionalidades consideras que debería estandarizarse?
- ¿Qué riesgos ves en estandarizar? ¿Qué debería quedar a criterio de cada equipo?

**Sobre expectativa y confianza**

- ¿Qué tendría que cumplir una herramienta así para que confiaras en un proyecto generado por ella tanto o más que en uno construido a mano, desde el criterio de tu función?
- Desde tu rol, ¿qué esperarías que una herramienta de este tipo hiciera bien, y qué te preocupa que hiciera mal?

**Parte B - Bloque específico del rol**

- Importancia de que una herramienta así respete los principios de tu función. 1–5
- Riesgo de propagar un error de tu área al embeberlo en plantillas replicables. 1–5
- Grado en que tu función debería condicionar el diseño de una herramienta de este tipo. 1–5
- Confianza que te daría un proyecto bien generado frente a uno hecho a mano. 1–5
