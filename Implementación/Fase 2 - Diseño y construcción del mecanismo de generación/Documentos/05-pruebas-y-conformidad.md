# Pruebas y conformidad del proyecto generado

Produce la evidencia ejecutable de que un comando deriva un producto que arranca sin que nadie edite un archivo y que es conforme al marco, y completa las pruebas que a la herramienta le faltan.

---

**La verificación no modifica lo verificado.** Acá no cambia el producto, ni los activos, ni la interfaz de la herramienta, ni los estándares de código, ni una decisión aceptada. Cuando una comprobación solo es posible cambiando algo de eso, se detiene, se declara como límite en §12 y el cambio se decide aparte.

Y es el punto donde los documentos anteriores pueden quedar invalidados: si al verificar aparece que el núcleo no sostiene lo que el doc 4 declara, se corrige el doc 4. No se anota la excepción acá.

## 1. Estrategia de prueba de la herramienta

Tres niveles, y el límite de cada uno está donde empieza lo que el nivel no puede ver.

| Nivel | Qué prueba | Contra qué corre |
| :-- | :-- | :-- |
| Unidad | Las reglas del modelo, la resolución de la entrada, la lectura del catálogo, la resolución de un activo, la escritura de un plan, la localización de un producto y las formas de nombre | Dobles en memoria |
| Operación | Las operaciones completas, de los valores recibidos al plan aplicado: qué escribe, qué reporta, qué comandos ejecuta y con qué falla | Dobles en memoria, más las plantillas y el activo reales leídos del disco |
| Extremo a extremo | La herramienta construida derivando productos reales, que se instalan y se verifican a sí mismos | Sistema real, sobre una copia temporal que se borra |

**Por qué el límite cae ahí.** La herramienta llega al entorno por seis puertos, y ningún archivo del núcleo ni de una operación toca disco, red o terminal por su cuenta. Eso es lo que permite que los dos primeros niveles corran sin entorno: una prueba sustituye el puerto y observa lo que la pieza decidió. Lo que esos niveles no pueden ver es si el entorno real se comporta como el doble supone, y es exactamente lo que hace el tercero: instala el producto, corre su verificación, lo arranca y le pide una ruta.

**Dobles.** Están escritos a mano e implementan el puerto, como pide el estándar de código. Ninguno es un mock de librería.

| Doble | Qué hace |
| :-- | :-- |
| Sistema de archivos falso | Sistema de archivos en memoria, con el comportamiento del que la herramienta depende |
| Sistema de archivos que registra | Lee del sistema real y guarda las escrituras en memoria. Permite correr una operación contra las plantillas reales sin dejar un producto en disco |
| Registro de paquetes falso | Registra qué paquete se pidió y deja el paquete en el destino |
| Prompter con guion | Responde desde un guion. Una pregunta sin guion falla la prueba en lugar de colgarla. Honra el contrato completo: rechaza la respuesta que la pregunta no acepta y la vuelve a pedir, y admite las dos teclas de la terminal como respuestas |
| Reporter que acumula | Guarda lo escrito, para poder afirmar sobre la salida. Aplana un bloque de pares a una línea por par, de modo que una prueba afirme el contenido y no el relleno |
| Ejecutor de comandos falso | Registra qué comando se pidió en lugar de ejecutarlo |

El sistema de archivos que registra es el único doble que lee del disco real, y ningún método suyo escribe, mueve ni borra nada fuera de sus propios mapas: el nivel de operación no puede dejar residuo en la máquina. Resuelve las dos cosas a la vez: probar la operación contra un sistema enteramente en memoria obligaría a inventar las plantillas, y entonces la prueba no diría nada sobre la derivación real; probarla contra el disco dejaría un producto por corrida.

## 2. Criterio de cobertura y archivos exentos

**Criterio.** Se prueba toda unidad con lógica propia. Un archivo sin lógica propia queda exento y la exención se declara acá con su razón. El estándar de código no cambia: su regla es de organización y de nombre, no una obligación de que todo archivo tenga prueba.

**Por qué no el criterio literal.** El adaptador del reloj son trece líneas que devuelven la fecha, y el del ejecutor de comandos veinte que envuelven una función de la plataforma. Una prueba suya no puede fallar por culpa de este proyecto: fallaría si fallara Node. Contarla como cobertura es inflar una cifra que después se cita como garantía.

| Archivo exento | Por qué |
| :-- | :-- |
| Los seis puertos del núcleo | Son interfaces y tipos. No hay comportamiento que ejecutar |
| Adaptador del reloj | Devuelve la fecha. Lo no determinista se fija por inyección y las pruebas ya inyectan el reloj |
| Adaptador del ejecutor de comandos | Envuelve una función de la plataforma. Su comportamiento real se ejercita en el circuito de generación, que corre comandos de verdad |
| Tabla de códigos de salida y banner | Constantes y presentación |
| Registro de operaciones | Declara el arreglo. El despacho se prueba sobre operaciones propias de la prueba |
| Composición del punto de entrada | Construye los adaptadores y llama al núcleo. Lo que decide se observa en el circuito, que invoca el binario |

**Cobertura indirecta declarada.** Dos archivos tienen lógica propia y no reciben suite, con su límite escrito: el adaptador de consola, cuya regresión de formato no la detecta ninguna puerta, y el adaptador del registro de paquetes, que el circuito no ejercita porque resuelve el activo por ruta local y cuya evidencia es el circuito del feed, que se repite al publicar.

**Los límites conocidos se fijan como aserción.** Un límite declarado en prosa que no está probado se «arregla» tarde o temprano sin que nadie decida arreglarlo. El límite de pluralización viaja como una prueba cuyo nombre dice que es un límite, no una expectativa de corrección.

**Una regla de nombre que el estándar no previó.** Dos archivos homónimos en carpetas distintas —las formas de nombre del núcleo y los nombres de la derivación— no pueden tener los dos la misma prueba. La del segundo lleva su carpeta como prefijo. Se resuelve acá sin tocar el estándar.

## 3. Las suites que esta fase agregó

Lo que faltaba no era refinamiento: eran dos de las piezas con más decisiones de la herramienta, el módulo de nombres de la derivación y el análisis de la invocación.

| Suite | Unidad probada | Qué fija |
| :-- | :-- | :-- |
| La operación de derivación | La operación completa | De dónde sale cada valor; qué escribe y qué no; qué reporta; la revisión enmendable; y los rechazos, incluido que **resuelve la plantilla antes que la entrada** |
| La operación de lectura del catálogo | La operación, no el resolutor | La tabla que escribe, el guion de un activo que ninguna release fija, el origen que informa al resolver y los dos fallos que distingue |
| Los nombres de la derivación | El módulo de nombres | Las siete reglas: nombre del caso de uso, del evento y de la ruta; que el calificador distingue dos operaciones del mismo término; el método y la ruta de cada término; el anidamiento de una operación de qualifier; que las rutas cuelgan del agregado en plural; que una iniciación responde `201` y el resto `200`; y qué términos derivan un caso de uso que carga su efecto de negocio |
| El análisis de la invocación | El análisis de argumentos | Tres reglas que nada más prueba —una bandera global se lee donde aparezca, un booleano se apaga con el prefijo `no-`, una lista se escribe con comas o repitiendo la bandera— y los cuatro rechazos |

**Por qué la operación de derivación era la más urgente.** Es la pieza con más ramas: mezcla valores de banderas, de archivo y de argumento posicional, resuelve la entrada contra el modelo, resuelve el activo contra el catálogo, obtiene la dirección del registro, deriva el plan y lo aplica, y recién entonces reporta, inicia el repositorio e instala. Antes de su suite, un fallo en cualquiera de esos pasos aparecía como una instalación rota en un directorio temporal, sin decir qué se había roto.

**Hueco de estrategia, declarado.** Los dos circuitos de la línea corren con banderas y sin interacción, de modo que **ningún camino automático pasa por una pregunta**. Lo que cubre el camino interactivo son pruebas unitarias contra el doble del prompter; el render y la captura de una tecla siguen exigiendo una terminal real, y los confirma el autor.

## 4. Equivalencia ante la misma entrada

RF-05 pide que dos ejecuciones con parámetros idénticos, por usuarios distintos, produzcan estructuras equivalentes. El circuito deriva el primer producto una segunda vez en otro directorio y compara las dos copias: el registro de versiones se compara quitándole el momento de la derivación, y todo lo demás con una comparación recursiva de directorios.

**Qué queda fuera y por qué no debilita la comprobación.** Solo el momento de la derivación. Es el único valor que la herramienta toma del reloj, y dos corridas no pueden compartirlo sin congelar el reloj, que es justamente lo que un producto real no hace. Todo el resto del registro —nombre, capacidad, operaciones, versión del activo y entrada resuelta— entra en la comparación, de modo que cualquier otra fuente de variación la encontraría el `diff`.

**Qué no cubre.** La equivalencia se comprueba entre dos corridas de la misma release en la misma máquina. Que dos máquinas distintas produzcan lo mismo depende de que resuelvan el mismo activo, y eso lo garantiza el pin de versiones, no esta comprobación.

## 5. Conformidad del producto derivado

Nueve comprobaciones. Es una lista cerrada: lo que no está acá no se afirma del producto.

| # | Comprobación | Cómo se comprueba | Requerimiento |
| :-- | :-- | :-- | :-- |
| 1 | Arranca sin que nadie edite un archivo | El circuito lo arranca sin escribir ningún archivo de entorno y espera su sonda (§6) | RF-01 |
| 2 | Supera su análisis estático con la regla de dependencia activa | El `verify` del producto, más la prueba negativa de la regla (§7) | RF-03, RNF-03 |
| 3 | Supera sus propias pruebas | El `verify` del producto | RF-03 |
| 4 | Compila | El `build` del mismo `verify` | RF-03 |
| 5 | Declara con qué versión del activo fue derivado | Su registro de versiones, comprobado en la prueba de la derivación y comparado en §4 | RF-10, RNF-06 |
| 6 | Declara su alcance: persistencia, andamios, eventos y ejemplos | El resumen de la derivación y el README del producto | RF-03 |
| 7 | Responde las dos sondas | Durante el arranque de §6 | RF-01 |
| 8 | No fija direcciones ni lee el entorno fuera de su configuración | Barrido de las fuentes del producto derivado (§8) | RNF-05 |
| 9 | Registra cada request y no registra las sondas | Entradas que el producto escribió durante el arranque de §6 | RNF-02 |

**Sobre qué producto corre cada una.** Las que no necesitan un proceso corren sobre todos los productos del circuito, que entre ellos ejercitan los cinco términos de acción, las dos variantes de piezas opcionales y una capacidad declarada fuera del catálogo. Las que necesitan un proceso en ejecución —1, 7 y 9— corren sobre el primero, por la razón de §6.

## 6. Comprobación del arranque y las sondas

**Por qué automatizarlo.** Una afirmación que solo una persona puede reproducir caduca con el primer cambio del activo y nadie se entera. El índice de la fase cita esta comprobación como evidencia de RF-01, y conviene que lo que cite sea una puerta y no un recuerdo.

**Por qué sobre un solo producto.** El arranque es la comprobación más cara: levanta un proceso, espera a que escuche y lo apaga. Correrlo sobre todos duplica el costo sin agregar evidencia, porque lo que se comprueba es que el activo arranca y todos los productos derivan del mismo activo. Corre sobre el primero, que es el que ya se deriva dos veces para la comprobación de equivalencia.

**Lo que hace que esto sea evidencia y no un trámite.** El verificador no escribe un archivo de entorno, no exporta variables de servicio y no edita un archivo del producto. Arranca con el script que el producto dice en su README y que el resumen de la derivación imprime como paso siguiente. Solo fija el puerto, porque la corrida necesita uno libre y no puede apropiarse del de la máquina. Si el producto necesitara cualquier edición previa, el arranque fallaría.

**Decisiones de la implementación.** El puerto se pide al sistema operativo en lugar de fijarse, para que dos corridas simultáneas no se estorben. La espera está acotada: si la sonda no responde en el plazo, la comprobación falla con el log capturado en el mensaje, en lugar de colgar la puerta. Y el proceso se lanza en su propio grupo, porque el gestor de paquetes lanza a su vez el servidor y apagar solo al gestor dejaría el servidor escuchando.

## 7. La regla de dependencia, comprobada rompiéndola

Que el lint del producto pase demuestra que el lint corre. No demuestra que la regla de dependencia esté **activa**, que es la palabra que usa la condición de llegada de la fase y lo que RNF-03 exige. Una configuración mal escrita, una exclusión de más o una ruta de capa que no coincide con el árbol dejan el lint verde y la regla muerta.

**Cómo se comprueba.** Sobre la copia temporal se escribe, en un archivo de la capa de dominio, una importación que la regla prohíbe —dominio hacia infraestructura—, se corre el lint del producto esperando que falle, y se restaura el archivo. Un fallo no basta: tiene que ser **el fallo correcto**, así que se exige que la salida nombre la regla de tipos de elemento. Si el lint falla por otra cosa, la comprobación también falla, con la salida en el mensaje.

La violación se escribe en la entidad raíz, que existe en todo producto derivado, y siempre en la copia temporal que el verificador borra al terminar, nunca en las plantillas ni en el activo: el principio del bloque también rige para una prueba negativa.

## 8. Registro de requests y ausencia de valores fijos

**Cada request queda registrado y las sondas no.** Se comprueba con las entradas que el producto escribió durante el arranque de §6, sin agregarle nada: el arranque pide una ruta de la capacidad, una ruta que no existe y las dos sondas, y las entradas tienen que mostrar las dos primeras y no mostrar las sondas. Se comprueba además que el producto informó en qué dirección quedó escuchando, que el framework escribió sus propias entradas por el mismo puerto con su `scope`, que toda entrada dice de qué despliegue viene, que el arranque y el apagado se nombran como eventos propios, que una request fallida se reporta como advertencia con su duración, que toda request lleva su identificador y que el identificador que el llamador manda sobrevive el viaje de ida y vuelta, que la traza del llamador se conserva y el span es propio, y que el producto declara en su arranque qué adaptador de persistencia quedó ligado y que el dato se pierde al reiniciar.

**Por qué no se agrega una prueba al producto.** La alternativa era hacer que la prueba del interceptor viajara con todo producto, incluso con el mínimo, y está decidido lo contrario: el interceptor viaja copiado y su prueba viaja con las de ejemplo. Cambiarlo sería cambiar el reparto de archivos de la derivación —el producto— para que una comprobación fuera más fácil, que es lo que el principio del bloque prohíbe. Se comprueba el comportamiento en ejecución, que además es evidencia más fuerte que una prueba copiada: dice que el producto **tal como se entrega** registra lo que se le pide.

**Nada fijo que deba ser configurable.** RNF-05 pide que el producto no contenga valores fijos susceptibles de cambio, y hasta esta fase eso se revisaba leyendo. Las dos reglas del barrido: el entorno se lee únicamente bajo la carpeta de configuración, que es donde el esquema lo valida y falla si el entorno es inválido; y ningún archivo de las fuentes lleva una dirección absoluta cuyo host tenga un punto. La segunda admite a propósito la dirección local que el arranque compone con el puerto configurado, y atrapa tanto un dominio como una IP, que es la forma que toma una dirección de servicio.

## 9. Las puertas de verificación

Cinco puertas del repositorio, y cada una existe porque la anterior no puede pagar su costo.

| Puerta | Qué corre | Cuándo |
| :-- | :-- | :-- |
| `check:commit` | Formato, lint, typecheck, pruebas de cada paquete y validación de los artefactos declarativos | Antes de cada commit |
| `verify:artifacts` | Los esquemas de los tres artefactos, más las reglas que un esquema no expresa: que los identificadores son únicos, que lo que la familia fija y lo que deja variar son **disjuntos**, y que todo pin existe en el manifiesto del catálogo | Dentro de las dos puertas y del `verify` de la herramienta |
| `verify` de cada activo | Lint, pruebas y compilación del paquete, más lo propio de su tipo: el manifiesto de una plantilla contra su esquema, y la instalación del activo aislado desde tarballs para correr su propia verificación | Antes de publicar, y dentro de `check:push` |
| `verify:generation` | Construye la herramienta, deriva los productos **nombrando la plantilla**, compara dos derivaciones de la misma entrada, los instala, corre su `verify`, barre su configurabilidad, prueba la regla de dependencia y arranca el primero | Dentro de `check:push` |
| `audit:prod` | Auditoría de las dependencias de producción, sobre la raíz y sobre el activo con su lockfile | Dentro de `check:push` (RNF-04) |

**Por qué el arranque no está en la puerta de commit.** El circuito instala productos y levanta uno: son minutos. Una puerta de commit que tarda minutos se empieza a saltar, y una puerta que se saltea no protege nada. Queda en la puerta de envío, donde el costo se paga una vez por envío.

**El circuito compara la lista de archivos, no su número.** Declaraba cuántos archivos debía escribir cada producto —un número movido a mano en cada grupo de cambios— y un conteo dice cuántos y nunca cuáles: una plantilla agregada y otra retirada se cancelaban y la puerta seguía en verde. Ahora cada producto tiene su manifiesto de rutas, y al diferir el circuito imprime los dos lados, qué ruta apareció y qué ruta desapareció, más el comando que acepta el cambio. La lista de rutas del documento OpenAPI **sigue escrita a mano a propósito**: derivarla con las mismas reglas que la producen haría que un error en esas reglas pasara la comprobación.

**La condición de orden de publicación no está en la puerta de envío**, y no es por costo sino por tiempo: al empujar, el contrato legítimamente puede no estar publicado todavía —subir el código y publicar son dos actos distintos, y en ese orden—, así que la condición solo es exigible en el momento de publicar, y por eso vive en el `prepublishOnly` de cada activo. Lo que la motiva ocurrió: el activo y la herramienta se publicaron antes que el contrato que declaran, y el feed sirvió un artefacto que no se podía instalar.

**Dos huecos de puerta que aparecieron ejecutándolas**, los dos de la misma clase —la puerta lenta comprobaba **menos** que la rápida—: el lint de los scripts del repositorio, que la puerta de envío no corría, y el typecheck del monorepo, que tampoco, porque el `build` de cada `verify` usa una configuración que no incluye las pruebas y un error de tipos en una prueba pasaba la puerta y lo atrapaba solo el gancho de commit. Los dos entraron a la puerta de envío.

**Una puerta que no arranca lo que verifica, declarado.** La verificación de la plantilla de Azure deriva un producto, comprueba que registre ese paquete y esa forma, lo instala y corre el `verify` que el producto trae, pero no lo arranca: correrlo exige una herramienta externa que ninguna puerta del repositorio puede dar por instalada. La superficie la ejercitan las pruebas que el producto trae, que invocan el handler de una función directamente con una request armada a mano.

## 10. Evidencia obtenida

Cada fila es una corrida concreta con su fecha, y es la que el índice de la fase cita en lugar de volver a producir la evidencia. Los conteos corresponden a esa fecha; las versiones vigentes están en el `package.json` de cada paquete.

| Comprobación | Comando | Resultado | Fecha |
| :-- | :-- | :-- | :-- |
| Pruebas de la herramienta | `npm test -w @bsl/cli` | 15 suites, 101 pruebas | 2026-10-31 |
| Pruebas del contract package | `npm test -w @bsl/contracts` | 2 pruebas en una suite | 2026-10-31 |
| Pruebas del activo | El `test` del activo | 5 suites, 14 pruebas | 2026-10-31 |
| Artefactos declarativos | `npm run verify:artifacts -w @bsl/cli` | Los tres válidos · `Every pinned asset is declared in the catalog.` | 2026-10-31 |
| Formato, capas y tipos | `npm run check:commit` | Formato, lint y typecheck sin hallazgos. La puerta termina en 0 | 2026-10-31 |
| El activo como proyecto independiente | El `verify:audit` del activo | Supera su lint, sus pruebas y su compilación, instalado aparte, más su auditoría de producción | 2026-10-31 |
| Derivación extremo a extremo | `npm run verify:generation -w @bsl/cli` | Cada producto derivado con los archivos que su manifiesto declara, y todos `passed its own verification.` | 2026-10-31 |
| Equivalencia ante la misma entrada | El mismo comando | `Two derivations of the same input produced the same product.` | 2026-10-31 |
| Configurabilidad del producto | El mismo comando | `No address and no read of the environment is fixed outside the configuration.` | 2026-10-31 |
| Regla de dependencia activa | El mismo comando | `The dependency rule of the product refuses an import from infrastructure.` | 2026-10-31 |
| Arranque, sondas y registro | El mismo comando | El producto arrancó, respondió las dos sondas y registró lo que sirvió | 2026-10-31 |
| Auditoría de producción | `npm run audit:prod` | Cero vulnerabilidades, sobre la raíz y sobre el activo con su lockfile | 2026-10-31 |
| Puerta completa de envío | `npm run check:push` | Termina en 0, con todo lo anterior dentro | 2026-10-31 |

## 11. Comprobación de que una prueba falla cuando debe

Una suite que pasa no dice si está mirando. Para cada pieza nueva se rompió a propósito lo que la prueba afirma, se comprobó que la prueba falla, y se restauró el archivo, quedando idéntico al original.

| Qué se rompió | Qué falló |
| :-- | :-- |
| La pluralización sin sus terminaciones irregulares | La prueba del plural regular |
| El resumen de la derivación dejando de nombrar los andamios | La prueba del efecto de negocio |
| La tabla de activos sin el guion del activo no fijado | La prueba del guion |
| El booleano negado dejando de apagarse | La prueba de la bandera negada |
| La ruta que el arranque afirma haber registrado | El circuito: `The product served a request and did not log it.` |

La prueba negativa de la regla de dependencia no necesita esta comprobación: falla por construcción si el lint acepta la importación prohibida, y además exige que el fallo nombre la regla.

## 12. Límites de esta verificación

| Límite | Razón |
| :-- | :-- |
| RNF-02, que el producto modificado siga admitiendo operaciones de la herramienta | Requiere las operaciones que la Fase 3 construye. Esta fase comprueba la mitad que puede: que el producto es código del equipo desde que se escribe, y que lo que incorpora queda en su registro |
| RNF-06, convivencia de versiones distintas entre productos | Requiere más de una versión publicada de un activo consumido por productos distintos. Se verifica cuando la Fase 3 publique la segunda |
| El adaptador de consola y el del registro de paquetes | Cobertura indirecta declarada en §2: una regresión de formato de terminal y una del trato con el registro no las detecta ninguna puerta |
| El límite de pluralización | Cubre las terminaciones regulares del inglés y falla con un plural irregular. Viaja como aserción |
| Alcance del barrido de configurabilidad | Atrapa direcciones con host y lecturas del entorno fuera de la configuración. No atrapa un número de puerto ni un parámetro de negocio escrito a mano. El juicio completo de RNF-05 sigue siendo de revisión |
| El arranque necesita un puerto libre y poder señalar al grupo de procesos | En una máquina donde el grupo no pueda señalarse, la comprobación falla aunque el producto esté bien. Es el costo asumido de verificar un proceso real |
| La prueba del interceptor en un producto mínimo | Viaja con las pruebas de ejemplo. Un producto derivado sin ejemplos no la lleva, y el comportamiento se verifica en ejecución (§8) |
| El adaptador del registro en el circuito | El verificador resuelve el activo por ruta local, que es lo que permite verificar sin red. El camino del registro se verifica con el circuito del feed |
| La comprobación 3 sobre un producto derivado sin pruebas de ejemplo | Un producto mínimo informa que no encontró pruebas y termina en 0. Que supere esa comprobación no dice nada de ese producto: dice que su entorno de pruebas está configurado y corre. La comprobación tiene contenido en el producto que sí lleva las pruebas de ejemplo. Lo encontró esta verificación y se declara en lugar de corregirse: que el equipo que recibe un producto mínimo escriba sus pruebas está decidido así |
| El espacio de selección con cinco entradas | No afecta al mecanismo: la variabilidad se resuelve igual con cinco entradas que con veinte |
| La bandera experimental en las pruebas del producto | El producto invoca su ejecutor de pruebas con una bandera experimental para poder cargar un paquete ESM. Se retira cuando el ejecutor deje de exigirla |
