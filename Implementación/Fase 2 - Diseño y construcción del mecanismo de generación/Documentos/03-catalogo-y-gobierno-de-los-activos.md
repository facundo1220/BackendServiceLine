# Catálogo y gobierno de los activos

Fija qué hace válido a un activo cualquiera sea su tipo, hasta dónde puede un producto alejarse de uno, qué constituye un cambio incompatible y cómo se versiona, qué declara una entrada del catálogo y quién la gobierna. Y lo pone en operación: el catálogo deja de ser una política y pasa a ser un archivo bajo control de versiones, publicado como artefacto versionado del que la herramienta lo obtiene.

---

Sin gestión los activos derivan, nadie responde por ellos y el catálogo se convierte en una lista de cosas que alguien publicó alguna vez. Es también lo único que responde a la brecha **B-03**, la ausencia de un mecanismo de catálogo con propiedad y reglas de incorporación.

## 1. Tipos de activo y condiciones de validez

El catálogo reconoce cuatro tipos de core asset.

| Tipo | Qué aporta |
| :---- | :---- |
| Plantilla | La estructura de partida de un producto de la familia, y la declaración de qué forma de producto deriva |
| Módulo | La realización de una o más capacidades técnicas |
| Contract package | Las declaraciones de los puertos técnicos de la línea |
| Activo base | El tipo que tuvo la plantilla antes de que la línea admitiera más de una. Se conserva porque hay entradas publicadas que lo usaron |

Tres condiciones son comunes a todo activo, con independencia de su tipo.

| Condición | Contenido |
| :---- | :---- |
| Responsable declarado | Todo activo tiene un equipo responsable nombrado en el catálogo |
| Versionado | Todo activo se distribuye con una versión que sigue la política de §3 |
| Dependencias declaradas | Todo activo declara de qué otros activos depende, y en qué versión |

La tercera es la que hace gobernable al conjunto: permite responder qué se ve afectado por un cambio consultando el catálogo, sin abrir los repositorios de los productos.

**El responsable es un equipo, no una persona.** Un activo cuyo responsable fuera una persona quedaría huérfano al salir esa persona de la organización. Un equipo es una entidad que sobrevive a la rotación de sus integrantes.

A esas tres se suman las condiciones específicas por tipo.

| Tipo | Condiciones específicas |
| :---- | :---- |
| Plantilla | Las siete del doc 2 §1, cada una con quién la comprueba |
| Módulo | Provee al menos un adaptador de un puerto técnico declarado; declara la versión de contrato que implementa; no declara ni se apropia de puertos de dominio |
| Contract package | Contiene únicamente declaraciones de tipo, sin implementación ni código ejecutable |

## 2. Escala de adaptación

El producto derivado se entrega a un equipo que conserva autonomía para modificarlo (RNF-02), y al mismo tiempo la línea debe poder propagarle cambios. La escala de adaptación resuelve esa tensión declarando tres niveles con consecuencias distintas.

| Nivel | En qué consiste | Efecto sobre la propagación |
| :---- | :---- | :---- |
| Configurar | Alterar el comportamiento del activo mediante configuración externa | Ninguno. El producto sigue recibiendo actualizaciones |
| Sustituir el adaptador | Implementar el mismo puerto con código propio y registrarlo en lugar del que provee el módulo | Ninguno sobre el producto. Lo que cambió es la elección de adaptador, no el activo. El mantenimiento del adaptador propio corresponde al equipo |
| Bifurcar | Copiar los fuentes del activo al producto, retirar la dependencia y editarlos | El activo deja de recibir propagación. Queda marcado como bifurcado en el registro de versiones |

**Por qué la bifurcación se admite.** Prohibirla no impediría que ocurra; solo la dejaría sin registro. Declararla con su consecuencia explícita es preferible a una prohibición que el marco no puede hacer cumplir.

**Reversión y señal.** La marca de bifurcación se retira cuando el producto vuelve a consumir el activo del catálogo. El marco no garantiza que eso sea posible, porque depende de que el activo llegue a cubrir lo que motivó la bifurcación. Por esa razón una bifurcación se interpreta como señal de que al activo le falta un punto de configuración o de sustitución, y alimenta el flujo de nuevos requerimientos hacia el análisis del dominio.

## 3. Versionado y cambio incompatible

Se adopta versionado semántico, y la política fija qué constituye cada clase de cambio.

| Clase | Qué la constituye |
| :---- | :---- |
| Mayor | Eliminar o alterar la firma de una operación de un puerto; agregar un parámetro de configuración obligatorio sin valor por defecto, o eliminar uno existente; alterar el identificador con que un módulo se registra; estrechar el rango soportado de la plataforma de ejecución; alterar el formato del registro de versiones del producto |
| Menor | Agregar una operación opcional a un puerto; agregar un parámetro de configuración con valor por defecto; agregar un adaptador alternativo |
| Parche | Corregir comportamiento sin alterar el contrato |

**Cómo se verifica.** La compatibilidad se determina por inspección de lo declarado: la firma de las operaciones, el esquema de configuración y el identificador de registro. Toda la evidencia necesaria está en el contrato, sin recurrir a ejecución. Con el lenguaje adoptado, además, el compilador detecta por sí mismo los cambios de firma que rompen a un consumidor.

**Limitación asumida.** La verificación por ejecución queda despriorizada, de modo que un cambio de comportamiento que conserve la firma intacta no se detecta por inspección. Se registra como limitación del marco y como punto de extensión.

**Declaración de compatibilidad de un módulo.** Un módulo declara la versión **mayor** del contrato que implementa, no una versión exacta ni un rango. Un cambio menor del contrato no obliga a republicar el módulo, porque por definición no rompe implementaciones existentes; solo un cambio mayor lo obliga.

**El rango `0.x`, y lo que ahí no se cumple.** Durante la construcción los activos se versionan en `0.x` y pasan a `1.0.0` al estabilizarse el contrato. En ese rango el versionado semántico no obliga a elevar la mayor ante un cambio incompatible, lo que permite iterar el contrato sin inflar el número. Pero tiene una consecuencia que apareció al ejecutarla y que invierte la frase anterior: **un rango de intervalo sobre `0.x` no admite la menor siguiente**, porque `^0.2.0` excluye `0.3.0`. Así que en `0.x` una menor del contrato **no** llega al producto sin intervención: obliga a republicar el activo y cada módulo con el rango movido, incluso sin un cambio de código.

## 4. La versión del contract package

El contract package se organiza en submódulos por capacidad pero se versiona como una unidad. Un cambio incompatible en una capacidad eleva la versión mayor de todas, aunque las demás no hayan cambiado.

**Consecuencia asumida.** Un producto que consume una sola capacidad recibe una versión mayor que no le afecta, y un módulo puede verse obligado a republicarse sin que su implementación haya cambiado.

**Paliativo adoptado.** El registro de cambios del contract package indica qué submódulos cambiaron en cada versión, de modo que un producto determine en una lectura si una versión mayor lo afecta.

**Criterio de migración.** La separación en artefactos independientes por capacidad queda prevista, con un disparador observable: cuando un módulo deba republicarse sin alterar su implementación más de dos veces, el acoplamiento de versión cuesta más de lo que ahorra en gobernanza y corresponde migrar. Hasta entonces, la versión compartida se mantiene.

## 5. El catálogo: qué declara una entrada

El catálogo es un manifiesto declarativo. Una entrada no contiene el activo: lo describe y señala dónde reside.

| Campo | Contenido |
| :---- | :---- |
| `id` | Nombre único del activo dentro del catálogo, en kebab-case |
| `type` | Plantilla, módulo, contract package o activo base |
| `package` | Paquete donde reside el artefacto distribuible |
| `owner` | El equipo que responde por el activo |
| `description` | Qué capacidad aporta |
| `contractVersion` | Versión mayor del contrato que implementa. Obligatoria para un módulo, admitida para una plantilla y prohibida para el contract package y para un activo base |
| `status` | `proposed`, `active` o `deprecated` |

*Archivo: `catalog.json` en `bsl-catalog`, una entrada*

```json
{
  "id": "persistence",
  "type": "module",
  "package": "@bsl/persistence",
  "owner": "Line governance",
  "description": "Relational persistence capability: connection to the product store and execution of statements inside a transaction. The product writes its own repository adapter on top of it.",
  "contractVersion": 0,
  "status": "active"
}
```

El esquema que lo valida vive al lado y es lo que hace exigibles esos campos: `additionalProperties: false` convierte un campo mal escrito en un error en lugar de ignorarlo en silencio, y una regla condicional declara `contractVersion` obligatoria para un módulo y prohibida para los dos tipos que no la tienen. El manifiesto apunta a su esquema y la validación corre en su `verify`.

**Por qué `contractVersion` no aplica a todo tipo.** Responde a una pregunta concreta: qué versión mayor del contrato implementa el activo, de modo que pueda saberse si sigue siendo compatible cuando el contrato sube de mayor. El contract package **es** el contrato, y su propia versión ya es esa información. Un activo base lo **consume**, y esa relación se expresa como dependencia en su manifiesto, donde el gestor de paquetes la hace cumplir; duplicarla en el catálogo crearía dos fuentes de verdad que pueden divergir. Una plantilla sí la declara, porque su manifiesto declara además la versión exacta contra la que se construyó.

**Por qué la plantilla es un tipo y no una segunda entrada de activo base.** No es cosmético: es lo que permite que `contractVersion` tenga reglas distintas por tipo, lo que `bsl templates list` distinga el almacén de los módulos sin leer nombres, y lo que vuelve exigible que una plantilla declare el contrato contra el que se construyó.

| Estado | Se ofrece al derivar o al componer | Efecto sobre los productos que lo consumen |
| :---- | :---- | :---- |
| `proposed` | No | No aplica |
| `active` | Sí | Reciben propagación |
| `deprecated` | No | Siguen funcionando y reciben correcciones |

**No se admite retirar un activo.** Un activo del que dependen productos existentes no puede eliminarse del catálogo sin romperlos. `deprecated` es el estado terminal: el activo deja de ofrecerse y permanece en el catálogo indefinidamente. El retiro acompañado de un procedimiento de migración queda como trabajo futuro.

**Un archivo único y no un directorio por activo.** Con el número de activos previsto, la división en archivos añadiría navegación sin aportar aislamiento: la política de revisión opera igual sobre una ruta que sobre muchas. La división queda como punto de extensión si el catálogo crece.

## 6. Gobernanza del catálogo

El catálogo se materializa en dos capas: el repositorio bajo control de versiones aporta la **gobernanza**, y el artefacto versionado publicado desde él aporta la **distribución**.

| Capa | Qué aporta |
| :---- | :---- |
| Repositorio | La incorporación de una entrada es una propuesta de cambio sujeta a revisión, y la propiedad declarada se hace exigible mediante políticas sobre las rutas del manifiesto |
| Distribución | Resolución versionada, inmutabilidad y uso del mismo canal, credenciales y red que los demás activos |

Esta combinación reproduce el patrón de catálogo con modelo de propiedad identificado en el estudio comparativo, sin desplegar ni operar una aplicación, que es precisamente lo que B-03 señala.

**Regla de incorporación.** Agregar o modificar una entrada exige una propuesta de cambio sobre el manifiesto, aprobada por el rol responsable del gobierno de la línea. La política se declara sobre la ruta del archivo, con un `CODEOWNERS` que nombra a ese rol. El marco define la existencia del rol y la obligatoriedad de la revisión; su asignación concreta dentro de la organización corresponde a cada instanciación.

**Procedimiento, en cinco pasos.**

| # | Paso |
| :---- | :---- |
| 1 | El activo satisface las condiciones de validez de su tipo y **está publicado en el registro** |
| 2 | Se propone la entrada sobre el manifiesto, en `proposed` |
| 3 | El responsable del gobierno la revisa y aprueba |
| 4 | **La entrada pasa a `active`**, que es lo que la vuelve ofrecible al derivar o al componer |
| 5 | Se publica una versión nueva del catálogo |

El cuarto paso es explícito porque su ausencia costó un rechazo: un paquete servido por el feed con su entrada todavía en `proposed` existe y no se puede usar, y el mensaje de la herramienta decía que no estaba en el catálogo. Publicar un activo y ofrecerlo son dos actos.

**Por qué el paso 4 no lo hace el `prepublishOnly` del activo.** Se evaluó y se descarta: el catálogo vive en otro repositorio y es la pieza que queda bajo revisión del gobierno de la línea, así que una publicación que lo escriba convierte el acto en un cambio no revisado de un repositorio ajeno. El segundo acto cuesta una publicación del catálogo, costo ya medido y aceptado.

**Condición del entorno de construcción.** En este entorno proponente y revisor coinciden en la misma persona. Es una condición del entorno y no una propiedad del mecanismo: la política queda instanciada y operativa, y trasladarla a operación consiste en cambiar quién figura como propietario. La aprobación queda registrada aunque sea propia, de modo que la traza de incorporación existe desde la primera entrada.

## 7. Distribución y resolución en ejecución

El manifiesto se publica como paquete versionado desde su repositorio, y la herramienta lo resuelve **en ejecución**, con tres fuentes en orden: la ruta que dé la invocación, la última versión que sirve el registro —cacheada por versión— y, cuando el registro no puede responder, la copia instalada con la herramienta. Cuál respondió se informa en la salida.

| Criterio | Qué vale |
| :---- | :---- |
| Un activo nuevo aparece | Publicando solo el catálogo. Una entrada cuesta **una** publicación |
| Determinismo | Intacto. Lo que determina la estructura de un producto es el **contenido** de la plantilla, que sigue fijada por el pin de la herramienta; el catálogo decide **qué activos existen** |
| Operación sin red | Posible: la copia instalada es el piso de la resolución, y la salida dice que respondió ella |
| Alcance de una entrada publicada por error | Inmediato, y acotado por el gobierno del repositorio: una entrada nace en `proposed` y no se ofrece hasta activarse, una `deprecated` se rechaza, y el repositorio tiene revisión y propiedad declarada |

La herramienta sigue declarando el catálogo como dependencia con versión exacta, pero eso **ya no es la fuente, es el respaldo**, y no hay que moverlo cuando el catálogo gana una entrada.

![][cap1]

El listado del almacén muestra las dos cosas que esta sección decide. La primera línea nombra la versión del catálogo y **de qué fuente salió**, que es lo que permite saber si una ejecución respondió con red o sin ella. Las dos filas traen el estado de cada entrada, que es lo que decide si una plantilla se puede derivar o solo mirar.

**Por qué no la versión fija como fuente.** Lo fue, con el argumento de que RF-05 exige que la misma entrada produzca el mismo resultado y que resolver siempre la última versión podría hacer que dos ejecuciones idénticas obtuvieran activos distintos. Medido, el costo era que una entrada nueva costaba **dos** publicaciones, y una de ellas era una versión de la herramienta cuyo único cambio sustantivo era un número. Y el determinismo que RF-05 pide no lo daba la versión del catálogo: lo da el pin, porque lo que determina la estructura de un producto es el contenido del activo del que se deriva.

**El pin de versiones de los activos.** Una entrada del catálogo declara el paquete de un activo, no su versión, de modo que el manifiesto no alcanza para saber cuál se incorpora al derivar. Ese dato lo declara la herramienta en un artefacto propio que fija la versión exacta de cada activo que esa release ofrece, con una versión exacta y nunca un rango: un rango haría que dos ejecuciones de la misma herramienta resolvieran versiones distintas, que es lo que el pin existe para evitar. Un módulo **no** se fija así —se resuelve a la última publicada y la versión obtenida queda registrada en el producto—, porque pinar cada módulo obligaría a publicar una versión de la herramienta por cada versión de cada módulo, que es exactamente la dependencia que el catálogo existe para evitar.

## 8. Organización de los repositorios

| Repositorio | Contenido |
| :---- | :---- |
| `bsl-catalog` | El manifiesto del catálogo y sus políticas de revisión |
| `bsl-assets` | El contrato, las plantillas bajo `packages/templates/`, los módulos bajo `packages/modules/` y la herramienta, como paquetes independientes |

**Por qué el catálogo va aparte.** El catálogo gobierna activos que no le pertenecen. Alojado junto a ellos, incorporar una entrada y modificar el activo que esa entrada describe serían el mismo cambio, revisado en el mismo acto, y la revisión que el marco exige perdería su objeto. El repositorio propio es lo que permite aplicar políticas sobre las rutas del manifiesto y hacer exigible la propiedad declarada.

**Por qué los activos van juntos.** Contrato, plantilla y herramienta se modifican en conjunto: un puerto nuevo cambia el contrato y el activo que lo implementa, y la herramienta se prueba contra la versión vigente del activo. En repositorios separados, cada iteración exigiría publicar antes de poder probar. Lo que no cambia es el gobierno, que no depende del número de repositorios sino de dos condiciones: que la incorporación al catálogo sea una propuesta revisable, y que cada activo se versione y se distribuya por separado. **Compartir repositorio es compartir historia, no versión.**

**Límite asumido.** La agrupación responde a las condiciones de construcción de este trabajo, donde una sola persona desarrolla los activos en paralelo. En una instanciación con equipos responsables distintos, la separación en repositorios propios es la disposición coherente con el modelo de propiedad del marco. Es una decisión de contexto, no una propiedad de la línea.

**Exclusión del contenido de plantilla.** La carpeta que contiene el proyecto que se deriva tiene su propio TypeScript, su propio analizador y su propio manifiesto, que son los del producto y no los del repositorio que lo aloja. Queda excluida en los tres lugares que la alcanzarían: los espacios de trabajo de la raíz, la configuración de TypeScript y la del analizador. **Consecuencia asumida:** ese contenido no se compila ni se analiza dentro del monorepo, de modo que un error en él se detecta al ejecutar el activo como proyecto independiente, que es lo que hace su propia verificación. Se declara para que nadie suponga que el monorepo verifica la plantilla.

## 9. Registro de paquetes y resolución del espacio de nombres

Los activos se distribuyen mediante un registro de paquetes privado compatible con el gestor del ecosistema. El marco exige que esa distribución sea agnóstica del proveedor: sustituir el registro es un cambio de configuración y no afecta a ningún activo ni a ningún producto.

El espacio de nombres, el feed y el nombre del comando coinciden deliberadamente: quien ve `@bsl/contracts` en un manifiesto deduce dónde reside sin consultar nada.

**La declaración se separa de la credencial.** El gestor de paquetes consulta el registro público por defecto, así que para que el espacio de nombres se resuelva hay que declarar que reside en otro sitio.

| Elemento | Dónde reside | Por qué |
| :---- | :---- | :---- |
| Asociación del espacio de nombres al feed | En el producto generado, en un archivo de configuración de registro versionado | Es una dirección, no un secreto. Hace el producto instalable sin configuración previa |
| Credencial de acceso | En la configuración del usuario o del proceso de publicación | Es un secreto y no puede residir en un repositorio |

Podría objetarse que ese archivo ata el producto a un proveedor. La dirección del feed es precisamente el punto de configuración que el marco declaró sustituible: cambiar de registro es cambiar esa línea, y que la sustitución sea un cambio de configuración es lo que el marco pide.

## 10. Procedimiento de publicación

La publicación se realiza de forma local, con credencial del usuario. La condición de validez que el marco exige no se delega en la memoria de quien publica: se aplica automáticamente.

*Archivo: `package.json` de cada activo publicable, extracto*

```json
{
  "scripts": {
    "verify": "npm run lint && npm run test && npm run build",
    "prepublishOnly": "npm run verify && node ../../scripts/verify-publish-order.mjs"
  }
}
```

`prepublishOnly` se ejecuta antes de publicar, así que un activo que no supera el análisis estático, que falla una prueba o que no compila no llega al registro ni, por tanto, al catálogo. Es la condición de validez del marco hecha exigible por construcción. El segundo script hace exigible la regla de orden que ya estaba escrita: **el contrato se publica primero, y nada que lo declare se publica antes que él**; rechaza publicar lo que declara un rango que el feed no sirve, comprobado rompiéndolo.

**Verificación previa del empaquetado.** Antes de publicar por primera vez, cada activo se empaqueta y se instala desde el archivo resultante en un proyecto de prueba. Es la única comprobación que detecta los problemas de empaquetado —archivos que quedaron fuera y nombres neutralizados que no se restituyen—, porque un paquete que funciona por enlace local puede fallar al publicarse por no incluir un archivo.

**Asociación del paquete con el feed.** Cada paquete publicable declara el feed en su propio manifiesto. Es la misma dirección que el producto derivado lleva en su configuración de registro, y no es un secreto; la credencial permanece en la configuración de quien publica.

**Una versión se vuelve a mover en cuanto un build de ella salió del checkout.** Publicado al feed *o* instalado en alguna parte, no solo al publicar. La regla existe porque se rompió dos veces el mismo día: un arreglo entró dentro de una versión ya servida, la copia instalada y el checkout declaraban la misma versión y se comportaban distinto. El mecanismo que la haría exigible —que el `prepublishOnly` compare el contenido del paquete contra el último publicado de esa versión y rechace si difiere— está escrito y sin construir.

**Punto de extensión: publicación automatizada.** La publicación mediante una canalización, disparada por una marca de versión en el repositorio, aportaría dos propiedades que el procedimiento local no da: la trazabilidad entre versión publicada y revisión del repositorio, y la garantía de que lo publicado procede del repositorio y no del equipo de quien publica. No cambia qué se publica ni bajo qué condiciones, porque la verificación ya es automática. Queda diferida como punto de extensión del entorno, no del mecanismo.

## 11. Límites declarados

| Límite | Razón |
| :---- | :---- |
| El catálogo no distribuye activos, solo los describe | Una entrada nombra el paquete y su responsable, de modo que un activo de otro equipo vive en el repositorio de ese equipo |
| Ningún producto se gobierna después de derivado | La línea mantiene un vínculo que permite propagar cambios, pero no impone su aceptación (RNF-02) |
| La verificación de compatibilidad no corre el activo | Un cambio de comportamiento con la firma intacta no se detecta por inspección: §3 |
| Un activo no se retira del catálogo | `deprecated` es terminal mientras no exista un procedimiento de migración de sus consumidores |

[cap1]: <../Insumos/Evidencias/MG-03_cap1_almacen_de_plantillas.png>
