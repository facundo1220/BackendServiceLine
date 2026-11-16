# Log de decisiones — Gestor de módulos reutilizables

Trabajo de grado: *Desarrollo de una herramienta CLI para la generación automatizada de proyectos backend e integración de módulos reutilizables*
Fase 3 — diseño y construcción del gestor de módulos reutilizables

Las decisiones que aparecieron al construir la fase (`Codigo/bsl-assets`, `Codigo/bsl-catalog`): las que sus documentos no habían resuelto, las que resolvían de una forma que el código no pudo sostener sin ajuste, y las que revisan una decisión de una fase anterior. Cada una es trazable a un documento de la fase, a un requerimiento de la Fase 1 o a una decisión previa del marco o del mecanismo.

## Convenciones

- **Terminología**: como en los logs anteriores, los términos técnicos se mantienen en inglés dentro de prosa en español.
- **Estados**: Aceptada · Aceptada (provisional) · Diferida · Revisada · Sustituida.
- **Numeración**: continúa la numeración global del proyecto. Este log abre en ADR-095, siguiendo a ADR-094 de la Fase 2.

**Significado de los estados**

| Estado | Qué indica |
| :---- | :---- |
| Aceptada | Decisión firme, aplicada en el código construido |
| Aceptada (provisional) | Decisión tomada sin evidencia suficiente para cerrarla, con su condición de revisión declarada |
| Diferida | Corresponde a una fase posterior o a trabajo futuro; se conserva como insumo |
| Revisada | Modifica una decisión previa de esta fase, de la Fase 1 o de la Fase 2 |
| Sustituida | Reemplazada por otra; se conserva por trazabilidad |

## Índice de decisiones

| ID | Decisión | Documento | Estado | Revisada después por |
| :---- | :---- | :---- | :---- | :---- |
| ADR-095 | Un solo módulo construido; el resto del catálogo queda declarado como crecimiento | el índice de la fase | Aceptada | **ADR-156** |
| ADR-096 | El uso del gestor no lleva documento propio: README más sección en `packages/cli/TUTORIAL.md` | el índice de la fase | Aceptada | — |
| ADR-097 | La capacidad del RF-09 es la persistencia relacional del producto | Doc 1 | Aceptada | — |
| ADR-098 | La categorización de capacidades técnicas no se apoya en BIAN | Doc 1 | Aceptada | — |
| ADR-099 | El motor de persistencia es un adaptador interno del módulo, no una entrada de catálogo por motor | Doc 1 | Aceptada | — |
| ADR-100 | Una entrada de catálogo se abre en estado `proposed` antes de que su paquete exista | Doc 1 | Aceptada | — |
| ADR-101 | El módulo declara su cableado en un manifiesto propio dentro del paquete | Doc 2 | Aceptada | — |
| ADR-102 | Cinco puntos de inserción en el producto, con región delimitada para la ligadura del repositorio | Doc 2 | Aceptada | **ADR-121**, **ADR-130**, **ADR-176** |
| ADR-103 | El plan de cambios gana modo `modify`, dos clases nuevas y respaldo del conjunto tocado | Doc 2 | Revisada | **ADR-121** |
| ADR-104 | La entrada de módulo guarda el cableado aplicado y la huella de cada archivo generado | Doc 2 | Aceptada | — |
| ADR-105 | El módulo aporta plantillas, nunca clases base: lo generado pasa a ser del producto | Doc 2 | Aceptada | — |
| ADR-106 | El contrato y el framework son `peerDependencies` del módulo | Doc 2 | Revisada | **ADR-181** |
| ADR-107 | Forma del puerto de base de datos: tres operaciones y valores enlazados aparte | Doc 3 | Aceptada | — |
| ADR-108 | El motor es el relacional embebido en la plataforma de ejecución | Doc 3 | Aceptada | — |
| ADR-109 | El adaptador generado crea su tabla en el primer uso y rehidrata con la fábrica del agregado | Doc 3 | Aceptada | — |
| ADR-110 | El módulo lee su configuración por el puerto del producto, que la expone en un módulo global | Doc 3 | Aceptada | — |
| ADR-111 | La documentación OpenAPI es pieza del activo base, no módulo del catálogo | Doc 4 | Aceptada | — |
| ADR-112 | El documento se arma con los esquemas de validación del producto; las rutas se escriben al derivar | Doc 4 | Aceptada | — |
| ADR-113 | Sin interfaz de exploración ni dependencia nueva para documentar la API | Doc 4 | Aceptada | **ADR-164** |
| ADR-114 | El archivo generado del documento queda fuera del formateador del repositorio | Doc 4 | Aceptada | — |
| ADR-115 | La herramienta comprueba el manifiesto en código; el esquema queda para el editor y la verificación | Doc 5 | Aceptada | — |
| ADR-116 | El renderizador de plantillas pasa al núcleo, porque dos operaciones lo usan | Doc 5 | Revisada | — |
| ADR-117 | Un marcador es una línea de comentario propia, no una mención del marcador | Doc 5 | Revisada | — |
| ADR-118 | Un plan puede tocar el mismo archivo varias veces; la ruta se mueve una sola vez | Doc 5 | Revisada | — |
| ADR-119 | El reemplazo de una ligadura incluye la región de su import | Doc 5 | Aceptada | — |
| ADR-120 | La versión de un módulo no se fija en la herramienta: se resuelve y se registra en el producto | Doc 5 | Aceptada | — |
| ADR-121 | Cada inserción de un módulo queda delimitada en una región propia | Doc 6 | Revisada | — |
| ADR-122 | La actualización reescribe lo que la herramienta escribió y preserva lo que el equipo cambió | Doc 6 | Aceptada | — |
| ADR-123 | Una sola operación de consulta responde lo disponible, lo incorporado y lo desactualizado | Doc 6 | Aceptada | — |
| ADR-124 | La versión disponible de un activo resuelto desde una ruta local es la que esa ruta declara | Doc 6 | Aceptada | — |
| ADR-125 | La verificación del circuito no depende del feed: paquetes empaquetados y catálogo de prueba | Doc 7 | Aceptada | — |
| ADR-126 | Cada regla se comprueba rompiéndola, y el rechazo tiene que dejar el producto idéntico | Doc 7 | Aceptada | — |
| ADR-127 | La verificación de la composición entra en `check:push`, no en `check:commit` | Doc 7 | Aceptada | — |
| ADR-130 | Un módulo escribe también en la documentación del producto, en una región que él declara | Doc 2 | Revisada | — |
| ADR-146 | El documento OpenAPI lleva el identificador y el grupo que el estándar da a cada operación | Doc 4 | Revisada | — |
| ADR-156 | El segundo módulo del catálogo es la observabilidad, y su alcance es la exportación | Doc 1 | Revisada | — |
| ADR-157 | `TelemetryPort` entra al contrato como puerto que ningún adaptador del activo base satisface | Doc 2 | Aceptada | — |
| ADR-158 | El módulo exporta en el protocolo del estándar, con su muestreo y una cola acotada | Doc 3 | Aceptada | — |
| ADR-159 | Un módulo no puede recibir el puerto al que el activo base reporta lo que él exporta | Doc 2 | Aceptada | — |
| ADR-160 | En `0.x`, subir una menor del contrato obliga a republicar el activo base y cada módulo | Doc 2 | Revisada | — |
| ADR-164 | El producto documenta su API como página, con el visor instalado y nunca desde internet | Doc 4 | Revisada | — |
| ADR-180 | El módulo declara a qué formas de producto sirve | Doc 2 | Aceptada | — |
| ADR-181 | `nest` pasa a `composition`: el framework es propiedad de la forma, no del módulo | Doc 2 | Revisada | — |
| ADR-182 | La actualización comprueba lo que comprueba la incorporación | Doc 6 | Aceptada | — |
| ADR-183 | Quitar un módulo restaura lo que la derivación escribió | Doc 6 / Doc 7 | Aceptada | — |
| ADR-190 | Un módulo en dos productos, con versiones distintas a la vez | Doc 7 | Aceptada | — |
| ADR-195 | Un solo tutorial, que viaja con la herramienta | `packages/cli/TUTORIAL.md` | Aceptada | — |

---

## ADR-095 · Un solo módulo construido; el resto del catálogo queda declarado como crecimiento

**Estado:** Aceptada · 2026-10-31 · el índice de la fase

**Contexto.** El triage de la revisión externa dejó dos módulos marcados como comprometidos —persistencia (#11) y observabilidad (#9)— y los dos invocan RF-09 como requisito que los sostiene. RF-09 pide otra cosa: «al menos un módulo transversal construido conforme al marco de referencia, que permita validar la composición y la actualización», y su criterio de aceptación cierra diciendo que las demás capacidades identificadas en el análisis quedan como catálogo a construir posteriormente.

**Decisión.** La fase construye un módulo. El doc 1 elige cuál entre las capacidades categorizadas, y las demás quedan declaradas como crecimiento del catálogo con su categorización escrita, que es lo que permite construirlas después sin volver a decidir.

**Por qué no dos.** El objeto de la fase es el mecanismo de composición, no el catálogo. Un segundo módulo duplica el Bloque A —puertos nuevos, adaptadores, manifiesto, entrada de catálogo, publicación— y no produce evidencia nueva sobre el mecanismo: la operación que incorpora un módulo es la misma para el segundo.

**Consecuencia.** Dos reglas del marco quedan sin ejercitar con un módulo solo: que un producto admite un único adaptador por puerto, y que dos productos conviven con versiones distintas del mismo activo (RNF-06). La primera se comprueba con una prueba negativa de la operación de composición, que rechaza incorporar un segundo adaptador del mismo puerto. La segunda se comprueba con dos versiones publicadas del mismo módulo, que la operación de actualización necesita de todos modos. Ninguna de las dos exige un módulo más.

**Traza.** RF-09, RNF-06, ADR-006, ADR-038, el índice de la fase, Doc 1, Doc 6, Doc 7, `Fase 4 .../Insumos/seguimiento-de-mejoras.md`.

---

## ADR-096 · El uso del gestor no lleva documento propio: README más sección en `packages/cli/TUTORIAL.md`

**Estado:** Aceptada · 2026-10-31 · el índice de la fase

**Contexto.** La Fase 2 cerró con un documento de instalación y uso (su doc 7) que recorre el camino de punta a punta: acceso al feed, instalación global, derivación, arranque del producto y catálogo de fallos con el mensaje real. Esta fase agrega tres operaciones a la misma herramienta. Un documento propio de uso en la Fase 3 obligaría a repetir los prerrequisitos y la instalación, y dejaría al lector con dos caminos que envejecen por separado.

**Decisión.** La fase no escribe un documento de uso. Lo que un usuario necesita para operar las tres operaciones nuevas se escribe en el README de `@bsl/cli`, y el camino —el orden de los pasos, qué prueba cada uno y qué falla si falta un prerrequisito— se agrega como sección nueva al `packages/cli/TUTORIAL.md`, que queda como el único documento de uso de la herramienta.

**Por qué el documento de una fase cerrada se amplía.** El doc 7 no documenta la Fase 2: documenta la herramienta, que es un artefacto vivo con una sola versión instalada. Congelarlo porque su fase cerró obligaría a que el usuario leyera dos documentos para operar un comando. La ampliación se registra acá y en el índice de la Fase 2, para que el cambio quede fechado y no parezca una edición silenciosa.

**Reparto heredado.** Vale el de ADR-093 sin cambios: el README es dueño del cómo —el comando, la opción, la ruta—, el documento de fase del camino y del por qué.

**Traza.** RNF-01, RNF-02, ADR-093, el índice de la fase, `packages/cli/TUTORIAL.md`.

---

## ADR-097 · La capacidad del RF-09 es la persistencia relacional del producto

**Estado:** Aceptada · 2026-10-31 · Doc 1

**Contexto.** RF-09 exige al menos un módulo transversal construido, y la elección de la capacidad nunca se cerró. La validación del marco afirmaba que quedaba decidida —«cifrado y manejo de tokens»— mientras la tabla de decisiones pendientes del log de la Fase 1 nombra otro candidato, el cliente de servicios corporativos, y mantiene ese item en `Pendiente`. El triage de la revisión externa, por su parte, compromete persistencia y observabilidad. Cuatro capacidades distintas propuestas por cuatro documentos, sin criterio escrito que permita comparar.

**Decisión.** El módulo de la fase es la persistencia de datos del producto (C-06 del inventario), con un motor relacional en proceso. Se identifica como `persistence` en el catálogo y se publica como `@bsl/persistence`.

**Criterio que la sostiene.** Cinco criterios ordenados por peso, en el doc 1 §6. Los que deciden son dos. El primero, que la capacidad sea verificable por comando sin infraestructura corporativa: la condición de llegada de la fase exige incorporar, arrancar y actualizar, y las capacidades de identidad, mensajería, notificaciones y consumo de servicios corporativos necesitan un servicio institucional o un proveedor externo para funcionar. El segundo, que ejercite el mecanismo de composición en su caso más exigente: la persistencia es el único candidato donde el puerto técnico es del contrato, el puerto de dominio es del producto y el adaptador lo escribe el equipo, que es exactamente el caso de referencia con que MR-04 §5 explicó el acople.

**Por qué no la más recurrente.** T-09 pone primero la autenticación y autorización. Queda como crecimiento porque su contrato de integración y permisos lo fija la organización, no este trabajo (T-08), y sin el proveedor de identidad no hay forma de comprobar por comando que un producto compuesto arranca y responde. Una versión simulada daría un módulo que nadie incorporaría y una evidencia que no prueba nada.

**Por qué no el cifrado, que es lo que la validación del marco afirmaba.** El módulo aportaría el adaptador completo y el producto no escribiría nada, así que el mecanismo de composición queda ejercitado en su caso más simple. Además ningún producto derivado exhibe hoy ese hueco, mientras la persistencia en memoria sí es un hueco declarado en el resumen y el README del producto (ADR-082) y señalado por la revisión externa. La parte difícil del cifrado —dónde viven las claves— es institucional.

**Consecuencia sobre un documento anterior.** La fila de RF-09 de la validación del marco quedaba incorrecta y debe decir que el marco aporta las condiciones de validez y la frontera entre lo empaquetado y lo generado, y que la elección de la capacidad es de esta fase. La corrección se aplica al cerrar ese documento, que sigue abierto por P-02, y queda anotada en `PENDIENTES.md`.

**Traza.** RF-09, T-05, T-08, T-09, T-04, ADR-082, ADR-095, MR-04 §5, P-02, P-14, Doc 1 §6, §7, §8, §11.

---

## ADR-098 · La categorización de capacidades técnicas no se apoya en BIAN

**Estado:** Aceptada · 2026-10-31 · Doc 1

**Contexto.** La actividad de la fase enunciada en el anteproyecto pide identificar y categorizar las funcionalidades transversales reutilizables «tomando como referencia los dominios funcionales definidos por BIAN». Las doce capacidades del inventario son técnicas: persistencia, observabilidad, cifrado, identidad, mensajería, notificaciones, consumo de servicios corporativos.

**Decisión.** La categorización se hace con ejes propios —clase de puerto, reparto de la realización, dependencia de infraestructura externa y estado en el artefacto— y no con los dominios de BIAN.

**Por qué.** BIAN modela capacidades de negocio bancario y no modela infraestructura técnica de aplicaciones, que es lo que la Fase 1 ya había decidido al declarar el catálogo de esta línea fuera del alcance del estándar y bajo gobierno del marco propio (MR-02 §2, ADR-006). No existe un Service Domain que signifique «persistencia»: forzar la correspondencia produciría etiquetas sin contenido y debilitaría la alineación real, que es la del producto.

**Dónde sí se cumple la referencia al estándar.** En el eje de dominio del producto derivado, que la Fase 2 construyó: la derivación sitúa cada producto en un Business Domain y un Service Domain, y ese metadato queda en su registro. La alineación con BIAN es del producto, no del catálogo técnico que lo compone.

**Consecuencia.** Un lector que compare el anteproyecto con lo construido encuentra la diferencia. Queda registrada acá y en el doc 1 §5 como decisión con fundamento, y se narra en el capítulo de la tesis.

**Traza.** ADR-006, MR-02 §2, Anteproyecto §6 (actividades de la Fase 3), Doc 1 §3, §5.

---

## ADR-099 · El motor de persistencia es un adaptador interno del módulo, no una entrada de catálogo por motor

**Estado:** Aceptada · 2026-10-31 · Doc 1

**Contexto.** El módulo de persistencia aporta conexión y transacción sobre un almacén relacional. Un producto puede necesitar un motor distinto del que el módulo trae, y había dos formas de admitirlo: una entrada de catálogo por motor, o un solo módulo con varios adaptadores internos elegidos por configuración.

**Decisión.** El catálogo guarda una entrada por capacidad. El motor es un adaptador interno de `@bsl/persistence`, y se elige por configuración del producto.

**Por qué.** Una entrada por motor multiplica el catálogo por el número de motores y obliga al producto a cambiar de dependencia cuando cambia de infraestructura, que es precisamente lo que el puerto técnico evita. La capacidad es la misma; lo que cambia es su realización.

**Consecuencia.** Un producto que necesite un motor que el módulo todavía no trae espera una versión del módulo, o escribe su propio adaptador del puerto técnico y lo registra en lugar del que el módulo provee. La segunda salida ya está admitida por el gobierno de activos: sustituir el adaptador no tiene efecto sobre el producto más allá de su punto de composición (MR-05 §3).

**Traza.** RF-14, MR-04 §3, MR-05 §3, Doc 1 §8, §9, Doc 3.

---

## ADR-100 · Una entrada de catálogo se abre en estado `proposed` antes de que su paquete exista

**Estado:** Aceptada · 2026-10-31 · Doc 1

**Contexto.** El esquema del manifiesto admite tres estados: `proposed`, `active` y `deprecated`, y el script de validación comprueba la forma del manifiesto, no la existencia del paquete. Al elegir la capacidad del módulo, la decisión está tomada pero el paquete no existe: el doc 3 lo construye y el autor lo publica.

**Decisión.** La entrada `persistence` entra al manifiesto con `status: "proposed"` en cuanto la capacidad queda elegida, y pasa a `active` cuando el paquete está publicado en el feed y la operación de composición lo resuelve.

**Por qué.** El manifiesto es el registro de gobierno de la línea, y una decisión tomada que no está en él obliga a buscarla en un documento. El estado `proposed` existe justamente para eso: declara que la línea comprometió la capacidad sin afirmar que ya se puede incorporar.

**Consecuencia para la herramienta.** La operación de composición debe rechazar un activo que no esté `active`, con un mensaje que diga en qué estado está. Es una regla de la operación, y se construye en el doc 5 con su prueba negativa.

**Traza.** RF-14, RF-16, ADR-048, MR-05 §5, Doc 1 §8, Doc 5.

---

## ADR-101 · El módulo declara su cableado en un manifiesto propio dentro del paquete

**Estado:** Aceptada · 2026-10-31 · Doc 2

**Contexto.** La operación de composición tiene que insertar el registro del módulo en el punto de composición del producto, agregar sus variables de configuración y declarar la dependencia. Había dos formas de que supiera qué insertar: que la herramienta conociera cada módulo del catálogo, o que cada módulo se describiera a sí mismo.

**Decisión.** Cada módulo publica `bsl-module.json` dentro de su paquete, con su esquema JSON al lado. Declara qué puertos provee, cómo entra al punto de composición, qué configuración necesita, qué plantillas aporta y qué regiones generadas reemplaza. La herramienta lee el manifiesto y traduce la declaración a cambios; no conoce ningún módulo por su nombre.

**Por qué dentro del paquete y no en el catálogo.** El cableado es parte del activo y cambia con él. En el catálogo obligaría a cambiar dos repositorios de forma coordinada para publicar una versión, y una desincronización dejaría a la herramienta aplicando el cableado de otra versión del módulo.

**Límite deliberado.** El manifiesto no admite condicionales, bucles ni expresiones evaluables. Las únicas sustituciones son los nombres del producto que la derivación ya resuelve. Un manifiesto capaz de ejecutar lógica sería código del módulo corriendo dentro de la herramienta, y la herramienta dejaría de poder mostrar en `--dry-run` qué va a cambiar.

**Consecuencia.** Incorporar un módulo nuevo al catálogo no exige publicar una versión de la herramienta, que es la dependencia que el catálogo existe para evitar (RF-14, RF-16).

**Qué se extendió (2026-11-09, ADR-180 y ADR-171).** Dos cosas, ninguna de las cuales toca lo decidido aquí. **ADR-180** agrega al manifiesto la declaración de a qué formas de producto sirve el módulo, que es lo que faltaba para que la línea pudiera tener más de una forma. Y **ADR-171** aplica esta misma decisión donde faltaba: una plantilla de la línea también se describe a sí misma, en un `bsl-template.json` dentro de su paquete, con el mismo argumento de por qué va en el paquete y no en el catálogo. El límite deliberado de esta decisión —sin condicionales, bucles ni expresiones evaluables en el manifiesto de un **módulo**— sigue vigente tal cual; el manifiesto de una plantilla sí los admite, con la gramática cerrada de ADR-173 y la frontera escrita de ADR-174, y la razón de la diferencia es que una plantilla declara **el producto entero** y un módulo declara **un injerto** en un producto que ya existe.

**Traza.** RF-06, RF-07, RF-14, RF-16, ADR-052, ADR-056, ADR-057, ADR-171, ADR-180, MR-04 §4, Doc 2 §4, Doc 5.

---

## ADR-102 · Cinco puntos de inserción en el producto, con región delimitada para la ligadura del repositorio

**Estado:** Revisada · 2026-10-31 · Doc 2 · revisada por ADR-130 · **revisada el 2026-11-09 por ADR-176**

**Contexto.** El activo base trae una sola marca, `// bsl:modules`, puesta en la Fase 2 para que la composición insertara ahí el registro del módulo. Al diseñar el cableado completo aparecieron cuatro necesidades más: la sentencia `import` del módulo, la entrada del esquema de configuración, el ejemplo de la variable de entorno, y el reemplazo de la ligadura entre el puerto de dominio del repositorio y su adaptador.

**Decisión.** El producto trae cinco puntos de inserción: `bsl:module-imports` y `bsl:modules` en el punto de composición, la región delimitada `bsl:repository-binding:start` … `:end` en el mismo archivo, `bsl:module-config` en el esquema de configuración y `bsl:module-env` en el ejemplo de entorno. Las cuatro nuevas se agregan a las plantillas de la herramienta y, por tanto, al activo base, que es su salida (ADR-066).

**Por qué una región delimitada para la ligadura.** Cambiar la ligadura es reemplazar una línea existente. Buscarla por su contenido obligaría a la herramienta a adivinar sobre código que el equipo pudo haber tocado. Las marcas de apertura y cierre declaran en el archivo qué parte es cableado generado: lo de adentro es de la herramienta, lo de afuera del equipo.

**Consecuencia.** Un producto derivado con una versión anterior de la herramienta no tiene las cuatro marcas nuevas, y la composición lo rechaza nombrando la marca que falta (regla 7 del doc 2 §9). No se adoptó una migración automática: insertar marcas en código ajeno es exactamente lo que la regla de no adivinar prohíbe. Hoy no hay productos derivados fuera de los de verificación, así que el costo real es nulo; cuando los haya, la salida es derivar de nuevo o agregar las marcas a mano, y el mensaje lo dice.

**Qué cambió (2026-11-09, ADR-176).** Los puntos de inserción dejaron de ser constantes del código de la herramienta y pasaron a ser un dato: la plantilla los declara en su `productShape`, el producto los copia en su `project.json` al derivarse, y el módulo declara a qué forma sirve. Lo que esta decisión describía en prosa quedó **comprobable**, incluido el supuesto que dejaba implícito —«el producto derivó del activo base que escribió esas marcas»—, que nadie verificaba y que ahora se comprueba por los dos lados: la composición rechaza un módulo que reemplaza una región que la forma del producto no declara, y rechaza un producto al que le falta un punto que su propia forma declara. Sobreviven intactas las dos razones de esta decisión: la región delimitada para no adivinar sobre código que el equipo pudo tocar, y el rechazo nombrando la marca que falta en vez de insertar marcas en código ajeno. **El conteo de este título quedó histórico**: eran cinco aquí, seis cuando las regiones absorbieron los `imports` de una ligadura, siete con ADR-130 y **ocho** desde la ronda del segundo módulo, que es lo que `nestjs-hexagonal@1` declara.

**Traza.** RF-06, RF-07, ADR-057, ADR-066, ADR-067, ADR-130, ADR-176, Doc 2 §6, Doc 5, Doc 7 de la Fase 2.

---

## ADR-103 · El plan de cambios gana modo `modify`, dos clases nuevas y respaldo del conjunto tocado

**Estado:** Revisada · 2026-10-31 · Doc 2 · revisa ADR-057

**Contexto.** ADR-057 fijó un plan de tres clases —`write`, `copy`, `edit-at-marker`— con la regla de que el destino debe no existir o estar vacío, sin sobrescritura ni fusión. Esa regla es correcta para derivar y hace imposible modificar un producto existente, que es lo que esta fase necesita. El propio ADR-057 dejó declarado el límite y su salida: «La Fase 3 lo resolverá con una copia de respaldo del conjunto tocado».

**Decisión.** El plan declara su modo. En `create` rige la regla de ADR-057 sin cambios. En `modify` el destino debe existir y traer un registro de producto, y se admiten dos clases nuevas: `rewrite`, que reemplaza el contenido completo de un archivo que ya existe, y `replace-region`, que reemplaza lo que hay entre dos marcas sin tocar el resto. Antes de mover nada, el núcleo copia cada archivo que el plan modifica, y si algo falla restituye las copias.

**Lo que no cambia.** Una operación sigue sin escribir: produce un plan como dato y el núcleo lo aplica. Las clases nuevas son datos, no una puerta para que la operación toque el disco. `--dry-run` sigue imprimiendo el plan completo y gana valor, porque ahora muestra qué archivos existentes cambiarían.

**Por qué no bastaba `edit-at-marker`.** Declarar la dependencia del módulo y escribir la entrada del registro son reemplazos de archivos JSON completos, no inserciones en un marcador. Forzarlos como inserción obligaría a marcar archivos de datos con comentarios, que JSON no admite.

**Traza.** RF-06, RF-07, RF-11, ADR-057, Doc 2 §7, Doc 5, Doc 6.

---

## ADR-104 · La entrada de módulo guarda el cableado aplicado y la huella de cada archivo generado

**Estado:** Aceptada · 2026-10-31 · Doc 2

**Contexto.** El registro del producto reserva `modules: []` desde la Fase 2 con su formato fijado (ADR-070), pero el contenido de una entrada quedó sin definir. La actualización necesita saber dónde quedó el cableado y si el equipo editó lo que la herramienta escribió, porque RF-13 exige preservar el código propio del producto.

**Decisión.** Cada entrada guarda identificador, paquete, versión, versión de contrato, fecha de incorporación en UTC y un bloque `wiring` con los marcadores editados, las regiones reemplazadas, los archivos generados con su huella `sha256` y las variables de configuración agregadas.

**Por qué la huella y no una copia.** Una copia duplicaría código del producto dentro de su propio registro y envejecería con cada edición. La huella responde la única pregunta que importa al actualizar: si el archivo sigue siendo el que la herramienta escribió. Si no lo es, la actualización informa y no lo toca.

**Consecuencia.** La consulta responde qué hay incorporado y en qué versión sin leer el código (RF-08), y la comparación contra el catálogo detecta lo desactualizado (RF-12). Retirar un módulo, que no es de esta fase, queda construible más adelante porque el cableado quedó escrito entero.

**Traza.** RF-08, RF-10, RF-11, RF-12, RF-13, ADR-070, ADR-083, Doc 2 §8, Doc 6.

---

## ADR-105 · El módulo aporta plantillas, nunca clases base: lo generado pasa a ser del producto

**Estado:** Aceptada · 2026-10-31 · Doc 2

**Contexto.** El adaptador del repositorio de un agregado realiza un puerto de dominio, que es del producto, apoyándose en la capacidad técnica que el módulo provee. Si el equipo tiene que escribirlo entero a mano, incorporar el módulo deja al producto sin persistir hasta que alguien escriba código, y RF-06 pide que el módulo quede integrado con un comando.

**Decisión.** Un módulo puede traer plantillas en su paquete, declaradas en su manifiesto, que la herramienta renderiza con el contexto del producto. Lo que producen es código del producto desde ese momento: el equipo lo edita sin pedir permiso, y la herramienta lo sabe porque guardó su huella.

**Por qué no una clase base del módulo.** La herencia entre un activo del catálogo y el código del producto crea un acoplamiento que ninguna de las dos partes controla por completo, y que la escala de adaptación no puede regular (MR-04 §5). Una plantilla renderizada corta el vínculo en el momento de la composición.

**Consecuencia.** Un cambio en la plantilla de una versión posterior del módulo no llega sola al producto. La actualización propone el archivo nuevo y, si la huella cambió, no lo pisa: lo informa. Es el precio de que el código generado sea del equipo, y es lo que RF-13 exige.

**Traza.** RF-06, RF-09, RF-13, MR-04 §4, §5, MR-05 (escala de adaptación), Doc 2 §5, Doc 3, Doc 6.

---

## ADR-106 · El contrato y el framework son `peerDependencies` del módulo

**Estado:** Revisada · 2026-10-31 · Doc 2 · **revisada el 2026-11-09 por ADR-181**

**Contexto.** El módulo exporta un módulo de NestJS y adaptadores que implementan puertos de `@bsl/contracts`. Declararlos como dependencias normales instala una segunda copia de cada uno dentro del módulo.

**Decisión.** `@bsl/contracts`, `@nestjs/common` y `@nestjs/core` se declaran como `peerDependencies` del módulo, con el mismo piso de Node que el activo base.

**Por qué.** Los tokens de inyección son símbolos, y dos copias del mismo paquete producen dos símbolos distintos: el producto pediría un adaptador por un token y el módulo lo habría registrado con otro, con un fallo en tiempo de ejecución que no dice nada. Es ADR-046 aplicado al framework además del contrato.

**Consecuencia.** El producto es el único dueño de la versión del framework y del contrato. Un módulo que exija un piso mayor que el del producto falla al instalarse, con un mensaje de npm que nombra el conflicto, que es preferible a fallar al arrancar.

**Qué se revisó (2026-11-09, ADR-181).** Lo sustantivo sigue firme: los tres paquetes son `peerDependencies` y el producto es el único dueño de la versión del framework y del contrato, por la razón de los dos símbolos. Lo que se revisa es la premisa tácita de que **el framework es del módulo**. No lo es: un módulo declara NestJS como peer porque el producto lo tiene, y que el producto lo tenga es parte de la **forma** del producto (ADR-176). El campo del manifiesto que se llamaba `nest` pasó a llamarse `composition`, y un módulo que sirva a una forma sin NestJS no declarará esos dos peers sin que ninguna razón de esta decisión cambie.

**Traza.** ADR-046, ADR-079, ADR-176, ADR-181, Doc 2 §3, Doc 3.

---

## ADR-107 · Forma del puerto de base de datos: tres operaciones y valores enlazados aparte

**Estado:** Aceptada · 2026-10-31 · Doc 3

**Contexto.** MR-04 §5 fijó la clase del puerto —conexión y gestión de transacciones, sin mención del dominio— pero no su forma. Un puerto demasiado rico convierte al contrato en infraestructura; uno demasiado pobre obliga a cada producto a inventar lo que falta.

**Decisión.** `DatabasePort` declara tres operaciones: `query` para lo que devuelve filas, `execute` para lo que no, y `withTransaction` como unidad de trabajo. Los valores se pasan siempre aparte de la sentencia, en un arreglo de `DatabaseValue`. Las fechas viajan como texto en ISO 8601, sin tipo propio en el contrato.

**Por qué los valores aparte.** Concatenar un valor dentro de una sentencia es la forma en que ocurre una inyección. Al no admitir otra forma, ningún adaptador del puerto puede aceptarla, y la propiedad se comprueba con una prueba que intenta cerrar la sentencia y borrar la tabla.

**Por qué `execute` no devuelve filas afectadas.** Ningún caso de uso de la línea lo necesita hoy. Agregarlo después es un cambio menor del contrato; quitarlo sería mayor.

**Efecto en la versión.** El puerto entra como submódulo nuevo, que es un cambio menor: `@bsl/contracts` pasa a `0.2.0` y el módulo declara `contractVersion: 0`, la versión mayor que implementa. Como consecuencia, el rango del activo base sube a `^0.2.0` y el pin de la herramienta al contrato también, porque un rango de intervalo sobre `0.x` no incluye la menor siguiente.

**Traza.** RF-09, MR-04 §5, MR-05, ADR-070, Doc 2 §10, Doc 3 §3, Doc 3 §11.

---

## ADR-108 · El motor es el relacional embebido en la plataforma de ejecución

**Estado:** Aceptada · 2026-10-31 · Doc 3

**Contexto.** El adaptador del puerto necesita un motor. Las opciones eran el motor embebido que la plataforma de ejecución ofrece por `node:sqlite`, un driver nativo de un motor embebido, un mapeador objeto-relacional, o un servidor relacional real.

**Decisión.** El adaptador usa el motor embebido de la plataforma. El paquete publicado no tiene dependencias de ejecución.

**Por qué.** Es la única opción que deja la capacidad verificable por comando en la máquina de quien desarrolla y en una tubería, sin levantar infraestructura y sin compilar nada al instalar, que es lo que la condición de llegada de la fase exige. El driver nativo agrega superficie de suministro en un entorno regulado para una capacidad que la plataforma ya ofrece. El mapeador lo descarta el marco, porque impondría una clase base que el producto extendería. El servidor real queda fuera del alcance del proyecto, que excluye la integración con infraestructura, y el puerto permite llegar a él sin tocar el dominio.

**Límite asumido.** `node:sqlite` es una interfaz de la plataforma y su estabilidad la fija Node, no este proyecto. Es el mismo tipo de dependencia que P-22 sigue para la bandera de Jest. El riesgo está contenido: si la interfaz cambia, el cambio alcanza un archivo —el adaptador— y no al puerto, al módulo ni a ningún producto.

**Traza.** RF-09, RNF-04, ADR-099, Anteproyecto §4 (fuera de alcance: infraestructura), MR-04 §5, Doc 3 §4, P-22.

---

## ADR-109 · El adaptador generado crea su tabla en el primer uso y rehidrata con la fábrica del agregado

**Estado:** Aceptada · 2026-10-31 · Doc 3

**Contexto.** La plantilla del adaptador de repositorio tiene que resolver dos cosas que el módulo no puede decidir por el producto: de dónde sale la tabla, y cómo se reconstruye el agregado desde una fila. El manifiesto no admite condicionales, así que la plantilla es una sola para todo producto.

**Decisión.** El adaptador generado crea su tabla con `CREATE TABLE IF NOT EXISTS` la primera vez que se usa, con el nombre del agregado en singular, y reconstruye el agregado llamando a su fábrica de inicio.

**Por qué no migraciones.** El esquema describe el dominio del producto, así que es del producto. Una herramienta de migraciones para la única tabla con que un producto nace es infraestructura sin trabajo que hacer. El límite queda escrito en el TSDoc del archivo generado: un producto con datos que preservar entre formas la incorpora cuando le toque.

**Por qué la fábrica de inicio.** La semilla del agregado no distingue crear de reconstruir. Agregar esa distinción desde el módulo sería imponer modelado de dominio desde el catálogo, que es lo que ADR-082 ya descartó para el asistente de atributos. Cuando el agregado gane invariantes de ciclo de vida, el equipo agrega su fábrica de rehidratación en un archivo que es suyo.

**Consecuencia.** Lo generado es del producto y la herramienta no lo pisa después: guarda su huella al incorporarlo y, si cambió, informa en lugar de sobrescribir (ADR-104, ADR-105).

**Traza.** RF-06, RF-13, ADR-082, ADR-101, ADR-104, ADR-105, Doc 3 §9, Doc 6.

---

## ADR-110 · El módulo lee su configuración por el puerto del producto, que la expone en un módulo global

**Estado:** Aceptada · 2026-10-31 · Doc 3

**Contexto.** El módulo necesita saber dónde está el archivo del almacén. Podía leer el entorno por su cuenta, recibir el valor como argumento de su método de registro, o leerlo por el puerto de configuración del producto. Hasta ahora el producto declara los tres puertos de la línea como proveedores de su módulo raíz, y un módulo importado no los alcanza: el contenedor de NestJS resuelve dentro del módulo que pide.

**Decisión.** El módulo inyecta el puerto de configuración y el de registro. Para que pueda hacerlo, el producto expone los tres puertos de la línea en un módulo global propio, que su módulo raíz importa.

**Por qué no leer el entorno dentro del módulo.** La configuración del producto se valida una sola vez al arrancar y falla nombrando la variable (RNF-05). Un módulo que leyera `process.env` por su cuenta se saltaría esa validación y el producto podría arrancar con un valor inválido.

**Por qué no pasarlo como argumento.** La expresión de registro del manifiesto quedaría con el valor adentro, o con una lectura del entorno en el punto de composición. Lo primero fija la configuración en el código; lo segundo la saca del esquema.

**Consecuencia.** La plantilla del punto de composición y el activo base ganan un módulo global, que se construye en el doc 5 junto con los puntos de inserción. Un módulo del catálogo puede, desde entonces, inyectar cualquiera de los puertos de la línea sin pedirle nada al producto.

**Traza.** RNF-05, ADR-067, ADR-101, ADR-102, MR-04 §1, Doc 3 §7, Doc 5.

---

## ADR-111 · La documentación OpenAPI es pieza del activo base, no módulo del catálogo

**Estado:** Aceptada · 2026-10-31 · Doc 4

**Contexto.** ADR-072 excluyó RF-04 de la Fase 2 y lo reasignó a esta, dejando abierto si se resolvía como módulo del catálogo o como pieza del activo base. El criterio de aceptación de RF-04 exige que la documentación quede disponible sin configuración adicional y refleje los endpoints del proyecto generado.

**Decisión.** La documentación de API es una pieza del activo base. Todo producto derivado trae su documento desde el primer commit y lo sirve en `GET /openapi.json`. No hay entrada de catálogo que incorporar.

**Por qué no un módulo.** El marco restringe lo que un módulo aporta a adaptadores de salida, con una única excepción declarada para las sondas de estado (MR-04 §3). Un documento de API describe la superficie de **entrada** del producto, que es su contrato con terceros, y para construirlo hay que conocer las rutas y los tipos expuestos de cada producto. Resolverlo como módulo exigía ampliar la excepción del marco y acoplar un activo genérico al dominio de cada producto. Es el caso que el índice de la fase anticipaba: cuando una decisión fuerza el marco, se busca la que no lo fuerza.

**Por qué no una herramienta externa que lea el código.** Agrega un paso que alguien tiene que ejecutar, contra el criterio de aceptación.

**Consecuencia.** El catálogo no gana una entrada, y la capacidad no depende de la operación de composición: un producto derivado antes de que exista el gestor también la tendría, si se vuelve a derivar.

**Traza.** RF-04, T-07, T-08, ADR-022, ADR-072, MR-04 §3, el índice de la fase, Doc 4 §2, P-15.

---

## ADR-112 · El documento se arma con los esquemas de validación del producto; las rutas se escriben al derivar

**Estado:** Aceptada · 2026-10-31 · Doc 4

**Contexto.** El riesgo de toda documentación de API es describir algo distinto de lo que el servicio hace. Las formas habituales de evitarlo —decoradores en el controlador, o un documento escrito a mano— tienen el mismo defecto: declaran por segunda vez lo que el código ya declara.

**Decisión.** El documento se arma con los esquemas que el servicio ya usa para validar: el del cuerpo de cada operación y el del tipo expuesto de salida, convertidos a JSON Schema en ejecución. Las rutas, los métodos y los códigos de estado se escriben como literal al derivar, con las mismas operaciones que escribieron el controlador. El título y la versión salen de la configuración.

**Lo que esto obliga.** El tipo expuesto de salida pasa de ser una interfaz de TypeScript a un esquema del que se infiere el tipo. Una interfaz no existe en ejecución, así que documentarla exigiría escribirla por segunda vez.

**Límite asumido.** Una ruta agregada a mano al controlador no aparece en el documento hasta que se agrega al archivo que lo arma. Las dos piezas nacen de la misma derivación y a partir de ahí son código del producto. El README del producto lo dice con esas palabras.

**Traza.** RF-04, ADR-022, ADR-065, ADR-082, Doc 4 §3, Doc 4 §4, Doc 4 §6.

---

## ADR-113 · Sin interfaz de exploración ni dependencia nueva para documentar la API

**Estado:** Aceptada · 2026-10-31 · Doc 4

**Contexto.** El hallazgo #8 de la revisión externa pedía Swagger y una forma de probar el servicio enseguida. La forma habitual es montar una interfaz de exploración dentro del producto.

**Decisión.** El producto sirve el documento y nada más. No se agrega una interfaz de exploración ni ninguna dependencia nueva.

**Por qué.** Montar la interfaz exige una dependencia en todo producto de la línea, o cargar un script desde internet, que no es admisible en el entorno al que la línea sirve. El documento se abre en cualquier visor, y la necesidad de probar enseguida ya la resuelve el README con ejemplos ejecutables (ADR-082).

**Consecuencia.** Quien quiera la interfaz la monta en su producto, que es código suyo, o la organización la publica una vez para todos los servicios a partir de sus documentos.

**Traza.** RF-04, RNF-04, ADR-082, Doc 4 §6, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` (#8).

---

## ADR-114 · El archivo generado del documento queda fuera del formateador del repositorio

**Estado:** Aceptada · 2026-10-31 · Doc 4

**Contexto.** El activo base es la salida de las plantillas y una prueba lo comprueba archivo por archivo (ADR-066). El documento de API se escribe como literal desde la herramienta, y el formateador del repositorio reordena ese literal de una forma que la herramienta no reproduce exactamente.

**Decisión.** El generador escribe el literal en el estilo del producto —comillas simples, claves sin comillas donde el lenguaje lo permite, y una línea por propiedad cuando no entra en el ancho— y el archivo del activo queda listado en `.prettierignore`.

**Por qué.** Si el formateador reescribe el archivo, el activo deja de ser idéntico a lo que la herramienta produce y la prueba de regeneración falla en cada formateo. La alternativa, reproducir el algoritmo del formateador dentro del generador, es trabajo sin fin para un archivo que nadie edita a mano.

**Traza.** ADR-066, Doc 4 §8.

---

## ADR-115 · La herramienta comprueba el manifiesto en código; el esquema queda para el editor y la verificación

**Estado:** Aceptada · 2026-10-31 · Doc 5

**Contexto.** El doc 2 fijó que el manifiesto de un módulo tiene su esquema JSON. La regla 10 del estándar de código valida los JSON declarativos con ajv dentro de `verify`. Pero el manifiesto lo lee la herramienta en ejecución, y ajv es hoy una dependencia de desarrollo: convertirla en dependencia de ejecución agrega superficie de suministro a una herramienta que hoy tiene tres.

**Decisión.** La herramienta comprueba en código lo que necesita del manifiesto, con mensajes que nombran el campo y dan un ejemplo. El esquema viaja en el paquete del módulo para que el editor ayude al escribirlo, y la prueba del propio módulo lo valida contra él con ajv, que es donde la regla 10 aplica.

**Por qué no basta el esquema.** Un esquema responde «no válido»; quien escribe un módulo necesita saber qué campo falta y cómo se escribe. El mensaje de la herramienta dice las dos cosas, en la forma que ADR-081 fijó para los rechazos.

**Consecuencia.** El doc 2 §4 se ajusta: la autoridad en ejecución es la comprobación de la herramienta, no la copia del esquema.

**Traza.** RNF-04, ADR-048, ADR-081, Estándar de código §10, Doc 2 §4, Doc 5 §3.

---

## ADR-116 · El renderizador de plantillas pasa al núcleo, porque dos operaciones lo usan

**Estado:** Revisada · 2026-10-31 · Doc 5 · revisa la ubicación fijada en el doc 4 de la Fase 2

**Contexto.** El motor de sustitución sin lógica (ADR-065) vivía en `src/operations/generate/render.ts`, porque una sola operación renderizaba plantillas. La composición también las renderiza: las que el módulo publica.

**Decisión.** El renderizador pasa a `src/core/templates/render.ts`. Su comportamiento no cambia: sustitución de marcadores, sin condicionales ni bucles, y error cuando un marcador no tiene valor.

**Por qué no importarlo de la otra operación.** Dos operaciones son hermanas: la regla de dependencia de la herramienta permite que una operación dependa del núcleo, no de otra operación. Importarlo de `generate` acoplaría la composición a la derivación por una pieza que no es de ninguna de las dos.

**Consecuencia documental.** El doc 4 de la Fase 2 nombra la ruta anterior en su árbol del paquete. Queda anotado para corregirlo con fecha, sin reescribir la evidencia de aquella fase.

**Traza.** ADR-054, ADR-065, Doc 5 §6, Fase 2 Doc 4 §4.

---

## ADR-117 · Un marcador es una línea de comentario propia, no una mención del marcador

**Estado:** Revisada · 2026-10-31 · Doc 5 · revisa ADR-057

**Contexto.** El escritor de planes buscaba el marcador con una comparación de contenido en cualquier parte de la línea. Al ejecutar la composición apareció el problema: el TSDoc del punto de composición **explica** dónde están los marcadores, así que la primera línea que contenía `bsl:repository-binding:start` era la prosa, y el reemplazo cayó dentro del bloque de documentación.

**Decisión.** Una línea es un marcador solo si, quitado su prefijo de comentario —`//` o `#`— y los espacios, es exactamente el marcador. La comprobación previa de la operación usa la misma noción, para que el rechazo y la escritura coincidan.

**Por qué importa más de lo que parece.** La documentación de un producto tiene que poder explicar sus propias marcas. Con la comparación anterior, documentarlas rompía la herramienta, que es el peor incentivo posible.

**Traza.** ADR-057, ADR-102, Doc 5 §6, `plan-writer.spec.ts`.

---

## ADR-118 · Un plan puede tocar el mismo archivo varias veces; la ruta se mueve una sola vez

**Estado:** Revisada · 2026-10-31 · Doc 5 · revisa ADR-057

**Contexto.** El escritor preparaba cada cambio leyendo el destino y después movía un archivo por cambio. La composición toca `app.module.ts` cuatro veces —dos marcadores y dos regiones—, así que cada cambio se preparaba sobre el original y el movimiento fallaba a partir del segundo.

**Decisión.** Cada cambio se prepara sobre lo ya preparado cuando el archivo está en la zona temporal, y el movimiento recorre las rutas distintas una sola vez, en el orden en que el plan las nombra por primera vez. El respaldo sigue la misma lista.

**Consecuencia.** El orden de los cambios de un plan pasa a ser significativo cuando varios tocan el mismo archivo, y la operación lo declara en su documento. Para la derivación nada cambia: un plan que crea no repite rutas.

**Traza.** ADR-057, RF-07, Doc 5 §5, Doc 5 §6, `plan-writer.spec.ts`.

---

## ADR-119 · El reemplazo de una ligadura incluye la región de su import

**Estado:** Aceptada · 2026-10-31 · Doc 5

**Contexto.** La primera versión del cableado insertaba el import del adaptador generado en el marcador de imports y reemplazaba la ligadura del repositorio. El producto compuesto dejaba de pasar su propio análisis estático: el import del adaptador en memoria quedaba sin usar, y la regla que prohíbe código muerto es de error.

**Decisión.** El import del adaptador del repositorio vive en su propia región delimitada, y el módulo la reemplaza junto con la ligadura. Un módulo no inserta imports sueltos para sus reemplazos: reemplaza la región que los contiene.

**Consecuencia.** El campo `imports` de una ligadura desaparece del manifiesto y de su esquema, porque las regiones lo cubren. El producto gana un punto de inserción más, seis en total.

**Por qué no relajar el lint del producto.** El producto compuesto tiene que superar su propia verificación sin excepciones añadidas: es la condición de llegada de la fase, y una excepción puesta para que el gestor funcione sería el gestor degradando el producto.

**Traza.** RF-06, RF-07, RNF-03, ADR-102, ADR-103, Doc 2 §6, Doc 5 §7.

---

## ADR-120 · La versión de un módulo no se fija en la herramienta: se resuelve y se registra en el producto

**Estado:** Aceptada · 2026-10-31 · Doc 5

**Contexto.** La herramienta fija con pines las versiones del activo base y del contrato (ADR-050), que es lo que hace reproducible una derivación. Un módulo también es un activo del catálogo, y había que decidir si se pina igual.

**Decisión.** No. La versión de un módulo viene de la invocación —`persistence@0.1.0`— o, si no se nombra, de la última publicada que el registro de paquetes informa. La versión resuelta queda escrita en el registro del producto.

**Por qué.** Pinar cada módulo obligaría a publicar una versión de la herramienta por cada versión de cada módulo del catálogo, que es la dependencia que el catálogo existe para evitar (RF-14, RF-16). La reproducibilidad que RF-05 exige es la de la derivación, y esa no cambia: el esqueleto del producto sigue saliendo de activos pinados.

**Consecuencia.** El puerto del registro de paquetes gana una operación: leer la última versión publicada. El adaptador la delega en el gestor de paquetes, así que ninguna credencial pasa por la herramienta.

**Traza.** RF-05, RF-11, RF-14, RF-16, ADR-050, ADR-104, Doc 5 §8.

---

## ADR-121 · Cada inserción de un módulo queda delimitada en una región propia

**Estado:** Revisada · 2026-10-31 · Doc 6 · revisa ADR-102 y ADR-103

**Contexto.** La composición insertaba su cableado después de cuatro marcadores. Al construir la actualización apareció el problema: para reemplazar lo que una versión anterior escribió hay que saber dónde empieza y dónde termina, y una inserción no lo declara. Buscarla por su contenido sería adivinar sobre un archivo que el equipo pudo tocar, y volver a insertar dejaría dos copias del mismo cableado.

**Decisión.** Lo que un módulo inserta se envuelve en una región nombrada con su identificador y el marcador donde entró —`bsl:module:persistence:modules`—, con el comentario que corresponde al archivo. El registro del producto guarda ese nombre junto al marcador, y la actualización reemplaza por región.

**Consecuencia.** Dos módulos pueden escribir en el mismo marcador sin pisarse, y el orden entre ellos deja de importar. Retirar un módulo queda construible, aunque no sea de esta fase. El precio son dos líneas de comentario por inserción, visibles en el código del equipo, que es lo que permite a la herramienta decir exactamente qué parte es suya.

**Consecuencia de código.** Lo que la composición y la actualización comparten —los archivos del producto, los marcadores, el nombre de una región, los nombres del producto y la huella— pasó a `src/core/modules/wiring.ts`. Dos operaciones hermanas no se importan entre sí: lo común es del núcleo, como ya ocurrió con el renderizador (ADR-116).

**Traza.** RF-07, RF-11, RF-13, ADR-102, ADR-103, ADR-104, ADR-116, Doc 5 §7, Doc 6 §7.

---

## ADR-122 · La actualización reescribe lo que la herramienta escribió y preserva lo que el equipo cambió

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** RF-13 pide que actualizar un módulo preserve el código propio del proyecto que lo consume. El módulo genera un archivo en el producto —el adaptador de repositorio— que desde ese momento es del equipo (ADR-105), y una versión nueva del módulo trae una versión nueva de esa plantilla.

**Decisión.** Antes de reescribir un archivo que generó, la herramienta compara la huella `sha256` de lo que hay en disco con la que registró al incorporarlo. Si coincide, lo reescribe. Si no, no lo toca, lo informa y conserva en el registro la huella anterior. El resto del cableado —dependencia, regiones, configuración y registro— se reescribe siempre, porque es lo que la herramienta escribió y nadie más mantiene.

**Por qué no fusionar.** Fusionar exigiría que la herramienta decidiera sobre código que no escribió, en un archivo que el equipo mantiene. El costo de no hacerlo está declarado: una mejora de la plantilla no alcanza sola a un producto cuyo equipo ya editó ese archivo, y tanto la consulta como la actualización lo dicen con el nombre del archivo.

**Dónde cae en la escala de adaptación.** Editar el adaptador generado es *sustituir el adaptador* según MR-05: el equipo se queda con su mantenimiento y el módulo sigue propagándose, porque lo que llega por el paquete es la capacidad técnica y no el archivo editado. No es una bifurcación, así que nada se marca como bifurcado.

**Traza.** RF-11, RF-13, ADR-104, ADR-105, MR-05 §2, Doc 6 §5, Doc 6 §6.

---

## ADR-123 · Una sola operación de consulta responde lo disponible, lo incorporado y lo desactualizado

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** RF-08 pide consultar qué módulos están disponibles y cuáles están incorporados; RF-12 pide informar si un proyecto tiene módulos desactualizados respecto del catálogo. Podían ser dos comandos.

**Decisión.** Una sola operación, `bsl status`, que lee el catálogo, el registro del producto y la versión disponible de cada módulo, y responde las tres cosas en una tabla. Debajo informa cada archivo generado que ya no es el que la herramienta escribió, y cada uno que desapareció.

**Por qué una.** Las tres respuestas salen de la misma lectura. Separarlas obligaría a leer dos veces lo mismo y a que el usuario cruzara dos salidas a mano para saber qué actualizar.

**Por qué informa los archivos cambiados.** Es exactamente lo que la actualización va a respetar, y quien decide actualizar necesita saberlo antes de hacerlo, no después.

**Traza.** RF-08, RF-12, ADR-060, ADR-122, Doc 6 §3.

---

## ADR-124 · La versión disponible de un activo resuelto desde una ruta local es la que esa ruta declara

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** La consulta y las dos operaciones que mueven versiones necesitan saber cuál es la versión disponible de un módulo. Preguntarle al registro de paquetes es la respuesta correcta cuando el activo viene del feed, y es un fallo sin sentido cuando el activo viene de una ruta local dada en la invocación: ese paquete no está publicado.

**Decisión.** Cuando la invocación da una ruta local para un activo, la versión disponible es la que esa ruta declara en su `package.json`. En los demás casos se consulta el registro.

**Por qué.** Lo disponible es lo que la resolución va a entregar. Así la consulta, la incorporación y la actualización dan la misma respuesta, y la verificación de la fase puede ejercitar el circuito completo sin depender del feed, como ya hacía la de la Fase 2 con el contrato empaquetado.

**Traza.** RF-08, RF-11, RF-12, ADR-050, ADR-120, Doc 6 §4, Doc 7.

---

## ADR-125 · La verificación del circuito no depende del feed: paquetes empaquetados y catálogo de prueba

**Estado:** Aceptada · 2026-10-31 · Doc 7

**Contexto.** El circuito de composición necesita un producto que reciba el módulo como lo recibiría un equipo. El módulo no está publicado, y la entrada del catálogo está en `proposed` hasta que lo esté (ADR-100).

**Decisión.** La verificación empaqueta el contrato y el módulo con el gestor de paquetes, instala el producto desde esos tarballs, y trabaja sobre una copia del catálogo con la entrada en `active`. La versión posterior del módulo, con la que se prueba la actualización, es otra copia con su versión y una variable de configuración más.

**Por qué.** Una verificación que dependiera de que alguien publicó algo no sería reproducible, y fallaría por una razón distinta de la que se está comprobando. Es el mismo criterio que la Fase 2 aplicó al contrato, por el que `verify:generation` tampoco toca el feed.

**Qué queda sin verificar por esta decisión.** Que la resolución desde el registro funcione para un módulo, y que dos productos convivan con versiones publicadas distintas (RNF-06). Las dos se comprueban al publicar, y están declaradas como límite en el doc 7 §9 y seguidas por P-28.

**Traza.** RF-14, RNF-06, ADR-100, ADR-124, Doc 7 §4, Doc 7 §9, P-28.

---

## ADR-126 · Cada regla se comprueba rompiéndola, y el rechazo tiene que dejar el producto idéntico

**Estado:** Aceptada · 2026-10-31 · Doc 7

**Contexto.** La Fase 2 fijó que cada pieza nueva se verifica rompiéndola a propósito. La composición agrega una exigencia que la derivación no tenía: trabaja sobre un producto que ya existe, así que un rechazo mal hecho puede dejarlo a medias.

**Decisión.** La verificación rompe cinco reglas a propósito y, en cada una, exige dos cosas: que el mensaje diga lo que corresponde —incluida la lista de lo que el catálogo sí ofrece— y que el archivo que el cambio habría tocado sea **byte por byte el mismo** después del rechazo.

**Por qué la segunda exigencia.** Un rechazo que deja cableado a medias es peor que no rechazar: el producto queda en un estado que nadie pidió y que la herramienta no sabe deshacer. Comprobar solo el mensaje dejaría eso fuera de la red.

**Cómo se consigue el quinto caso.** El rechazo de un segundo adaptador para el mismo puerto necesita otro módulo. La verificación lo fabrica copiando el real y cambiándole identificador y paquete, y no lo agrega al catálogo de la línea: existe mientras dura la comprobación, porque lo que se prueba es la regla.

**Traza.** RF-06, RF-07, ADR-086, ADR-081, Doc 2 §9, Doc 7 §5.

---

## ADR-127 · La verificación de la composición entra en `check:push`, no en `check:commit`

**Estado:** Aceptada · 2026-10-31 · Doc 7

**Contexto.** El circuito instala dos productos reales y arranca uno dos veces, así que tarda minutos. Las puertas del repositorio son dos: una de confirmación y otra de publicación.

**Decisión.** `check:commit` mantiene lo que tarda segundos —formato, lint, typecheck, las 184 pruebas y los artefactos declarativos— y `check:push` suma la verificación de cada paquete, la de generación, la de composición y las auditorías.

**Por qué.** Una puerta de confirmación que tarda minutos se termina salteando, y una puerta que se saltea no verifica nada. La de publicación se corre menos veces y es donde el costo se justifica.

**Traza.** ADR-049, ADR-086, Doc 7 §7.

---

## ADR-130 · Un módulo escribe también en la documentación del producto, en una región que él declara

**Estado:** Revisada · 2026-11-02 · Doc 2 · revisa ADR-102

**Contexto.** La fase cerró con el circuito comprobando que un producto compuesto persiste de verdad y que el dato sobrevive al reinicio. Al volver a pasar la revisión externa del 2026-10-28 por el artefacto terminado apareció que ese mismo producto, en su `README.md`, sigue diciendo *every record is lost when the process stops*. No es un texto desactualizado por descuido: el manifiesto del módulo declara cableado sobre `src/app.module.ts` y sobre la configuración, y nada más, porque los seis puntos de inserción que ADR-102 y el doc 2 fijaron son todos de código.

Es el hallazgo central del informe reaparecido un nivel más arriba. **ADR-082** lo cerró para la derivación: el producto declara su alcance fuera del código, porque el TSDoc era honesto y nada afuera lo decía. La composición volvió a abrirlo, porque incorporar un módulo cambia lo que el producto es y no lo que el producto dice de sí mismo.

**Decisión.** Lo que el producto declara de sí mismo es parte de lo que un módulo cambia. El manifiesto puede declarar un binding sobre un archivo de documentación del producto, y lo hace con el mismo mecanismo que usa para el código: una región delimitada, declarada por el módulo, reemplazada por la operación. `@bsl/persistence` declara la región `bsl:persistence` del `README.md`, que es el séptimo punto de inserción.

El marcador admite una tercera forma de comentario, la de Markdown —`<!-- bsl:persistence:start -->`—, junto a las dos que ya reconocía. **ADR-117** sigue firme: es una línea de comentario propia y no una mención del marcador.

**Por qué lo declara el módulo y no la operación.** La alternativa era que `bsl add` reescribiera la sección de persistencia sin que el manifiesto dijera nada. Cuesta menos y no toca el esquema, y deja a la herramienta conociendo un módulo por su nombre, que es exactamente lo que **ADR-101** evitó: el manifiesto viaja en el paquete para que incorporar un módulo nuevo no cueste una versión de la herramienta. Con la decisión tomada, el próximo módulo del catálogo se documenta solo; con la alternativa, cada módulo nuevo habría pedido una rama más en la operación.

**Por qué no se resuelve regenerando el README.** Reescribirlo completo al componer perdería lo que el equipo haya escrito en él, contra RNF-02 y contra ADR-122, que es la regla que distingue lo que la herramienta escribió de lo que el equipo cambió. La región acota el cambio a lo que la línea posee.

**Qué cambia del marco.** `MR-04` §5 reparte entre lo que es implementación —va en el paquete— y lo que es cableado —se genera—, y no dice nada de prosa. Esta decisión agrega que la descripción que el producto hace de sí mismo sigue al cableado, y queda por anotar en ese documento.

**Consecuencia.** `bsl add persistence` rechaza un producto cuyo `README.md` no delimita la región, con el mismo mensaje que ya daba para un marcador ausente: derivar de nuevo, o agregar la región donde va. Un producto derivado con `@bsl/cli` `0.8.0` o antes la necesita antes de incorporar el módulo. La entrada de módulo del registro guarda ahora tres regiones en lugar de dos, así que la actualización reaplica también la del README.

**Verificación (2026-11-02).** `verify:composition` corre el circuito completo y agrega tres comprobaciones sobre el producto compuesto: que el aviso de pérdida de datos ya no está, que el README dice que los registros sobreviven al reinicio, y que nombra el adaptador que el módulo generó. La incorporación pasó de nueve a diez cambios aplicados. Comprobado rompiéndolo, como pide **ADR-126**: quitado el binding del manifiesto, el circuito falla con `The readme still claims the product stores nothing after the module went in.`

**Traza.** RF-06, RF-07, RF-13, RNF-02, ADR-082, ADR-101, ADR-102, ADR-117, ADR-121, ADR-122, ADR-126, Doc 2 §6, Doc 5 §6, Doc 5 §7, Doc 7 §5, MR-04 §4, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G1-a.

---

## ADR-146 · El documento OpenAPI lleva el identificador y el grupo que el estándar da a cada operación

**Estado:** Revisada · 2026-11-03 · Doc 4

**Contexto.** El doc 4 construyó el documento OpenAPI del producto derivándolo de lo que el producto ya declara: una ruta por operación elegida, con el esquema de su entrada y de su salida. Lo que el documento **no** llevaba era ningún rastro del estándar: el `operationId` era el nombre local del caso de uso en camelCase —`initiateTermDeposit`— y el `tags` era el título del agregado.

Eso bastaba mientras la forma de las rutas fuera una sola. Con la forma de ruta convertida en punto de variación (ADR-140), deja de bastar: dos productos de la misma capacidad sirven rutas distintas, y si además nombran sus operaciones con su vocabulario local, no queda nada en el documento que permita leerlo contra el publicado. La alineación con el estándar pasaría a ser una afirmación del README y no un hecho comprobable, que es exactamente lo que MR-02 §3 prohíbe para el metadato de dominio.

**Decisión.** El documento OpenAPI del producto lleva, para cada operación, el **identificador y el grupo que el estándar le da**, en las dos formas de ruta:

| | Qué lleva | Ejemplo |
| :-- | :-- | :-- |
| `operationId` | El action term más el calificador, como el estándar lo publica | `Initiate`, `Update`, `ExecuteInterest` |
| `tags` de una operación del control record | El nivel y el control record | `CR - TermDepositFacility` |
| `tags` de una operación de behavior qualifier | El nivel y el qualifier | `BQ - Interest` |

El `summary` sigue siendo el de la línea, en inglés claro: el del documento oficial trae un código de nivel de dos letras delante —`InCR`, `ReBQ`— que no aporta a quien lee el documento del producto.

**Por qué el identificador y no el nombre local.** El `operationId` es lo único del documento que no depende de la forma de las rutas ni del vocabulario del equipo. Con él, el documento de un producto en forma de recurso sigue siendo comparable con el publicado, operación por operación. Es la razón por la que el documento existe.

**Consecuencia.** El documento declara además los **dos** parámetros de ruta de una operación de behavior qualifier. Declarar solo el del control record dejaba un documento con el que no se puede llamar a la operación.

Para una capacidad declarada fuera del catálogo (ADR-143) el grupo es `CR - <control record declarado>`. El tag nombra el nivel y no la procedencia; lo que dice que el estándar no publica esa capacidad es `declaredOutsideCatalog` en el registro del producto.

El circuito de generación gana una comprobación por producto: cada operación del registro tiene que aparecer en el documento con el identificador del estándar y bajo el grupo de su nivel. Se rompió a propósito quitando el prefijo `BQ - ` y el circuito lo rechazó nombrando la operación.

**Verificación (2026-11-03).** `verify:generation` comprueba los cuatro productos; `term-deposit-api` sirve diez rutas en forma `bian` y `deposit-rest-api` las sirve en forma de recurso, los dos con los identificadores del estándar.

**Traza.** RF-04, ADR-111, ADR-112, ADR-113, ADR-140, ADR-142, ADR-143, MR-02 §3, Doc 4, documento OpenAPI de `Term Deposit` v14.0.

---

## ADR-156 · El segundo módulo del catálogo es la observabilidad, y su alcance es la exportación

**Estado:** Revisada · 2026-11-05 · Doc 1 · revisa ADR-095

**Contexto.** ADR-095 construyó un módulo y dejó el resto del catálogo declarado como crecimiento, con el orden del doc 1 §10. RF-09 pide un módulo funcional y su criterio de aceptación declara que las demás capacidades quedan como catálogo a construir después, así que un segundo módulo no es deuda: es alcance que el autor abre.

La primera de ese orden es **C-02, observabilidad**, y lo que le faltaba, según la tabla, era «decidir qué parte es independiente de la plataforma corporativa». Entre el cierre de la fase y hoy esa decisión se tomó tres veces desde el otro lado: **ADR-151** metió la traza del estándar W3C al activo base, **ADR-152** fijó lo que dice cada asiento con el modelo de datos de OpenTelemetry, y **ADR-153** puso todo fallo en un solo lugar. Las tres dejaron escrito, con el mismo argumento, qué queda del lado del módulo: exportar, el muestreo y las métricas.

Los cinco criterios del doc 1 §6, releídos contra el artefacto de hoy, dan a C-02 el primer lugar: es verificable por comando si se apoya en un protocolo publicado; cierra un hueco que el propio activo base declara; su contrato no lo fija la organización, que solo elige una dirección; y es el caso de composición que el primer módulo no ejercitó, porque no llena un hueco del producto sino que recibe lo que el producto ya produce.

**Decisión.** La línea construye `@bsl/observability` `0.1.0` como segundo módulo del catálogo, con la capacidad C-02 y un alcance acotado a **la exportación**: entrega a un colector las entradas del log, el span de cada request y las mediciones que el producto reporta, con muestreo y con una cola propia.

Lo que **no** entra, y la razón es del marco: un endpoint para que la plataforma **raspe** las métricas. El doc 2 §12 restringe un módulo a adaptadores de salida, porque la superficie externa del producto es su contrato con terceros; un `GET /metrics` sería una entrada. Es la misma frontera por la que RF-04 terminó siendo pieza del activo base y no módulo (**ADR-111**). Las mediciones se empujan al colector, que es además lo que el protocolo define.

**Por qué la observabilidad y no el consumo de servicios corporativos.** C-10 es el segundo del orden y lo que T-05 señala como lo más costoso de propagar, pero su valor está en los contratos reales de los servicios consumidos, que son privados, y el activo base todavía no trae cliente HTTP al que engancharlo. Queda en su lugar del orden, y con una razón más para ir después: la propagación saliente que ADR-151 dejó pendiente necesita primero ese cliente.

**Consecuencia.** El catálogo pasa a cuatro entradas y la segunda abre en `proposed`, como pide **ADR-100**, hasta que el paquete esté publicado. La línea tiene por primera vez **dos módulos**, y un producto puede llevar los dos a la vez, que es lo que el circuito comprueba.

**Verificación (2026-11-05).** `verify:composition` incorpora `@bsl/observability` al mismo producto que ya tenía `@bsl/persistence`, con el registro del producto declarando los dos módulos, y el producto pasa su propia verificación con ambos.

**Traza.** RF-09, RF-14, T-08, T-09, C-02, ADR-095, ADR-097, ADR-100, ADR-111, ADR-151, ADR-152, ADR-153, Doc 1 §6, Doc 1 §10, Doc 2 §12, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G11.

---

## ADR-157 · `TelemetryPort` entra al contrato como puerto que ningún adaptador del activo base satisface

**Estado:** Aceptada · 2026-11-05 · Doc 2

**Contexto.** El módulo tiene que recibir tres cosas del producto —las entradas del log, el span de cada request y las mediciones— y el marco prohíbe que un módulo declare un puerto propio (doc 2 §12): si lo hiciera, el producto dependería del módulo y la dirección de la dependencia quedaría invertida. El puerto va entonces en `@bsl/contracts`.

Había dos formas de entregarle esas tres cosas. La primera era que el módulo **reemplazara** el adaptador del `LoggerPort`, como anticipaba el propio TSDoc del puerto. La segunda, un puerto nuevo que recibe lo que el producto ya escribió.

**Decisión.** Entra un puerto nuevo, `TelemetryPort`, con tres operaciones —`record`, `span`, `measure`— y ningún adaptador del activo base lo satisface. El producto reporta a un puerto que puede no tener implementación, y por eso **todo consumidor lo inyecta como opcional**. Sin módulo, la telemetría se queda adentro del proceso y el producto responde exactamente igual.

**Por qué no reemplazar el adaptador del logger.** El asiento del log es del producto: **ADR-152** fijó qué dice, qué se iza al nivel superior y qué se redacta por nombre de clave. Un módulo que reemplazara el adaptador tendría que reimplementar el formato y la redacción, y el día que una de las dos cambiara, lo escrito en el stream y lo exportado dirían cosas distintas. Con un puerto nuevo, el adaptador del producto sigue siendo el único que decide la forma de una entrada y entrega **la misma entrada** al exportador. Lo que el nivel descartó tampoco se exporta, que es la consecuencia deseada: el producto no exporta lo que no está dispuesto a escribir.

**Por qué el puerto no tiene adaptador por defecto.** Un adaptador que no hace nada obligaría a elegir entre dos males: ligarlo en el módulo global del activo base y que el módulo del catálogo tuviera que reemplazar esa ligadura —un punto de inserción más, sobre un archivo que hoy no tiene ninguno—, o fingir una capacidad que no existe. La ausencia declarada es más honesta y más barata: el README del producto dice que nada sale del proceso, y lo dice en una región que el módulo reemplaza.

**Consecuencia.** `@bsl/contracts` pasa a `0.3.0`, que es el crecimiento menor que el doc 2 §10 describe: un submódulo nuevo con su puerto y su token. El activo base gana `src/infrastructure/logging/telemetry.ts`, que es donde se arma lo que se reporta, y con él los productos derivados pasan a 67, 39 y 42 archivos.

**Verificación (2026-11-05).** Las 98 pruebas del activo base incluyen que el logger reporta cada entrada escrita y ninguna que el nivel descartó, que el span de una request fallida sale con `failed` solo en un `5xx`, y que un producto sin módulo no falla al reportar.

**Traza.** RF-09, RNF-02, ADR-105, ADR-128, ADR-151, ADR-152, ADR-153, ADR-156, ADR-161, Doc 2 §10, Doc 2 §12, MR-04 §2.

---

## ADR-158 · El módulo exporta en el protocolo del estándar, con su muestreo y una cola acotada

**Estado:** Aceptada · 2026-11-05 · Doc 3

**Contexto.** El criterio 1 del doc 1 §6 exige que la capacidad se pueda comprobar por comando sin infraestructura corporativa, y el criterio 4 que el trabajo de grado no fije un contrato que pertenece a la organización. Un exportador los cumple los dos solo si habla un protocolo publicado.

**Decisión.** El adaptador habla el **protocolo OpenTelemetry en su codificación JSON sobre HTTP**, contra la dirección que `OTEL_EXPORTER_OTLP_ENDPOINT` nombra, y arma el cuerpo él mismo con `fetch`: **sin dependencias de ejecución**, como `@bsl/persistence`. Las seis variables que declara son las que el estándar nombra, de modo que un entorno ya preparado para un colector no necesita traducción.

Tres reglas gobiernan lo que sale:

| Regla | Forma |
| :-- | :-- |
| Muestreo | El del estándar: una traza que llegó de otro servicio conserva la decisión que ese servicio tomó, y solo una que este servicio abrió se decide por `OTEL_TRACES_SAMPLER_ARG`, sobre el final del identificador de la traza para que dos réplicas nunca discrepen |
| Cola | 2048 señales, la que el estándar fija por defecto. Lo que no entra se cuenta y se informa |
| Series | Acumulativas: una exportación reemplaza a la anterior, así un envío perdido no abre un hueco en la gráfica de una tasa |

El fallo de una exportación se informa por el logger y el lote se descarta. La telemetría no es el trabajo del servicio: un colector caído, lento o que rechaza no puede hacer fallar la request que se estaba atendiendo, ni crecer en memoria sin tope.

**Por qué el muestreo del estándar y no uno propio.** Es el mismo criterio de **ADR-139** y **ADR-151**: cuando hay estándar publicado, la línea no inventa. Y tiene consecuencia observable: muestrear una traza en un servicio y descartarla en el siguiente produce una traza con un hueco en el medio, que es peor que no tenerla.

**Consecuencia.** Las métricas se empujan y no se exponen (ADR-156), así que una plataforma que solo sabe raspar necesita un colector en el medio. El valor de `OTEL_EXPORTER_OTLP_HEADERS`, que es donde viaja la credencial del colector, **nunca se escribe en el log**: el informe de un fallo nombra la dirección y nada más.

**Verificación (2026-11-05).** 36 pruebas del módulo, y el circuito contra un colector de verdad: el producto exportó sus entradas, tres spans y la duración de sus requests, continuando la traza del llamador y sin responder bajo el span de quien lo llamó.

**Traza.** RF-09, RNF-01, RNF-02, C-02, ADR-108, ADR-139, ADR-151, ADR-156, Doc 1 §6, Doc 3, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G11.

---

## ADR-159 · Un módulo no puede recibir el puerto al que el activo base reporta lo que él exporta

**Estado:** Aceptada · 2026-11-05 · Doc 2

**Contexto.** El adaptador del módulo se escribió como se escribe cualquier adaptador de la línea: `@Injectable()` con sus puertos inyectados, entre ellos `LOGGER_PORT`, para informar una exportación fallida. Al ejecutarlo, el producto arrancó, atendió requests, dijo en su log que exportaba a un colector… y **no exportó nada**. Ni una señal, ni un aviso de error.

La causa es un ciclo que solo existe con este módulo: el logger del producto reporta cada entrada a `TelemetryPort` (ADR-157), y el adaptador que satisface ese puerto pedía `LOGGER_PORT`. El contenedor lo resolvió dejando al logger sin puerto, en silencio. El mismo grafo en una prueba de integración **sí** lo grita: `A circular dependency has been detected inside "ConsoleLoggerAdapter"`.

**Decisión.** Un módulo del catálogo no recibe por constructor un puerto que el activo base reporta a su propio puerto. El adaptador recibe el contenedor y **pide el logger la primera vez que tiene algo que informar**, cuando todo está construido. Al momento de construirse, el módulo no tiene arista hacia el logger y el ciclo no existe.

**Por qué no se rompe del lado del producto.** La alternativa era que el logger dejara de depender del puerto y recibiera la telemetría en el arranque, desde `main.ts`. Funciona, pero mete estado mutable en un adaptador del producto y pierde para la exportación las entradas escritas antes de esa entrega, que son justamente las del arranque. Romperlo del lado del módulo no cuesta nada al producto.

**Lo que esto deja escrito para el catálogo.** Es una condición de validez más, y general: un módulo que provee un puerto del que el activo base es *productor* no puede depender de otro puerto que el activo base haga depender del suyo. Vale para el módulo de observabilidad y valdrá para cualquiera que reciba lo que el producto produce.

**Consecuencia.** El activo base gana la prueba que habría atrapado esto: un módulo falso con la forma de un módulo de observabilidad —provee el puerto y necesita el logger— compone y recibe las entradas, y la variante que toma el logger por constructor **tiene que fallar**. La segunda es una prueba de regresión del ciclo, no del módulo.

**Verificación (2026-11-05).** Las dos pruebas pasan en el activo base, y el módulo prueba además que no pide el logger mientras se construye. El circuito, que antes terminaba sin una sola señal y sin un solo aviso, exporta.

**Traza.** RF-09, ADR-110, ADR-156, ADR-157, ADR-161, Doc 2 §2, Doc 2 §12, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G11-a.

---

## ADR-160 · En `0.x`, subir una menor del contrato obliga a republicar el activo base y cada módulo

**Estado:** Revisada · 2026-11-05 · Doc 2 · revisa el doc 2 §10

**Contexto.** El doc 2 §10 cierra con una afirmación: «Un contrato que sube de menor llega al producto en la próxima instalación sin intervención, que es lo que hace barato agregar puertos». Al subir el contrato a `0.3.0` por `TelemetryPort` esa frase resultó falsa, y por la razón que **P-30** ya había encontrado en otro lugar: en `0.x`, `^0.2.0` **no acepta** `0.3.0`. El rango que el propio documento prescribe pinea la menor.

**Decisión.** Queda registrado que, mientras la línea esté en `0.x`, un cambio menor del contrato obliga a mover el rango declarado en el activo base y en cada módulo del catálogo, y por lo tanto a publicar una versión de cada uno. `@bsl/persistence` pasó a `0.3.0` sin un solo cambio de código, solo por su rango.

**Por qué no se levanta con un rango más ancho.** `>=0.2.0 <1.0.0` lo resolvería, y es lo que se descarta: deja a un módulo declarando que implementa un contrato que todavía no existe, y la línea pierde la única señal que hoy dice contra qué se compiló. El costo de republicar es conocido y acotado, y se termina solo: al pasar a `1.0.0`, `^1.x` acepta toda menor y la frase del documento vuelve a ser cierta.

**Consecuencia.** La corrección se aplica al doc 2 §10 con su nota fechada. La `contractVersion` del manifiesto no se toca: sigue declarando la versión **mayor**, que es `0`, como fijó MR-05.

**Traza.** MR-05, ADR-046, ADR-106, ADR-157, P-30, P-52, Doc 2 §10.

---

## ADR-164 · El producto documenta su API como página, con el visor instalado y nunca desde internet

**Estado:** Revisada · 2026-11-06 · Doc 4 · revisa ADR-113

**Contexto.** **ADR-113** excluyó la interfaz de exploración con dos razones, y conviene leerlas separadas porque no son la misma: montarla exige **una dependencia en todo producto de la línea**, o **cargar un script desde internet**, que no es admisible en el entorno al que la línea sirve.

El requerimiento volvió del autor el 2026-11-06, con un propósito más preciso que el del hallazgo #8 que ADR-113 respondió: no es «probar enseguida», que el README ya resuelve con ejemplos ejecutables, sino **validar visualmente cómo está construida la API** en los ambientes de desarrollo y de prueba, y que la dirección de esa página salga en el log de arranque igual que la de las sondas.

**Decisión.** El producto sirve `GET /docs`: una página que renderiza el documento que `/openapi.json` ya sirve, con el visor de OpenAPI que todo el mundo lee, cargado **de la copia instalada con el producto** y nunca de internet.

| Pieza | Forma |
| :-- | :-- |
| El visor | `swagger-ui-dist` como **dependencia de desarrollo** del producto. No está en una instalación de producción, así que no cambia lo que un servicio desplegado carga |
| Qué se sirve | La página, y dos archivos del visor, cada uno en su propia ruta explícita. No hay ruta que componer ni directorio que exponer |
| Qué renderiza | `/openapi.json` del propio servicio, así que la página no puede divergir de lo que el servicio acepta, y cada operación se prueba contra ese servicio |
| Cuándo existe | `API_DOCS`, con `on`, `off` y `auto`. `auto` es el default y resuelve a prendida en todo ambiente salvo producción |
| Qué dice el log | Cuando la página responde, el asiento de arranque nombra su dirección al lado de la de las sondas |

Con la documentación apagada, `/docs` y sus dos archivos responden `404`: un servicio con la página apagada tiene **exactamente la superficie que tenía antes de que esta ruta existiera**.

**Por qué esto no contradice las razones de ADR-113.** La segunda razón no se toca: no se carga nada de internet, ni un script ni una fuente, y el circuito lo comprueba buscando `http` en la página servida. La primera se respeta donde importaba: ADR-113 protegía lo que un producto **desplegado** carga, y eso no cambia, porque una dependencia de desarrollo no está en una instalación de producción y la auditoría de RNF-04 corre con `--omit=dev`. Lo que ADR-113 dejó abierto —«quien quiera la interfaz la monta en su producto, que es código suyo»— es lo que esta decisión resuelve una vez para toda la línea, en lugar de que cada equipo lo rehaga: que es la razón de ser de una línea de producto.

**Por qué no un visor propio.** Era la alternativa sin dependencia alguna: una página escrita por la línea que renderizara el documento. Se descartó por una razón de propósito, no de costo: lo que el requerimiento pide es validar la API en la herramienta que el equipo ya sabe leer, y un visor propio obliga a aprender otro y nos deja manteniendo el que nadie pidió.

**Por qué no un comando de la herramienta.** `bsl docs` levantando el visor en la máquina de quien desarrolla tendría huella cero en el producto, y no cumple el requerimiento: la página se pide en ambientes de desarrollo y de prueba **desplegados**, donde no hay una CLI instalada.

**Consecuencias asumidas.** La instalación de desarrollo de todo producto crece lo que pesa el visor, unos diez megabytes, y eso no afecta ni a la imagen de producción ni a la auditoría. Prender `API_DOCS` en producción exige instalar ahí el visor, y expone la superficie de la API a quien llegue al servicio: es una decisión de quien opera el producto, y el default no la toma por él. Un producto derivado gana un archivo, `api-docs.controller.ts`, que viaja copiado.

**Verificación (2026-11-06).** El activo base levantado con `NODE_ENV=development`: `/docs` responde `200` como `text/html`, la hoja de estilos y el script del visor responden `200` desde `node_modules`, la página no contiene ninguna dirección `http` y el asiento de arranque lleva `docs` al lado de `health`. Con `NODE_ENV=production`: `/docs` y sus archivos responden `404`, el asiento de arranque no nombra `docs`, y `/openapi.json` y las sondas siguen respondiendo `200`. El circuito de generación comprueba las cuatro cosas sobre un producto derivado, y el activo base tiene nueve pruebas nuevas, entre ellas que la página no carga nada de internet.

**Traza.** RF-04, RNF-02, RNF-04, ADR-082, ADR-111, ADR-113, Doc 4 §6, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` (#8, G12).

---

## ADR-180 · El módulo declara a qué formas de producto sirve

**Estado:** Aceptada · 2026-11-09 · Doc 2 · extiende ADR-101

**Contexto.** **ADR-101** hizo que un módulo se describa a sí mismo, y con eso la herramienta no conoce ningún módulo por su nombre. Lo que el manifiesto nunca declaró es **a qué clase de producto sirve**: un módulo escribe en los puntos de inserción de un producto y liga sus puertos, así que sirve a una forma y no a todo producto de la línea. Mientras existió una sola forma eso no se notaba. Con la forma del producto declarada (ADR-176) y con el almacén de plantillas abierto (ADR-171), un módulo incorporado a un producto de otra forma es un producto roto en silencio: el cableado va a un punto que no está, o la operación falla a mitad nombrando un archivo.

**Decisión.** El manifiesto de un módulo declara `serves`, una lista de formas con su versión entera. La comparación es **por identificador y por versión entera, nunca por rango**: una versión de forma se mueve cuando un punto se mueve o desaparece, que es exactamente cuando el cableado de un módulo deja de aterrizar donde esperaba. Ser indulgente ahí convertiría un rechazo que nombra la causa en un producto roto sin aviso.

La comprobación **nunca necesita la plantilla**: la forma la lleva el producto en su registro, y la plantilla que lo derivó puede no estar instalada, no estar publicada o no existir. Se hace en tres lugares: como regla de la composición, antes de las ocho que ya había y antes de producir un solo cambio; como información en `bsl templates show` y en `bsl modules list`; y como parte de la verificación de cada activo.

**La cláusula de lectura, con su fecha y su fin.** `@bsl/persistence` y `@bsl/observability` están publicados con manifiesto `1.0` y sin `serves`, y cuando se publicaron existía **una** forma de producto. Un manifiesto que no declara `serves` se lee como si sirviera a `nestjs-hexagonal@1`. Esto es lo que hace que el orden de publicación de esta ronda no tenga ninguna restricción nueva: la herramienta nueva lee los módulos viejos, y los módulos nuevos entran en los productos viejos, cuyo registro sin `shape` se lee por la cláusula gemela de ADR-176. Las dos se retiran en `1.0.0`.

**Alternativas.** Declarar la compatibilidad en el catálogo, en la entrada del módulo. Se descarta por el argumento de ADR-101: la compatibilidad cambia con el módulo, y ponerla en el catálogo obliga a cambiar dos repositorios de forma coordinada para publicar una versión, con una desincronización que dejaría a la herramienta comparando contra la declaración de otra versión.

**Verificación.** Un paso nuevo del circuito de composición incorpora un módulo cuyo `serves` no coincide con el `shape` del producto, **construido rompiéndolo** como pide ADR-126: una copia del módulo donde lo único que cambia es su manifiesto, lo que hace el rechazo atribuible a la declaración y a nada más. El producto queda idéntico. Son dos pruebas más en `compose.spec.ts` —otra forma y otra versión de la misma forma— y cuatro en `product-shape.spec.ts`.

**Traza.** RF-06, RF-07, RF-14, ADR-101, ADR-102, ADR-126, ADR-171, ADR-176, Doc 2 §4 y §9, Doc 7 §5.

---

## ADR-181 · `nest` pasa a `composition`: el framework es propiedad de la forma, no del módulo

**Estado:** Revisada · 2026-11-09 · Doc 2 · revisa ADR-106

**Contexto.** El manifiesto de un módulo declaraba cómo entra al punto de composición del producto en un campo llamado `nest`. El nombre estaba equivocado sobre lo que el campo contiene: **entrar al punto de composición es lo que hace todo módulo de toda forma**, y en qué framework está escrito ese punto es una propiedad de la forma del producto, no del módulo. Con una sola forma el nombre pasaba por descriptivo; con `serves` declarado, un módulo de la forma `python-batch` tendría que llenar un campo llamado `nest`.

**Decisión.** El campo se llama `composition`. `nest` se sigue leyendo como alias durante todo `0.x`, porque hay dos módulos publicados que lo usan, y se retira en `1.0.0` junto con las otras dos cláusulas de lectura de esta ronda.

**Qué de ADR-106 sigue firme y qué se revisa.** Sigue firme lo sustantivo: `@bsl/contracts`, `@nestjs/common` y `@nestjs/core` son `peerDependencies` del módulo, y el producto es el único dueño de la versión del framework y del contrato, porque dos copias del mismo paquete producen dos símbolos distintos y un fallo en tiempo de ejecución que no dice nada. Lo que se revisa es la premisa tácita de que **el framework es del módulo**: no lo es. Un módulo declara el framework como peer porque el producto lo tiene, y que el producto lo tenga es parte de la forma. Un módulo que sirva a una forma sin NestJS no declarará esos dos peers, y eso no cambia ninguna de las razones de ADR-106.

**Traza.** ADR-046, ADR-101, ADR-106, ADR-176, ADR-180, Doc 2 §3 y §4.

---

## ADR-182 · La actualización comprueba lo que comprueba la incorporación

**Estado:** Aceptada · 2026-11-09 · Doc 6 · cierra una asimetría de ADR-122

**Contexto.** `compose.ts` comprueba ocho reglas antes de producir un solo cambio, y `upgrade.ts` **no repetía ninguna**: comprobaba que el producto tenga el módulo y que la versión sea distinta, y nada más. Eso no era una economía, era un hueco: un `bsl update` podía mover un módulo a una versión construida contra **otro mayor del contrato** —exactamente lo que la regla 3 de la composición rechaza— sin que nadie lo mirara, y con `serves` declarado podía además meter un módulo que cambió de forma.

**Decisión.** La actualización comprueba lo mismo que la incorporación en lo que depende de la versión a la que se mueve: que el módulo sirva a la forma del producto y que implemente el mismo mayor del contrato que el producto declara. Las reglas que solo tienen sentido al incorporar —que el producto no tenga ya el módulo, que el puerto no tenga ya adaptador, que el archivo a escribir no exista— no se repiten, porque al actualizar son falsas por construcción.

El mensaje del rechazo por forma dice lo que pasó, que es distinto de lo que dice al incorporar: *la versión incorporada sí cabía; el módulo cambió de forma, así que esto no es una actualización de este producto.*

**Lo que la actualización empezó a recordar.** Con `bsl modules remove` (ADR-183), lo que una región del producto decía **antes** de que el módulo la reemplazara pasó a ser dato del registro. La actualización lo **conserva del registro y no lo vuelve a leer del archivo**: a esa altura la región contiene lo que el módulo escribió, así que leerla otra vez grabaría al módulo como la cosa a restaurar cuando se lo quite. Es un detalle de una línea y es la diferencia entre que quitar un módulo funcione y que deje el producto ligado a sí mismo.

**Traza.** RF-12, RF-13, ADR-105, ADR-122, ADR-176, ADR-180, ADR-183, Doc 6 §4, Doc 7 §5.

---

## ADR-183 · Quitar un módulo restaura lo que la derivación escribió

**Estado:** Aceptada · 2026-11-09 · Doc 6 / Doc 7 · amplía el alcance de la línea

**Contexto.** La línea sabía incorporar un módulo, consultarlo y actualizarlo, y no sabía quitarlo. **Ningún requerimiento lo pide**: RF-06 a RF-13 cubren las tres primeras. Lo pidió el autor al revisar la superficie de comandos (P-59), y la decisión de construirlo es de alcance y es suya, declarada como tal. El argumento que la sostiene es de método y no de comodidad: **una decisión que no se puede deshacer no es una decisión, es un compromiso**, e incorporar un módulo lo era. Para una línea de productos cuyo valor depende de que los equipos prueben sus activos, el costo de probar uno tiene que estar acotado.

**Decisión.** `bsl modules remove <módulo>` deshace lo que la herramienta escribió, leyendo **solo el `project.json` del producto**: no resuelve el módulo, no lo descarga y no exige que siga existiendo en el catálogo. Quitar algo no debería depender de que la cosa esté ahí, y de paso es lo que hace que la operación funcione en un producto cuyo módulo quedó deprecado.

| Qué hace | Con qué criterio |
| :---- | :---- |
| Quita la dependencia del `package.json` | La escribió la herramienta |
| Borra las regiones que el módulo escribió, **con sus dos marcas** | La región se llama por el módulo, así que cuando el módulo se va las marcas se van. El punto de inserción del producto que la contenía **se queda donde está** |
| **Restaura** la región del producto que el módulo había reemplazado | Desde lo que el registro guardó de ella al incorporar. `compose.ts` lo graba con `readRegion`, que ya estaba exportada |
| Borra un archivo que el módulo generó | Solo si conserva la huella que la herramienta dejó. Si el equipo lo cambió, es suyo y se queda, y la operación lo dice (ADR-122, ADR-105) |
| Quita la entrada del registro | — |
| Reporta la consecuencia sobre cada puerto | Qué resuelve el producto desde ahora para cada token que el módulo ligaba |

**Rechaza antes de tocar nada** cuando un puerto quedaría sin adaptador y no hay qué restaurar: un producto compuesto por una versión anterior, que no grabó lo que la región decía. No cambia un byte y explica por qué. Una región que no liga ningún puerto y de la que el registro no se acuerda se deja como está, diciéndolo, porque dejar prosa de un módulo en un README es un defecto menor que dejar un producto que no arranca.

**El hallazgo que el circuito encontró, y que no era un defecto.** El paso del circuito que quita el módulo falló la primera vez porque el archivo generado **seguía ahí**. Era correcto: un paso anterior del mismo circuito edita ese archivo para probar que la actualización lo preserva, así que por el criterio de ADR-122 ese archivo es del equipo y la remoción lo conserva. Lo que el hallazgo mostró es una consecuencia que nadie había dicho: **un archivo conservado sigue importando el paquete que el producto acaba de dejar de declarar**, así que el producto no compila hasta que alguien decida qué hacer con ese archivo. La herramienta lo dice ahora en la advertencia; decidir qué hacer con lo que es del equipo no es de la herramienta.

**Verificación.** El circuito de composición pasó de 19 a 21 pasos y de 6 a **8 rechazos**. Los dos pasos nuevos quitan los dos módulos de un producto que los tiene, y el último comprueba lo que esto tiene que probar: que el producto **pasa su propia verificación otra vez sin ningún módulo incorporado**, que es la forma de decir que quitar un módulo deja un producto de la línea y no un producto a medias. Los dos rechazos nuevos son el de ADR-180 y el de este: un `remove` sin memoria de lo que el módulo reemplazó, construido borrando ese campo del registro. Ocho pruebas en `remove.spec.ts`, incluidas la restauración del README, el archivo conservado y el puerto que nadie liga.

**Traza.** RF-06, RF-07, RF-13, RNF-02, ADR-103, ADR-105, ADR-122, ADR-126, ADR-176, ADR-178, ADR-182, P-59, Doc 6 §5, Doc 7.

---

## ADR-190 · Un módulo en dos productos, con versiones distintas a la vez

**Estado:** Aceptada · 2026-11-09 · Doc 7 · cierra una brecha de declaración del objetivo específico 3

**Contexto.** El objetivo específico 3 del anteproyecto pide «un gestor de módulos reutilizables que permita incorporar funcionalidades transversales mediante contratos de integración definidos y **compartidos entre proyectos**», y el resultado esperado 3 pide que esas funcionalidades sean «incorporadas y **compartidas entre múltiples proyectos** de forma desacoplada». Las dos cláusulas dicen lo mismo y las dos dicen **más de uno**.

Hasta esta fecha nada lo mostraba. El circuito de composición trabajaba sobre **un** producto, y el de generación derivaba tres o cuatro **sin módulos**. La afirmación «compartido entre proyectos» descansaba en un argumento —el módulo es un paquete versionado, el cableado se renderiza con los nombres del producto, así que nada lo ata al primero que lo tome— y un argumento no es evidencia. Es además el argumento más fácil de romper sin que nadie lo note: un módulo cuyo adaptador quedara nombrado por el agregado del primer producto habría funcionado perfectamente en los circuitos y habría sido inservible en el segundo.

La brecha la encontró la auditoría de cumplimiento del anteproyecto de **ADR-184**, y su causa mecánica está ahí: el índice de la Fase 4 colapsaba los objetivos 2 y 3 en uno, y al colapsarlos perdía justamente esta cláusula.

**Decisión.** El circuito de composición incorpora **el mismo módulo a un segundo producto**, derivado de otra capacidad y con otro agregado, y comprueba lo que hace que el módulo sea reutilizable y no acoplado:

| Qué se comprueba | Por qué es lo que importa |
| :---- | :---- |
| El registro del segundo producto declara el módulo con su versión | Es la condición mínima: el módulo entró |
| El adaptador generado se llama `sql-party-reference.repository.ts` y la clase `SqlPartyReferenceRepository` | El cableado se nombra por **el agregado de cada producto**, no por el del primero |
| El archivo generado **no** contiene `TermDeposit` | Es la comprobación negativa, y es la que atrapa el acoplamiento: sin ella, un nombre filtrado del primer producto pasa desapercibido |
| La ligadura del segundo producto nombra `PARTY_REFERENCE_REPOSITORY` | El puerto de dominio es del producto, y el módulo liga el que ese producto declara |

**Y una comprobación que el objetivo no pedía, porque el circuito la regaló.** El segundo producto se compone **después** de que el primero fuera actualizado, así que los dos quedan con **versiones distintas del mismo módulo al mismo tiempo**: `deposit-api` con la versión posterior y `party-directory-api` con la anterior, cada uno con su propia entrada en su registro. Eso es exactamente el criterio de aceptación de **RNF-06** —«dos proyectos operan simultáneamente con versiones distintas de un mismo módulo»—, que la medición de requerimientos declaraba cumplido por la evolución comprobada y **sin comprobarse por ejecución**, porque exigía dos productos a la vez. Ahora se comprueba, y el circuito **falla si los dos quedaran en la misma versión**, de modo que el día que el orden de los pasos cambie y la coincidencia desaparezca, la puerta lo dice en vez de seguir en verde.

**Lo que esa comprobación mira, y lo que no.** Mira **lo que cada registro declara**, que es lo que una resolución posterior lee y lo que la línea posee. No compara los rangos de los dos `package.json`, y la razón es un hallazgo de la primera corrida: el rango del primer producto **ya no es el que la incorporación escribió**, porque el paso que lo instala lo apunta a un tarball local para que el circuito no dependa del feed. Comparar los dos rangos pasaba —`file:…tgz` contra `^0.4.0`— por una razón que no tiene nada que ver con lo que se quiere probar, y una comprobación que pasa por la razón equivocada es peor que no tenerla. Del segundo producto sí se comprueba el rango, que es `^` de la versión incorporada y lo escribió la operación.

**Por qué el segundo producto no corre su propia verificación.** Instalar y verificar un segundo producto agrega minutos a una puerta que ya instala tres veces, y no agrega evidencia sobre lo que esta decisión prueba: que el cableado se nombra por cada producto es una propiedad del plan de cambios, visible en los archivos que la operación escribió. Que un producto compuesto es conforme ya lo prueba el primero, cuatro veces. Queda declarado como el límite de esta comprobación.

**Consecuencia.** El circuito pasa de 21 a **22 pasos**, y los 8 rechazos siguen siendo 8. El objetivo específico 3 y el resultado esperado 3 quedan cumplidos **con evidencia por ejecución** y no por argumento, y RNF-06 queda comprobado en su criterio literal.

**Traza.** Objetivo específico 3, resultado esperado 3, RF-06, RF-07, RF-09, RNF-06, ADR-101, ADR-105, ADR-122, ADR-126, ADR-184, Doc 2 §8, Doc 7 §4 y §6.

---

## ADR-195 · Un solo tutorial, que viaja con la herramienta

**Estado:** Aceptada · 2026-11-09 · `packages/cli/TUTORIAL.md` · reparte con ADR-093 y ADR-094

**Contexto.** La documentación de uso quedó repartida en tres lugares de los que ninguno es el primero:
el camino en `packages/cli/TUTORIAL.md`, su §12 agregada al cerrar esta fase, y la referencia en el README
de `@bsl/cli`. Cada pieza es correcta. Lo que no existe es **el** documento que alguien lee para
empezar, y eso obliga a saber de antemano que el camino vive en el expediente de una fase y la
referencia en el README de un paquete. Nadie que recibe una herramienta sabe eso. El autor pidió **un
solo documento** de tutorial de uso e instalación, el que se le entrega a un desarrollador.

**Decisión.** Entra `packages/cli/TUTORIAL.md`, y entra **en el paquete publicado**: el `files` de su
`package.json` lo lista junto a `bin` y `dist`. El README abre con un enlace a él y conserva la
referencia.

| Archivo | Lector | Qué tiene |
| :---- | :---- | :---- |
| `TUTORIAL.md` | Quien recibe la herramienta | El camino de punta a punta, una vez y en orden |
| `README.md` | Quien ya la usa | La referencia: cada flag, el archivo de entrada, el catálogo de fallos |

**Por qué no en el expediente.** El reparto de `packages/cli/TUTORIAL.md` es que cada documento responde a
**un** lector, y el de un desarrollador que recibe la herramienta es el que menos razones tiene para
entrar a un expediente de tesis. El **`packages/cli/TUTORIAL.md` de esta fase** registra el tutorial y sus decisiones; el
tutorial se entrega con el paquete. Es el reparto que ADR-093 y ADR-094 aplicaron a los READMEs.

**Por qué no dentro del README.** Son dos lecturas y mezclarlas era el problema. Un tutorial se lee una
vez, en orden, haciendo lo que dice; una referencia se consulta en desorden buscando un flag. Un
documento que intenta las dos obliga a quien empieza a saltearse la mitad y a quien consulta a buscar
entre prosa.

**Por qué al final de la fase.** Un tutorial escrito antes de que la superficie esté completa documenta
algo que va a cambiar. Escrito al cerrar la fase que trajo las operaciones de módulo, cubre las cinco
operaciones, las dos plantillas y el contrato de forma.

**La decisión de método que lo hace valer: la salida transcrita es real.** Cada bloque se obtuvo
**corriendo** el comando. Eso encontró **tres defectos** que ninguna prueba veía, el peor que la regla 0
de ADR-180 **no se ejecutaba**, porque `compose` resolvía los puntos de inserción antes de comprobar la
forma. Están en ADR-194.

**Límite asumido.** La salida transcrita **se desactualiza en silencio**: `verificar-bloques.mjs`
compara bloques contra un archivo del repositorio, y la salida de un comando no es uno. No se agregó
una puerta que corra el tutorial: partirlo en un script lo convertiría en un circuito más, y los dos que
existen ya cubren lo que ejercita. Lo que el tutorial aporta no es cobertura sino **el orden en que
alguien lo usa**. Lo contiene una recomendación: al cerrar una ronda que cambie la superficie, volver a
correrlo y retranscribir lo que cambió.

**Consecuencia.** El `packages/cli/TUTORIAL.md` deja de ser donde se lee el camino y se conserva como el
registro de cómo se construyó, con una nota que remite al tutorial. Tres READMEs quedaron corregidos al
hacer la tabla del reparto: los de los dos módulos no decían **a qué forma de producto sirven**, que es
el dato que decide si se pueden incorporar, y el del monorepo seguía presentando la línea como «el
activo base del que todo producto se deriva». Ningún requerimiento cambia de veredicto: RNF-01 ya
estaba cumplido y queda mejor sostenido, porque la documentación de una operación dejó de depender de
saber dónde buscarla.

**Traza.** RF-02, RF-06, RF-12, RF-13, RNF-01, T-14, ADR-082, ADR-093, ADR-094, ADR-096, ADR-178, ADR-183, ADR-192, ADR-194, `packages/cli/TUTORIAL.md`, `packages/cli/TUTORIAL.md`.

---

## Decisiones pendientes de esta fase

Las decisiones abiertas al abrir la fase están enumeradas en `00-indice-de-fase.md`, con el documento donde cada una se resuelve. Mientras una siga abierta, no se registra acá: este log guarda lo decidido, no lo que falta decidir.

**Pendiente de aplicar a los documentos (2026-11-02).** ADR-130 agrega el séptimo punto de inserción y la forma de marcador de Markdown. Quedan por ajustar el doc 2 §6 y su nota de alineación, que declara que los puntos son seis; el doc 5 §6, donde la fila «Un marcador es una línea de comentario propia» describe las formas admitidas, y el doc 5 §7, que enumera los puntos de inserción. El doc 7 §5 gana las tres comprobaciones nuevas del circuito. Fuera de esta fase, el doc 5 §8 de la Fase 2 transcribe `README.md.tpl`, que ahora lleva la región; es un caso más de **P-21**.
