# Plantillas y contratos de la línea

Fija qué puede ser una plantilla de la línea —el manifiesto con que se describe a sí misma, la frontera entre lo que puede declarar como dato y lo que no, y el contrato de forma del producto que un módulo necesita para saber si cabe— y construye los dos primeros activos: el artefacto de contratos, que declara los puertos técnicos, y la plantilla de la que se deriva un producto. Es el primer código ejecutable del trabajo, y lo que verifica el marco antes de que exista la herramienta.

---

## 1. Una plantilla como activo del catálogo

Una plantilla de la línea es un activo del catálogo del mismo rango que un módulo, y se describe a sí misma. Siete condiciones la hacen válida, cada una con su forma concreta y quién la comprueba.

| Condición | Forma en el artefacto | Cómo se comprueba |
| :-- | :-- | :-- |
| Se describe a sí misma | El paquete trae `bsl-template.json` con su esquema al lado | `verify:manifest` del paquete, contra el esquema |
| Declara el contrato contra el que se construyó | `contract`, con paquete y versión exacta | El esquema lo exige; el `prepublishOnly` comprueba que el feed lo sirva |
| Declara qué forma de producto deriva | `productShape`, con identificador, versión entera, puntos de inserción y puertos | El esquema lo exige; `bsl templates show` lo imprime |
| Dice dónde viven sus archivos | `files.assetRoot` y `files.templates` | `verify:manifest`, que comprueba que cada archivo nombrado está donde dice |
| Declara de qué está hecho su producto | `catalog`, con sus tres clases de entrada | `verify:manifest`, con tres reglas que el esquema no puede expresar |
| Se llama como el catálogo la llama | El `id` del manifiesto es el de su entrada del catálogo | La herramienta, al derivar y al mostrar |
| Viaja completa en su paquete | El `files` del `package.json` lista el manifiesto, su esquema y la carpeta de plantillas | `npm pack --dry-run` |

**Por qué el manifiesto en el paquete y no en el catálogo.** Lo que la plantilla declara de sí misma cambia con ella, y ponerlo en el catálogo obligaría a cambiar dos repositorios de forma coordinada para publicar una versión. Una desincronización dejaría a la herramienta derivando con el catálogo de archivos de otra versión de la plantilla.

**Forma del paquete.** Toda plantilla vive bajo `packages/templates/`, una carpeta cada una.

```
packages/templates/<plantilla>/
  package.json                 files lista las tres piezas de abajo
  bsl-template.json            el manifiesto
  bsl-template.schema.json     su esquema
  templates/                   los archivos que se renderizan
  template/                    lo que el producto recibe tal cual, cuando la plantilla trae activo
  scripts/                     validación del manifiesto y verificación del activo
```

Dos cosas que esto hace posibles: una plantilla de otro equipo vive en el repositorio de ese equipo, como un módulo, y una versión de la plantilla no cuesta una versión de la herramienta. La dependencia queda en una sola dirección: la herramienta depende del contrato del manifiesto, y la plantilla de nada de la herramienta.

## 2. Secciones del manifiesto

| Sección | Qué declara |
| :-- | :-- |
| `schemaVersion`, `id`, `package`, `description` | Identidad. El `id` es el del catálogo, y es también el nombre por el que se la nombra al derivar |
| `contract` | Paquete y versión exacta del contrato contra el que se construyó |
| `productShape` | La forma del producto que deriva: §4 |
| `files` | `assetRoot` y `templates`, relativos al paquete |
| `vocabulary` | Cómo se arma el scope con que se renderiza: `lists`, `groups`, `derived`, `picks` |
| `catalog` | De qué está hecho el producto, entrada por entrada |

**Las tres clases de entrada del catálogo** son las mismas tres clases de archivo que toda derivación distingue, y no hay archivo del producto que no salga de una de ellas.

| Clase | Campos | Qué hace |
| :-- | :-- | :-- |
| `copy` | `from`, `to`, `when` | Los bytes viajan sin leerse |
| `render` | `from`, `to`, `when`, `forEach`, `forItem`, `collapseBlankLines` | El contenido se rinde desde una plantilla. `forEach` escribe un archivo por ítem de una lista; `forItem` lo escribe una vez, para el ítem que un `pick` eligió. Los dos a la vez están prohibidos por el esquema |
| `json` | `from`, `to`, `when`, `set`, `unset` | Se lee un JSON del activo y se cambian campos concretos |

**Por qué la clase `json` y no una plantilla.** Las versiones de las dependencias son del activo: ahí se decidieron y ahí se actualizan. Si viajaran en una plantilla, cada subida de versión del activo exigiría tocar la plantilla y las dos listas divergirían en silencio. Cambiar campos concretos conserva una sola fuente.

**Las cuatro primitivas del vocabulario** resuelven lo que una plantilla no puede decir con marcadores sueltos: `lists` arma una lista con deduplicación y orden, `groups` la agrupa, `derived` compone un valor de otros y `picks` elige un ítem. Hay un hueco declarado: ninguna de las cuatro **filtra una lista en otra lista**, y el rodeo es agrupar y quedarse con un grupo. Queda como candidata a quinta primitiva.

## 3. La frontera: qué es expresable como dato

Esta es la parte que impide que el manifiesto se vuelva un lenguaje de programación en JSON, que es la forma conocida de llegar a lo que está prohibido para un módulo: código del activo corriendo dentro de la herramienta.

**Lo que una plantilla puede decidir, enumerado.** Tres construcciones del motor y dos tablas cerradas, y nada más.

```
{{nombre}}  {{nombre|transform}}
{{#when <expresión>}} … {{:else}} … {{/when}}
{{#each <lista>}} … {{/each}}        {{#each <lista> between="\n\n"}} … {{/each}}
```

| Tabla cerrada | Contenido |
| :-- | :-- |
| Transforms | `pascal` `camel` `kebab` `snake` `upperSnake` `words` `title` `plural` `lowerFirst` `compact` `tsLiteral` |
| Formas de la condición | Las del evaluador del modelo —identificador, `!`, `.length <op> n`, `.some(x => x.f)`, implicación— más igualdad y desigualdad contra un literal, igualdad entre dos nombres, `some` con igualdad e `includes` |

**La condición la lee el mismo evaluador que lee una restricción del modelo de variabilidad.** No hay `eval`, no hay forma de que una plantilla nombre una función, y no existe una segunda gramática. Un transform o una etiqueta que el motor no reconoce levantan un error de sintaxis de plantilla, que es un defecto del activo y aparece en la verificación del paquete que lo posee. Un marcador sin valor es un error y no se sustituye por vacío.

**La propiedad que esto garantiza** es más fuerte que «las plantillas no deciden nada», que era sostenible mientras hubo una sola: **todo lo que una plantilla puede decidir está enumerado arriba**. La vista previa del plan sigue mostrándolo entero, porque la evaluación ocurre al construir el plan y no al escribirlo.

**Lo que no es expresable, con su destino.** La morfología del idioma queda en la herramienta y se expone como el vocabulario de transforms; la cirugía sobre un JSON queda como la clase `json`; las huellas, el reloj, la inicialización del repositorio, la instalación de dependencias, el respaldo, las preguntas, el registro, el catálogo y los códigos de salida quedan en la herramienta, porque son el mecanismo y no el producto. Dos cosas se **eliminaron** en vez de expresarse: el formato por ancho de línea, que es formato y lo comprueba el `prettier --check` del propio producto, y el impresor de literales del documento OpenAPI, que pasó a ser texto en su plantilla.

**Lo que todavía no es dato, como punto de extensión.** Los nombres que el estándar impone sobre una operación —su término de acción, su ruta, su método, su evento— y el modelo de variabilidad, que sigue siendo de la herramienta. Mover los dos exige transforms encadenados en el motor.

## 4. El contrato de forma del producto

La compatibilidad de un módulo se decide contra el producto, y la plantilla que lo derivó puede no estar instalada, no estar publicada o no existir. Por eso la forma es un dato con nombre y versión, declarado en tres lugares que se comparan entre sí.

| Quién | Dónde | Qué dice |
| :-- | :-- | :-- |
| La plantilla | `productShape` de su manifiesto | Qué forma derivan sus productos |
| El producto | `shape` de su `project.json` | La misma forma, copiada al derivar |
| El módulo | `serves` de su `bsl-module.json` | A qué formas sirve |

Es la misma razón por la que el producto registra con qué versión del activo fue derivado (RF-10): lo que el producto es tiene que poder leerse del producto.

**La forma de la plantilla hexagonal: `nestjs-hexagonal@1`**, con ocho puntos de inserción.

| Punto | Archivo | Clase | Rol | Comentario |
| :-- | :-- | :-- | :-- | :-- |
| `bsl:module-imports` | `src/app.module.ts` | marca | `imports` | `//` |
| `bsl:modules` | `src/app.module.ts` | marca | `modules` | `//` |
| `bsl:module-config` | `src/config/config.schema.ts` | marca | `configuration` | `//` |
| `bsl:module-env` | `.env.example` | marca | `environment` | `#` |
| `bsl:repository-import` | `src/app.module.ts` | región | — | `//` |
| `bsl:repository-binding` | `src/app.module.ts` | región | — | `//` |
| `bsl:persistence` | `README.md` | región | — | `<!--` … `-->` |
| `bsl:telemetry` | `README.md` | región | — | `<!--` … `-->` |

**Marca y región son dos cosas.** Una **marca** es una línea de comentario después de la cual un módulo inserta una región propia, nombrada por él, de modo que dos módulos escriben en el mismo punto sin chocar. Una **región** es un par de marcas que la plantilla escribió alrededor de código suyo, que un módulo reemplaza completo. El **rol** lo declaran solo los cuatro puntos donde el mecanismo de composición escribe por su cuenta, porque es él quien decide qué va en cada uno.

**Los puertos de la forma.** `DATABASE_PORT`, ligado por la plantilla en `bsl:repository-binding`, y `TELEMETRY_PORT`, que la plantilla no liga porque el producto lo inyecta opcional. Los dos son reemplazables por un módulo.

**Los supuestos, declarados como hechos.** Lo que la forma supone del producto más allá de sus puntos de inserción: `npm-package-manifest`, `project-record-1.0`, `single-aggregate` y `zod-config-schema`. `bsl templates show` los imprime. No se comprueban: declararlos es lo que los saca de lo tácito, y comprobarlos exigiría inventar semántica que ninguna decisión tomó.

**Cómo un módulo decide si cabe.** La plantilla declara `productShape` y lo escribe en el registro del producto al derivarlo; el módulo declara `serves`; la composición compara **antes de producir un solo cambio** y rechaza nombrando las dos formas; y la actualización comprueba lo mismo. La comparación es por identificador y por versión entera, nunca por rango: una versión de forma se mueve cuando un punto se mueve o desaparece, que es exactamente cuando el cableado de un módulo deja de aterrizar donde esperaba. Ser indulgente ahí convertiría un rechazo que nombra la causa en un producto roto sin aviso.

**El supuesto que nadie comprobaba, comprobado por los dos lados.** «El producto derivó del activo que escribió esas marcas» es hoy dos rechazos de la composición: uno cuando un módulo reemplaza una región que la forma del producto no declara —el producto y el módulo no están de acuerdo sobre de qué está hecho el producto, y la herramienta no adivina cuál tiene razón— y otro cuando al producto le falta un punto que su propia forma declara.

**La cláusula de lectura, con su fecha y su fin.** Un registro sin `shape` se lee como `nestjs-hexagonal@1`, porque hasta la ronda que introdujo el almacén existía una sola forma y todo producto derivado la tenía. Es una cláusula fechada y no un valor por defecto: una segunda forma vuelve ambiguo el silencio, y por eso todo producto derivado desde entonces la escribe. Se retira en `1.0.0`. Lo que cuesta es que la forma implícita vive en el código de la herramienta **y** en el manifiesto de la plantilla, y una prueba las compara exigiendo igualdad: sin esa comparación la cláusula valdría lo que vale una esperanza.

## 5. El artefacto de contratos y las dos clases de puerto

Un módulo debe poder servir a más de un producto, y para eso alguien tiene que declarar el puerto. Si lo declarara el módulo, el producto acabaría dependiendo del módulo y la dirección de dependencia quedaría invertida en la práctica, aunque el documento afirmara lo contrario.

El **contract package** es ese artefacto neutral: un core asset que contiene las declaraciones de los puertos técnicos de la línea, del que dependen tanto los productos como los módulos, y del que ninguno de los dos depende del otro.

**La propiedad que lo hace viable.** La dependencia de un producto hacia él es exclusivamente de tipos, y una importación de tipos se elimina durante la compilación. El producto declara el contrato y en ejecución no existe referencia alguna a él. Sin esa propiedad el contract package sería una dependencia real y la solución perdería la mitad de su valor.

**Regla de contenido.** No contiene implementación ni código ejecutable: únicamente declaraciones de tipo. La regla no es «solo interfaces», porque una interfaz necesita tipos para sus parámetros y retornos; es la ausencia de todo lo que sobreviva a la compilación.

**Datos específicos del producto.** Cuando un puerto opera sobre datos que pertenecen al dominio de un producto, el puerto se declara genérico y el producto aporta el tipo. Así el contrato nunca conoce el dominio de ningún producto, y el producto nunca depende del módulo.

**Organización.** Se organiza en submódulos por capacidad y se versiona como una unidad, de modo que el producto declara una sola dependencia pero importa únicamente lo que nombra.

![][image2]

**Las dos clases de puerto.** El criterio que las separa es la firma, no el uso: *un puerto es de dominio si su firma menciona conceptos del dominio del producto, y técnico si su firma es expresable sin conocer el dominio.*

| Clase | Ejemplos | Quién lo declara | Dónde reside | Quién lo implementa |
| :---- | :---- | :---- | :---- | :---- |
| Puerto de dominio | Repositorio de un agregado, publicador de eventos de dominio | El producto | La capa de dominio del producto | El producto |
| Puerto técnico | Registro de eventos, configuración, cifrado, persistencia, telemetría | El contract package | El contract package | Un módulo del catálogo, o el propio producto |

**Consecuencia de propiedad.** Ningún módulo puede declarar ni apropiarse de un puerto de dominio. Un repositorio expresa intención de negocio en el lenguaje del producto y no puede provenir de un activo genérico sin arrastrar el dominio hacia el catálogo.

**Puertos técnicos nuevos.** Un módulo puede proponer uno en el contract package. La alternativa —exigir aprobación previa para cada puerto— convertiría el contrato en cuello de botella del catálogo.

**Los puertos de la versión inicial.** El criterio es el mínimo que permite que la plantilla opere y que el mecanismo de puertos quede ejercitado de extremo a extremo sin depender de ningún módulo. Anticipar puertos que nadie implementa produciría declaraciones sin realización.

| Puerto | Qué declara | Por qué entra |
| :---- | :---- | :---- |
| `LoggerPort` | Registro de eventos de aplicación | Todo producto lo usa desde su arranque |
| `ConfigPort<TConfig>` | Acceso a la configuración externalizada | RNF-05 exige que los valores residan fuera del código |
| `EventPublisherPort` | Publicación de eventos de dominio | Lo requiere el punto de variación `domainEvents` |
| `DatabasePort` | Conexión y ejecución de sentencias en una transacción | Lo implementa el módulo de persistencia |
| `TelemetryPort` | Entrega de entradas, spans y mediciones a un colector | Lo implementa el módulo de observabilidad |

*Archivo: `src/logging/logger.port.ts`*

```ts
export type LogContext = Record<string, unknown>;

export interface LoggerPort {
  debug(message: string, context?: LogContext): void;
  info(message: string, context?: LogContext): void;
  warn(message: string, context?: LogContext): void;
  error(message: string, error?: Error, context?: LogContext): void;
}

export const LOGGER_PORT = Symbol('LoggerPort');
```

Cada puerto exporta un símbolo junto a su interfaz. La interfaz desaparece al compilar, de modo que el contenedor de dependencias necesita un identificador que exista en ejecución; el símbolo cumple esa función sin obligar al dominio a conocer el mecanismo de inyección. `ConfigPort` es genérico en la forma de la configuración: así el contrato pertenece a la línea mientras la forma concreta —qué variables existen y de qué tipo son— pertenece a cada producto.

**Los dos últimos puertos no los satisface ningún adaptador de la plantilla**, y eso no contradice la regla del marco. Lo que el marco prohíbe es que un **producto válido** declare un puerto de **dominio** sin realización. Un puerto técnico cuya capacidad vive en el catálogo es otra cosa, y lo que la plantilla hace con él es declararlo ausente —el README del producto dice que nada sale del proceso— e inyectarlo **opcional** donde el producto reporta. Sin módulo, el producto responde igual. Lo que se evita así es peor que una declaración sin realización: un adaptador que no hace nada, ligado en el módulo global, que el módulo del catálogo tendría que reemplazar.

## 6. Las capas de la plantilla y el análisis estático

La plantilla de referencia de la línea materializa la estructura canónica del doc 1 y es un proyecto ejecutable: se clona, se instala y arranca por sí mismo. Esa condición es la que la convierte en verificación del marco. Si no arranca, no supera su propio análisis estático o exige editar algo a mano para funcionar, el problema está en el marco, y conviene descubrirlo cuando corregirlo es barato y no después de construir un generador alrededor de una estructura que no se sostiene.

| Capa | Qué contiene | De qué puede depender |
| :---- | :---- | :---- |
| `domain` | Entidades, objetos de valor, eventos y contratos de repositorio | De sí misma y del artefacto de contratos |
| `application` | Casos de uso que orquestan el dominio | De sí misma y del dominio |
| `infrastructure` | Adaptadores de entrada y de salida | De todas las anteriores y de la configuración |
| `config` | Lectura y validación de la configuración externalizada | De sí misma |

`app.module.ts`, `platform.module.ts` y `main.ts` son el punto de composición y quedan fuera de la restricción: son los únicos lugares donde se conocen todas las capas a la vez, porque su función es unirlas.

![][image1]

**Cómo se hace cumplir la regla de dependencia.** Con `eslint-plugin-boundaries`, dentro del analizador que el contexto ya usa. La configuración declara un tipo por capa, una regla por dirección permitida, la prohibición de que `domain` y `application` importen el framework, y `boundaries/no-unknown-files` en error: sin esa última, un archivo que no coincide con ningún patrón simplemente no se examina, y la regla se queda ciega sobre él en lugar de rechazarlo.

**Por qué dentro del analizador y no como paso aparte.** Una herramienta dedicada de análisis de dependencias es más expresiva y detecta ciclos, pero reporta al ejecutar un comando. La regla es útil cuando corrige en el momento en que se está por romper: quien escribe un import prohibido y ve el error en el editor aprende la regla; quien lo descubre al final, cuando ya construyó encima, la vive como un obstáculo. A ello se suma que el analizador ya está presente en todos los proyectos del contexto, de modo que la verificación opera desde el primer minuto sin configurar nada.

Los mensajes se redactan explícitamente y nombran la salida correcta, porque un error que dice qué hacer convierte al analizador en el canal por el que el marco se enseña, y uno que solo prohíbe, en un obstáculo que se busca cómo silenciar. La configuración lleva además las reglas de TSDoc que exige el estándar de documentación, de modo que el analizador verifica en una sola pasada la regla de capas y la documentación del código.

**Límite asumido.** No detecta ciclos de importación. Entre capas el ciclo es imposible por construcción, dado que las dependencias van en una sola dirección; el ciclo posible es entre archivos de una misma capa, que es un problema de diseño de quien escribe y no una violación del marco.

## 7. El agregado de referencia

Para ser un proyecto ejecutable la plantilla necesita un agregado. Se adopta **Party Reference Data Directory**, con el agregado `PartyReference` y dos operaciones, `initiate` y `retrieve`.

**Por qué un Service Domain real y no uno inventado.** El activo es también la demostración de que la cadena del estándar se materializa: el metadato de dominio registrado, el agregado derivado del control record, las operaciones convertidas en casos de uso y rutas. Un agregado inventado rompería esa demostración justo en el artefacto que debe darla, y obligaría a inventar operaciones que no corresponden a ningún término de acción.

**Por qué este en particular.** Es el más genérico del subconjunto declarado: gestiona datos de referencia de una parte, el caso más común en cualquier dominio bancario, y sus operaciones son las canónicas. No se parece a ningún producto comercial concreto, de modo que nadie lo tomará por una plantilla de depósitos o de préstamos.

**Qué ocurre con él al derivar.** Nada de este agregado llega al producto. El mecanismo no agrega contenido sobre el activo: sustituye el agregado de referencia por el que la entrada resuelta declara. Un producto derivado para `TermDeposit` contiene `term-deposit.entity.ts` y sus casos de uso, y no conserva rastro de `PartyReference`, ni carpetas vacías ni código sin uso.

**Cómo se declara que es referencia.** El campo `kind` del registro lo identifica como plantilla y no como producto, el README lo declara en su primera línea, y la tabla de §14 lo sitúa entre lo que se reescribe.

**Qué fija cada pieza del agregado.** La entidad no tiene constructor público: la fábrica estática `initiate` es el único camino de creación y valida los invariantes, de modo que una entidad inválida no puede existir. El puerto de repositorio vive en el dominio, no en el artefacto de contratos, y declara un método por operación. El caso de uso no lleva decoradores del framework, recibe sus puertos por constructor y toma la fuente de identificadores como dependencia con valor por defecto, que es lo que permite fijarla en las pruebas. El orden de efectos es crear, persistir, publicar el evento y registrar el log.

## 8. Configuración externalizada

RNF-05 exige que ningún valor susceptible de cambiar entre entornos resida en el código. Se resuelve con un punto central de configuración, leído y validado una sola vez al arrancar.

**Por qué un módulo propio y no el del framework.** Si el acceso a la configuración se hiciera con el mecanismo del framework, el código que la consulta dependería de él, y esa dependencia alcanzaría capas donde la regla la prohíbe. Un módulo propio mantiene la declaración de variables en un solo lugar conocido, al que se acude para agregar una nueva, y deja el framework confinado a la infraestructura.

**Qué aporta la validación.** Las variables de entorno llegan como texto y pueden faltar. Sin validación, un valor ausente produce un fallo tardío y oscuro en la primera operación que lo necesite; con validación, el proceso no arranca y nombra la variable y el problema. El esquema además convierte los tipos, de modo que el puerto devuelve el puerto de escucha como número sin que nadie lo transforme. `SERVICE_NAME` es la única variable sin valor propio declarado: toma por defecto el nombre del paquete, de modo que el producto derivado arranca sin que nadie complete un archivo de entorno.

El adaptador es la única pieza que conoce el módulo central; las capas de dominio y aplicación consultan el puerto y no saben de dónde proviene el valor. El archivo de ejemplo declara los nombres de las variables sin sus valores: es documentación ejecutable de qué hay que definir antes de arrancar.

## 9. Adaptadores iniciales

El marco establece que un producto válido no puede declarar un puerto de dominio sin adaptador, y la condición de llegada de la fase exige que el producto arranque sin edición previa. La plantilla provee entonces los adaptadores de todo puerto de dominio y de los puertos técnicos que no dependen de la organización.

| Puerto | Adaptador de la plantilla | Qué lo sustituye |
| :---- | :---- | :---- |
| `LoggerPort` | Registro por salida estándar, en la forma que el entorno pide | Nada: el asiento es del producto |
| `ConfigPort` | Lectura del entorno de ejecución | Nada: es infraestructura propia del producto |
| `EventPublisherPort` | Publicación en proceso | Un módulo de mensajería del catálogo |
| `DatabasePort` | Ninguno | El módulo de persistencia del catálogo |
| `TelemetryPort` | Ninguno | El módulo de observabilidad del catálogo |
| Repositorio del agregado | Implementación en memoria | El adaptador que el equipo escribe sobre `DatabasePort` |

**Por qué el logger no lo sustituye un módulo.** El asiento del log es del producto, y qué dice, qué se iza y qué se redacta está fijado acá. Un módulo que reemplazara el adaptador tendría que reimplementar el formato y la redacción, y el día que una de las dos cambiara, lo escrito en el stream y lo exportado dirían cosas distintas. El adaptador del producto se queda y entrega **la misma entrada que escribió** al puerto de telemetría.

**Por qué los adaptadores iniciales son del producto.** El reparto deja demostradas dos propiedades en fases distintas y sin solaparse. Esta fase demuestra que el mecanismo de puertos opera: hay una declaración, hay una realización y el dominio no conoce la segunda. La Fase 3 demuestra que un adaptador del catálogo sustituye al propio sin que la capa de dominio cambie, que es la propiedad que la arquitectura hexagonal promete.

**Condición del adaptador en memoria.** Es provisional por diseño y es la única pieza destinada a ser reemplazada. El archivo lo declara en su encabezado, nombrando qué lo sustituye. No es código de ejemplo que sobra, sino infraestructura que permite arrancar sin base de datos y que tiene un reemplazo previsto.

**Sondas de salud.** La plantilla incorpora un adaptador de entrada que no realiza ningún puerto: el controlador montado en `health`. Expone `GET /health/live`, que responde mientras el proceso vive, y `GET /health/ready`, que responde mientras el producto puede atender y devuelve `503` en cuanto una comprobación falla. Son dos preguntas distintas: confundirlas en una sola sonda convierte una dependencia caída en un ciclo de reinicios. Ninguna de las dos respuestas lleva variables de entorno, versiones de dependencias, direcciones internas ni trazas de error, porque una sonda es alcanzable antes de que se pida credencial alguna. La lista de comprobaciones de disponibilidad nace vacía —el producto persiste en memoria y no tiene dependencia externa que comprobar— y el lugar donde un módulo registra la suya queda marcado en el archivo.

**Una entrada de log por request, y todo fallo en un solo lugar.** El contexto de la request se abre en un **middleware** y no en el interceptor, porque un interceptor corre después de los guards: una request rechazada por el guard que agregue un módulo de autenticación quedaría rechazada antes de que nada la nombrara. Desde ahí, todo lo escrito mientras se atiende esa request lleva sus identificadores. El interceptor escribe el asiento cuando el servicio respondió y un filtro registrado para toda ruta lo escribe cuando falló, que es la pieza que sabe por qué; con eso hay una entrada por request y también la hay para una ruta que el servicio no tiene.

El filtro clasifica lo que se lance mientras se atiende: una excepción del framework levantada a propósito, un error que nadie esperaba, y un valor que no es ni un error. Al llamador le responde siempre la misma forma —estado, razón, una línea de mensaje, la lista de problemas cuando lo que está mal es el request, y el identificador de la request para que pueda citarlo—, y un `5xx` responde una línea genérica porque el mensaje de un error interno nombra tablas y hosts. Al log le escribe lo contrario: un `4xx` como `warn` con la lista de campos y reglas que la validación produjo, y un `5xx` como `error` con el nombre, el mensaje, el `code`, el stack y la cadena de causas. **El cuerpo no se registra, ni cuando falla**: lo que se registra es qué campo y qué regla, nunca el valor. Tampoco la dirección del llamador, que es dato personal. Las rutas bajo `health` se escriben en `debug`, de modo que al nivel con que corre un servicio desplegado no se ve ninguna.

**Qué dice cada asiento.** De qué despliegue viene —`service`, `serviceVersion`, `environment`, `host`, `pid` y el número de severidad del modelo de datos de logs de OpenTelemetry, que permite ordenar severidades sin conocer las palabras de esta línea—. Lo que un operador consulta se iza al nivel superior, en un conjunto cerrado: el nombre del evento, el `scope`, los identificadores de request y de traza, y después del mensaje el método, la ruta, el estado, la duración y el agente del llamador, más el error con su `code` y su cadena de causas. Lo que un caso de uso adjunta se queda en `context`, donde no puede chocar con un campo de la línea: un tablero nombra `route` y no `context.route`.

**Un asiento nunca lleva un secreto.** `LogContext` es abierto por diseño, así que nada impedía que un caso de uso adjuntara un token o el documento de una persona. Lo que un llamador adjunta pasa por una redacción por nombre de clave y queda acotado en profundidad, en largo de texto y en cantidad de elementos. La clave no alcanza para distinguir dato de negocio —el nombre de una persona llega como `partyName` y el de un servicio como `serviceName`—, así que de no adjuntarlo responde quien escribe la entrada.

**Dos formas del asiento, una por entorno.** `LOG_FORMAT` decide la forma: `json`, una línea por evento, es la que lee un colector; `pretty` alinea hora, nivel, `scope` y mensaje en columnas para quien desarrolla; `auto`, el valor por defecto, resuelve a `pretty` solo mientras el entorno sea de desarrollo y la salida sea un terminal, y a `json` en todo lo demás. La forma vive en dos funciones puras y el adaptador la resuelve una sola vez al construirse.

**El framework también escribe por el puerto.** NestJS registra por su cuenta lo que carga y las rutas que monta, con su propio formato. Dejarlo así deja dos idiomas en el mismo flujo de salida, y el activo termina predicando un puerto que no usa en su propio arranque. Un adaptador implementa la interfaz de registro del framework y delega en el puerto, con el nombre de la parte que lo escribió como `scope`.

**La traza del estándar.** El producto lee `traceparent` del estándar W3C Trace Context cuando llega, abre la traza cuando no, siempre acuña su propio span y devuelve un `traceparent` que lo nombra. Es lo que permite leer el log de este servicio junto al del servicio que lo llamó. El span de un `4xx` no declara que el servicio falló, porque una request que el llamador mandó mal no es un fallo de quien la respondió, y contarla como tal esconde las que sí lo son.

**El ciclo de vida del proceso.** El servicio dice qué es al arrancar, dice que le pidieron parar y dice por qué se muere ante una excepción o un rechazo que nadie manejó. Sin esa última entrada, una caída y un reinicio ordenado por la plataforma se leen igual en un stream.

**Límite asumido.** No hay métricas ni exportación de señales. Exportar la traza a la plataforma de observabilidad de la organización, el muestreo y la propagación saliente son capacidades de un módulo transversal; acá está el mínimo que no puede faltar el primer día. Lo que el producto hace es reportar en los tres lugares donde produce telemetría —el adaptador del logger entrega cada entrada que escribió, el interceptor el span y la duración de la request que respondió, y el filtro los de la que falló—, con el puerto inyectado opcional. Lo que `LOG_LEVEL` descartó tampoco se exporta: el producto no exporta lo que no está dispuesto a escribir.

## 10. Punto de composición

El punto de composición es el único lugar que conoce todas las capas a la vez. Son dos archivos, no uno: `platform.module.ts` asocia los puertos técnicos de la línea, que son los mismos en todo producto, y `app.module.ts` asocia lo que este producto decidió sobre su propio dominio y registra los módulos que se incorporen.

**Por qué fábricas y no proveedores de clase.** Un caso de uso no puede llevar anotaciones del framework: la capa de aplicación tiene prohibido depender de él y el propio analizador haría fallar esa anotación. El punto de composición los construye con una fábrica, pasando los puertos ya resueltos en el orden declarado. Los adaptadores, que son infraestructura, sí se asocian por clase.

**El módulo global.** `platform.module.ts` provee y exporta los puertos técnicos y es global, porque sin eso un módulo del catálogo no alcanza el puerto de configuración ni el de registro: el contenedor del framework resuelve dentro del módulo que pide.

**El arranque informa dónde escucha, y retiene lo que se escribió antes.** `main.ts` obtiene el puerto de registro del contenedor y, una vez que el servidor escucha, escribe la dirección en la que responde, con el entorno y la ruta de la sonda de vida como contexto. Se escribe por el puerto y no por la salida estándar: el activo no puede exigir puertos a los productos y saltárselos en su propio arranque. La aplicación se crea reteniendo las entradas que el framework escribe antes de que el contenedor exista, y se le entrega el adaptador en cuanto existe, momento en que vuelca todo lo retenido por el puerto.

**El interceptor y el filtro se registran acá**, como proveedores de ámbito de aplicación y no en la lista de controladores: son adaptadores que envuelven a todos. Registrarlos acá es lo que permite que la inyección les entregue el puerto de registro, igual que a cualquier otro adaptador del producto.

**Los puntos de inserción existen desde la derivación.** Los ocho puntos de §4 viajan en el producto desde su primer commit, porque un punto de inserción agregado después obligaría a modificar todos los productos ya derivados.

## 11. Registro de versiones del producto

RF-10 exige que el producto declare qué activos incorpora y en qué versión. El archivo reside en la raíz, la plantilla lo lleva como parte de su estructura y el mecanismo de derivación lo rellena. Se define acá, y no en el documento de la herramienta, porque es contenido del producto y no del mecanismo. Su formato se fija completo desde el principio, incluidas las secciones que la Fase 3 utiliza: un cambio posterior de formato invalidaría los productos ya derivados.

*Archivo: `project.json` del activo de la plantilla*

```json
{
  "schemaVersion": "1.0",
  "kind": "template",
  "project": {
    "name": "@bsl/nestjs-hexagonal-api",
    "description": "Reference product of the hexagonal template of the line. The aggregate it contains is a reference.",
    "owner": "",
    "author": ""
  },
  "domain": {
    "businessArea": "Sales and Service",
    "businessDomain": "Customer Management",
    "serviceDomain": "Party Reference Data Directory",
    "controlRecord": "Party Reference Data Directory Entry",
    "declaredOutsideCatalog": false
  },
  "assets": [],
  "modules": []
}
```

El registro de un producto derivado lleva los mismos campos con `kind: "product"`, y además los cuatro
que solo tienen sentido después de derivar: el agregado, la forma, la entrada con que se derivó y los
activos que incorporó con su versión.

| Campo | Para qué existe |
| :---- | :---- |
| `kind` | Distingue la plantilla del producto; impide tomar el activo por un producto |
| `domain` | Metadato de dominio exigido por el marco |
| `aggregate` | Nombre del agregado raíz, que es el vocabulario del producto y puede diferir del que la capacidad sugiere |
| `shape` | La forma del producto, copiada del manifiesto de la plantilla: §4 |
| `derivation` | Con qué se derivó: operaciones elegidas y banderas de eventos y de pruebas de ejemplo |
| `assets` | Qué activos y versiones incorporó el producto y cuándo |
| `modules` | Cada módulo incorporado, su versión y su cableado. Lo escribe la Fase 3 |

El formato es **aditivo** y `schemaVersion` no sube, por la razón que su propia definición anticipaba. Lo que cambió es cómo se compara esa versión: **por versión mayor y no por igualdad exacta**, en los tres lectores que la hacen —el registro del producto, el manifiesto de un módulo y el manifiesto de una plantilla—. Una mayor distinta significa que el archivo dice algo distinto; una menor posterior significa que dice más, y más se lee. El arreglo `modules` se declara vacío desde el principio: su presencia es lo que permitió que la Fase 3 escribiera en él sin cambiar el formato.

## 12. Documentación OpenAPI del producto

RF-04 pide que el proyecto generado produzca su documentación de API bajo el estándar OpenAPI de forma automática, disponible sin configuración adicional y reflejando los endpoints del proyecto. Se resuelve como **pieza de la plantilla, generada al derivar**, y no como módulo del catálogo.

| Opción | Qué exigía | Veredicto |
| :-- | :-- | :-- |
| Módulo del catálogo | Ampliar la excepción del marco a una segunda capacidad, y que un activo genérico conociera las rutas y los tipos expuestos de cada producto | Descartada: fuerza la regla que mantiene el desacoplamiento, y acopla un activo del catálogo al dominio de cada producto |
| Pieza de la plantilla, generada al derivar | Que la derivación escriba el documento con las operaciones que el producto seleccionó | **Elegida** |
| Herramienta externa que lee el código del producto | Un paso más que alguien tiene que ejecutar, contra el criterio de aceptación | Descartada |

Un documento de API es lo contrario de un adaptador de salida: describe la superficie de entrada del producto, que es su contrato con terceros, y para construirlo hay que conocer las rutas, los tipos expuestos de entrada y los de salida. Un módulo no aporta adaptadores de entrada. La consecuencia es que la documentación no depende de incorporar nada —un producto la trae desde su primer commit— y que el catálogo no gana una entrada acoplada a la forma de cada producto.

**De dónde sale el documento.** El riesgo de toda documentación de API es que describa algo distinto de lo que el servicio hace, y acá se ataca por el origen: el documento se arma con los mismos esquemas de validación que el servicio usa para aceptar y devolver datos.

| Parte del documento | De dónde sale | Qué garantiza |
| :-- | :-- | :-- |
| Esquema del cuerpo de una operación | El esquema del tipo expuesto de entrada, convertido a JSON Schema en ejecución | Si el servicio rechaza un campo, el documento no lo ofrece |
| Esquema de la respuesta | El esquema del tipo expuesto de salida | Un campo agregado a la respuesta aparece en el documento sin escribirlo dos veces |
| Rutas, métodos y códigos de estado | La derivación, con las mismas operaciones que escribieron el controlador | El documento y el controlador salen de la misma selección |
| Título y versión | La configuración del producto | Dos despliegues del mismo producto se distinguen en su documento |
| Sondas de estado | Fijas: todo producto de la línea las responde | Quien lee el documento sabe cómo comprobar el servicio |

**Por qué el tipo expuesto de salida se declara como esquema y no como tipo.** Un tipo de TypeScript no existe en ejecución, así que para documentar la respuesta habría que escribirla por segunda vez a mano. El esquema sirve para las dos cosas y el tipo se infiere de él, de modo que la forma de la respuesta tiene un solo dueño.

**Códigos de estado que el documento declara**, derivados del término de acción igual que el controlador: `Initiate` responde `201` y `400`; `Update`, `200`, `400` y `404`; `Retrieve`, `200` y `404`; `Execute` y `Control`, `200` y `404`. Las operaciones de behavior qualifier anidan bajo la instancia sobre la que actúan y el documento declara sus dos parámetros de ruta; una que inicia no nombra el segundo porque lo crea, y ninguna recibe cuerpo, así que ninguna declara `400`.

**Lo que el documento lleva del estándar.** El `operationId` del término de acción —`Initiate`, `ExecuteInterest`— y el grupo del nivel sobre el que actúa la operación, `CR - <control record>` o `BQ - <qualifier>`. Es lo que permite leer el documento del producto contra el publicado operación por operación, que es donde vive la trazabilidad con el estándar. El `summary` sigue siendo el de la línea, porque el del documento publicado trae un código de nivel de dos letras que no aporta a quien lee el del producto.

**La API como página.** El producto sirve además `GET /docs`, que renderiza con el visor de OpenAPI el mismo documento que `/openapi.json` ya sirve, **cargado de la copia instalada con el producto y nunca de internet**. La dependencia es de desarrollo, así que lo que un servicio desplegado carga no cambia y la auditoría de dependencias de producción corre sin ella. `API_DOCS` decide si la ruta existe, con `auto` por defecto: prendida salvo en producción, donde responde `404` y la superficie es la de antes. Cuando responde, el asiento de arranque nombra su dirección al lado de las sondas.

| Pieza | Clase | Qué hace |
| :-- | :-- | :-- |
| `openapi.controller.ts` | Copiada, igual en todo producto | Responde `GET /openapi.json` leyendo el nombre y la versión por el puerto de configuración |
| `api-docs.controller.ts` | Copiada | Responde `GET /docs` con el visor, en dos rutas explícitas |
| `openapi.ts` | Rendida por producto | El documento: rutas literales y esquemas convertidos en ejecución |
| `SERVICE_VERSION`, `API_DOCS` | Copiadas al esquema de configuración | Versión publicada en el documento, y existencia de la página |

Las rutas se escriben como literal al derivar y los esquemas se convierten en ejecución. El reparto responde a qué puede cambiar: las rutas de un producto las fija su selección de operaciones, y los esquemas los edita el equipo mientras desarrolla. El documento generado queda fuera del formateador del repositorio, porque su estilo lo fija quien lo escribe y dejar que el formateador lo reescriba crearía una diferencia permanente entre el activo y lo que la plantilla produce.

**Qué queda fuera, con su razón.** Decoradores de documentación en el controlador, porque son una segunda declaración de lo que el esquema de validación ya dice y dos fuentes divergen. Documentación de los eventos de dominio, porque OpenAPI describe una API HTTP y ningún requerimiento pide otro estándar. Y documentar las rutas que un módulo agregue, porque un módulo no aporta adaptadores de entrada.

**Límite declarado.** Una ruta agregada a mano al controlador no aparece en el documento hasta que se agrega al archivo del documento. Las dos piezas salen de la misma derivación, pero a partir de ahí son código del producto, y el README del producto lo dice con esas palabras para que la ausencia no se lea como un fallo.

## 13. Entorno de trabajo

El manifiesto del activo lleva nombre neutro y `private: true`, para que no se publique por error; el mecanismo de derivación lo reescribe con el nombre del producto, que sí es publicable por su equipo.

| Decisión | Contenido |
| :---- | :---- |
| Ejecutor de pruebas | Jest con `ts-jest`, el que el contexto ya utiliza, invocado con la bandera que habilita módulos ESM |
| Rango de Node | 24.9 o superior, que es lo que exige el ejecutor de pruebas para cargar los paquetes del framework |
| Versión del framework | La estable vigente de NestJS, y la línea permanece en ese major |
| Resto del toolchain | TypeScript, ESLint, `eslint-plugin-boundaries`, Zod |
| Formato | Prettier, con configuración incluida en el activo |

**Criterio de versión.** El activo es la dependencia común de toda la familia, de modo que la versión del framework alcanza a todos los productos a la vez. El criterio inicial era conservador —descartar una mayor publicada en los últimos meses— y mostró su costo cuando un aviso de severidad alta sobre una dependencia transitiva del framework, sin arreglo dentro de la mayor anterior, dejó a la línea sin poder publicar. Lo sustituyen dos reglas: se adopta la estable vigente y la línea permanece en ese major, resolviendo dentro de él los avisos que aparezcan. Lo que controla el riesgo no es la antigüedad de la versión, sino que el activo supere su verificación completa con ella.

**Módulos de CommonJS sobre paquetes ESM.** El framework publica sus paquetes como ESM y el producto sigue siendo CommonJS, que es lo que la propia versión declara soportado. De ahí dos ajustes visibles en el manifiesto y en el `tsconfig`: el script de pruebas invoca el binario de Jest con la bandera experimental, porque Jest sí la necesita, y la resolución de módulos pasa a la que admite esa importación y sigue emitiendo CommonJS. Lo que se descartó, y a qué costo, queda declarado: la alternativa era fijar el ejecutor de pruebas en una versión anterior, que no carga los paquetes del framework.

**Fuera del activo.** No incluye contenedorización ni definición de integración continua. Ambas son infraestructura de despliegue, excluida del alcance del marco, y su forma depende de la plataforma de cada equipo. Se declara explícitamente para que la ausencia no se lea como omisión.

**El comando `verify`** del producto reúne las tres comprobaciones que debe superar: análisis estático, pruebas y compilación.

## 14. Frontera entre lo empaquetado y lo generado

*Todo lo que es implementación va en el paquete. Todo lo que es cableado o configuración específica del producto se genera.*

| Elemento | Al derivar |
| :---- | :---- |
| Entorno de trabajo: analizador, pruebas, formato, TypeScript | Viaja tal cual |
| Módulo central de configuración y su esquema | Viaja tal cual |
| Adaptadores técnicos: registro, configuración, eventos | Viajan tal cual |
| Sondas de salud, registro de requests, filtro de errores y arranque | Viajan tal cual: no dependen del agregado |
| Controlador del documento OpenAPI y de la página | Viajan tal cual |
| Punto de composición | Se rinde: depende de las operaciones, del repositorio y de si hay eventos |
| Capa de dominio y de aplicación | Se reescriben según el agregado y las operaciones de la entrada resuelta |
| Adaptador de entrada, tipos expuestos y documento OpenAPI | Se reescriben según las operaciones |
| Adaptador de persistencia en memoria | Se reescribe con el nombre del agregado |
| `package.json`, `project.json`, `README.md` | Se reescriben con los valores de identidad |
| Archivo de ejemplo del entorno | Viaja tal cual |
| Configuración del registro de paquetes | Se reescribe con la dirección del feed |

**Empaquetado.** Los contenidos del activo viven bajo `template/` dentro del paquete publicado, separados del manifiesto. Los archivos cuyo nombre el gestor de paquetes altera al empacar se almacenan con el nombre neutralizado —`gitignore`, `env.example`, `npmrc`— y se restituyen durante la generación.

## 15. Qué verifica el paquete de una plantilla

| Comprobación | Qué atrapa |
| :-- | :-- |
| El manifiesto contra su esquema | Un campo mal escrito, un tipo equivocado, una entrada sin su origen o su destino |
| Cada archivo copiado o reescrito existe | Un archivo que el catálogo nombra y el paquete no trae |
| Cada plantilla renderizada existe | Lo mismo, del lado de la carpeta de plantillas |
| Ninguna plantilla del paquete queda sin usar | Una plantilla huérfana, que es el síntoma de un colapso de familia a medias |
| La verificación del activo aislado | Que el activo es un proyecto que se sostiene solo, instalado desde tarballs como lo recibe un producto |
| La prueba de igualdad con el activo | Que el activo es exactamente la salida de las plantillas, archivo por archivo |
| `prepublishOnly` | Que el rango de contrato que declara lo sirva el feed |
| `npm pack --dry-run` | Que el manifiesto y las plantillas viajen en el tarball. Está acá porque falló: el `files` no listaba el manifiesto, el tarball salía sin él, y ninguna prueba lo habría encontrado porque todas corren contra el directorio del repositorio |

**La prueba de igualdad y lo que cuesta.** La plantilla hexagonal trae un producto de referencia, así que el agregado del activo y las plantillas describen el mismo código y pueden divergir sin que nadie lo note. El mecanismo que lo impide es rendir las plantillas con la entrada de `Party Reference Data Directory` y comparar el resultado con los archivos del activo, byte a byte. El efecto es que el activo deja de ser un proyecto parecido a lo que la herramienta genera y pasa a ser **exactamente** lo que la herramienta genera, verificado en cada ejecución de `verify`. Desde entonces el activo no se edita a mano: se cambia la plantilla y el activo se ajusta a lo que ella produce.

**Y la forma recomendada es no traer producto de referencia.** La plantilla hexagonal trae el suyo por historia y lo paga con esa prueba. Una plantilla sin producto de referencia no tiene dos fuentes del mismo código y nada puede divergir: su verificación deriva un producto y lo deja juzgarse a sí mismo.

## 16. La evidencia de que el intérprete es genérico

Todo lo afirmado acá descansa en una proposición: que lo que queda en la herramienta es un mecanismo y no la descripción de un ejemplo. Con una sola plantilla esa proposición no es comprobable, porque un intérprete genérico y una función escrita para ese caso se comportan igual. La evidencia es de dos clases, y prueban cosas distintas.

**Una plantilla de otra familia, como fixture de prueba.** Un trabajo por lotes agendado, en Python, con comentarios `#`, forma `python-batch@3`, un puerto propio y un contrato que no es el de esta línea. Once pruebas derivan un producto de ella y recorren las cuatro primitivas del vocabulario, la condición, la repetición por lista, la repetición por grupo, el ítem elegido, la reescritura de un JSON del activo, los archivos copiados y la forma del producto escrita en su propio registro. Prueba que el intérprete no está escrito para esta familia.

**Una segunda plantilla publicada, de otro modelo de ejecución.** `@bsl/azure-functions-api` deriva un API HTTP de un Service Domain sobre Azure Functions, forma `azure-functions@1`, **sin contenedor de inyección, sin servidor propio y sin producto de referencia**. Prueba que el diseño no quedó atado al framework de la primera plantilla: entró sin que una línea de la herramienta cambiara. Y prueba que el contrato de forma funciona cuando toca rechazar, porque ningún módulo del catálogo sirve esa forma —los dos exportan un módulo de NestJS que un host de funciones no sabe registrar— y la composición los rechaza nombrando la causa.

**El hallazgo del contrato de forma.** Los puntos de inserción de la segunda plantilla son **cinco** en vez de ocho, y uno de los cuatro roles **no existe**: los settings de una function app viven en un archivo JSON estricto, y un marcador es una línea de comentario que ahí dejaría el archivo inválido. Una forma cuyo archivo de settings es JSON **no puede tener punto de entorno**, y el contrato lo expresa sin inventar nada: la forma declara los puntos que tiene, la resolución de un punto rechaza nombrando el rol que falta, y los supuestos lo dicen.

**Lo que ninguna de las dos prueba.** Que una plantilla de otro equipo pase la verificación de su propio paquete, y que se publique bien. Las dos son las comprobaciones de §15, que las dos plantillas de la línea pasan.

## 17. Qué queda fuera

| Queda fuera | Razón |
| :-- | :-- |
| El modelo de variabilidad por plantilla | Sigue siendo de la herramienta. Una plantilla puede referirse a él y no reemplazarlo |
| Los nombres del estándar BIAN como dato | Exige transforms encadenados en el motor |
| Retirar el pin de la plantilla | El pin de la herramienta sigue fijando el contrato y la plantilla. Quitarlo es lo que ya se midió y resolvió para el catálogo, y no se aplicó acá |
| La cláusula de lectura de un registro sin `shape` | Se retira en `1.0.0`, junto con las de `nest` y `serves` del manifiesto de un módulo |
| Un adaptador de entrada aportado por un módulo | La superficie externa del producto es contrato con terceros. La única excepción del marco son las sondas de estado, que ya están en la plantilla |

[image1]: <../Insumos/Diagramas/MG-02_fig1_capas_y_dependencias.svg>
[image2]: <../Insumos/Diagramas/MG-02_fig2_contract_package.svg>
