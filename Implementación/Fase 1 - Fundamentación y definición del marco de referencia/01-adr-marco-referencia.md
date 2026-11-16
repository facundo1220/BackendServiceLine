# Log de decisiones — Marco de referencia técnico de la solución

Trabajo de grado: *Desarrollo de una herramienta CLI para la generación automatizada de proyectos backend e integración de módulos reutilizables*
Fase 1 — dimensión de la solución · Sección 3.2 del documento

Las decisiones estructurales que conforman el marco de referencia técnico. Cada una es trazable a una necesidad (N-xx), una brecha (B-xx) o un requerimiento (RF-xx / RNF-xx) ya establecidos, y su campo *Consecuencias* la convierte en restricción vinculante para las fases posteriores.

## Convenciones

- **Terminología**: los términos técnicos se mantienen en inglés dentro de prosa en español, en cursiva la primera aparición de cada capítulo, sin traducir después. Glosario al cierre del capítulo 3.
- **Estados**: Aceptada · Aceptada (provisional) · Diferida · Revisada · Sustituida.
- **Numeración**: ADR-xxx para decisiones; MR-xx para los documentos del marco que las desarrollan.

**Significado de los estados**

| Estado | Qué indica |
| :---- | :---- |
| Aceptada | Decisión firme del marco. Vincula a las fases posteriores |
| Aceptada (provisional) | Decisión tomada sin evidencia de implementación, con su condición de revisión declarada |
| Diferida | Decisión que se tomó anticipadamente pero que, según el criterio de alcance de ADR-026, corresponde a una fase posterior. Se conserva como insumo, no como regla del marco |
| Revisada | Decisión modificada tras evidencia posterior. Conserva el registro del cambio y su motivo |
| Sustituida | Decisión reemplazada por otra. Se conserva por trazabilidad |

## Items del marco

El marco se desarrolla en cinco documentos independientes.

| Item | Documento | Contenido |
| :---- | :---- | :---- |
| MR-01 | Encuadre como línea de producto de software | Por qué la solución es una LPS, alcance de la familia, organización general en cuatro cuadrantes, desviaciones declaradas, mecanismo de evolución del marco |
| MR-02 | Fundamentos adoptados | Qué se toma y qué queda fuera de BIAN, DDD y hexagonal; unidad de derivación y metadato de dominio; exclusión de ISO 20022 |
| MR-03 | Organización del código del proyecto generado | Estructura canónica, direcciones de dependencia y regla verificable, nomenclatura, frontera del contrato externo |
| MR-04 | Puertos y contratos de integración | Las dos clases de puerto y su propiedad, contract package como core asset, qué es un módulo en términos arquitectónicos, caso de persistencia |
| MR-05 | Gobierno de los core assets | Qué hace válido a un activo, escala de adaptación, cambio incompatible, política de versionado, catálogo con propiedad y reglas, distribución agnóstica |

## Índice de decisiones

| ID | Decisión | Item | Estado | Revisada después por |
| :---- | :---- | :---- | :---- | :---- |
| ADR-001 | Adoptar línea de producto de software como encuadre teórico | MR-01 | Aceptada | — |
| ADR-002 | Alcance declarado de la familia de productos | MR-01 | Revisada | **ADR-191** |
| ADR-003 | Correspondencia entre fases y ciclo domain/application engineering | MR-01 | Aceptada | — |
| ADR-004 | Un proyecto generado equivale a un bounded context | MR-02 | Aceptada | — |
| ADR-005 | TypeScript como lenguaje del marco y de los artefactos | MR-01 | Aceptada | — |
| ADR-006 | BIAN gobierna el dominio del proyecto, no el catálogo de módulos | MR-02 | Aceptada | — |
| ADR-007 | Exclusión razonada de ISO 20022 | MR-02 | Aceptada | — |
| ADR-008 | Marco tecnológicamente neutral respecto del framework destino | MR-02 | Aceptada | — |
| ADR-009 | Entrega híbrida de módulos: paquete más wiring generado | MR-04 | Aceptada | — |
| ADR-010 | Contract package como propietario de los technical ports | MR-04 | Aceptada | — |
| ADR-011 | Dos clases de port: domain ports y technical ports | MR-04 | Revisada | — |
| ADR-012 | Escala de adaptación de tres niveles | MR-05 | Revisada | — |
| ADR-013 | Definición operativa de cambio incompatible | MR-05 | Revisada | — |
| ADR-014 | Actualización sin fusión a tres vías | Fase 3 | Diferida | — |
| ADR-015 | Catálogo en dos capas: Git como gobernanza, registro como distribución | MR-05 | Aceptada | — |
| ADR-016 | Distribución agnóstica del registro de paquetes | MR-05 | Aceptada | — |
| ADR-017 | Una sola plantilla base canónica | Fase 2 | Revisada | **ADR-171** |
| ADR-018 | Validación del marco por walkthrough documentado | Cierre del proyecto | Aceptada | — |
| ADR-019 | Registro del Service Domain como metadato obligatorio | MR-02 | Aceptada | — |
| ADR-020 | Organización por capas con agrupación por agregado en el dominio | MR-03 | Aceptada | — |
| ADR-021 | Los datos de referencia residen en la infraestructura | MR-03 | Aceptada | — |
| ADR-022 | Dirección de dependencia y severidad de la regla verificable | MR-03 | Aceptada | — |
| ADR-023 | Inglés como idioma del código | MR-03 | Aceptada | — |
| ADR-024 | Sufijos de rol y convención de nombres de archivo | MR-03 | Aceptada | — |
| ADR-025 | Separación del contrato externo respecto del dominio | MR-03 | Aceptada | — |
| ADR-026 | Criterio de alcance del marco | Transversal | Aceptada | — |
| ADR-027 | Mecanismo de evolución del marco | MR-01 | Aceptada | — |
| ADR-028 | Contract package organizado en submódulos por capacidad | MR-04 | Aceptada | — |
| ADR-029 | El contract package contiene únicamente declaraciones de tipo | MR-04 | Aceptada | — |
| ADR-030 | Criterio de clasificación de puertos por su firma | MR-04 | Aceptada | — |
| ADR-031 | Condiciones de validez de un módulo | MR-04 | Aceptada | — |
| ADR-032 | Reglas de composición de módulos | MR-04 | Aceptada | — |
| ADR-033 | Un módulo puede proponer puertos técnicos nuevos | MR-04 | Aceptada | — |
| ADR-034 | Tipos de activo y condiciones comunes de validez | MR-05 | Aceptada | — |
| ADR-035 | El responsable de un activo es un equipo | MR-05 | Aceptada | — |
| ADR-036 | Declaración de compatibilidad por versión mayor del contrato | MR-05 | Aceptada | — |
| ADR-037 | Criterio de migración del contract package | MR-05 | Aceptada (provisional) | — |
| ADR-038 | Estados del catálogo y no admisión de retiro | MR-05 | Aceptada | — |
| ADR-039 | Contenido de una entrada del catálogo | MR-05 | Aceptada | — |
| ADR-040 | Registro de versiones del producto | MR-05 | Aceptada | — |
| ADR-041 | Despriorización de la verificación de conformidad | Transversal | Aceptada | — |
| ADR-165 | Cómo se toma la línea base con la ventana vencida | Bloque A | Aceptada | — |
| ADR-191 | La familia admite un producto sin servidor propio | MR-01 | Revisada | — |

La numeración del proyecto es global continua y cada decisión va al log de la fase cuyo artefacto toca. ADR-165
se escribe aquí, fuera del rango ADR-001..041 de esta fase, porque el artefacto que decide es el documento 7
de su Bloque A.

---

## ADR-001 · Adoptar línea de producto de software como encuadre teórico

**Estado:** Aceptada · 2026-09-11 · Item MR-01

**Contexto.** El artefacto produce múltiples proyectos backend a partir de un conjunto común de activos reutilizables. El capítulo 2 no cuenta con un encuadre teórico que nombre ese tipo de solución ni que explique por qué el problema levantado tiene la forma que tiene.

**Decisión.** Adoptar línea de producto de software (*software product line*) como encuadre teórico formal del artefacto. La plantilla base, los módulos, los contratos y el catálogo constituyen los *core assets*; la herramienta CLI constituye el mecanismo de derivación; la familia de productos se declara en ADR-002.

**Alternativas.** Usar LPS solo como lente conceptual, sin incorporarlo al marco teórico. Se descarta porque deja sin nombre la separación entre construir los activos y derivar un producto, que es la estructura de las fases 2, 3 y 4.

**Por qué.** La práctica actual documentada en T-04, reutilizar copiando código entre proyectos, corresponde a lo que la literatura de LPS denomina *clone-and-own*. El problema que la literatura atribuye de manera característica a ese enfoque, la divergencia progresiva entre productos clonados, coincide con la brecha B-02 identificada de forma independiente en el estudio comparativo. El encuadre explica el problema, no solo lo describe.

**Matices declarados.** El encaje no es el de una LPS clásica en dos aspectos que el marco reconoce explícitamente. Primero, los productos derivados quedan bajo control autónomo del equipo que los recibe y pueden modificarse libremente (RNF-02), a diferencia de la derivación gobernada permanentemente por la línea. Segundo, la derivación no ocurre en un solo acto: el RF-06 exige incorporar capacidades a un proyecto ya derivado, lo que corresponde a configuración por etapas (*staged configuration*).

**Consecuencia.** El marco teórico incorpora siete términos: línea de producto de software, core asset, alcance de la línea, domain engineering y application engineering, variabilidad y punto de variación, feature model, binding time y clone-and-own. Bibliografía base: Clements y Northrop (2001); Clements (2002); Pohl, Böckle y van der Linden (2005); Apel et al. (2013); Kang et al. (1990); Dubinsky et al. (2013).

**Traza.** T-04, T-06, B-01, B-02.

---

## ADR-002 · Alcance declarado de la familia de productos

**Estado:** Revisada · 2026-09-11 · Item MR-01 · **revisada el 2026-11-09 por ADR-191**

**Contexto.** Una línea de producto exige un alcance gestionado. Sin él los core assets se vuelven genéricos e inservibles, o se acoplan a un caso particular.

**Decisión.** La familia de productos se declara como: servicios backend sobre Node.js y TypeScript, cada uno responsable de un único bounded context, que exponen al menos una API HTTP documentada bajo OpenAPI, consumen servicios corporativos y pueden publicar o consumir eventos.

**Fuera de la familia.** Aplicaciones frontend; aplicaciones serverless; procesos batch o workers sin API expuesta; scripts de propósito único; aplicaciones que alojan varios bounded contexts; servicios en lenguajes o ecosistemas distintos de los declarados.

**Por qué.** La exposición de API como condición mínima garantiza que todo producto de la familia comparte la misma superficie de entrada, lo que hace viable sostener una plantilla base única, y da sentido a la generación automática de documentación OpenAPI como capacidad transversal de la línea.

**Consecuencia.** La Fase 2 dimensiona los core assets para esta familia y no para casos fuera de ella. La Fase 4 selecciona el caso de estudio dentro de la familia declarada.

**Qué se revisó (2026-11-09, ADR-191).** La línea «fuera de la familia» excluía **las aplicaciones serverless**, y queda reescrita por lo que de verdad excluye: **las aplicaciones sin API HTTP expuesta**, cualquiera sea su modelo de ejecución. Un producto cuyo host invoca una función por ruta cumple la condición mínima de pertenencia que esta decisión fija —expone al menos una API HTTP documentada bajo OpenAPI, es responsable de un único bounded context y está sobre los lenguajes declarados— y lo que no tiene es *servidor propio*, que era la razón de la exclusión y no la condición. Un worker agendado sin rutas sigue fuera, y eso no se movió.

**Qué no se tocó, que es lo que hace que esto sea una Revisión y no una Ruptura.** La declaración de la familia —el párrafo de la decisión— no cambia en una palabra, ni la condición mínima, ni la unidad de derivación, ni la dirección de dependencia. De la justificación cae la parte que deducía «una plantilla base única», que **ADR-171** ya había revisado por su cuenta.

**Traza.** Alcance del proyecto, RF-01, RF-04, ADR-017, ADR-171, ADR-191, MR-01 §5, MR-01 §7.

---

## ADR-003 · Correspondencia entre fases y ciclo domain/application engineering

**Estado:** Aceptada · 2026-09-11 · Item MR-01

**Decisión.** Las fases 1, 2 y 3 se encuadran como *domain engineering*: construyen los core assets reutilizables, incluida la arquitectura de referencia. El uso de la herramienta por parte de un desarrollador para obtener un proyecto concreto se encuadra como *application engineering*. La Fase 4 evalúa el ciclo de application engineering.

**Por qué.** Da un nombre preciso a lo que hace cada fase y explica por qué la evaluación mide el costo de derivar un producto, y no atributos de calidad del artefacto en abstracto.

**Consecuencia.** Los criterios de evaluación de la Fase 4 se redactan en términos de derivación de un producto.

**Traza.** Objetivo específico 4, ADR-001.

---

## ADR-004 · Un proyecto generado equivale a un bounded context

**Estado:** Aceptada · 2026-09-11 · Item MR-02 · Remapeado desde MR-01 el 2026-09-14

**Decisión.** La unidad de derivación es un proyecto que aloja exactamente un bounded context, correspondiente a un Service Domain. No se admite la derivación de productos que alojen varios.

**Alternativas.** Permitir varios contextos por proyecto, con separación interna por capacidad. Se descarta porque diluye la frontera que hace verificable el desacoplamiento y porque el contexto de aplicación trabaja con repositorios independientes por proyecto.

**Por qué.** Se apoya en el criterio de elementalidad de BIAN, que define cada Service Domain como una capacidad de negocio discreta cuyo alcance es elemental (ADR-006). La propiedad de no solapamiento aporta la contraparte: impide que dos proyectos del laboratorio gobiernen la misma información. La regla deja de ser una preferencia del autor y pasa a apoyarse en un referente de industria.

**Delimitación necesaria.** La regla prohíbe alojar más de una capacidad de negocio. No prohíbe que un proyecto contenga capacidades técnicas del catálogo, datos de referencia ni servicios operativos, que no constituyen contextos adicionales.

**Consecuencia.** La estructura canónica de MR-03 se dimensiona para un solo contexto. La composición de módulos opera sobre esa unidad. El registro de versiones es único por repositorio.

**Traza.** ADR-006, ADR-019, RF-01.

---

## ADR-005 · TypeScript como lenguaje del marco y de los artefactos

**Estado:** Aceptada · 2026-09-11 · Item MR-01

**Decisión.** Los core assets y el mecanismo de derivación se construyen sobre Node.js y TypeScript, conforme al alcance declarado en la especificación de requerimientos.

**Por qué.** Los contratos de integración se declaran como interfaces y tipos. Una importación exclusivamente de tipos se elimina en compilación, de modo que el dominio del producto derivado no adquiere dependencia en tiempo de ejecución hacia el contract package. El desacoplamiento arquitectónico pasa a ser verificable por el compilador en lugar de ser una convención documentada.

**Consecuencia.** ADR-010 y ADR-022 se apoyan en esta propiedad. El RNF-03 puede satisfacerse con el análisis estático estándar del ecosistema.

**Traza.** RNF-02, RNF-03, ADR-010, ADR-022.

---

## ADR-006 · BIAN gobierna el dominio del proyecto, no el catálogo de módulos

**Estado:** Aceptada · 2026-09-11 · Item MR-02

**Contexto.** Los objetivos del trabajo comprometen alineación con BIAN. El catálogo de módulos agrupa capacidades técnicas transversales: registro de eventos, observabilidad, cifrado, identidad, persistencia y consumo de servicios corporativos.

**Decisión.** Se adopta la versión 14.0 del Service Landscape. BIAN gobierna tres aspectos del proyecto generado y ninguno más: identidad, expresada como un Service Domain; frontera, según el criterio de elementalidad y no solapamiento; y nomenclatura del agregado raíz, orientada por el control record. BIAN **no** se adopta como taxonomía del catálogo de módulos.

**Por qué.** El modelo de referencia BIAN describe capacidades de negocio bancario y deliberadamente no modela infraestructura técnica de aplicaciones. Afirmar que el catálogo se clasifica según BIAN sería una alineación nominal sin contenido verificable. La delimitación explícita del alcance de aplicabilidad de un estándar de industria a un artefacto de este tipo constituye en sí misma un resultado de la fase.

**Objeción anticipada.** La Business Area de Business Support contiene un Business Domain llamado IT Management. Sus Service Domains modelan la gestión de tecnología del banco como función organizacional, no componentes técnicos reutilizables, por lo que no alteran la delimitación.

**Espacio de selección.** De los 38 Business Domains del Service Landscape, nueve corresponden al tipo de productos del contexto: Customer Management, Sales, Servicing, Cross Channel, Party, Loans and Deposits, Payments, Account Management, Operational Services y Collateral Administration.

**Consecuencia.** El Service Domain se incorpora como punto de variación de la derivación, cuya formalización corresponde a la Fase 2. La extensión del catálogo con módulos de dominio alineados a BIAN se registra como punto de extensión y trabajo futuro. El acceso requerido se limita al Service Landscape público.

**Traza.** Objetivo específico 1, objetivo específico 3, sección 3.1.1.

---

## ADR-007 · Exclusión razonada de ISO 20022

**Estado:** Aceptada · 2026-09-11 · Item MR-02

**Decisión.** Se documenta la no aplicabilidad de ISO 20022 al artefacto, manteniendo sin cambios la redacción de los objetivos. La exclusión se presenta como hallazgo de la Fase 1.

**Por qué.** ISO 20022 es un estándar de mensajería financiera: define modelos de negocio y esquemas de mensajes para el intercambio de información entre instituciones. El artefacto no produce, transforma ni transporta mensajes financieros; produce estructuras de proyecto y componentes técnicos transversales. BIAN referencia correspondencias hacia ISO 20022 en la capa de especificación de mensajes, que es exactamente la capa que el artefacto no produce.

**Consecuencia.** La actividad de verificación de alineación prevista para la Fase 3 se reinterpreta como verificación de alineación con BIAN únicamente. Se registra como punto de extensión que un módulo de dominio que encapsule mensajería ISO 20022 sería un consumidor legítimo del marco, no parte de él.

**Traza.** Objetivo general, objetivo específico 1, Fase 3 actividad 5.

---

## ADR-008 · Marco tecnológicamente neutral respecto del framework destino

**Estado:** Aceptada · 2026-09-11 · Item MR-02

**Decisión.** El marco de referencia define reglas, estructuras y contratos sin fijar el framework de aplicación destino. La elección del framework se declara como decisión de instanciación al inicio de la Fase 2.

**Precisión de alcance.** Neutralidad respecto del framework significa que el núcleo del producto no depende de construcciones del framework. No significa que el marco evite nombrar capas, rutas o convenciones: ADR-020 y ADR-024 fijan estructura y nomenclatura concretas sin fijar framework.

**Por qué.** Preserva la frontera entre lo que el marco fundamenta y lo que las fases posteriores construyen. Permite además que el marco sea evaluable con independencia de la implementación concreta.

**Consecuencia.** MR-03 describe la estructura canónica en términos de capas, responsabilidades y direcciones de dependencia, no de artefactos de un framework particular. La primera decisión de la Fase 2 documenta la instanciación.

**Traza.** Metodología, separación Fase 1 / Fase 2, ADR-026.

---

## ADR-009 · Entrega híbrida de módulos: paquete más wiring generado

**Estado:** Aceptada · 2026-09-11 · Item MR-04 · Remapeado desde MR-05 el 2026-09-14

**Contexto.** Un módulo puede entregarse como dependencia consumida en ejecución, como código copiado dentro del proyecto, o como combinación de ambos. La decisión determina cómo se resuelven B-01 y B-02.

**Decisión.** Entrega híbrida. La implementación del módulo, es decir sus adapters, reside en un paquete versionado distribuido por el registro. El mecanismo de derivación genera únicamente el *wiring* específico del proyecto: el registro en el punto de composición, la entrada correspondiente en el esquema de configuración, las variables de entorno de ejemplo y, cuando aplique, la declaración del port en el proyecto.

**Regla de frontera.** Todo lo que es implementación va en el paquete. Todo lo que es cableado o configuración específica del proyecto se genera.

**Alternativas.** (a) Solo paquete: resuelve la propagación de forma trivial pero elimina toda capacidad de adaptación, lo que choca con T-10 y RNF-02. (b) Solo código inyectado: maximiza la adaptabilidad pero convierte la propagación en un problema de fusión a tres vías con conflictos, reproduciendo la limitación que el estudio comparativo identificó en Copier y Cruft.

**Por qué.** La lógica se propaga por versionado del paquete, lo que resuelve B-02 sin merges. La incorporación a un proyecto en curso es real porque el mecanismo modifica código existente, patrón que el estudio comparativo identificó en los generadores de Nx. La adaptación se canaliza por sustitución de adapter (ADR-012) en lugar de edición de fuentes.

**Por qué pertenece al marco.** Dos equipos que diseñaran el mecanismo por separado y eligieran formas de entrega distintas producirían líneas con garantías de propagación incompatibles: en una, un cambio alcanza a los productos existentes; en la otra, no. Es una regla, no una decisión de diseño.

**Consecuencia.** La Fase 3 construye dos artefactos por módulo: el paquete y el generador de wiring, versionados de forma coordinada. La forma concreta del wiring corresponde a la Fase 3. El RF-13 se satisface por construcción, dado que el código del módulo no reside en el proyecto consumidor.

**Traza.** B-01, B-02, T-04, T-09, T-05, RF-06, RF-07, RF-11, RF-13, RNF-02.

---

## ADR-010 · Contract package como propietario de los technical ports

**Estado:** Aceptada · 2026-09-11 · Item MR-04

**Contexto.** Si el módulo publica el port y el proyecto lo importa, el dominio del proyecto queda dependiendo del paquete del módulo y el desacoplamiento es nominal. Si cada proyecto declara sus propios ports técnicos, ningún módulo puede servir a dos proyectos.

**Decisión.** Se introduce un *contract package* que contiene exclusivamente interfaces y tipos, sin implementación. El proyecto derivado depende de él y el módulo también; ninguno depende del otro. El contract package se define en el marco y se construye como parte del mecanismo en la Fase 2.

**Por qué.** Invierte la dependencia en ambos sentidos hacia un artefacto neutral. En TypeScript (ADR-005) la dependencia del proyecto hacia el contract package es exclusivamente de tipos y desaparece en compilación, por lo que no existe acoplamiento en ejecución.

**Consecuencia.** El contract package se versiona de forma independiente de los módulos. Un cambio en él es un cambio de contrato y se rige por ADR-013. Un módulo declara qué versión de contrato implementa. La regla de dependencia de ADR-022 admite el contract package como destino permitido desde la capa de aplicación.

**Traza.** T-04, T-09, B-01, RF-06, RF-07, RNF-02.

---

## ADR-011 · Dos clases de port: domain ports y technical ports

**Estado:** Revisada · 2026-09-11 · revisada el 2026-09-16 · Item MR-04

**Decisión.** El marco distingue dos clases de port con propiedad distinta.

*Domain ports*: expresan intención del negocio en el lenguaje del dominio, por ejemplo un repositorio de un agregado o un publicador de eventos de dominio. Pertenecen al proyecto y ningún módulo puede apropiárselos.

*Technical ports*: expresan una capacidad técnica con contrato estable e independiente del dominio, por ejemplo logger, cifrador, cliente de identidad, publicador de mensajes o unidad de trabajo. Residen en el contract package y los implementan los módulos.

**Caso de referencia: persistencia.** El módulo de base de datos aporta la capacidad técnica: la conexión y la gestión de transacciones. El proyecto declara el domain port de repositorio y escribe su adapter concreto, apoyándose en la capacidad que el módulo provee. El dominio no conoce el motor de persistencia.

**Regla adicional.** Un producto válido de la familia no puede tener domain ports sin adapter. La realización concreta de esta regla en los artefactos generados corresponde a la Fase 2.

**Traza.** RF-01, RF-06, RNF-02, ADR-010, ADR-012, ADR-020.

---

## ADR-012 · Escala de adaptación de tres niveles

**Estado:** Revisada · 2026-09-11 · revisada el 2026-09-16 · Item MR-05

**Contexto.** El RNF-02 exige que el código generado sea modificable sin perder la capacidad de seguir usando la herramienta; el RF-11 exige poder actualizar un módulo sin intervención manual. Ambos entran en tensión si la adaptación se entiende como edición de los fuentes del módulo.

**Decisión.** La adaptación se define como una escala de tres niveles con consecuencias declaradas.

1. **Configurar.** Alterar el comportamiento mediante configuración externa. No afecta la actualización.
2. **Sustituir el adapter.** Implementar el mismo port con código propio y registrarlo en lugar del que provee el módulo. El proyecto conserva la capacidad de actualización, porque lo que cambió fue la elección de adapter y no el módulo.
3. **Bifurcar.** Copiar el módulo al proyecto y desvincularlo del catálogo. Permitido, con la consecuencia declarada de que ese módulo deja de recibir propagación; el registro de versiones lo marca como bifurcado.

**Por qué se admite la bifurcación.** Prohibirla no impediría que ocurra; solo la dejaría sin registro. Declararla con su consecuencia explícita es preferible a una prohibición que el marco no puede hacer cumplir.

**Reversión y señal (añadido el 2026-09-16).** La marca de bifurcación se retira cuando el producto vuelve a consumir el activo del catálogo. El marco no garantiza que eso sea posible, porque depende de que el activo llegue a cubrir lo que motivó la bifurcación. Por esa razón, una bifurcación se interpreta como señal de que al activo le falta un punto de configuración o de sustitución, y alimenta el flujo de nuevos requerimientos hacia el análisis del dominio.

**Por qué.** Resuelve la tensión RNF-02 / RF-11 sin sacrificar ninguno de los dos. La adaptabilidad se satisface como propiedad arquitectónica derivada de la arquitectura hexagonal, no como permiso de edición de archivos.

**Traza.** T-10, RF-11, RF-13, RNF-02, ADR-027.

---

## ADR-013 · Definición operativa de cambio incompatible

**Estado:** Revisada · 2026-09-11 · revisada el 2026-09-16 · Item MR-05

**Contexto.** El versionado semántico define las categorías pero no qué constituye incompatibilidad en este dominio. Sin esa definición, el RNF-06 y la política de actualización quedan sin criterio.

**Decisión.** La compatibilidad se define sobre el contrato, no sobre el código.

Constituye cambio **mayor**: eliminar o alterar la firma de una operación del port; agregar un parámetro de configuración obligatorio sin valor por defecto, o eliminar uno existente; alterar el identificador con que el módulo se registra en el punto de composición; alterar el comportamiento observable de modo que una prueba de conformidad previa deje de pasar; estrechar el rango soportado de Node.js o de versión de los activos base; alterar el formato del registro de versiones del proyecto.

Constituye cambio **menor**: agregar una operación opcional al port; agregar un parámetro de configuración con valor por defecto; agregar un adapter alternativo.

Constituye **parche**: corregir comportamiento sin alterar el contrato.

**Definición operativa (revisada el 2026-09-16).** La compatibilidad se determina por **inspección de lo declarado**: la firma de las operaciones, el esquema de configuración y el identificador de registro. Toda la evidencia necesaria está en el contrato, sin recurrir a ejecución. Con TypeScript, además, el compilador detecta por sí mismo los cambios de firma que rompen a un consumidor.

**Motivo de la revisión.** La redacción original definía la compatibilidad como pasar la suite de pruebas de conformidad de la versión anterior. La verificación por ejecución queda despriorizada (ADR-041), por lo que esa definición operativa pierde su respaldo. La enumeración de qué constituye cambio mayor, menor y parche se conserva sin cambios, porque está formulada sobre el contrato declarado y no requiere ejecución.

**Limitación asumida.** Un cambio de comportamiento que conserve la firma intacta no se detecta por inspección. Se registra como limitación del marco y como punto de extensión.

**Por qué.** Convierte el RNF-06 de una afirmación de diseño en una propiedad comprobable, aunque por lectura del contrato y no por ejecución.

**Traza.** T-12, RNF-06, RF-11, RF-12, ADR-022, ADR-041.

---

## ADR-014 · Actualización sin fusión a tres vías

**Estado:** Diferida · 2026-09-11 · reclasificada el 2026-09-14 · Corresponde a la Fase 3

**Decisión original.** La actualización de un módulo se resuelve elevando la versión del paquete. El wiring generado se regenera únicamente cuando la versión nueva declara una migración asociada. No se implementa reconstrucción con fusión a tres vías al estilo de Copier.

**Motivo del diferimiento.** Aplicado el criterio de ADR-026, esta decisión describe el mecanismo de actualización y no una regla que dos equipos tuvieran que compartir para que la línea siga siendo una línea. Lo que sí pertenece al marco es la definición de compatibilidad (ADR-013) y la garantía de propagación que se deriva de ADR-009.

**Carácter provisional conservado.** Si la Fase 3 evidencia que la regeneración de wiring produce conflictos con frecuencia, la decisión se revisa e incorpora un mecanismo de fusión acotado al wiring.

**Traza.** B-02, RF-11, RF-13, ADR-009, ADR-026.

---

## ADR-015 · Catálogo en dos capas

**Estado:** Aceptada · 2026-09-11 · Item MR-05 · Remapeado desde MR-06 el 2026-09-14

**Decisión.** El catálogo se materializa en dos capas. La **fuente de verdad y punto de gobernanza** es un repositorio Git que contiene un manifiesto declarativo con los activos, sus metadatos, su responsable y su estado. El **canal de distribución** es un paquete versionado publicado automáticamente desde ese repositorio.

**Por qué.** La capa Git aporta gobernanza real sin costo adicional: la incorporación de una entrada al catálogo es un pull request, el control de acceso son políticas de rama con revisores obligatorios por ruta, y las aprobaciones son revisiones. La capa de paquete aporta resolución versionada, inmutabilidad y caché, y usa el mismo canal, credenciales y red que los módulos. La combinación reproduce el patrón de catálogo con modelo de propiedad identificado en Backstage y Port, sin desplegar ni operar una aplicación, que es precisamente la brecha B-03.

**Instanciación de referencia.** En Azure DevOps Repos, la propiedad declarada en el manifiesto se hace exigible mediante políticas de rama con revisores obligatorios por ruta. La gobernanza se redacta como propuesta genérica con esta instanciación como ejemplo.

**Consecuencia.** El formato concreto del manifiesto corresponde a la Fase 3.

**Traza.** B-03, T-15, RF-14, RF-16.

---

## ADR-016 · Distribución agnóstica del registro de paquetes

**Estado:** Aceptada · 2026-09-11 · Item MR-05 · Remapeado desde MR-06 el 2026-09-14

**Contexto.** El RF-15 asume la existencia de un registro de paquetes en la organización. Al momento de definir el marco no existe tal registro y su creación está fuera del control del autor.

**Decisión.** El marco define que módulos, activos base y contract package se distribuyen mediante un registro de paquetes compatible con el gestor de paquetes del ecosistema, sin acoplarse a un proveedor concreto. La Fase 2 instancia la distribución con un registro privado propio. La migración al registro de la organización queda definida como cambio de configuración, sin impacto en el artefacto.

**Ajuste de requerimiento.** El criterio de aceptación del RF-15 se reformula: la herramienta obtiene los activos del registro configurado, sin canal propio de distribución.

**Riesgo asociado.** Se documenta como riesgo del trabajo la dependencia de una capacidad organizacional no disponible al inicio, junto con la mitigación adoptada.

**Traza.** T-12, RF-15, ADR-015.

---

## ADR-017 · Una sola plantilla base canónica

**Estado:** Revisada · 2026-09-11 · reclasificada el 2026-09-14 · **revisada el 2026-11-09 por ADR-171**

**Decisión original.** El catálogo contiene un único activo base, correspondiente a la familia de productos declarada en ADR-002. La variabilidad se expresa mediante puntos de variación sobre ese activo y mediante composición de módulos, no mediante activos base alternativos.

**Motivo del diferimiento.** Qué es una plantilla y qué contiene pertenece al diseño del mecanismo de derivación. Lo que sí pertenece al marco es el alcance de la familia (ADR-002), que es lo que hace viable sostener un único activo base.

**Cómo se resolvió (2026-11-09, ADR-171).** El diferimiento se retomó en la fase destino, como la regla manda, y la decisión original **no se aceptó**: el catálogo admite más de una plantilla, y una plantilla es un activo del mismo rango que un módulo, que se describe a sí mismo en su propio manifiesto. La razón no es técnica sino de cumplimiento: el alcance del anteproyecto compromete el «desarrollo de un sistema de almacenamiento de plantillas», el objetivo específico 2 habla de «plantillas configurables» en plural, y RF-14 y RF-15 hablan del «catálogo de plantillas y módulos». Sostener un único activo base habría dejado esa parte del alcance sin construir.

**Qué sobrevive de ella.** Los dos enunciados que la justificaban siguen vigentes y no se tocan. **ADR-002**, el alcance de la familia, queda intacto: MR-01 §7 lo declara estable por diseño, y lo que esta revisión cambia es dejar de **deducir** «una sola plantilla» de él. Y la variabilidad de un producto se sigue expresando con puntos de variación sobre su plantilla y con composición de módulos: lo que el almacén agrega es que puede haber más de una plantilla, no que la variabilidad se resuelva eligiendo entre ellas.

**Traza.** Alcance del proyecto, OE2, RF-01, RF-02, RF-14, RF-15, ADR-002, ADR-026, ADR-171, MR-01 §5, MR-01 §7.

---

## ADR-018 · Validación del marco por walkthrough documentado

**Estado:** Aceptada · 2026-09-11 · Cierre del proyecto · Remapeado desde MR-07 el 2026-09-14

**Decisión.** El marco de referencia se valida mediante un walkthrough documentado que recorre cada requerimiento funcional y no funcional y establece qué decisión del marco lo habilita, junto con una matriz de trazabilidad de cada decisión hacia la necesidad, brecha o requerimiento que la origina.

**Alternativas.** Revisión con las funciones de arquitectura y liderazgo técnico. Se difiere por disponibilidad; queda registrada como posible refuerzo de la validación.

**Por qué.** La dimensión del problema cerró con evidencia empírica. Cerrar la dimensión de la solución únicamente con decisiones declaradas dejaría la fase metodológicamente asimétrica.

**Consecuencia.** El walkthrough y la matriz se hacen en el documento de trazabilidad con que se cierra el proyecto, no dentro del marco: la cobertura de un requerimiento solo es medible contra lo construido, y medirla al definir el marco obliga a reescribirla en cada fase.

**Traza.** RF-01 a RF-16, RNF-01 a RNF-06.

---

## ADR-019 · Registro del Service Domain como metadato obligatorio

**Estado:** Aceptada · 2026-09-13 · Item MR-02

**Contexto.** La delimitación del dominio por BIAN (ADR-006) carece de efecto verificable si no deja rastro en el producto derivado.

**Decisión.** Todo proyecto derivado registra, como metadato, el Service Domain al que corresponde y el Business Domain que lo contiene. El mecanismo de derivación solicita ese dato al generar y lo escribe en el proyecto junto al registro de versiones.

**Excepción y prohibición.** Si el producto corresponde a una capacidad que no figura en el espacio de selección por defecto, se permite declarar un Service Domain fuera de ese subconjunto, registrando el Business Domain que lo contiene. Lo que no se admite es omitir el metadato.

**Por qué.** La asimetría entre la excepción admitida y la prohibición es lo que convierte la alineación con BIAN en una propiedad comprobable en lugar de una afirmación declarativa. Un espacio de selección cerrado sería inaplicable; la ausencia de metadato haría inverificable la delimitación.

**Consecuencia.** El formato concreto del metadato corresponde a la Fase 2. Sostiene RF-10 y habilita la verificación del RF-16.

**Traza.** ADR-004, ADR-006, RF-10, RF-16.

---

## ADR-020 · Organización por capas con agrupación por agregado en el dominio

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Contexto.** La práctica actual del contexto organiza el primer nivel del proyecto por capacidad, siguiendo el principio de que la estructura debe revelar qué hace el sistema. Es una decisión deliberada del equipo, no acumulación sin criterio.

**Decisión.** El proyecto generado se organiza primero por capa: `domain`, `application`, `infrastructure`. Dentro de la capa de dominio se agrupa por agregado, con una carpeta `shared` para los objetos de valor comunes a más de un agregado.

**Alternativas.** (a) Capas arriba con agrupación por tipo de patrón dentro del dominio: más fácil de recorrer con un solo agregado, pero obliga a tocar varias carpetas ante un cambio y se degrada al crecer. (b) Capacidad arriba con capas dentro: agrupa bien, pero repite la estructura de capas por cada agregado, complica la expresión de la regla de dependencia y hace visualmente natural agregar una carpeta hermana, que es lo que ADR-004 prohíbe.

**Por qué.** La organización por capacidad resuelve un problema real cuando un repositorio aloja varias capacidades. La regla de ADR-004 elimina ese problema: el repositorio, su nombre y su metadato de Service Domain (ADR-019) declaran la capacidad antes de abrir una carpeta. La estructura interna queda liberada de esa responsabilidad y puede dedicarse a hacer visible y verificable la frontera entre el núcleo y el exterior. La práctica actual no se descarta por inferior: se vuelve innecesaria porque la condición que la justificaba desaparece.

**Por qué pertenece al marco.** Un activo del catálogo debe poder incorporarse a cualquier producto de la familia, y para eso necesita una forma conocida: dónde se declara un puerto, dónde se ubica su adaptador, cómo se nombra lo que busca. La estructura común es condición previa para que los core assets existan.

**Traza.** ADR-004, ADR-019, ADR-022, RNF-02, T-02, T-10.

---

## ADR-021 · Los datos de referencia residen en la infraestructura

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Decisión.** Los catálogos de valores que un producto consulta pero no gobierna se modelan como capacidades técnicas de consulta y residen en la infraestructura, no en el dominio.

**Por qué.** No tienen ciclo de vida propio dentro del producto ni reglas de negocio asociadas. Ubicarlos en el dominio lo llenaría de entidades sin comportamiento y diluiría la frontera que ADR-022 hace verificable.

**Traza.** ADR-020, ADR-022.

---

## ADR-022 · Dirección de dependencia y severidad de la regla verificable

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Decisión.** Las dependencias permitidas son: `domain` únicamente hacia `domain`; `application` hacia `domain` y contratos de puerto; `infrastructure` hacia `application`, `domain` y contratos de puerto. De esas direcciones se deriva la regla verificable: ningún elemento de `domain` importa un elemento de `application` o de `infrastructure`.

**Verificación.** Análisis estático sobre las rutas de importación, no revisión manual. El marco fija el tipo de mecanismo; la herramienta concreta corresponde a la Fase 2.

**Severidad.** La violación se reporta como error, no como advertencia. Un proyecto que la incumpla no supera la verificación de integración continua.

**Por qué.** Una regla que solo advierte no restringe. La severidad es lo que da contenido al RNF-03 y convierte la independencia tecnológica del núcleo en una propiedad comprobable en lugar de una convención documentada.

**Consecuencia sobre la verificabilidad.** La dirección de dependencia determina qué puede probarse y cómo: el dominio se verifica sin sustituir elementos, la capa de aplicación sustituyendo puertos, y un adaptador contra el puerto que implementa. Esta última correspondencia es la que ADR-013 emplea para definir la conformidad entre versiones.

**Traza.** ADR-005, ADR-010, ADR-013, RNF-03.

---

## ADR-023 · Inglés como idioma del código

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Decisión.** Todo el código se escribe en inglés, incluidos los nombres del dominio, que provienen del vocabulario del Service Domain.

**Por qué.** El lenguaje ubicuo exige que los nombres del dominio correspondan al vocabulario de su Service Domain, que está en inglés. Extender la regla a todo el código evita la mezcla de idiomas dentro de un mismo archivo y elimina la ambigüedad sobre qué elementos deben traducirse.

**Traza.** ADR-006, ADR-019.

---

## ADR-024 · Sufijos de rol y convención de nombres de archivo

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Decisión.** El nombre de cada identificador incorpora el rol del elemento como sufijo. Los archivos se nombran en minúsculas con guiones, seguidos del sufijo de rol y la extensión, con el formato `consumer-loan.entity.ts`.

**Por qué.** La redundancia entre el sufijo del archivo y el del identificador es deliberada: hace que el rol sea reconocible tanto al recorrer el árbol de directorios como al leer una importación aislada, y da al mecanismo de derivación una convención determinista sobre la que operar.

**Consecuencia.** La generación de nombres en la Fase 2 se ajusta a esta convención. Un activo del catálogo puede localizar elementos del proyecto por convención, sin inspección.

**Traza.** ADR-020, RNF-02.

---

## ADR-025 · Separación del contrato externo respecto del dominio

**Estado:** Aceptada · 2026-09-13 · Item MR-03

**Decisión.** Los tipos que un adaptador de entrada expone al exterior son distintos de los objetos de dominio. El adaptador traduce explícitamente entre unos y otros.

**Por qué.** Son dos contratos con ciclos de vida independientes. El objeto de dominio cambia cuando cambian las reglas del negocio; el tipo expuesto solo debe cambiar cuando cambia el acuerdo con los consumidores. Si el adaptador expone el objeto de dominio, cualquier reorganización interna se convierte en un cambio incompatible para los consumidores.

**Consecuencia.** Los tipos expuestos, al ser explícitos, constituyen la fuente desde la cual puede derivarse la documentación del contrato, lo que el RF-04 aprovecha. El mecanismo concreto de esa derivación corresponde a la Fase 2.

**Traza.** RF-04, ADR-013, ADR-022.

---

## ADR-026 · Criterio de alcance del marco

**Estado:** Aceptada · 2026-09-14 · Transversal

**Contexto.** Sin un criterio explícito, el marco tiende a absorber decisiones de diseño que corresponden a las fases posteriores, lo que anticipa trabajo sin evidencia y obliga a revisar la Fase 1 cada vez que la construcción enseña algo.

**Decisión.** Una decisión pertenece al marco si dos equipos, diseñando el mecanismo de derivación por separado, tendrían que llegar obligatoriamente a la misma respuesta para que la línea siga siendo una línea. Si pueden divergir sin romper nada, es diseño y corresponde a una fase posterior.

**Consecuencias sobre la estructura del marco.** El marco pasa de siete a seis documentos. Los antiguos MR-05 (módulos y composición) y MR-06 (ciclo de vida) se reorganizan: sus partes arquitectónicas se absorben en MR-04 y sus partes de gobierno se concentran en el nuevo MR-05. El antiguo MR-07 pasa a MR-06.

**Decisiones reclasificadas.** ADR-014 y ADR-017 quedan en estado Diferida.

**Qué recibe la Fase 2.** Qué es una plantilla y qué contiene; el punto de composición del producto; el modelo de variabilidad concreto; tratamiento de errores y su taxonomía; convenciones de registro de eventos de operación; suite de pruebas y umbrales; mecanismo de generación de la documentación del contrato; versionado del contrato externo; herramienta de análisis estático; framework de aplicación destino.

**Qué recibe la Fase 3.** Forma del wiring generado; reglas de composición y detección de conflictos; formato del manifiesto del catálogo; mecanismo de actualización y de detección de desviación; suite de conformidad concreta.

**Traza.** Metodología, ADR-008, ADR-014, ADR-017.

---

## ADR-027 · Mecanismo de evolución del marco

**Estado:** Aceptada · 2026-09-14 · Item MR-01

**Contexto.** El marco se define antes de construir el mecanismo. La implementación producirá aprendizaje que el diseño inicial no puede anticipar. Sin un mecanismo declarado, cualquier cambio posterior se leería como defecto de la Fase 1.

**Decisión.** El marco es revisable, y el flujo de nuevos requerimientos del modelo de referencia adoptado es su mecanismo: al residir el marco en el cuadrante de análisis del dominio, ese flujo alcanza tanto al catálogo como al propio marco. Todo cambio se clasifica en una de cuatro categorías.

| Categoría | Qué es | Qué exige |
| :---- | :---- | :---- |
| Refinamiento | Agrega detalle donde el marco dejó un espacio abierto | Nada. El marco ya lo difirió |
| Extensión | Agrega una regla nueva que no contradice ninguna existente | Se suma al documento correspondiente |
| Revisión | Contradice una regla existente | Se cambia la decisión y se registra el motivo con estado Revisada |
| Ruptura | Invalida un elemento constitutivo del encuadre | Obliga a revisar MR-01. Debe ser excepcional |

**Qué es estable por diseño.** Los elementos constitutivos y sus consecuencias directas: el encuadre de línea de producto, el alcance de la familia, la unidad de derivación y la dirección de dependencia. Si alguno cambia, no se está refinando el marco sino construyendo otro.

**Qué se espera que se mueva.** Convenciones y mecanismos: nomenclatura, agrupación interna del dominio, forma de los contratos y política concreta de versionado.

**Regla de registro.** Toda decisión tomada sin evidencia de implementación se marca como Aceptada (provisional) con su condición de revisión escrita. Toda revisión posterior registra qué la motivó.

**Por qué.** El diseño de ciencia aplicada es iterativo por definición: construir y evaluar alimentan de vuelta al diseño. Un marco incapaz de cambiar sería incompatible con la metodología declarada. Con el mecanismo explícito, un cambio en la Fase 3 deja de leerse como corrección de la Fase 1 y pasa a leerse como el flujo de retroalimentación funcionando según lo previsto.

**Traza.** Metodología, ADR-001, ADR-026.

---

## ADR-028 · Contract package organizado en submódulos por capacidad

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Decisión.** El contract package se organiza en submódulos por capacidad, de modo que el producto declara una sola dependencia pero importa únicamente lo que nombra.

**Alternativas.** (a) Un artefacto plano con todos los puertos: la importación deja de ser granular y el producto arrastra lo que no usa. (b) Un artefacto independiente por capacidad: versiona de forma independiente, pero multiplica las entradas del catálogo y el coste de gobernanza sin justificación mientras el catálogo es pequeño.

**Migración prevista.** La versión del contract package es compartida por todas las capacidades, de modo que un cambio incompatible en una obliga a revisar la versión en todas. Cuando ese efecto resulte oneroso, cada submódulo puede convertirse en un artefacto independiente cambiando únicamente la ruta de importación. La migración se declara prevista, no como revisión del marco sino como extensión anticipada. Su disparador se fija en ADR-037.

**Traza.** ADR-010, ADR-037.

---

## ADR-029 · El contract package contiene únicamente declaraciones de tipo

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Decisión.** El contract package no contiene implementación ni código ejecutable: contiene únicamente declaraciones de tipo.

**Precisión de la regla.** La regla no es "solo interfaces", porque una interfaz necesita tipos para sus parámetros y retornos. Es la ausencia de todo lo que sobreviva a la compilación, que es lo que preserva la propiedad de ADR-005.

**Tratamiento de los datos del producto.** Cuando un puerto opera sobre datos que pertenecen al dominio de un producto, el puerto se declara genérico y el producto aporta el tipo. Así el contrato nunca conoce el dominio de ningún producto, y el producto nunca depende del módulo.

**Traza.** ADR-005, ADR-010, ADR-011.

---

## ADR-030 · Criterio de clasificación de puertos por su firma

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Contexto.** ADR-011 distingue dos clases de puerto con ejemplos, pero sin una regla que resuelva los casos ambiguos. Sin criterio, el primer caso dudoso se decide por opinión.

**Decisión.** Un puerto es **de dominio** si su firma menciona conceptos del dominio del producto. Es **técnico** si su firma es expresable sin conocer el dominio.

**Por qué.** El criterio se apoya en lo declarado y no en el uso, de modo que dos equipos que lo apliquen por separado llegan a la misma clasificación. Un repositorio menciona el agregado; un registro de eventos de operación no menciona nada del dominio.

**Traza.** ADR-011.

---

## ADR-031 · Condiciones de validez de un módulo

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Decisión.** Tres condiciones hacen válido a un módulo: provee al menos un adaptador de un puerto técnico declarado en el contract package; declara explícitamente qué versión del contract package implementa; y no declara ni se apropia de puertos de dominio, ni contiene conceptos del dominio de ningún producto.

**Consecuencia de la primera condición.** Implementar un contrato es lo que hace sustituible al módulo. Código compartido que no implementa ningún puerto no es un módulo del catálogo sino una biblioteca de apoyo, y queda fuera del gobierno de la línea.

**Condición retirada.** La redacción de trabajo incluía una cuarta condición, proveer pruebas de conformidad contra el puerto implementado. Se retira por ADR-041 y reaparecerá cuando se defina la verificación de conformidad.

**Traza.** ADR-009, ADR-010, ADR-011, ADR-041.

---

## ADR-032 · Reglas de composición de módulos

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Decisión.** Tres reglas gobiernan la composición.

*Un módulo depende de contratos, nunca de otro módulo.* Evita un grafo de dependencias entre activos, que complicaría la actualización y acoplaría ciclos de vida independientes. Cuando un módulo necesita una capacidad de otro, la declara como puerto y el producto decide qué adaptador la satisface.

*Un producto admite un solo adaptador por puerto.* Más de uno exigiría una noción de calificador o identificador que el marco no necesita todavía. La restricción puede levantarse después sin invalidar nada de lo definido.

*Los módulos aportan adaptadores de salida.* Un adaptador de entrada escribe en la superficie externa del producto, que es contrato con terceros. Se admite una excepción: un módulo de verificación de estado, por tratarse de una capacidad operativa sin lógica de negocio ni impacto sobre el contrato funcional.

**Traza.** ADR-009, ADR-011, ADR-025.

---

## ADR-033 · Un módulo puede proponer puertos técnicos nuevos

**Estado:** Aceptada · 2026-09-16 · Item MR-04

**Decisión.** Un módulo puede proponer un puerto técnico nuevo en el contract package.

**Alternativas.** Exigir aprobación previa para cada puerto nuevo antes de construir el módulo. Se descarta porque convertiría el contrato en cuello de botella del catálogo.

**Consecuencia.** La propuesta queda sujeta a las reglas de incorporación del catálogo (ADR-015), de modo que la apertura no elimina el control: lo traslada al punto de gobernanza.

**Carácter iterable.** La decisión se toma para la primera versión del marco y puede endurecerse si el vocabulario del contrato crece sin criterio.

**Traza.** ADR-010, ADR-015.

---

## ADR-034 · Tipos de activo y condiciones comunes de validez

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** El catálogo reconoce tres tipos de core asset: activo base, módulo y contract package. Tres condiciones son comunes a todo activo con independencia de su tipo: tiene un equipo responsable declarado, se distribuye con una versión que sigue la política del marco, y declara de qué otros activos depende y en qué versión.

**Condiciones específicas por tipo.** El activo base produce un producto conforme a la estructura canónica y a las reglas de dependencia. El módulo cumple ADR-031. El contract package cumple ADR-029.

**Justificación de la tercera condición común.** Es la que hace gobernable al conjunto: permite responder qué se ve afectado por un cambio consultando el catálogo, sin abrir los repositorios de los productos.

**Alcance.** La lista de tipos es cerrada en esta versión del marco. La admisión de tipos adicionales se registra como trabajo futuro.

**Traza.** ADR-029, ADR-031, ADR-015.

---

## ADR-035 · El responsable de un activo es un equipo

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** El responsable declarado de un activo es un equipo, no una persona.

**Por qué.** Un activo cuyo responsable fuera una persona quedaría huérfano al salir esa persona de la organización. Un equipo es una entidad que sobrevive a la rotación de sus integrantes, lo que hace sostenible la propiedad declarada a lo largo del tiempo.

**Consecuencia.** La exigibilidad de la propiedad mediante políticas sobre las rutas del manifiesto requiere que el equipo exista como entidad nombrable en la plataforma de control de versiones.

**Traza.** ADR-015, ADR-034, RF-16.

---

## ADR-036 · Declaración de compatibilidad por versión mayor del contrato

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** Un módulo declara la versión mayor del contract package que implementa, no una versión exacta ni un rango.

**Consecuencia.** Un cambio menor del contrato no obliga a republicar el módulo, porque por definición no rompe implementaciones existentes. Solo un cambio mayor lo obliga.

**Alternativas.** (a) Versión exacta: cada publicación del contrato arrastraría una publicación de cada módulo. (b) Rango de versiones: resuelve lo mismo que la versión mayor pero introduce sintaxis de rangos sin beneficio adicional en esta etapa.

**Por qué.** Aprovecha directamente lo que la política de versionado de ADR-013 ya garantiza, con una sola línea de declaración.

**Traza.** ADR-013, ADR-031, RNF-06.

---

## ADR-037 · Criterio de migración del contract package

**Estado:** Aceptada (provisional) · 2026-09-16 · Item MR-05

**Contexto.** El contract package se versiona como una unidad (ADR-028), de modo que un cambio incompatible en una capacidad eleva la versión mayor de todas.

**Consecuencia.** Un producto que consume una sola capacidad recibe una versión mayor que no le afecta, y un módulo puede verse obligado a republicarse sin que su implementación haya cambiado.

**Paliativo adoptado.** El registro de cambios del contract package indica qué submódulos cambiaron en cada versión, de modo que un producto puede determinar en una lectura si una versión mayor lo afecta.

**Criterio de migración.** Cuando un módulo deba republicarse sin alterar su implementación más de dos veces, el acoplamiento de versión cuesta más de lo que ahorra en gobernanza y corresponde migrar a artefactos independientes por capacidad. Hasta entonces, la versión compartida se mantiene.

**Carácter provisional.** El umbral de dos republicaciones es una estimación sin evidencia de operación. Se revisa cuando el catálogo tenga historial suficiente.

**Traza.** ADR-013, ADR-028, ADR-036.

---

## ADR-038 · Estados del catálogo y no admisión de retiro

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** Una entrada del catálogo admite tres estados: *propuesto*, que no se ofrece al derivar; *activo*, que se ofrece y propaga cambios; y *en desuso*, que no se ofrece al derivar pero cuyos productos consumidores siguen funcionando y reciben correcciones.

**No se admite retirar un activo.** Un activo del que dependen productos existentes no puede eliminarse del catálogo sin romperlos.

**Consecuencia.** *En desuso* es el estado terminal de esta versión del marco: el activo permanece en el catálogo indefinidamente. El retiro acompañado de un procedimiento de migración se registra como trabajo futuro.

**Traza.** ADR-015, ADR-039, RF-16.

---

## ADR-039 · Contenido de una entrada del catálogo

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** Una entrada del catálogo declara: identificador, tipo de activo, responsable, descripción, paquete asociado, versión de contrato que implementa cuando aplica, y estado.

**Naturaleza de la entrada.** Una entrada no contiene el activo: lo describe y señala dónde reside. El catálogo cumple dos funciones con ella: el mecanismo de derivación la consulta para saber qué puede ofrecer y de dónde obtenerlo, y la gobernanza opera sobre ella, porque incorporar un activo consiste en agregar un registro.

**Consecuencia.** El formato concreto del manifiesto corresponde a la Fase 3. Lo que el marco fija es qué debe declarar cada entrada, no cómo se escribe.

**Traza.** ADR-015, ADR-034, ADR-035, ADR-038.

---

## ADR-040 · Registro de versiones del producto

**Estado:** Aceptada · 2026-09-16 · Item MR-05

**Decisión.** Todo producto derivado mantiene un registro de los activos que incorporó y en qué versión. El marco exige que ese registro exista y que permita responder tres preguntas, sin fijar su formato: qué activos incorporó el producto y en qué versión; cuáles de ellos están bifurcados; y con qué versión del activo base fue derivado.

**Justificación de cada pregunta.** La primera permite determinar si un cambio en un activo alcanza a este producto. La segunda hace visible que un activo bifurcado no recibe propagación (ADR-012). La tercera permite detectar la desviación entre el producto y su origen.

**Consecuencia.** El formato del registro y el mecanismo que lo lee y actualiza corresponden a las fases posteriores. El metadato de dominio de ADR-019 se escribe junto a este registro.

**Traza.** ADR-012, ADR-019, RF-10, RF-12.

---

## ADR-041 · Despriorización de la verificación de conformidad

**Estado:** Aceptada · 2026-09-16 · Transversal

**Contexto.** El marco preveía verificar la conformidad entre un adaptador y su puerto mediante una suite de pruebas ejecutable, sobre la que se apoyaba la definición operativa de compatibilidad.

**Decisión.** La verificación de conformidad por ejecución queda despriorizada, y con ella la obligación de que un módulo provea pruebas de conformidad. La compatibilidad se verifica por inspección del contrato declarado (ADR-013).

**Motivo.** Priorización del alcance del trabajo hacia los objetivos comprometidos, dado el tiempo disponible.

**Limitación asumida.** Un cambio de comportamiento que conserve la firma intacta no se detecta por inspección. Es un caso real aunque minoritario, y se registra como limitación del marco.

**Consecuencia sobre los requerimientos.** El criterio de aceptación de **RNF-06** no se verifica por ejecución: la convivencia de versiones se sostiene en la compatibilidad declarada y comprobada por inspección. El walkthrough del marco debe registrarlo así y no como omisión.

**Punto de extensión.** La reintroducción de la verificación de conformidad restituye la detección de cambios de comportamiento y la cuarta condición de validez de ADR-031.

**Traza.** ADR-013, ADR-022, ADR-031, RNF-06.

---

## ADR-165 · Cómo se toma la línea base con la ventana vencida

**Estado:** Aceptada · 2026-11-06 · Bloque A, doc 07

**Contexto.** El índice de esta fase declaró el documento 7 con una condición explícita sobre su oportunidad: la línea base del costo de arrancar un proyecto sin la herramienta debía tomarse *antes* de que la herramienta produjera proyectos, porque el dato es más creíble recogido antes de que exista el artefacto. No se tomó, y la condición se venció: la herramienta deriva productos verificables desde octubre de 2026. El primer criterio del objetivo específico 4 —el tiempo de configuración inicial frente a la línea base de proyectos existentes— no se puede evaluar sin ella, y por eso el pendiente P-01 figuró como riesgo declarado al cerrar las fases 2 y 3. La pregunta que esta decisión resuelve no es si la línea base se toma, sino con qué evidencia se toma ahora que la ventana se cerró.

**Decisión.** La línea base se constituye como **reconstruida y no prospectiva**, sobre dos fuentes y ninguna más:

1. **El autoreporte ya recogido.** Las preguntas cerradas de las entrevistas del 5 y 6 de agosto de 2026, anteriores a la primera línea de la herramienta, aportan el tiempo de arranque declarado por los roles del contexto estudiado, y los temas T-01 a T-05 aportan el mecanismo y su costo percibido. No se levanta autoreporte nuevo: el equipo ya conoce la herramienta y una respuesta de hoy no mediría el proceso anterior.
2. **Un inventario de las tareas de arranque**, reconstruido de T-01 y de lo que hoy entrega el activo base de la línea, con cada tarea clasificada en **cubierta**, **parcialmente cubierta** o **fuera del alcance** de la herramienta.

Con ellas se fija la definición operacional que gobierna las dos mediciones, la de esta fase y la de la Fase 4:

| Elemento | Definición |
| :---- | :---- |
| Inicio | La decisión de construir el proyecto, no su primer commit, que ya es trabajo hecho |
| Fin | El proyecto corre correctamente en local y queda desplegable en la rama principal, de modo que el resto del equipo pueda aportar cambios reales |
| Unidad primaria | Días, reportados como banda y nunca como promedio |
| Unidad derivada | Horas-persona, con los supuestos S-1, S-2 y S-3 declarados en el documento 7 |
| Métricas | M1 días · M2 horas-persona · M3 pasos manuales · M4 superficie que hoy no se escribe · M5 divergencia · M6 costo de propagar un cambio |
| Regla de las tres cubetas | La comparación principal se reporta sobre las tareas cubiertas por la herramienta; el total se reporta al lado, como contexto |
| Contraste externo | El dato del contexto externo se reporta aparte y no se suma a la banda del contexto estudiado |

**Alternativas.**

*Reconstruir la línea base de la historia de los repositorios de proyectos anteriores.* Se descarta por dos razones independientes, cada una suficiente: no existe acceso institucional a esos repositorios, y su historial es material privado de la organización que este expediente no publica, ni completo ni anonimizado, por la regla de confidencialidad del proyecto. Ninguna afirmación de la línea base se apoya en ese material.

*Ejecución controlada hoy: construir un proyecto a mano, cronometrado, sin la herramienta.* Se descarta porque está contaminada en su origen —quien la ejecutara ya conoce la estructura objetivo que la línea produce, de modo que mediría un arranque informado y no el arranque real— y porque cuesta días-persona que no mejoran la evidencia.

**Por qué.** El autoreporte es la única fuente de esta medición que es anterior al artefacto, y su valor no depende de que la herramienta exista hoy. El inventario es lo que vuelve la comparación conmensurable: el fin declarado es más ancho que el alcance de la herramienta, que deja un proyecto que corre y pasa su verificación pero no crea el repositorio ni despliega el servicio, de modo que comparar el tiempo de una derivación contra el proceso completo sobreestimaría la ganancia. La regla de las tres cubetas es la que impide ese error, y por eso es parte de la decisión y no del documento.

**Límites declarados.** La línea base queda con dos puntos de dato para el contexto estudiado y sin corroboración independiente **publicable** del autoreporte. El documento 7 lo declara en su sección de límites, en lugar de presentar una banda como si fuera una medición instrumentada. Cuántos repositorios hay que tocar para propagar un cambio de una capacidad compartida queda como dato no disponible, también declarado.

**Consecuencia.** El documento 7 del Bloque A se escribe sobre esta decisión y cierra el pendiente P-01. La Fase 4 mide el otro lado con esta misma definición operacional y reporta su comparación sobre la cubeta de las tareas cubiertas. Las afirmaciones de las fases 2 y 3 que declaran la línea base como no tomada quedan anotadas con nota fechada, sin reescribir su texto de cierre. El log de decisiones de la Fase 4 abre en **ADR-166**, porque la numeración es global continua y este número queda tomado.

**Traza.** T-01, T-03, T-04, T-05, T-14, P-01, objetivo específico 4.

---

## ADR-191 · La familia admite un producto sin servidor propio

**Estado:** Revisada · 2026-11-09 · Item MR-01 · **revisa ADR-002** y el alcance de la Fase 1 doc 06

**Contexto.** El autor pidió una plantilla con enfoque serverless, para Azure Functions. El proyecto lo tiene excluido **dos veces**, y las dos son suyas:

| Dónde | Qué dice |
| :---- | :---- |
| Fase 1, doc 06, «Fuera del alcance» | «Aplicaciones serverless. La herramienta se orienta a servicios backend **con servidor propio**» |
| **ADR-002**, «Fuera de la familia» | «aplicaciones frontend; **aplicaciones serverless**; procesos batch o workers sin API expuesta; …» |

MR-01 §5 lo repite nombrando su origen: «las aplicaciones serverless **ya excluidas del alcance de la solución**».

**Lo primero que hay que decir, porque cambia la categoría.** **El anteproyecto no excluye serverless.** Sus tres exclusiones son el despliegue y la automatización DevOps, las funcionalidades específicas de negocio, y «lenguajes o ecosistemas distintos de Node.js» — y una Azure Function sobre el runtime de Node.js **es** Node.js. La exclusión es una restricción que el proyecto se puso y que el anteproyecto nunca pidió, igual que el «una sola plantilla» que **ADR-017** sostenía y que **ADR-171** revisó. Así que esto **no es una divergencia respecto del anteproyecto**: es el proyecto revisando su propio estrechamiento.

**Por qué no es una Ruptura, que es la pregunta que el marco obliga a contestar.** MR-01 §7 declara estable por diseño el alcance de la familia, y una Ruptura «debe ser excepcional». La condición **mínima de pertenencia** que ADR-002 fija es «exponer al menos una API HTTP documentada bajo OpenAPI», y un producto de esta plantilla la cumple entera: sirve rutas HTTP con trigger HTTP, responde `GET /api/openapi.json` con su documento, es responsable de un único bounded context, está sobre Node.js y TypeScript, y puede consumir servicios corporativos. Lo que **no** tiene es *servidor propio*, que es la razón declarada de la exclusión y no la condición de pertenencia. La categoría es **Revisión** de una exclusión con criterio acotado, más un **Refinamiento** de MR-01 §5; el encuadre de MR-01, la unidad de derivación y la dirección de dependencia no se tocan.

**Y hay una razón más, que conviene no esconder.** La justificación de ADR-002 decía que la condición mínima «hace viable sostener **una plantilla base única**». Esa deducción ya cayó con ADR-171. Una exclusión cuya justificación se apoyaba en parte sobre una premisa revisada es, por lo menos, revisable.

**Decisión.** La familia admite un producto **sin servidor propio**, siempre que cumpla la condición mínima de pertenencia. La exclusión se reescribe por lo que de verdad excluye:

| Antes | Ahora |
| :---- | :---- |
| «Aplicaciones serverless» | **Aplicaciones sin API HTTP expuesta**, cualquiera sea su modelo de ejecución. Un producto cuyo host invoca una función por ruta pertenece a la familia; un worker agendado sin rutas no, y eso no cambia |

**Qué sigue fuera, y sin moverse.** Las aplicaciones frontend, los procesos batch y workers **sin API expuesta** —que es el caso que el fixture de ADR-179 imita, y por eso es un fixture y no un activo publicado—, los scripts de propósito único, las aplicaciones con más de un bounded context y los lenguajes distintos de los declarados. El plan de esta ronda ofreció un worker como tercera opción y quedó descartado por esto.

**Qué cambia de lo construido, y es poco.** Nada del contrato, nada del catálogo, nada del mecanismo. Lo que cambia es que una forma de producto puede no tener punto de composición con contenedor de inyección, y eso ya era expresable desde **ADR-176**: la forma del producto es un dato que la plantilla declara. Una plantilla sin contenedor declara los puntos que de verdad tiene, y la composición compara contra eso.

**Consecuencia asumida, declarada.** Ningún módulo del catálogo sirve la forma nueva: `@bsl/persistence` y `@bsl/observability` exportan un módulo de NestJS, que un host de funciones no sabe registrar, y los dos declaran servir `nestjs-hexagonal@1`. La composición los rechaza nombrando la causa, que es **ADR-180 funcionando** y no un hueco. Que la línea tenga una forma sin módulos es un estado legítimo del catálogo, y el orden de crecimiento del doc 1 de la Fase 3 sigue siendo el que manda sobre qué capacidad se construye después.

**Qué hay que ajustar fuera del código.** La frase de la Fase 1 doc 06 y la de MR-01 §5, las dos con nota fechada. Y el **capítulo 3 de la tesis**, que narra el marco y transcribe el alcance de la familia: queda en **P-42**.

**Traza.** Alcance del anteproyecto, objetivo específico 2, RF-01, RF-02, RF-04, ADR-002, ADR-008, ADR-017, ADR-171, ADR-176, ADR-179, ADR-180, ADR-194, MR-01 §5 y §6, MR-01 §7, Fase 1 doc 06, el índice de la Fase 2 y su doc 7.

---

## Decisiones diferidas a fases posteriores

| ID | Decisión | Fase | Motivo |
| :---- | :---- | :---- | :---- |
| ADR-014 | Actualización sin fusión a tres vías | Fase 3 | Describe el mecanismo de actualización, no una regla compartida |
| ADR-017 | Una sola plantilla base canónica | Fase 2 | Qué es una plantilla y qué contiene pertenece al diseño del mecanismo. **Retomada y revisada el 2026-11-09 por ADR-171**, que es ese diseño: una plantilla es un activo del catálogo que se describe a sí mismo, y el catálogo admite más de una |

## Alcance diferido del marco

Lo que el marco deja explícitamente fuera, con su destino. Se enumera para que su ausencia no se lea como omisión.

| Decisión | Dónde se resuelve | Origen |
| :---- | :---- | :---- |
| Qué es una plantilla y qué contiene | Fase 2 | MR-03 |
| Forma y ubicación del punto de composición del producto | Fase 2 | MR-03 |
| Tratamiento de errores y su taxonomía | Fase 2 | MR-03 |
| Convenciones de registro de eventos de operación | Fase 2 | MR-03 |
| Composición de la suite de pruebas y umbrales de cobertura | Fase 2 | MR-03 |
| Mecanismo de generación de la documentación del contrato | Fase 2 | MR-03 |
| Estrategia de versionado del contrato externo | Fase 2 | MR-03 |
| Herramienta concreta de análisis estático | Fase 2 | MR-03 |
| Framework de aplicación destino | Fase 2 | MR-02 |
| Formato concreto del contrato de integración | Fase 2 | MR-04 |
| Expresión de la transaccionalidad entre repositorios | Fase 2 | MR-04 |
| Formato del registro de versiones del producto | Fase 2 | MR-05 |
| Forma del cableado generado | Fase 3 | MR-04 |
| Detección de conflictos entre módulos | Fase 3 | MR-04 |
| Formato concreto del manifiesto del catálogo | Fase 3 | MR-05 |
| Mecanismo de publicación desde el repositorio al registro | Fase 3 | MR-05 |
| Mecanismo de detección de desviación | Fase 3 | MR-05 |
| Procedimiento operativo de incorporación al catálogo | Fase 3 | MR-05 |
| Asignación del rol de gobierno dentro de la organización | Instanciación | MR-05 |
| Verificación de conformidad por ejecución | Despriorizada | ADR-041 |
| Retiro de activos con procedimiento de migración | Trabajo futuro | ADR-038 |
| Admisión de tipos de activo adicionales | Trabajo futuro | ADR-034 |
| Relación entre bounded contexts de proyectos distintos | Trabajo futuro | MR-02 |
| Extensión del catálogo con módulos de dominio alineados a BIAN | Trabajo futuro | ADR-006 |
| Patrones tácticos diferidos: factoría y especificación | Ampliación posterior | MR-02 |

## Decisiones pendientes

| Pendiente | Item | Estado |
| :---- | :---- | :---- |
| Módulo comprometido para el RF-09 | MR-04, MR-05 | **Resuelto el 2026-10-31 por la Fase 3.** El candidato que esta fase había identificado —el cliente de servicios corporativos, por T-05— no fue el elegido. El doc 1 de la Fase 3 comparó doce capacidades con cinco criterios y **ADR-097** eligió la **persistencia relacional**, construida como `@bsl/persistence`. El marco aportó lo que le correspondía: las condiciones de validez y la frontera entre lo empaquetado y lo generado. La fila de RF-09 de la trazabilidad de cierre del proyecto quedó corregida el 2026-11-04, porque daba la decisión por tomada aquí |
| Framework de aplicación destino | Fase 2 | Instanciación al inicio de la fase |
| Listado acotado de Service Domains con nombre exacto | MR-02 | **Resuelto el 2026-11-02.** El espacio queda delimitado a nueve Business Domains —`Party` salió por ADR-137— y los Service Domains del subconjunto están extraídos del portal en `Insumos/Teoria/BIAN/MR-00_BIAN_service-domains-extraidos.md`, con su control record y sus operaciones. Cuántos entran al espacio de selección es decisión de la Fase 2 y la toma ADR-138: una entrada existe cuando sirve a un propósito escrito, y hoy son cinco |
| Modelo de variabilidad y puntos de variación concretos | Fase 2 | Depende del diseño del mecanismo |

## Estado del marco

| Item | Documento | Estado |
| :---- | :---- | :---- |
| MR-01 | Encuadre como línea de producto de software | Cerrado |
| MR-02 | Fundamentos adoptados | Cerrado |
| MR-03 | Organización del código del proyecto generado | Cerrado |
| MR-04 | Puertos y contratos de integración | Cerrado |
| MR-05 | Gobierno de los core assets | Cerrado |

El mecanismo de evolución que pide ADR-027 está en MR-01 §7. El walkthrough de los veintidós
requerimientos y la matriz de cada decisión hacia su origen, que pide ADR-018, se hacen al cerrar el
proyecto en su documento de trazabilidad, porque la cobertura solo es medible contra lo construido.
