# Identificación de stakeholders

Identifica qué roles entrevistar y qué puede afirmar cada perspectiva, clasificados por su distancia respecto de la solución. De acá sale la población del protocolo de entrevistas, y de acá sale el peso que el análisis cualitativo le da a cada respuesta.

## 1. Criterio de identificación

- **Uso:** Interactúa directamente con la herramienta.
- **Definición:** Establece reglas, lineamientos o restricciones que la solución debe respetar.
- **Autorización:** Habilita, bloquea la adopción o el acceso al contexto.
- **Afectación:** Su trabajo, o lo que recibe, cambia como consecuencia de la solución, aunque no la use directamente.

## 2. Marco de clasificación

Se adopta el modelo de capas (onion model) de Alexander para ingeniería de requerimientos, que organiza a los stakeholders por su distancia respecto del artefacto.

| Capa | Contenido |
| :---- | :---- |
| **Núcleo** Operadores y beneficiarios directos | Quienes usan la herramienta y quienes trabajan sobre lo que genera |
| **Sistema contenedor** Laboratorio Digital | Quienes deciden, priorizan y se benefician dentro del equipo |
| **Entorno** Arquitectura | La función que establece las reglas a las que se subordina la forma de lo generado |
| **Latentes** | Actores que aún no existen o no participan, pero condicionan el diseño |

## 3. Núcleo - Operadores y beneficiarios directos

**ST-01 Desarrolladores backend**

Son quienes ejecutan el proceso que la solución busca transformar y los únicos que operarían la herramienta. La caracterización establece que el arranque de un proyecto lo realiza una sola persona de este grupo y que las funcionalidades transversales se reutilizan mediante copiar y pegar entre proyectos.

**Aporte esperado:** Desagregación del proceso de arranque, puntos de dolor concretos, criterio sobre qué debería y qué no debería estandarizarse, y validación de las convenciones propuestas.

**ST-02 Testers**

El tester no operaría la herramienta, pero todo lo que la herramienta produce pasa por su trabajo. Realiza pruebas de caja negra en dos formas: sobre las interfaces de frontend como usuario real, y sobre las APIs como cliente que verifica su funcionamiento.

Esto lo sitúa como beneficiario funcional, recibe y usa lo generado sin manipular la herramienta. Una salida homogénea de la herramienta cambia directamente cómo prueba y qué puede dar por supuesto entre un producto y otro.

**Aporte esperado:** Requerimientos sobre consistencia externa de las APIs y las interfaces, y evidencia de la heterogeneidad actual entre productos desde una perspectiva de cliente.

## 4. Sistema contenedor - Laboratorio Digital

**ST-03 Líder Técnico**

Es el único rol con visión horizontal del conjunto de productos. La caracterización establece que gestiona y organiza las prioridades del equipo técnico y que participa en la definición de proyectos e iniciativas con la dirección de la unidad y con los líderes de producto, trasladando el contexto al equipo técnico.

Su visión transversal lo convierte en la fuente más completa sobre la divergencia entre proyectos y sobre qué tendría sentido estandarizar. Es, además, el candidato natural a custodio del catálogo de plantillas y módulos, función que hoy no tiene titular.

**Aporte esperado:** Visión consolidada de la divergencia entre proyectos, criterio sobre qué debe estandarizarse, y consideraciones para el modelo de gobernanza del catálogo.

**ST-04 Líderes de Producto**

Este rol es quien dispara el inicio de un proyecto, gestiona los productos de su equipo y percibe de forma directa tanto el costo de oportunidad del tiempo de arranque como el de la incorporación de nuevas funcionalidades transversales sobre productos ya en curso, ambos con impacto sobre la planeación.

**Aporte esperado:** Impacto del tiempo de arranque y de la integración de funcionalidades a lo largo del ciclo de vida sobre la planeación de productos, y expectativas sobre el valor de reducir ambos.

## 5. Entorno: la función que define las restricciones

Arquitectura no usa la herramienta ni pertenece al Laboratorio, y entra porque es la función cuyas definiciones condicionan la forma de lo generado: a qué se subordina la estructura de un proyecto y cómo se consume el core. Las demás funciones institucionales —ciberseguridad, seguridad de la información, soporte y despliegue— condicionan la aprobación y la operación, no la forma, y por eso quedan fuera del levantamiento: lo que imponen entra al proyecto como requerimiento no funcional y no como perspectiva entrevistada.

**ST-05 Arquitectura**

La función de arquitectura define las definiciones arquitectónicas, la taxonomía de dominios y la frontera de integración a las que el desarrollo se subordina, y establece la forma de consumir el core: reglas, protocolos y seguridad.

**Aporte esperado:** Desde su función y principios, qué condiciona el diseño de un módulo de integración y la organización de dominios en una herramienta de generación de proyectos.

## 6. Stakeholders latentes

Actores que hoy no existen o no participan, pero cuya consideración condiciona decisiones de diseño. No participan del levantamiento, pero se registran porque el diseño debe responder por ellos.

**ST-06 Mantenedor del catálogo de plantillas y módulos**

Su definición pertenece al modelo de gobernanza del marco de referencia y es una de las condiciones para que la solución no repita el fracaso que diagnostica.

**ST-07 Desarrolladores que se incorporen al equipo**

Toda solución que estandarice y documente el arranque actúa también como mecanismo de incorporación de nuevos desarrolladores. Se considera para que las convenciones queden expresadas de forma explícita y transferible, no solo ejecutable.

**ST-08 Otras organizaciones o equipos adoptantes**

La solución busca ser replicable más allá del contexto de aplicación. Un equipo adoptante en otra organización tendría su propia función de arquitectura, de seguridad y de despliegue, con reglas distintas. Se considera a este actor para decidir qué elementos del artefacto se dejan configurables (contratos de integración, catálogos de dependencias, plantillas de empaquetado) y cuáles se atan al contexto observado.
