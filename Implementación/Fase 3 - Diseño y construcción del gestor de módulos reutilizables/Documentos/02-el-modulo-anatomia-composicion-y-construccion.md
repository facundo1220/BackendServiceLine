# El módulo: anatomía, reglas de composición y construcción

Fija la forma de un módulo —el manifiesto con que se describe a sí mismo, los puntos del producto donde entra su cableado, la entrada que queda en el registro del producto y las reglas que la operación comprueba antes de tocar nada— y construye el primero: el puerto técnico en el contract package, el paquete publicable con su adaptador y la plantilla del adaptador de repositorio que el producto recibe.

---

Sin esa forma, la operación de composición solo puede escribirse de una manera: conociendo cada módulo por dentro. Entonces incorporar un módulo nuevo al catálogo obligaría a publicar una versión de la herramienta, que es exactamente la dependencia que el catálogo existe para evitar. La forma queda como dato, y la operación no conoce ningún módulo: lee el manifiesto.

El módulo se construye **antes** que la operación que lo incorpora, por la misma razón que la plantilla se construyó antes que la herramienta: si la forma no sirve para un módulo real, conviene descubrirlo donde el costo de cambiarla es un documento y no una operación ya escrita.

## 1. Qué es un módulo, en la forma del artefacto

Un módulo es un core asset que aporta la realización de una o más capacidades técnicas a un producto de la familia. Tres condiciones lo hacen válido, y cada una tiene su forma concreta y quién la comprueba.

| Condición | Forma en el artefacto | Cómo se comprueba |
| :-- | :-- | :-- |
| Implementa contrato | El paquete exporta un módulo del framework que registra al menos un adaptador de un puerto técnico declarado en el contract package | El manifiesto declara qué puertos provee; la operación verifica que el producto no tenga ya un adaptador de ese puerto |
| Declara versión de contrato | El manifiesto trae la versión **mayor** del contrato que implementa, y la entrada del catálogo repite el mismo número | La operación la compara con la versión mayor del contrato que el producto declara en su registro |
| No invade el dominio | El contract package es su única dependencia de la línea; no declara puertos propios ni nombra conceptos del dominio de ningún producto | El análisis estático del módulo lo comprueba en su propio repositorio, y la revisión de la entrada de catálogo al incorporarla |

**Un módulo no depende de otro módulo.** Si necesita una capacidad de otro, la declara como puerto en el contract package y el producto decide qué adaptador la satisface. La regla es del marco; su consecuencia operativa es que la operación de composición nunca resuelve un grafo: incorpora un módulo y solo uno.

**Ningún módulo puede declarar ni apropiarse de un puerto de dominio.** Un repositorio expresa intención de negocio en el lenguaje del producto y no puede provenir de un activo genérico sin arrastrar el dominio hacia el catálogo. Y **ningún módulo aporta adaptadores de entrada**: la superficie externa del producto es contrato con terceros, y la única excepción que el marco declara son las sondas de estado, que ya viajan en la plantilla.

## 2. Anatomía del paquete

Un módulo es un paquete publicado en el feed de la línea, con la forma del contract package: compila a su directorio de salida, publica solo lo necesario y se verifica solo.

```
packages/modules/<capacidad>/
  package.json              nombre, versión, peerDependencies y files
  bsl-module.json           manifiesto: qué provee y qué cableado necesita
  bsl-module.schema.json    su esquema, para la ayuda del editor y su propia prueba
  README.md                 qué capacidad aporta, qué configura y qué escribe el equipo
  src/
    index.ts                superficie pública: el módulo del framework y sus tipos
    <capacidad>.module.ts   módulo del framework con su método de registro
    adapters/               los adaptadores de los puertos que provee
  templates/                plantillas de cableado que la herramienta renderiza, cuando las hay
  test/                     pruebas del módulo, sin producto alrededor
```

| Campo obligatorio del manifiesto de paquete | Valor | Por qué |
| :-- | :-- | :-- |
| `name` | El espacio de nombres de la línea más el identificador del catálogo | Quien lee el nombre sabe de qué entrada se trata |
| `peerDependencies` | El contract package y el framework | El módulo no instala su propia copia: usa la del producto. Dos copias del contrato producen dos símbolos distintos y el producto no resuelve el adaptador |
| `files` | El compilado, el manifiesto y las plantillas | El manifiesto y las plantillas viajan al producto; el código fuente no |
| `engines.node` | El mismo piso que la plantilla | Un módulo que exija más que el producto lo rompe al instalarse |

**Un módulo puede no traer plantillas**, y uno de los dos construidos no las trae: no todo módulo genera un archivo en el producto.

## 3. El manifiesto del módulo

Es la pieza que hace genérica a la operación. Un módulo declara acá qué provee y qué cableado necesita, y la herramienta traduce esa declaración a cambios sobre el producto sin saber qué es la persistencia.

*Archivo: `bsl-module.json`*

```json
{
  "$schema": "./bsl-module.schema.json",
  "schemaVersion": "1.1",
  "id": "persistence",
  "package": "@bsl/persistence",
  "contractVersion": 0,
  "provides": ["DATABASE_PORT"],
  "serves": [{ "shape": "nestjs-hexagonal", "version": 1 }],
  "composition": {
    "import": "import { PersistenceModule } from '@bsl/persistence';",
    "register": "PersistenceModule.register(),"
  },
  "configuration": [
    {
      "name": "DATABASE_FILE",
      "schema": "z.string().min(1).default('./data/store.db')",
      "example": "./data/store.db",
      "comment": "File the relational store writes to. A relative path resolves from the working directory of the service."
    }
  ],
  "scaffolds": [
    {
      "template": "templates/sql-repository.ts.tpl",
      "target": "src/infrastructure/persistence/sql-{{aggregateKebab}}.repository.ts",
      "describe": "Repository adapter of the aggregate, written on the database port"
    }
  ],
  "bindings": [
    {
      "region": "bsl:repository-binding",
      "path": "src/app.module.ts",
      "replace": "{ provide: {{aggregateUpperSnake}}_REPOSITORY, useClass: Sql{{aggregatePascal}}Repository },"
    }
  ]
}
```

| Nivel | Campos obligatorios |
| :---- | :---- |
| Raíz | `schemaVersion`, `id`, `package`, `contractVersion`, `provides`, `serves`, `composition` |
| Una forma servida | `shape`, `version` |
| `composition` | `import`, `register` |
| Una variable de configuración | `name`, `schema`, `example`, `comment` |
| Un scaffold | `template`, `target`, `describe` |
| Un cableado | `region`, `path`, `replace` |

Un manifiesto que no las cumpla falla al verificar el paquete del módulo, no al incorporarlo a un producto.

**Dónde vive el esquema, y quién decide.** El esquema viaja junto al manifiesto, dentro del paquete, para que el editor ayude y valide mientras se escribe, y la prueba del propio módulo lo valida contra él. En ejecución, quien decide si la herramienta compone es la comprobación que la herramienta hace en código, campo por campo, con mensajes que nombran lo que falta y dan un ejemplo. Un esquema responde «no válido»; quien escribe un módulo necesita saber qué campo y cómo.

**Por qué el manifiesto viaja dentro del paquete y no en el catálogo.** El catálogo gobierna qué activos ofrece la línea; el cableado es parte del activo y cambia con él. Si viviera en el catálogo, incorporar una versión nueva de un módulo exigiría cambiar dos repositorios coordinadamente, y una desincronización dejaría a la herramienta aplicando el cableado de otra versión.

**Lo que el manifiesto no admite.** No hay condicionales, bucles ni expresiones evaluables. Las únicas sustituciones posibles son los nombres del producto que §5 enumera. Un manifiesto capaz de ejecutar lógica sería código del módulo corriendo dentro de la herramienta, y la herramienta dejaría de poder prever qué va a cambiar.

**Dos cláusulas de lectura, con su fecha y su fin.** El nombre anterior de la sección de composición se sigue leyendo como alias de la actual, y un manifiesto que no declara a qué formas sirve se lee como si sirviera a la forma hexagonal, porque cuando los dos módulos se publicaron existía una sola. Las dos se retiran en `1.0.0`, y son lo que hizo que el orden de publicación de esa ronda no tuviera ninguna restricción nueva: la herramienta nueva lee los módulos viejos, y los módulos nuevos entran en los productos viejos por la cláusula gemela del registro del producto.

## 4. Frontera entre lo empaquetado y lo generado

*Todo lo que es implementación va en el paquete. Todo lo que es cableado o configuración específica del producto se genera.*

| Pieza | Dónde vive | Por qué |
| :-- | :-- | :-- |
| Adaptadores del puerto técnico | Paquete | Es implementación. Actualizarla no debe tocar el producto |
| El módulo del framework y su método de registro | Paquete | Es parte de la implementación: decide cómo se construyen sus proveedores |
| Línea que registra el módulo en el punto de composición | Generado en el producto | Es cableado: nombra al módulo dentro del árbol del producto |
| Entrada del esquema de configuración y variable de entorno | Generado en el producto | La configuración es del producto. El módulo declara qué necesita, no dónde se guarda |
| Adaptador del repositorio del agregado | Generado en el producto, desde una plantilla del módulo | Es realización de un puerto de dominio, que es del producto. El módulo aporta la plantilla, nunca una clase base que el producto extienda |
| Dependencia del paquete en el manifiesto del producto | Generado en el producto | Es la declaración de consumo, y debe quedar bajo control de versiones del producto |
| Entrada en el registro del producto | Generado en el producto | Es la memoria de lo incorporado |

![][image1]

**Por qué el módulo no aporta una clase base.** La herencia entre un activo del catálogo y el código del producto crea un acoplamiento que ninguna de las dos partes controla por completo. Una plantilla renderizada produce código que desde ese momento es del equipo: puede editarlo sin pedir permiso, y la herramienta lo sabe porque guarda su huella.

## 5. Los puntos de inserción del producto

Un producto derivado trae marcas en los archivos que el cableado toca, escritas por la derivación, así que todo producto las tiene desde su primer commit. Son los ocho que la forma del producto declara, y el contrato de forma del doc 2 §4 de la Fase 2 los enumera con su clase, su rol y su estilo de comentario.

De esos ocho, **solo el de registrar un módulo existía al cerrar la Fase 2**. Los otros siete se agregaron a las plantillas y, por tanto, al activo, que es la salida de esas plantillas.

**Por qué el import es una región y no una inserción.** Reemplazar la ligadura del repositorio deja sin uso el import del adaptador anterior, y el producto compuesto dejaría de pasar su propio análisis estático. Un módulo no inserta imports sueltos para sus reemplazos: reemplaza la región que los contiene.

**Por qué una región delimitada y no una sustitución por texto.** Cambiar la ligadura del repositorio es reemplazar una línea que ya existe. Buscarla por su contenido obligaría a la herramienta a adivinar sobre código que el equipo pudo haber tocado. Una región con marcas de apertura y cierre declara qué parte del archivo es cableado generado: lo de adentro es de la herramienta, lo de afuera es del equipo, y la frontera está escrita en el archivo.

**Sustituciones admitidas dentro del manifiesto**, las mismas que la derivación ya resuelve, tomadas del registro del producto: el nombre del agregado en sus seis formas —PascalCase, kebab, camel, mayúsculas con guión bajo para un token, minúsculas con guión bajo para un nombre de tabla, y separado en palabras para la prosa de la documentación— y el nombre del producto.

## 6. Las nueve reglas que la operación comprueba

Se comprueban **antes de producir un solo cambio**, así que un rechazo deja el producto exactamente como estaba. Ninguna se comprueba a mitad de la escritura.

| # | Regla | Origen | Qué hace si no se cumple |
| :-- | :-- | :-- | :-- |
| 1 | El módulo sirve a la forma del producto | El contrato de forma | Rechaza nombrando las dos formas. Va primero porque es la más general: si el módulo no cabe en esta clase de producto, las demás responden preguntas que no vienen al caso |
| 2 | El destino es un producto derivado: existe y su registro lo declara producto | Esta fase | Rechaza nombrando el archivo que buscó |
| 3 | El activo pedido está en el catálogo y es de tipo módulo | RF-14 | Rechaza y lista los módulos que el catálogo tiene |
| 4 | El activo está activo | El estado de su entrada | Rechaza diciendo en qué estado está |
| 5 | El módulo no está ya incorporado | RF-06 | Rechaza diciendo qué versión tiene el producto y cuál es la del catálogo, y nombra la operación de actualización |
| 6 | Ningún puerto que el módulo provee tiene ya un adaptador de otro módulo | Un adaptador por puerto | Rechaza nombrando el puerto y el módulo que lo provee hoy |
| 7 | La versión de contrato del módulo coincide con la versión mayor que el producto declara | El versionado del marco | Rechaza nombrando las dos versiones y qué habría que actualizar primero |
| 8 | Están los puntos de inserción que el cableado necesita, **y los declara la forma del producto** | La forma del producto | Rechaza nombrando la marca y el archivo. Y rechaza también el caso inverso: un módulo que reemplaza una región que la forma del producto no declara, donde el producto y el módulo no están de acuerdo sobre de qué está hecho el producto y la herramienta no adivina cuál tiene razón |
| 9 | Ningún archivo que el módulo genera existe ya en el producto | RF-07 | Rechaza nombrando el archivo. Lo que el equipo escribió no se pisa |

Hay una condición más, del producto y no del módulo: su registro tiene que declarar el agregado, porque de ahí salen los nombres del cableado. Un producto derivado antes de que el registro lo guardara se rechaza diciéndolo.

**Las reglas 1, 6 y 7 las comprueba también la actualización**, que no repetía ninguna: un cambio de versión podía mover un módulo a una versión construida contra otra mayor del contrato, o que cambió de forma, sin que nadie lo mirara.

**Por qué rechazar en lugar de arreglar.** Cada regla describe un producto que la herramienta no sabe componer sin suponer algo sobre código que no escribió. Suponer en código ajeno es el modo más caro de equivocarse: el daño aparece después, en un producto que ya nadie relaciona con el comando que lo tocó.

## 7. Qué queda registrado en el producto

El registro del producto reserva su arreglo de módulos desde la Fase 2, con el formato fijado. Esta es la forma de una entrada.

*Archivo: `project.json` de un producto que incorporó el módulo, fragmento*

```json
{
  "modules": [
    {
      "id": "persistence",
      "name": "@bsl/persistence",
      "version": "0.1.0",
      "contractVersion": 0,
      "provides": ["DATABASE_PORT"],
      "incorporatedAt": "2026-10-31T18:20:14.000Z",
      "wiring": {
        "edits": [{ "path": "src/app.module.ts", "marker": "bsl:module-imports", "region": "bsl:module:persistence:module-imports" }],
        "regions": [{ "path": "src/app.module.ts", "region": "bsl:repository-binding" }],
        "files": [{ "path": "src/infrastructure/persistence/sql-party-reference.repository.ts", "digest": "sha256:4f1c0d8b…" }],
        "configuration": ["DATABASE_FILE"]
      }
    }
  ]
}
```

| Campo | Para qué sirve después |
| :-- | :-- |
| `version` y `contractVersion` | La consulta informa qué hay incorporado y la comparación con el catálogo detecta lo desactualizado (RF-08, RF-12) |
| `provides` | Permite comprobar la regla del adaptador único en la siguiente incorporación sin volver a resolver el módulo que ya está |
| `incorporatedAt` | Desde cuándo el producto tiene la capacidad. No participa de ninguna comparación |
| `wiring.edits` y `wiring.regions` | La actualización y la remoción saben dónde quedó el cableado, en lugar de volver a buscarlo |
| `wiring.files` con su huella | La actualización compara la huella antes de tocar un archivo generado. Si el equipo lo editó, no lo pisa: lo informa (RF-13) |
| `wiring.configuration` | Enumera las variables que el producto necesita por causa del módulo |

**Por qué se guarda la huella y no una copia.** Una copia del archivo generado duplicaría código del producto dentro de su propio registro, y envejecería con cada edición. La huella responde la única pregunta que importa al actualizar: ¿esto sigue siendo lo que la herramienta escribió?

## 8. Cómo crece el contract package

Un módulo nuevo normalmente necesita puertos que todavía no existen.

| Cambio | Efecto en la versión | Por qué |
| :-- | :-- | :-- |
| Agregar un submódulo con un puerto nuevo y su token | Menor | Nada de lo publicado cambia de forma. Un producto que no lo importa no se entera |
| Agregar un método opcional a un puerto existente | Menor | Las implementaciones existentes siguen siendo válidas |
| Cambiar la firma de un método, quitar un método o renombrar un token | Mayor | Rompe toda implementación existente |

Los puertos de los dos módulos entraron como submódulo nuevo, que es la primera fila: ninguna implementación existente dejó de ser válida. La versión de contrato que un módulo declara sigue siendo la **mayor**, no la exacta.

**Lo que el rango `0.x` cobra.** Un cambio menor del contrato no obliga a republicar un módulo *por compatibilidad*, pero en `0.x` sí obliga a republicar por el rango: un intervalo sobre `0.2.0` no acepta `0.3.0`, así que el activo y cada módulo se republican con el rango movido, sin un cambio de código.

## 9. El puerto técnico del módulo de persistencia

Entra al contract package como submódulo nuevo, con el puerto y su token.

*Archivo: `packages/contracts/src/persistence/database.port.ts`*

```ts
export type DatabaseValue = string | number | bigint | boolean | null | Uint8Array;

export interface DatabasePort {
  query<TRow>(statement: string, parameters?: readonly DatabaseValue[]): Promise<readonly TRow[]>;

  execute(statement: string, parameters?: readonly DatabaseValue[]): Promise<void>;

  withTransaction<TResult>(work: () => Promise<TResult>): Promise<TResult>;
}

export const DATABASE_PORT = Symbol('DatabasePort');
```

El archivo real lleva el TSDoc completo de cada miembro, que es lo que ve quien instala el paquete.

| Decisión del puerto | Por qué |
| :-- | :-- |
| Tres operaciones, no más | Lectura, escritura y la unidad de trabajo. Un cuarto método sería infraestructura disfrazada de contrato |
| Los valores van aparte de la sentencia | Construir una sentencia concatenando valores es como ocurre una inyección. El puerto no admite otra forma, así que ningún adaptador puede aceptarla |
| La fecha no tiene tipo propio | Se guarda como texto en ISO 8601. Un tipo de fecha en el contrato obligaría a cada motor a traducir su representación, que es exactamente lo que el adaptador debe resolver |
| La escritura no devuelve el número de filas afectadas | Ningún caso de uso de la línea lo necesita hoy, y agregarlo después es un cambio menor. Quitarlo sería mayor |

**El reparto que esto respeta.** El repositorio del agregado es un puerto de dominio y es del producto; la conexión y la transacción son puertos técnicos y son del contrato; el adaptador del repositorio lo escribe el equipo apoyándose en la capacidad técnica que el módulo provee. El dominio del producto no conoce el motor, y cambiarlo no altera ninguna declaración de la capa de dominio.

## 10. Por qué el motor embebido de la plataforma

El adaptador usa el motor relacional que la plataforma de ejecución trae consigo. Se comparó con tres alternativas.

| Opción | Qué costaba | Veredicto |
| :-- | :-- | :-- |
| Motor embebido de la plataforma | Es una interfaz de la plataforma, no una dependencia del paquete | **Elegida**: cero dependencias de ejecución, nada que compilar al instalar, y la capacidad se verifica en la máquina de quien desarrolla y en una tubería de integración |
| Driver nativo de un motor embebido | Compilación al instalar o binarios precompilados por plataforma, y superficie de suministro nueva en un entorno regulado | Descartada: agrega riesgo de suministro para una capacidad que la plataforma ya ofrece |
| Mapeo objeto-relacional | Impone un modelo de mapeo a todo producto de la línea y una clase base que el producto extendería | Descartada por el marco: el módulo aporta la capacidad técnica, no una base de adaptador |
| Servidor relacional real | Infraestructura que levantar para verificar, y un proveedor concreto que el expediente no documenta | Descartada: la integración con infraestructura está fuera del alcance, y el puerto permite llegar a ella sin cambiar el dominio |

**Límite asumido.** El motor embebido es una interfaz de la plataforma de ejecución y su estabilidad la fija Node, no este proyecto. La condición de revisión es la misma que se aplicó a la bandera experimental del ejecutor de pruebas: si la interfaz cambia de forma, el cambio queda contenido en un archivo —el adaptador— y no alcanza al puerto, al módulo ni a ningún producto.

## 11. El adaptador y el módulo del framework

Tres piezas del adaptador merecen su justificación.

**El enlace de valores.** El motor no acepta booleanos, así que la conversión vive en el adaptador, que es el único lugar que conoce el motor. El puerto admite booleanos porque el dominio los usa.

**Apertura perezosa y cierre.** El almacén se abre la primera vez que se usa, no al construir el adaptador: un producto que no toca la base no crea el archivo. El cierre lo llama el framework por el nombre del método, así que el adaptador no importa nada del framework.

**Unidad de trabajo.** Una unidad abierta dentro de otra se une a la que ya está abierta en lugar de anidar. La alternativa —puntos de guardado— agrega una noción que ningún caso de uso de la línea necesita todavía, y que se puede agregar después sin romper el puerto.

*Archivo: `packages/modules/persistence/src/persistence.module.ts`, método de registro*

```ts
  static register(): DynamicModule {
    return {
      module: PersistenceModule,
      providers: [
        {
          provide: DATABASE_PORT,
          useFactory: (config: ConfigPort<PersistenceConfig>, logger: LoggerPort) =>
            new SqliteDatabaseAdapter(config.get('DATABASE_FILE'), logger),
          inject: [CONFIG_PORT, LOGGER_PORT]
        }
      ],
      exports: [DATABASE_PORT]
    };
  }
```

El módulo lee su configuración **por el puerto de configuración del producto**, en lugar de leer el entorno por su cuenta. Así la variable del módulo se valida junto con las del producto, una sola vez al arrancar, y el producto sigue siendo el dueño de su configuración. Para que eso sea posible el producto tiene que exponer sus puertos técnicos más allá de su módulo raíz, que es lo que hace el módulo global de la plantilla.

**El valor por defecto de la variable** hace que un producto compuesto arranque sin que nadie defina nada, que es la condición de llegada de la fase. Quien necesite otro archivo lo define en su entorno.

## 12. La plantilla del adaptador de repositorio

El módulo entrega el adaptador como plantilla, y lo que produce es código del producto desde el momento en que se escribe.

| Decisión | Por qué | Límite que deja |
| :-- | :-- | :-- |
| El esquema se crea en el primer uso | Un producto de la línea arranca con una tabla, y una herramienta de migraciones para una tabla es infraestructura sin trabajo que hacer | Un producto con datos que preservar entre formas reemplaza esto por la herramienta de migración que elija. Está dicho en la documentación del archivo generado |
| La tabla toma el nombre del agregado, en singular | La derivación ya declaró su límite de pluralización, y un nombre singular no depende de ella | Un equipo que prefiera plural renombra la tabla y la sentencia, que están en su código |
| La rehidratación usa la fábrica de inicio del agregado | La semilla no distingue crear de reconstruir, y agregar esa distinción al agregado sería imponer modelado de dominio desde el catálogo | Cuando el agregado gane invariantes de ciclo de vida, el equipo agrega su propia fábrica. El archivo es suyo |
| La plantilla implementa los dos métodos posibles del puerto | Un manifiesto sin condicionales no puede elegir cuáles escribir, y una clase puede implementar más métodos de los que su interfaz declara | Ninguno observable: el producto que solo declara uno compila igual |

**Dos ligaduras, no una.** El manifiesto reemplaza dos regiones del punto de composición: la que declara de dónde viene el adaptador del repositorio y la que lo liga al puerto de dominio. La razón apareció al construir la operación: reemplazar solo la ligadura deja sin uso el import anterior y el producto compuesto no pasa su propio análisis estático.

## 13. Pruebas del módulo

Doce pruebas, sin producto alrededor. El almacén de las pruebas es el mismo adaptador sobre un archivo que vive lo que vive el proceso.

| Archivo | Qué fija |
| :-- | :-- |
| Prueba del adaptador | Que una fila guardada se lee de vuelta; que un booleano se enlaza como el entero que el motor acepta; que una consulta sin coincidencias devuelve vacío; que un valor **nunca se interpola en la sentencia**, probado con un valor que intenta cerrarla y borrar la tabla; que lo confirmado en una unidad de trabajo queda; que lo escrito en una unidad que falla se deshace; que una unidad dentro de otra se une a la abierta; y que la apertura del almacén se informa por el puerto de registro |
| Prueba del manifiesto | Que valida contra su esquema; que declara el mismo paquete en el que viaja; que su versión de contrato es la mayor que el paquete declara como peer; y que cada plantilla que declara existe en el paquete |

**Por qué la prueba de la inyección de valores está acá y no en la verificación del circuito.** Es una propiedad del adaptador, no del sistema compuesto: si el adaptador deja de preparar la sentencia, esta prueba falla sola, sin levantar un producto.

## 14. El segundo módulo del catálogo

El módulo de la fase es el de persistencia. El catálogo tiene dos, y el segundo —`@bsl/observability`— no sale de esta fase: construye la primera capacidad del orden de crecimiento del doc 1 §9. Queda registrado acá porque es lo que prueba que la forma de este documento sirve para un módulo de otra naturaleza.

| | `@bsl/persistence` | `@bsl/observability` |
| :-- | :-- | :-- |
| Capacidad | C-06, persistencia relacional | C-02, exportación de la telemetría |
| Puerto que provee | Un puerto que nada de la plantilla ligaba | Un puerto que nada de la plantilla liga **y al que el producto ya reporta** |
| Reparto | Módulo más adaptador del producto | Todo el módulo: el producto no escribe nada |
| Qué genera en el producto | Un archivo, desde plantilla | Ninguno |
| Cableado | Cuatro inserciones, dos regiones de código y una del README | Dos inserciones, la configuración y una región del README |
| Configuración | Una variable | Seis, todas con el nombre que el estándar les da |

**Lo que esto comprueba del mecanismo.** Un módulo de otra naturaleza entró **sin cambiar el núcleo, ni el esquema del manifiesto, ni la operación**: los scaffolds y los cableados ya eran opcionales y la herramienta sigue sin conocer un módulo por su nombre. La única pieza que creció fue el catálogo, con una entrada.

**Qué exporta el segundo.** Entrega a un colector las entradas del log, el span de cada request y la duración de cada una, en el protocolo OpenTelemetry sobre HTTP y sin dependencias de ejecución, con el muestreo del estándar y una cola acotada. **No expone un endpoint para raspar métricas**, y la razón es del marco: un módulo no aporta adaptadores de entrada.

**El hallazgo que dejó al construirlo, y es una regla nueva.** Un módulo **no puede recibir por constructor un puerto al que el producto le reporta lo que ese módulo exporta**. El adaptador pedía el puerto de registro, cerró un ciclo con el logger del producto, y el contenedor lo resolvió dejando al logger sin puerto **en silencio**: el producto arrancó, atendió y no exportó nada. Está en los límites de §15 y tiene su prueba de regresión en la plantilla.

## 15. Límites declarados

| Límite | Razón |
| :-- | :-- |
| Un módulo no puede declarar un puerto propio | Si lo hiciera, el producto dependería del módulo y la dirección de dependencia quedaría invertida, que es lo que el contract package existe para evitar |
| Un módulo no puede aportar adaptadores de entrada | La superficie externa del producto es contrato con terceros. La única excepción del marco son las sondas de estado, que ya están en la plantilla |
| Un módulo no puede recibir por constructor un puerto al que el producto le reporta lo que ese módulo exporta | Cierra un ciclo con el módulo global de la línea, y resuelto en el contenedor ese ciclo deja al puerto sin adaptador **en silencio** |
| Una plantilla de módulo solo sustituye los nombres de §5 | Un manifiesto capaz de ejecutar lógica sería código del módulo corriendo dentro de la herramienta |
| Un producto admite un solo adaptador por puerto | Restricción del marco. Puede levantarse después sin invalidar nada: exigiría un calificador en lo que el módulo provee y en la entrada del registro |
| Un solo motor por versión del módulo | El motor es un adaptador interno. Otro motor llega como versión del módulo, elegida por configuración |
| Sin migraciones de esquema | El esquema describe el dominio del producto. La creación en el primer uso alcanza mientras el producto tenga una tabla |
| Sin puntos de guardado en la unidad de trabajo | Una unidad dentro de otra se une a la abierta. Agregarlos después no rompe el puerto |

[image1]: <../Insumos/Diagramas/GM-02_fig1_del_paquete_al_producto.svg>
