# Las operaciones del gestor

Construye las cuatro operaciones que convierten el mecanismo de derivación en un mecanismo de composición: incorporar un módulo del catálogo a un producto que ya existe, saber qué tiene el producto y qué ofrece el catálogo, moverse a una versión posterior sin perder lo que el equipo escribió, y deshacer la incorporación. Ninguna exige que nadie edite un archivo.

---

La composición es la primera operación de la herramienta que **modifica** en lugar de crear. La Fase 2 construyó el núcleo para derivar, que es escribir un árbol nuevo donde no había nada, y dejó declarado el límite: el destino debe estar vacío, sin sobrescritura ni fusión. Ese límite se levanta acá.

## 1. Las cuatro operaciones

| Comando | Qué hace | Requerimientos |
| :-- | :-- | :-- |
| `bsl modules add <módulo>[@versión]` | Incorpora un módulo del catálogo al producto | RF-06, RF-07, RF-10 |
| `bsl modules list` · `bsl status` | Qué módulos ofrece el catálogo, cuáles tiene el producto, en qué versión, cuáles quedaron atrás, y qué archivo generado cambió el equipo | RF-08, RF-12 |
| `bsl modules update <módulo>[@versión]` | Mueve un módulo incorporado a otra versión, reescribiendo solo lo que la herramienta escribió | RF-11, RF-13 |
| `bsl modules remove <módulo>` | Saca un módulo incorporado, restituyendo lo que reemplazó | Ninguno: §10 |

Las cuatro aceptan el directorio del producto y la vista previa del plan; `add` y `update` aceptan además instalar las dependencias al terminar. Las tres primeras se montaron sobre el núcleo de la Fase 2 **sin modificarlo en su interfaz**: agregar una operación es escribirla y registrarla.

**Por qué una sola operación responde lo disponible y lo desactualizado.** RF-08 pide consultar lo disponible y lo incorporado; RF-12 pide informar lo desactualizado. Las tres cosas se responden con la misma lectura —catálogo, registro del producto y versión disponible— y separarlas obligaría a leer dos veces lo mismo y a que quien consulta cruzara dos salidas a mano.

## 2. Qué hace la composición al invocarse

| Paso | Qué ocurre | Qué lo decide |
| :-- | :-- | :-- |
| 1 | Localiza el producto: busca su registro desde el directorio dado hacia arriba | El núcleo |
| 2 | Lee el catálogo y busca la entrada del identificador | El catálogo, resuelto en ejecución |
| 3 | Rechaza lo que no es un módulo o no está activo | Reglas 3 y 4 |
| 4 | Resuelve la versión: la de la invocación, o la última publicada | §5 |
| 5 | Resuelve el activo y deja su contenido en disco | El resolutor del núcleo, sin cambios |
| 6 | Lee el manifiesto del módulo y comprueba lo que la herramienta necesita de él | Doc 2 §3 |
| 7 | Comprueba las nueve reglas sobre el producto | Doc 2 §6 |
| 8 | Produce el plan de cambios | §3 |
| 9 | Con la vista previa, imprime el plan y termina | El modo de prueba del núcleo |
| 10 | Aplica el plan con respaldo de cada archivo que toca | §4 |
| 11 | Informa qué incorporó, qué puertos quedaron provistos, qué configuración apareció y qué archivos son ahora del equipo | §6 |

**Nada de esto conoce a la persistencia.** La operación no nombra ningún módulo: todo lo que escribe sale del manifiesto que el módulo publica.

![][image1]

## 3. El plan que produce

Diez cambios sobre siete archivos, en el orden en que se aplican.

| # | Cambio | Qué escribe |
| :-- | :-- | :-- |
| 1 | Reescritura del manifiesto del producto | La dependencia del módulo, con las dependencias ordenadas |
| 2 | Escritura del adaptador de repositorio | La plantilla del módulo, renderizada con los nombres del producto |
| 3 | Inserción en el punto de los imports | El import del módulo |
| 4 | Inserción en el punto de los módulos | La expresión de registro, dentro de la lista de imports del framework |
| 5 | Reemplazo de la región del import del repositorio | El import del adaptador generado, en lugar del de memoria |
| 6 | Reemplazo de la región de la ligadura | La ligadura del puerto de dominio al adaptador generado |
| 7 | Reemplazo de la región del README | Qué almacén usa el producto y si el dato sobrevive a un reinicio |
| 8 | Inserción en el punto de la configuración | La variable con su validación y su documentación |
| 9 | Inserción en el punto del archivo de entorno | El ejemplo y el comentario de la variable |
| 10 | Reescritura del registro del producto | La entrada del módulo |

**Por qué el README entra al plan.** Un producto que declara en su readme que persiste en memoria y que
acaba de incorporar el módulo de persistencia se contradice a sí mismo. La región la escribió la plantilla
para que el módulo la reemplace, y es la misma mecánica del cableado: lo de adentro es de la herramienta.

**Por qué el orden importa.** La vista previa ordena por ruta para que se lea; la aplicación respeta el orden declarado, porque varios de los cambios tocan el mismo archivo y cada uno se apila sobre el anterior.

## 4. Qué creció en el núcleo

| Pieza | Qué resuelve |
| :-- | :-- |
| Modo del plan | En modo de creación rige la regla de la Fase 2, el destino vacío. En modo de modificación el destino tiene que existir y traer un registro de producto |
| Clase de reescritura | Reemplaza un archivo completo que ya existe. El manifiesto y el registro del producto son JSON: no admiten un marcador en comentario |
| Clase de reemplazo de región | Reemplaza lo que hay entre dos marcas y deja el resto intacto |
| Respaldo del conjunto tocado | Antes de mover nada, cada archivo que el plan modifica se copia. Si un cambio falla, se restituye lo movido y el producto queda como estaba |
| La escritura no pisa | En modo de modificación, escribir sobre un archivo que ya existe es un error, no una sobrescritura |
| **Una ruta se mueve una sola vez** | Apareció al ejecutar: tres cambios sobre el punto de composición intentaban mover el mismo archivo tres veces y fallaban. Cada cambio se prepara sobre lo ya preparado, y la ruta se mueve al final |
| **Un marcador es una línea de comentario propia** | Apareció al ejecutar: la documentación del punto de composición menciona sus marcadores, y la inserción caía dentro del bloque de documentación. Ahora un marcador se reconoce solo si la línea es ese comentario y nada más |

**Lo que no cambió.** Una operación sigue sin escribir: produce un plan como dato y el núcleo lo aplica. Las clases nuevas son datos, no una vía para que una operación toque el disco, y la vista previa gana valor: muestra qué archivos existentes van a cambiar.

## 5. Cómo se resuelve la versión del módulo

| Qué | Cómo se resuelve |
| :-- | :-- |
| El módulo con una versión en la invocación | Esa versión exacta |
| El módulo sin versión | La última publicada, consultada al registro de paquetes |
| El módulo resuelto desde una ruta local | La que esa ruta declara en su manifiesto |

**Por qué un módulo no se fija en la herramienta.** Pinar cada módulo obligaría a publicar una versión de la herramienta por cada versión de cada módulo del catálogo, que es exactamente la dependencia que el catálogo existe para evitar. La reproducibilidad no se pierde: la versión que se resolvió queda escrita en el registro del producto, y de ahí la lee la actualización.

**Por qué la ruta local también responde una versión.** Un activo resuelto desde una ruta no tiene versión publicada que consultar, y preguntarle al registro daría un fallo que no describe la situación. Lo disponible es lo que esa ruta trae, que es además lo que la resolución va a entregar. Así la consulta, la incorporación y la actualización dan la misma respuesta, y la verificación de la fase puede trabajar sin feed.

**Esto agregó una operación al puerto del registro**: leer la última versión publicada de un paquete. El adaptador la delega en el gestor de paquetes, como todo lo demás, de modo que la credencial del registro sigue sin pasar por la herramienta.

## 6. Qué queda en el producto, y qué informa la operación

*Salida real de la incorporación*

```
  >   Resolving @bsl/persistence@0.1.0
  ok  @bsl/persistence@0.1.0 resolved  0ms

@bsl/persistence@0.1.0 incorporated
───────────────────────────────────
  Product         deposit-api
  Ports provided  DATABASE_PORT
  Configuration   DATABASE_FILE
  Written         src/infrastructure/persistence/sql-term-deposit.repository.ts · Repository adapter of the aggregate, written on the database port
  ok  10 changes applied; the record of the product declares the module

Next steps:
───────────
  npm install
  review src/infrastructure/persistence/sql-term-deposit.repository.ts, which is yours from now on
```

El activo se resolvió por ruta local, de ahí la duración nula. La forma de la salida la decide el adaptador de consola y no el texto de cada mensaje: lo que la operación decide es qué escribe.

Lo que queda registrado en el producto —la entrada del módulo con su versión, sus puertos, el momento y su cableado completo— es el formato del doc 2 §7.

## 7. La consulta

*Salida real sobre un producto con el módulo incorporado y una versión posterior disponible*

```
Modules of deposit-api
──────────────────────
ID           PACKAGE           IN PRODUCT  PUBLISHED  STATE
───────────────────────────────────────────────────────────
persistence  @bsl/persistence  0.1.0       0.2.0      outdated
  src/infrastructure/persistence/sql-term-deposit.repository.ts was changed after 'persistence' was incorporated; an update will leave it as it is.

Next steps:
───────────
  bsl modules update persistence
```

| Columna | De dónde sale |
| :-- | :-- |
| Identificador y paquete | El manifiesto del catálogo, filtrado a los activos de tipo módulo |
| En el producto | El registro del producto. Un guión significa que no lo tiene |
| Publicada | La versión disponible (§5). Un guión significa que no se pudo averiguar |
| Estado | Lo que el producto **tiene** —incorporado, no incorporado, desactualizado— o el estado del catálogo cuando no está activo |

**La línea que no es una columna.** Debajo de la tabla, la consulta informa cada archivo generado cuyo contenido ya no es el que la herramienta escribió, y cada uno que desapareció. Está ahí porque es exactamente lo que la actualización va a respetar, y quien decide actualizar necesita saberlo antes.

**La consulta no escribe nada.** Es la misma razón por la que la Fase 2 construyó una operación de lectura antes que la de derivación: lo que depende del entorno tiene que poder ejercitarse sin efectos. Lee el catálogo, el registro del producto y la versión disponible; no resuelve el activo ni lo descarga.

**Y dice lo que el producto tiene, no lo que podría tener.** Decía `can be added` y `available` de módulos que la composición rechaza, porque la consulta no comprobaba la forma del producto. Lo encontró recorrer la herramienta de punta a punta para el tutorial, y no una prueba.

**Comparación de versiones.** Se comparan por partes numéricas, de izquierda a derecha. No se interpretan rangos ni etiquetas: la pregunta es si lo que el producto tiene quedó por detrás de lo disponible.

## 8. La actualización, y el criterio de preservación

*Salida real de la actualización, con una versión posterior que agrega una variable de configuración*

```
  >   Resolving @bsl/persistence@0.2.0
  ok  @bsl/persistence@0.2.0 resolved  0ms

@bsl/persistence updated from 0.1.0 to 0.2.0
────────────────────────────────────────────
  Product        deposit-api
  Configuration  DATABASE_FILE, DATABASE_BUSY_TIMEOUT_MS
  !   src/infrastructure/persistence/sql-term-deposit.repository.ts kept as it is: it was changed after the module was incorporated, so the update left it as it is
  ok  9 changes applied
```

| Qué | Cómo se toca |
| :-- | :-- |
| La dependencia del módulo | Reescritura, al rango de la versión nueva |
| El import del módulo y su registro en el punto de composición | Reemplazo de la región que ese módulo dejó al incorporarse |
| Las regiones que el módulo liga | Reemplazo, con lo que el manifiesto nuevo declara |
| Las entradas de configuración y del archivo de entorno | Reemplazo, de modo que una variable nueva aparece y una que el módulo dejó de pedir desaparece |
| Un archivo generado cuya huella coincide con la registrada | Reescritura, con lo que la plantilla nueva produce |
| Un archivo generado que el equipo cambió | **No se toca.** Se informa y se conserva la huella anterior |
| El registro del producto | Reescritura, con la versión nueva, el momento de la actualización y el cableado vigente |

Son **nueve** cambios y no diez como al incorporar: el archivo generado quedó fuera del plan porque el
equipo lo había cambiado. Con el archivo intacto son diez, los mismos que al incorporar.

**Ninguna inserción.** La actualización no inserta en marcadores: reemplaza regiones. Insertar otra vez dejaría dos copias del cableado del mismo módulo, y buscar la copia anterior por su contenido sería adivinar sobre un archivo que el equipo pudo tocar.

**El criterio de preservación.** RF-13 pide que la actualización preserve el código propio del proyecto que lo consume, y la herramienta lo resuelve con la huella que la incorporación guardó: antes de reescribir un archivo que generó, compara la huella de lo que hay en disco con la que registró.

| Caso | Qué hace | Por qué |
| :-- | :-- | :-- |
| La huella coincide | Reescribe el archivo con la plantilla de la versión nueva | Nadie lo tocó: el equipo recibe la mejora sin hacer nada |
| La huella cambió | No lo toca, lo informa y conserva en el registro la huella anterior | Es código del equipo desde que se escribió. Fusionarlo sería inventar una resolución de conflicto sobre código ajeno |
| El archivo ya no está | Lo vuelve a escribir | Un archivo borrado no tiene cambios que preservar |

**Dónde cae esto en la escala de adaptación.** Editar el adaptador de repositorio generado es **sustituir el adaptador**: el equipo se queda con su mantenimiento y el módulo sigue propagándose, porque lo que llega por el paquete —la capacidad técnica— no es lo que el equipo editó. Por eso la actualización no marca nada como bifurcado: bifurcar sería copiar los fuentes del módulo al producto y retirar la dependencia, que es otra cosa y la herramienta no la provoca.

**Lo que esta decisión cuesta.** Una mejora de la plantilla no alcanza a un producto cuyo equipo ya editó el archivo. La herramienta lo dice en la actualización y en la consulta, de modo que el equipo sabe que hay una versión nueva de ese archivo y puede compararla cuando quiera. Automatizar la fusión exigiría que la herramienta decidiera sobre código que no escribió.

**Qué conserva el registro.** El momento de la incorporación no se pisa: dice desde cuándo el producto tiene la capacidad, y el de la actualización dice desde cuándo la tiene en esta versión. La huella de un archivo preservado sigue siendo la de la versión en que se generó, porque es la referencia contra la que se comparó.

## 9. Las regiones nombradas, y lo que la actualización obligó

Para que una actualización pueda reemplazar exactamente lo que una versión anterior escribió, lo insertado tiene que estar delimitado. Cada inserción de un módulo queda envuelta en una región nombrada con el identificador del módulo y el punto donde entró, y el registro del producto guarda ese nombre junto al punto.

*Fragmento real del punto de composición de un producto compuesto*

```ts
  imports: [
    // bsl:modules
    // bsl:module:persistence:modules:start
    PersistenceModule.register(),
    // bsl:module:persistence:modules:end
    PlatformModule
  ],
```

| Consecuencia | Qué permite |
| :-- | :-- |
| La actualización reemplaza por región | Reescribir lo que escribió una versión anterior, sin buscarlo por contenido |
| Dos módulos en el mismo punto no se pisan | Cada uno tiene su región, y el orden entre ellos no importa |
| La remoción es construible | El cableado está delimitado y registrado, así que la operación no tiene que adivinar qué parte del producto era suya |

**El precio.** Dos líneas de comentario por inserción en el producto. Es visible en el código del equipo, y es el precio de que la herramienta pueda decir exactamente qué parte es suya.

## 10. La remoción

**Ningún requerimiento la pide.** Es una ampliación del alcance de la línea, decidida por el autor, con el argumento de que una decisión que no se puede deshacer no es una decisión sino un compromiso: incorporar un módulo lo era, y ahora el costo de probar uno está acotado.

| Propiedad | Qué significa |
| :-- | :-- |
| Lee solo el registro del producto | No necesita el registro de paquetes ni que el módulo siga existiendo |
| Restituye la región que el módulo reemplazó | Lo que el producto tenía antes vuelve a su lugar, desde lo que el registro guardó |
| Conserva lo que el equipo editó | Mismo criterio de huella que la actualización |
| **Rechaza antes de tocar nada** si un puerto quedaría sin adaptador | Un producto compuesto por una versión anterior, cuyo registro no guardó qué había antes, se rechaza nombrando el caso. Es el criterio de las marcas que faltan: no se adivina sobre código ajeno |

**Una consecuencia que apareció al verificarla, y que nadie había dicho.** Un archivo generado que el equipo editó y la remoción conserva **sigue importando el paquete que el producto acaba de dejar de declarar**, así que el producto no compila hasta que alguien decida qué hacer con él. La herramienta lo dice en su advertencia, y la decisión es del equipo y no de la herramienta.

## 11. Pruebas

| Qué prueba | Qué fija |
| :-- | :-- |
| El manifiesto del módulo, 7 pruebas | Que un paquete sin manifiesto no es un módulo; que un formato desconocido se rechaza; que el campo que falta se nombra con un ejemplo; que un identificador mal formado se rechaza; que lo opcional queda en listas vacías; y que un manifiesto que no es JSON lo dice |
| La composición, 9 pruebas | Que el plan trae exactamente los diez cambios y nada más, en su orden; que las plantillas se renderizan con los nombres del producto; que la dependencia queda ordenada; que el registro guarda el cableado y la huella; y las reglas que rechazan, cada una con su mensaje |
| La operación de incorporación, 7 pruebas | Que deja el producto declarando el módulo; que sin versión se consulta la publicada; que la vista previa no escribe; que se rechaza un módulo propuesto, un activo que no es módulo y un identificador inexistente listando lo que el catálogo ofrece; y que sin módulo nombrado se dice cómo se nombra |
| La actualización, 7 pruebas | Que el plan solo reescribe y reemplaza regiones, sin una sola inserción; que la dependencia se mueve de versión; que un archivo generado intacto se reescribe; que uno cambiado se preserva, se informa y conserva su huella; que el registro guarda versión, momento y configuración vigente; y los dos rechazos |
| La consulta, 5 pruebas | Que un módulo del catálogo que el producto no tiene aparece como no incorporado; que uno por detrás aparece como desactualizado con el comando que lo mueve; que uno al día no propone nada; que un archivo generado cambiado se informa; y que uno que desapareció también |
| El escritor del plan, 7 pruebas nuevas | Que la reescritura reemplaza y deja el resto; que el reemplazo de región toca solo lo que hay entre marcas; que varios cambios se apilan sobre el mismo archivo; que una mención del marcador en un comentario no se confunde con el marcador; que la escritura no pisa; que un fallo restituye el producto; y que no se modifica un destino que no existe |

**Las pruebas de la actualización trabajan sobre un producto compuesto por la propia operación de composición**, no sobre un árbol escrito a mano. Así nunca prueban contra una forma que la composición ya no produce.

## 12. Evidencia de ejecución

El circuito completo, corrido el 2026-11-11 con `npm run verify:composition -w @bsl/cli`, sobre un producto
derivado con la misma release:

| Paso | Resultado |
| :-- | :-- |
| Derivación del producto | Producto derivado con la plantilla nombrada |
| Los cinco rechazos previos a incorporar | Un activo que no es módulo, un módulo que el catálogo no tiene, un directorio que no es un producto, un módulo que no sirve a la forma del producto, y un README sin la región que el módulo reemplaza |
| Incorporación del módulo | `10 changes applied; the record of the product declares the module`, y el registro del producto declara el módulo y su cableado |
| Los dos rechazos con el módulo adentro | Un módulo que el producto ya tiene, y un segundo adaptador para un puerto que ya tiene uno |
| Verificación del producto compuesto | `passed its own verification with the module incorporated` |
| Arranque, escritura por su API y reinicio | `restarted and the record was still there`: **el dato sobrevive al reinicio** |
| Actualización | La versión se movió, el archivo que el equipo editó se conservó y la configuración nueva apareció; el producto volvió a superar su verificación |
| Segundo módulo | `declares @bsl/observability@0.2.0 beside the first module`, y el producto `exported 3 spans, its entries and the duration of its requests, continuing the trace of its caller` |
| El rechazo de la remoción | Un módulo cuyo registro no recuerda qué reemplazó |
| Remoción de los dos módulos | `passed its own verification again with no module incorporated` |

## 13. Límites declarados

| Límite | Razón |
| :-- | :-- |
| Un módulo no se incorpora al derivar | La derivación no toma módulos. Hacerlo agrega un camino más que probar y una pregunta más, y no resuelve nada que la incorporación no resuelva en el paso siguiente. La revisión externa lo pedía como selector de persistencia, y sigue siendo candidato |
| No se fusiona un archivo que el equipo cambió | Exigiría que la herramienta decidiera sobre código que no escribió. Lo informa y lo deja |
| No se baja de versión | Pedir una versión anterior aplica el cableado de esa versión: la herramienta no distingue subir de bajar, y no lo impide. Lo que no hace es deshacer migraciones de datos, que no existen |
| No se actualiza el contrato | Si una versión del módulo implementa otra versión mayor del contrato, la actualización no lo resuelve: el producto tiene que recibir ese contrato primero |
| Un producto compuesto por una versión anterior se rechaza | No tiene los puntos de inserción ni las regiones nombradas. La herramienta no inserta marcas en código ajeno: lo dice y nombra lo que falta |
| El catálogo tiene que ofrecer el módulo como activo | Mientras el paquete no esté publicado, la entrada está propuesta y la operación lo dice |

[image1]: <../Insumos/Diagramas/GM-03_fig1_camino_de_la_composicion.svg>
