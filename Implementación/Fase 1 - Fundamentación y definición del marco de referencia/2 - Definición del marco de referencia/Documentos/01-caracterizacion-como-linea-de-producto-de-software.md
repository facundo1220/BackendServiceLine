# Caracterización como Línea de Producto de Software

Encuadra la solución como una línea de producto de software y declara sus cuatro elementos constitutivos: el alcance de la familia, su arquitectura común, el conjunto de activos y el procedimiento de derivación. Las tres brechas no se cierran eligiendo otra herramienta sino definiendo el enfoque que gobierna su uso.

## 1. Enfoque adoptado

Se opta por una línea de producto de software: un enfoque de ingeniería que declara un alcance, una arquitectura común, un conjunto de activos y un procedimiento de derivación.

Las soluciones del estudio comparativo son mecanismos de reutilización. Cada una atiende una preocupación concreta y la resuelve dentro de su ámbito: copiar y adaptar un producto existente, distribuir una capacidad ya construida, producir el punto de partida de un proyecto nuevo, o catalogar los activos y asignarles propiedad. Ninguna declara un alcance, una arquitectura común ni un procedimiento de derivación, porque no es su propósito.

Las tres brechas identificadas no se cierran eligiendo una herramienta distinta, sino definiendo el enfoque que gobierna su uso. El artefacto propuesto implementa este gobierno.

## 2. Elementos de una línea de producto

Una línea de producto de software es un conjunto de sistemas intensivos en software que comparten un conjunto común y gestionado de características, que satisfacen las necesidades de un segmento determinado y que se desarrollan a partir de un conjunto común de activos siguiendo un procedimiento establecido.

De la definición se desprenden cuatro elementos constitutivos.

| Elemento | Qué exige | Qué lo llena en este trabajo |
| :---- | :---- | :---- |
| Alcance declarado | Declaración explícita de qué productos pertenecen a la familia | La familia declarada en el punto 6 |
| Arquitectura común | Estructura compartida por todos los productos de la familia, que hace posible que un mismo activo sirva a varios | Domain-Driven Design y arquitectura hexagonal |
| Core assets | Activos reutilizables que incluyen arquitectura, contratos y modelos, no solo código | Plantilla base, módulos, contract package y catálogo |
| Mecanismo de derivación | Procedimiento que produce un producto a partir de los activos y de una selección de características | La herramienta de línea de comandos |

## 3. Por qué el enfoque aplica al problema

La práctica actual del contexto corresponde a lo que la literatura denomina clone-and-own: construir un producto nuevo copiando uno existente, sin conservar vínculo entre la copia y el origen. Es una estrategia de bajo costo inicial, ampliamente documentada en la industria, cuyo problema característico es que los productos se separan con el tiempo: al no existir un mecanismo que propague los cambios, cada copia evoluciona por su cuenta y la divergencia crece con el número de copias (Dubinsky et al., 2013).

Que el enfoque aplique depende de que los cuatro elementos que una línea de producto exige:

- Existe una familia, aunque no esté declarada: los productos del contexto comparten propósito y estructura, no son casos aislados entre sí.
- Existe una arquitectura común, aunque no esté codificada: T-02 registra la existencia de un patrón arquitectónico de la organización que el desarrollador debe dominar antes de ser productivo, hoy transmitido por imitación visual de otros proyectos en lugar de por un activo.
- Existe un núcleo común, aunque no esté gestionado como activo: T-09 registra un conjunto reconocido de funcionalidades transversales que se repite entre productos, hoy reutilizado por copia.
- Existe un mecanismo de derivación, aunque no esté formalizado: copiar un proyecto y ajustarlo es, en sí mismo, una forma de derivar un producto a partir de un origen común; carece de trazabilidad y de vínculo con ese origen, pero cumple la función.

El enfoque se adopta porque el problema tiene la forma que una línea de producto está diseñada para tratar, y porque los elementos que exige ya están presentes, aunque de forma informal.

## 4. Organización general de la línea

Los cuatro elementos del punto 2 describen qué debe existir, pero no cómo se articulan. Para eso se adopta el modelo de referencia de Apel, Batory, Kästner y Saake (2013), que cruza dos ejes: el espacio del problema frente al espacio de la solución, y la ingeniería de dominio frente a la ingeniería de aplicación.

![][image1]

| Cuadrante | Qué contiene |
| :---- | :---- |
| Análisis del dominio | Alcance de la familia, modelo de dominio de referencia y modelo de variabilidad |
| Implementación del dominio | Arquitectura de referencia, plantilla, módulos, contratos y catálogo |
| Análisis de requerimientos | Selección de características al generar o al componer |
| Derivación del producto | Ensamblaje y producción del proyecto |

Cinco flujos conectan los cuadrantes: el mapeo entre características y activos, el uso del mismo modelo de variabilidad para configurar un producto, el retorno de nuevos requerimientos hacia el dominio, el consumo de activos comunes en cada derivación, y la selección de características que determina qué se ensambla.

Los dos cuadrantes superiores son ingeniería de dominio y corresponden a las fases 1, 2 y 3. Los dos inferiores son ingeniería de aplicación y ocurren cada vez que un desarrollador usa la herramienta.

## 5. Alcance de la familia de productos

Servicios backend sobre Node.js y TypeScript, cada uno responsable de un único bounded context, que exponen al menos una API HTTP documentada bajo el estándar OpenAPI, consumen servicios corporativos y pueden publicar o consumir eventos.

Quedan fuera de la familia las aplicaciones frontend, las aplicaciones sin API HTTP expuesta —procesos batch, workers agendados—, los scripts de propósito único, las aplicaciones con más de un bounded context, y los servicios sobre lenguajes o ecosistemas distintos de los declarados.

La exposición de al menos una API HTTP es la condición mínima de pertenencia. Garantiza que todos los productos comparten la misma superficie de entrada, lo que **hace viable** una plantilla única sin obligarla, y da sentido a la documentación OpenAPI como capacidad transversal de la línea.

**Qué no es la exclusión.** No excluye un modelo de ejecución. Un producto sin servidor propio —una función con trigger HTTP— cumple la condición mínima y pertenece a la familia; lo que no pertenece es lo que no expone API. Cuántas plantillas tiene la línea, y sobre qué modelo de ejecución deriva cada una, es decisión del mecanismo de derivación y no del alcance de la familia: dos plantillas derivan dos clases de producto que cumplen las mismas condiciones de pertenencia, y lo que las distingue es de qué está hecho su producto, que es lo que cada manifiesto declara.

## 6. Desviaciones declaradas

El modelo de referencia presenta dos asunciones implícitas que el contexto no satisface. Se declaran como desviaciones en lugar de forzar el caso dentro de un esquema que no lo previó.

Productos autónomos. El modelo no contempla flujo de retorno desde el producto derivado. Aquí el proyecto se entrega a un equipo que conserva autonomía para modificarlo (RNF-02). La línea no gobierna el producto después de derivado: mantiene un vínculo que permite propagar cambios, pero no impone su aceptación.

Derivación por etapas. En el modelo la selección de características ocurre una sola vez y precede a la derivación. Aquí puede repetirse sobre un producto ya derivado (RF-06), lo que convierte la derivación en una actividad recurrente.

Ambas se originan en la misma condición: los productos pertenecen a equipos autónomos que trabajan en repositorios independientes.

## 7. Mecanismo de evolución del marco

Un marco definido antes de construir no puede ser inmutable: la construcción produce aprendizaje que el diseño inicial no anticipa. Sin un mecanismo declarado, todo cambio posterior se leería como defecto de esta fase. El marco se declara revisable y que el flujo de nuevos requerimientos del modelo de referencia adoptado es su mecanismo: al residir el marco en el cuadrante de análisis del dominio, ese flujo alcanza tanto al catálogo como al propio marco.

Todo cambio se clasifica en una de cuatro categorías, y la categoría determina qué exige.

| Categoría | Qué es | Qué exige |
| :---- | :---- | :---- |
| Refinamiento | Agrega detalle donde el marco dejó un espacio abierto | Nada. El marco ya lo difirió |
| Extensión | Agrega una regla nueva que no contradice ninguna existente | Se suma al documento correspondiente |
| Revisión | Contradice una regla existente | Se cambia la decisión y se registra el motivo con estado Revisada |
| Ruptura | Invalida un elemento constitutivo del encuadre | Obliga a revisar MR-01. Debe ser excepcional |

**Qué es estable por diseño.** Los elementos constitutivos y sus consecuencias directas: el encuadre de línea de producto, el alcance de la familia, la unidad de derivación y la dirección de dependencia. Si alguno cambia, no se está refinando el marco sino construyendo otro.

**Qué se espera que se mueva.** Convenciones y mecanismos: nomenclatura, agrupación interna del dominio, forma de los contratos y política concreta de versionado.

**Regla de registro.** Toda decisión tomada sin evidencia de implementación se marca como Aceptada (provisional) con su condición de revisión escrita, y toda revisión posterior registra qué la motivó. Es lo que convierte el mecanismo en algo comprobable y no en una licencia para cambiar de opinión sin dejar rastro.

**Dónde está cada regla del marco.** El marco son dos documentos: el encuadre, acá, y los fundamentos adoptados en el documento siguiente. Las reglas que gobiernan la forma concreta de lo que la línea produce viven en el documento de la fase que las construye y las verifica, porque una regla escrita en abstracto y vuelta a escribir en concreto son dos fuentes de la misma verdad.

| Regla del marco | Dónde vive |
| :---- | :---- |
| Estructura canónica del producto, reglas de dependencia y nomenclatura | Fase 2, doc 1 |
| Contract package, las dos clases de puerto y la frontera entre lo empaquetado y lo generado | Fase 2, doc 2, y Fase 3, doc 2 para lo que hace válido a un módulo |
| Tipos de activo, escala de adaptación, versionado, catálogo y gobernanza | Fase 2, doc 3 |

Un cambio sobre una de ellas se clasifica con la tabla de arriba y se aplica donde la regla vive. «Se cambia el documento correspondiente» es ese documento, no este.

**Cómo ha operado, de hecho.** La sección se escribió al cerrar el marco, cuando el mecanismo era una previsión. Con las Fases 2 y 3 cerradas se puede mostrar funcionando. Nueve cambios lo han ejercido:

| Qué cambió | Categoría | Dónde quedó |
| :---- | :---- | :---- |
| Las dos clases de puerto, la escala de adaptación y la definición de cambio incompatible se precisaron al construir | Revisión | Las tres decisiones originales quedaron revisadas, cada una con su motivo escrito |
| RF-04 quedaba sin cubrir y sin fase asignada al cerrar la Fase 2 | Extensión | Quedó excluido de esa fase y reasignado a la Fase 3, donde se construyó |
| Una decisión del marco atribuía su consecuencia a RNF-04 en lugar de RNF-06 | Revisión | Corregida con nota fechada; RNF-04 quedó fuera de su traza |
| El formato legible del log del producto, que se había diferido al módulo de observabilidad | Refinamiento | Se adelantó al activo base, dejando al módulo la correlación y las métricas |
| La jerarquía del estándar: el Business Domain de una capacidad estaba mal situado | Revisión | Corregido, fijando además que ante una discrepancia manda la fuente oficial |
| De dónde se transcribe el dato de una capacidad | Extensión | Del documento oficial del Service Domain, no de una vista del portal ni de una paráfrasis |
| El catálogo admite más de una plantilla, y una plantilla se describe a sí misma | Refinamiento, con una revisión adentro | El refinamiento es de MR-01 §5: la superficie común **hace viable** una plantilla única, que habilita y no obliga. La revisión alcanza a la decisión que sostenía la lectura contraria, que estaba diferida a la Fase 2 y se resolvió allí sin aceptarse. La tabla de tipos de activo gana la plantilla como cuarto tipo, en el doc 3 §1 de la Fase 2 |
| La forma del producto es un contrato declarado, con nombre y versión, que el producto lleva y el módulo compara | Extensión | Lo que antes se describía en prosa pasó a dato, y su supuesto implícito —«el producto derivó del activo base que escribió esas marcas»— pasó a comprobable |
| La familia excluía «las aplicaciones serverless», y queda excluyendo las aplicaciones **sin API HTTP expuesta** | Revisión de una exclusión, más un refinamiento de MR-01 §5 | Revisa un elemento constitutivo del encuadre y la exclusión del doc 06 del Bloque A. Lo construido es `@bsl/azure-functions-api`, una plantilla que deriva un producto sin servidor propio |

**Ninguno de los nueve es una Ruptura.** Los cuatro elementos constitutivos siguen en pie y el encuadre de MR-01 no se revisó. En el caso de la novena fila, que es el único que toca una exclusión del alcance, la condición mínima de pertenencia —exponer al menos una API HTTP documentada bajo OpenAPI— no se tocó, y el producto de la plantilla nueva la cumple entera. Lo revisado fue una exclusión cuya razón declarada era otra: «servidor propio». La exclusión que de verdad protege el encuadre, las aplicaciones sin API expuesta, sigue vigente, y es la que dejó fuera la tercera opción que esa ronda evaluó, un worker agendado.

**Dos de las nueve no las motivó la construcción.** La de la segunda plantilla y la de la exclusión de serverless corrigen estrechamientos que el proyecto se puso a sí mismo y que el anteproyecto nunca pidió: no habla de una sola plantilla ni excluye serverless. Las dos aparecieron en una auditoría del anteproyecto, no al construir. El mecanismo de este punto las clasificó bien; lo que no existía era un paso que comparara lo construido contra el compromiso original antes de evaluarlo, y eso es un hueco del método, no del marco.

[image1]: <../Insumos/Diagramas/MR-01_fig1_modelo_de_referencia.svg>
