# Fundamentos adoptados

Adopta los fundamentos sobre los que se construye la línea, y de cada uno declara qué se toma y qué se deja. Son dos cosas distintas: el **modelo de dominio**, que delimita y nombra lo que cada producto representa, y la **arquitectura común** que todos los productos comparten, cuya contraparte informal ya existe en el contexto.

## 1. Los tres fundamentos, y qué se adopta de cada uno

| Fundamento | Elemento que llena | Qué se adopta | Qué queda fuera |
| :---- | :---- | :---- | :---- |
| BIAN | Delimitación y nomenclatura del dominio | Service Landscape como taxonomía, criterio de elementalidad, no solapamiento, control récord como referencia de nombre | Functional patterns, Semantic APIs, Business Object Model, catálogo de módulos técnicos |
| Domain-Driven Design | Arquitectura común: organización interna del dominio | Nivel estratégico acotado a un contexto y seis patrones tácticos | Patrones tácticos diferidos, relación entre contextos de proyectos distintos |
| Arquitectura hexagonal | Arquitectura común: relación entre el núcleo y el exterior | Separación núcleo-adaptadores y dirección de dependencia | - |

## 2. Implementación de BIAN

Se adopta la versión 14.0 del Service Landscape. Toda referencia a Business Areas, Business Domains o Service Domains en este marco corresponde a esa versión.

[https\://bian.org/servicelandscape-14-0-0/index.html](https://bian.org/servicelandscape-14-0-0/index.html)

BIAN gobierna tres aspectos del proyecto generado.

| Aspecto | Qué determina |
| :---- | :---- |
| Identidad | Qué capacidad de negocio representa el proyecto, expresada como un Service Domain del Service Landscape [https\://bian.org/servicelandscape-14-0-0/views/view_54054.html](https://bian.org/servicelandscape-14-0-0/views/view_54054.html)  |
| Frontera | Hasta dónde llega la responsabilidad del proyecto, según el criterio de elementalidad y no solapamiento |
| Nomenclatura | El nombre del agregado raíz del esqueleto de dominio, orientado por el control record del Service Domain |

**Lo que BIAN no gobierna**

El catálogo de módulos agrupa capacidades técnicas transversales: registro de eventos, observabilidad, cifrado, identidad, persistencia y consumo de servicios corporativos. BIAN modela capacidades de negocio bancario y no modela infraestructura técnica de aplicaciones, por lo que el catálogo queda fuera de su alcance y su gobierno corresponde al marco de referencia propio.

La existencia del Business Domain llamado IT Management dentro del área Business Support no altera esta delimitación: sus Service Domains modelan la gestión de tecnología del banco como función organizacional, no componentes técnicos reutilizables.

La extensión del catálogo con módulos de dominio alineados a BIAN se registra como punto de extensión y no forma parte de este trabajo.

**Espacio de selección**

De los 38 Business Domains del Service Landscape, nueve corresponden al tipo de productos que construye el contexto de aplicación: Customer Management, Sales, Servicing, Cross Channel, Loans and Deposits, Payments, Account Management, Operational Services y Collateral Administration.

El subconjunto de Service Domains contenidos en ellos constituye el espacio de selección por defecto del mecanismo de derivación.

## 3. Unidad de derivación y criterio de granularidad

Cada ejecución del mecanismo de derivación produce un proyecto que aloja exactamente un bounded context, correspondiente a un Service Domain. No se admite la derivación de productos que alojen varios.

El criterio que fundamenta la regla es la elementalidad definida por BIAN: un Service Domain es una capacidad de negocio discreta cuyo alcance es elemental, de modo que si se descompone más, las partes pierden su contexto de negocio propio y pasan a ser de naturaleza utilitaria.

La propiedad de no solapamiento aporta la contraparte: los Service Domains definen capacidades discretas y no solapadas, por lo que la información que gobiernan también lo es. Trasladada al contexto, esa propiedad impide que dos proyectos del laboratorio sean dueños de la misma información.

**Registro del dominio como metadato**

Todo proyecto derivado registra, como metadato, el Service Domain al que corresponde y el Business Domain que lo contiene. El mecanismo de derivación solicita ese dato al generar y lo escribe en el proyecto junto al registro de versiones.

La regla admite un caso de excepción y una prohibición. Si el producto corresponde a una capacidad que no figura en el espacio de selección por defecto, se permite declarar un Service Domain fuera de ese subconjunto, registrando el Business Domain que lo contiene. Lo que no se admite es omitir el metadato: sin él, la delimitación de dominio queda sin efecto verificable y la alineación con BIAN se vuelve declarativa.

![][image1]

## 4. Domain-Driven Design

**Nivel estratégico**

Al corresponder cada proyecto a un único bounded context, el nivel estratégico se reduce a tres reglas.

| Regla | Contenido |
| :---- | :---- |
| Un contexto por producto | El proyecto derivado delimita un solo bounded context, identificado por su Service Domain |
| Lenguaje ubicuo | Los nombres del dominio dentro del proyecto corresponden al vocabulario de su Service Domain, no a términos técnicos ni a abreviaturas locales |
| No solapamiento | Ningún proyecto modela información que otro ya gobierna |

La relación entre bounded contexts de proyectos distintos queda fuera del alcance de este marco y se registra en los pendientes.

**Nivel táctico**

Se adoptan seis patrones. Cuatro constituyen el núcleo mínimo sin el cual no hay modelado táctico, y dos entran por decisiones ya tomadas en el marco.

| Patrón | Qué aporta |
| :---- | :---- |
| Entidad | Objeto con identidad propia que persiste a través de cambios de estado |
| Objeto de valor | Objeto sin identidad, definido por sus atributos e inmutable |
| Agregado y raíz de agregado | Frontera de consistencia y único punto de entrada a su interior |
| Repositorio | Única salida del dominio hacia la persistencia, expresada en lenguaje del dominio |
| Servicio de dominio | Lógica de negocio que no pertenece naturalmente a una sola entidad |
| Evento de dominio | Hecho relevante del dominio que otros pueden observar |

**Nota terminológica.** En este trabajo el término módulo designa un core asset del catálogo. El patrón táctico de Domain-Driven Design denominado Module no se adopta con ese nombre, para evitar que un mismo término designe dos cosas distintas dentro del marco.

## 5. Arquitectura hexagonal

La arquitectura hexagonal aporta la regla que separa el núcleo del producto de todo lo que no es dominio.

| Principio | Contenido |
| :---- | :---- |
| Separación | El núcleo agrupa el dominio y la capa de aplicación. Todo lo demás —transporte, persistencia, mensajería, servicios externos, observabilidad— es exterior y se comunica con el núcleo a través de adaptadores |
| Dirección de dependencia | Las dependencias apuntan siempre hacia el núcleo. Ningún elemento del núcleo conoce un elemento del exterior |
| Independencia tecnológica | El núcleo no conoce el framework de aplicación, el motor de persistencia ni el protocolo de transporte |

De esos tres principios se deriva una regla verificable que el marco adopta como criterio: el núcleo no importa ningún artefacto del exterior. Al construirse los productos en TypeScript, esa regla puede comprobarse mediante análisis estático, conforme a RNF-03, en lugar de depender de revisión manual.

La articulación entre Domain-Driven Design y arquitectura hexagonal es directa: los patrones tácticos describen qué contiene el núcleo, y la arquitectura hexagonal describe cómo el núcleo se relaciona con lo que está afuera. El repositorio es el punto donde ambos se encuentran, porque es un patrón táctico cuya realización concreta vive en el exterior.

![][image2]

## 6. Ejemplo de aplicación

Los tres fundamentos anteriores se aplican de forma conjunta en cada derivación. El siguiente caso ilustra el recorrido completo, desde la selección en el Service Landscape hasta el esqueleto generado.

| Etapa | Qué ocurre |
| :---- | :---- |
| Selección | El desarrollador identifica la capacidad del producto en el Service Landscape: Operations and Execution → Loans and Deposits → Consumer Loan |
| Registro | El mecanismo escribe el metadato de dominio en el proyecto, junto al registro de versiones |
| Derivación de nombres | El Service Domain da nombre al bounded context, el control record al agregado raíz, y las service operations orientan los casos de uso y las rutas de la API |
| Generación | Se produce la estructura de capas con los elementos del dominio nombrados y los contratos declarados |

**Qué se genera y qué no**

El mecanismo produce la estructura, los nombres y los contratos vacíos. Las reglas de negocio del producto las construye el equipo que lo recibe. Esta distinción es la que mantiene al artefacto dentro de su alcance: genera el punto de partida de un producto, no el producto.

## 7. Exclusión de ISO 20022

ISO 20022 es un estándar de mensajería financiera: define modelos de negocio y esquemas de mensajes para el intercambio de información entre instituciones financieras. El artefacto de este trabajo no produce, transforma y transporta mensajes financieros; produce estructuras de proyecto y componentes técnicos transversales.

La relación entre ambos estándares delimita el punto de contacto con precisión. BIAN referencia correspondencias hacia ISO 20022 en la capa de especificación de mensajes, y la versión 14.0 incorporó vínculos adicionales hacia ese estándar. Esa capa es exactamente la que el artefacto no produce.

La adopción de ISO 20022 corresponde a la lógica de negocio que cada equipo implementa sobre el proyecto derivado, explícitamente fuera del alcance de la solución. Se documenta el análisis y se registra como punto de extensión: un módulo de dominio que encapsule mensajería ISO 20022 sería un consumidor legítimo del marco, no parte de él.

[image1]: <../Insumos/Diagramas/MR-02_fig1_service_domain_a_proyecto.svg>
[image2]: <../Insumos/Diagramas/MR-02_fig2_arquitectura_referencia.svg>
