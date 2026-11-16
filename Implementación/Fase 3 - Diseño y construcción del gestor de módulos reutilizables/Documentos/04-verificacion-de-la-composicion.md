# Verificación de la composición

Produce la evidencia de que el conjunto cumple la condición de llegada de la fase, y que la cumple por las razones que los documentos dan y no por casualidad.

---

Rige el mismo principio que el bloque de verificación de la Fase 2: **la verificación no modifica lo verificado**. Si acá aparece algo que no funciona, se corrige en el documento que lo construyó; la verificación no agrega funcionalidad.

## 1. Tres niveles

| Nivel | Qué prueba |
| :-- | :-- |
| Unidad | Que cada pieza decide lo que su documento dice: el manifiesto que se lee, el plan que se arma, las reglas que rechazan |
| Artefacto | Que lo declarativo es válido y que el activo de la plantilla sigue siendo la salida de sus plantillas |
| Circuito | Que un producto real recibe el módulo, arranca, persiste, sobrevive a un reinicio, se actualiza sin perder lo del equipo y vuelve a ser conforme sin ningún módulo |

**Por qué hace falta el tercer nivel.** Las operaciones se pueden probar enteras con dobles, y eso prueba que el plan es el correcto. No prueba que el producto resultante compile, que el framework resuelva el adaptador que el módulo registró, ni que el dato llegue al disco. Esas tres cosas solo las dice un producto en ejecución.

**Las pruebas de la actualización trabajan sobre un producto compuesto de verdad.** El doble no escribe a mano cómo quedó el producto: lo compone llamando a la operación de composición, así que no pueden pasar contra una forma que la composición ya no produce.

## 2. El circuito

Veintidós pasos, en este orden.

| Fase del circuito | Qué comprueba |
| :-- | :-- |
| Preparación | Compila la herramienta, el contrato y los módulos, y empaqueta lo que el producto va a recibir, que es lo que se publica y no lo que hay en el repositorio. Copia el catálogo con las entradas activas, escribe una versión posterior de un módulo con una variable de configuración más, y levanta un colector propio |
| Derivación | Deriva un producto con el activo de este repositorio, **nombrando la plantilla** |
| Rechazos antes de incorporar | Los cinco que no necesitan el módulo adentro: §3 |
| Incorporación | El registro del producto declara el módulo, su versión y el archivo que generó |
| Rechazos con el módulo adentro | Los tres restantes |
| Conformidad del producto compuesto | Lo instala desde los paquetes empaquetados y corre su verificación: análisis estático, pruebas y compilación |
| Ejecución | Arranca el producto, guarda un registro por su API y lo lee. El framework resuelve el adaptador que el módulo registró |
| Reinicio | Apaga, vuelve a arrancar y lee el mismo registro: **el dato sobrevive al reinicio** |
| Edición del equipo | Agrega una línea al archivo generado, como haría el equipo, y pide el estado: informa el módulo por detrás y el archivo cambiado |
| Actualización | Mueve la versión, conserva el archivo del equipo, agrega la configuración de la versión nueva, y el producto vuelve a superar su verificación |
| Segundo módulo | Incorpora el segundo módulo al mismo producto y comprueba contra el colector que las señales salen y que la traza del llamador se continúa |
| Segundo producto | Incorpora **el mismo módulo a otro producto, con otro agregado**, y comprueba que el cableado se nombra por el agregado de cada uno. Como el segundo se compone después de actualizar el primero, los dos quedan con **versiones distintas del mismo módulo a la vez**, que es el criterio literal de RNF-06 |
| Remoción | Quita los dos módulos del primer producto y comprueba que **vuelve a ser conforme sin ninguno** |

**El segundo producto no corre su propia verificación**, y es un límite declarado: lo que ese paso prueba es que el cableado se nombra por cada producto, visible en los archivos que la operación escribió, y que un producto compuesto es conforme ya lo prueba el primero cuatro veces.

**Por qué el colector es del script y no un contenedor.** La misma razón por la que el motor de la persistencia es el embebido en la plataforma y por la que el circuito no depende del feed: una verificación que necesita infraestructura para correr no se puede exigir en una puerta del repositorio. Treinta líneas alcanzan para comprobar lo único que importa acá, que es que las señales salen y con qué forma.

**Por qué no depende del feed.** Igual que la verificación de la Fase 2 empaqueta el contrato en lugar de instalarlo del registro, ésta empaqueta los módulos y usa una copia del catálogo. Una verificación que dependiera de que alguien publicó algo no sería reproducible, y fallaría por una razón que no es la que se está comprobando.

**Un hallazgo de la remoción, que no era un defecto.** La primera corrida falló porque el archivo que el módulo generó seguía ahí. Era correcto: un paso anterior lo edita para probar que la actualización lo preserva, así que por el criterio de la huella ese archivo es del equipo y la remoción lo conserva. Lo que el hallazgo mostró es la consecuencia que nadie había dicho, y que ahora el doc 3 §10 declara.

## 3. Lo que se comprueba rompiéndolo

Ocho rechazos, cada uno con una exigencia doble: que el mensaje diga lo que corresponde, y que el producto quede **idéntico** después del rechazo.

| Regla rota | Lo que se exige del mensaje |
| :-- | :-- |
| El módulo no sirve a la forma del producto | Que nombre las dos formas. La copia del módulo difiere **solo** en su manifiesto, lo que hace el rechazo atribuible a la declaración y a nada más |
| Se incorpora un activo que no es módulo | Que diga de qué tipo es el activo pedido |
| Se incorpora un módulo que no está en el catálogo | Que liste lo que el catálogo **sí** tiene |
| El README del producto no delimita la región que el módulo reemplaza | Que nombre la región que falta |
| Se invoca sobre un directorio que no es un producto | Que nombre el archivo que buscó |
| Se incorpora un módulo que el producto ya tiene | Que diga qué versión tiene y qué comando lo mueve |
| Se incorpora un segundo módulo que provee el mismo puerto | Que nombre el puerto y quién lo provee hoy |
| Se quita un módulo cuyo registro no guardó qué reemplazó | Que diga que quitarlo dejaría un puerto del producto sin adaptador |

![][cap1]

El primero de los ocho, ejecutado sobre un producto derivado de la plantilla de funciones. Lo que hay que leer es el mensaje: nombra **las dos formas**, la que el módulo sirve y la que el producto tiene, y dice por qué la incompatibilidad no es cuestión de esfuerzo sino de que el módulo escribe en puntos de inserción que esa forma no tiene. El código de salida es 1 y el producto queda sin tocar.

**Por qué se comprueba que nada quedó escrito.** Un rechazo que deja medio cableado puesto es peor que no rechazar: el producto queda en un estado que nadie pidió y que la herramienta no sabe deshacer. La verificación lee el archivo antes y después del rechazo y exige que sean el mismo.

**El rechazo del puerto ocupado necesita un segundo módulo.** Se construye en la propia verificación, copiando el módulo real y cambiándole el identificador y el paquete. No se agrega al catálogo de la línea: existe el tiempo que dura la comprobación, porque lo que se prueba es la regla, no el módulo.

## 4. Qué significa que el producto compuesto es conforme

| Comprobación | Cómo se hace | Requerimiento |
| :-- | :-- | :-- |
| Supera su análisis estático con la regla de dependencia activa | El lint del producto, sin excepciones agregadas | RNF-03, RF-06 |
| Supera sus pruebas y su compilación | El resto de su verificación | RF-03 |
| Arranca sin que nadie edite un archivo | Se arranca con su script y solo se fija el puerto | RF-01, RF-06 |
| El adaptador del módulo queda resuelto en ejecución | Una petición real guarda y otra lee | RF-06, RF-07 |
| El producto declara qué tiene incorporado | Se lee su registro y se comprueban módulo, versión y cableado | RF-10 |
| El dato sobrevive al reinicio | Se apaga, se arranca y se vuelve a leer | RF-09 |
| La actualización preserva el código del equipo | Se compara el archivo antes y después | RF-13 |
| Lo desactualizado se informa | Se lee la salida de la consulta | RF-08, RF-12 |
| Dos productos conviven con versiones distintas del mismo módulo | Se leen los rangos que **cada registro declara**, que es lo que una resolución posterior lee | RNF-06 |
| El producto vuelve a ser conforme sin ningún módulo | Se corre su verificación otra vez después de la remoción | RF-06 |

**Lo que el producto no hizo falta tocar.** Ninguna excepción de análisis estático, ninguna configuración extra, ningún archivo editado a mano. Si hubiera hecho falta, la condición de llegada no estaría cumplida, por más que el comando terminara bien.

**Un hallazgo de la comprobación de convivencia.** La comparación de los rangos de los dos manifiestos pasaba **por la razón equivocada**: el del primer producto ya no es el que la incorporación escribió, porque el paso que lo instala lo apunta a un tarball local. Se compara lo que cada **registro** declara.

## 5. Las puertas del repositorio

| Puerta | Qué corre | Cuánto tarda |
| :-- | :-- | :-- |
| `check:commit` | Formato, lint, typecheck, las pruebas de cada paquete y la validación de los artefactos declarativos | Segundos |
| `check:push` | La verificación de cada paquete, la de generación, **la de composición**, la auditoría del activo y la de producción | Minutos |

**Por qué la composición va en la puerta de envío y no en la de commit.** Instala productos reales y arranca uno dos veces. Una puerta de confirmación que tarda minutos se termina salteando, y una puerta que se saltea no verifica nada.

## 6. Evidencia fechada

**Al cerrar la fase, el 2026-10-31**, la puerta de envío en verde de punta a punta, con el circuito en sus pasos de entonces y sus cinco rechazos, 184 pruebas —2 en el contrato, 12 en el módulo, 19 en el activo y 151 en la herramienta—, los dos productos de la generación derivados, verificados y arrancados con su documento OpenAPI servido, y cero vulnerabilidades en el activo y en las dependencias de producción.

**Con los dos módulos del catálogo**, la salida del circuito:

```
refused: a module the catalog does not have, listing what it offers
deposit-api declares @bsl/persistence@0.3.0 and its wiring.
deposit-api stored a record through its API and read it back.
deposit-api restarted and the record was still there.
update moved the module to 0.4.0, kept the file of the team and added its configuration.
refused: a product whose readme has no region for what the module replaces
deposit-api declares @bsl/observability@0.1.0 beside the first module.
deposit-api passed its own verification with both modules incorporated.
deposit-api exported 3 spans, its entries and the duration of its requests, continuing the trace of its caller.
```

| Comprobación | Resultado |
| :-- | :-- |
| Pruebas | 342: 2 en el contrato, 12 en persistencia, 36 en observabilidad, 98 en el activo, 194 en la herramienta |
| Generación | Tres productos derivados, verificados y arrancados |
| Composición | El circuito completo, con un producto que lleva **dos módulos** del catálogo |
| Auditorías | Cero vulnerabilidades en el activo y en las dependencias de producción del monorepo |

El tarball del segundo módulo se revisó antes de considerarlo publicable, como exige el estándar de código: dieciséis archivos, solo el compilado, el manifiesto, su esquema, el manifiesto de paquete y el README.

## 7. Qué quedó sin cubrir

| Qué | Por qué no se cubre acá | Dónde se cubre |
| :-- | :-- | :-- |
| Que la resolución desde el feed funcione para un módulo | El circuito prueba la resolución desde una ruta local, que es el mismo camino con otro origen. Depender del feed haría la verificación no reproducible | La comprobación del feed, que se repite al publicar |
| Que un módulo de otra forma de producto se incorpore | Ningún módulo del catálogo sirve a la segunda forma: los dos exportan un módulo de un framework que un host de funciones no sabe registrar. Lo que sí se comprueba es el rechazo | Crecimiento del catálogo |
| Pruebas de integración HTTP dentro del producto | El circuito ejerce la API real del producto en ejecución, así que no hicieron falta | Registrado como candidato no construido |
| El camino interactivo de las operaciones | El circuito corre con banderas. Lo cubren pruebas unitarias contra el doble del prompter | El render lo confirma el autor en una terminal real |

## 8. Qué cambió en lo ya construido al verificarlo

Nada del mecanismo. Lo único que cambió es la puerta, que incorpora la verificación del circuito. El principio del bloque se mantuvo: todo lo que esta verificación encontró mientras se construía —el archivo movido dos veces, el marcador confundido con su mención, el import que quedaba sin uso— se corrigió en el documento que lo construyó, y no acá.

[cap1]: <../Insumos/Evidencias/GM-04_cap1_rechazo_de_la_composicion.png>
