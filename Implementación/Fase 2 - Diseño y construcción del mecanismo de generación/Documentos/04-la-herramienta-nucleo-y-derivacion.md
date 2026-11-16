# La herramienta: núcleo y derivación

Construye la herramienta de línea de comandos: el núcleo común a toda operación, con su punto de extensión, y la operación de derivación, que convierte una entrada resuelta en un producto de la familia. En términos de la línea es el mecanismo de derivación, la pieza de ingeniería de aplicación que toma los activos y una selección de características y produce un producto.

---

Esa condición impone tres propiedades que la herramienta mantiene: la variabilidad sigue siendo dato y no código del generador, el consumo de activos sigue gobernado por el catálogo y no por el programa, y nada de la herramienta conoce un dominio de negocio.

El núcleo y la operación se construyen separados porque la Fase 3 monta operaciones nuevas sobre la misma herramienta. Si se escribieran confundidos, esa fase rehace la herramienta y migra los productos ya derivados. Lo que el núcleo fija es un contrato: qué puede suponer una operación que existe, y qué no tiene que volver a construir.

## 1. El reparto entre el núcleo y una operación

El criterio es uno: el núcleo decide **cómo** se hace algo que toda operación necesita; la operación decide **qué** se hace. El núcleo sabe aplicar un cambio sobre un directorio, no sabe qué dice ese cambio; sabe resolver un activo del catálogo, no sabe qué hacer con él.

| Pieza | Núcleo | Operación |
| :---- | :---- | :---- |
| Punto de entrada, análisis de argumentos, ayuda | Sí | Declara sus parámetros |
| Contrato de operación, registro, punto de extensión | Sí | — |
| Resolución de la entrada: banderas, archivo, preguntas | Sí, el mecanismo | Declara qué puntos de variación resuelve |
| Evaluación de las reglas del modelo | Sí | — |
| Normalización de nombres | Sí, las funciones | Decide dónde se aplica cada forma |
| Lectura del catálogo, pin de versiones, resolución de activos | Sí | Invoca el resolutor |
| Contexto de proyecto: localizar la raíz y leer su registro | Sí, lectura y validación | Escribe lo que corresponda |
| Plan de cambios y escritura transaccional | Sí | Produce el plan |
| Contenido de cada archivo generado, reglas de derivación | — | Sí |
| Errores y códigos de salida | Sí, las clases | Usa las clases existentes |

**Lo que queda fuera del núcleo, con su destino.** El descubrimiento dinámico de operaciones desde paquetes instalados y la salida estructurada para consumo por otros programas quedan como puntos de extensión declarados. La carga dinámica, además, haría que el comportamiento de la herramienta dependiera de lo que haya instalado, lo que rompe el determinismo que RF-05 exige.

## 2. Organización del paquete

La herramienta no es un producto de la familia: no expone una API HTTP ni modela un bounded context, así que la estructura canónica no la obliga y aplicarla produciría una capa de dominio vacía. Se organiza por responsabilidad, con la misma disciplina de fondo: el centro es puro y los efectos quedan confinados en adaptadores detrás de puertos.

| Grupo | Qué contiene |
| :---- | :---- |
| `core/` | Lo común a toda operación: contrato, puertos, resolución de la entrada, evaluador, activos, contexto de proyecto, plan de cambios, errores |
| `operations/` | Una carpeta por operación, más el registro que las enumera |
| `cli/` | La composición: análisis de argumentos, despacho, adaptadores y traducción de error a código de salida |
| `model/`, `domain-space/`, `assets/` | Los artefactos declarativos del doc 1 y el pin de versiones |

**Por qué el centro es puro.** `core` no importa el sistema de archivos, el proceso, la ejecución de comandos ni la librería de preguntas. La consecuencia práctica es que cada pieza se prueba con dobles escritos a mano, sin directorio temporal, sin red y sin terminal, lo que hace que las pruebas del núcleo corran en cualquier entorno y sean deterministas. La composición de rutas se admite, porque compone cadenas y no toca el sistema de archivos. La regla se hace cumplir con el analizador, igual que en el producto, acotada por ruta: los adaptadores sí pueden importar esos módulos, porque es su función.

**Por qué el registro de operaciones no vive en el núcleo.** Enumerar las operaciones obliga a importarlas, y `core` no puede importar `operations` sin invertir la regla de dependencia que este mismo documento declara. El registro es del grupo `operations` y el despacho vive en `cli`, que sí puede depender de `core`. El núcleo aporta el *contrato* de operación, no la lista de las que existen. La consecuencia práctica es que el despachador recibe las operaciones en sus servicios en lugar de importarlas: una prueba despacha contra un registro propio sin tocar el real.

## 3. Contrato de una operación y punto de extensión

Una operación es un objeto declarativo: declara su nombre, su resumen y sus parámetros como datos, y expone una función de ejecución. El núcleo construye con esa declaración el análisis de argumentos, la ayuda y la validación; la operación no los escribe.

**Por qué declarativo y no una clase que analiza los argumentos.** Si cada operación analizara los suyos, la Fase 3 duplicaría tres veces la validación y la ayuda, y nada garantizaría que tres operaciones traten igual una bandera ausente. Con la declaración como dato, agregar una operación es escribir qué recibe y qué hace; el resto ya existe. Es la misma razón por la que el modelo de variabilidad es un archivo y no código.

*Archivo: `src/core/operation.ts`, la declaración de un parámetro y la de una operación*

```ts
export interface ParameterDeclaration {
  readonly name: string;
  readonly type: ParameterType;
  readonly description: string;
  readonly required?: boolean;
  readonly asked?: boolean;
  readonly defaultValue?: ParameterValue;
  readonly group?: string;
}

export interface Operation {
  readonly name: string;
  readonly summary: string;
  readonly parameters: readonly ParameterDeclaration[];
  readonly positionals?: readonly PositionalDeclaration[];
  readonly examples?: readonly string[];
  execute(input: OperationInput, context: OperationContext): Promise<void>;
}
```

**`required` y `asked` son dos campos y no uno.** `required` dice que la operación no puede correr sin el valor; `asked`, que en una terminal se pregunta por él. Marcarlos con un solo campo habría exigido trece banderas antes de preguntar nada. Con los dos separados, la ayuda marca lo obligatorio —`(required)` o `(required; asked when omitted)`— sin que ninguna invocación automática gane una bandera nueva.

**El punto de extensión es el arreglo del registro.** Una operación nueva se escribe en su carpeta y se nombra ahí con una línea; no hay otro archivo que cambie. El registro es estático y no descubre operaciones desde paquetes instalados: nada en los requerimientos pide extensibilidad por terceros.

**Banderas globales**, que resuelve el núcleo y no se declaran en ninguna operación: `--help`, `--version`, `--dry-run`, `--non-interactive`, `--registry <url>` y `--asset-source <id>=<ruta>`, esta última repetible y resuelta contra el directorio desde el que se invocó el comando, porque si no, leer el activo dependería del directorio en que un paso posterior se encuentre.

El análisis de argumentos se apoya en la biblioteca estándar del entorno, sin dependencia externa, y valida los valores contra la declaración de la operación: una bandera desconocida, una obligatoria ausente o un valor con el tipo equivocado producen un error de uso que nombra la bandera.

## 4. Puertos del núcleo

Seis puertos, uno por clase de efecto. El criterio es el mismo que el marco aplica a un producto: el puerto declara lo que el núcleo necesita, no lo que la tecnología ofrece.

| Puerto | Qué usa su adaptador |
| :---- | :---- |
| Sistema de archivos | El sistema de archivos del entorno |
| Registro de paquetes | El gestor de paquetes, invocado con sus argumentos despiezados |
| Preguntas | La librería de preguntas interactivas |
| Reporte | Salida estándar y de error, con color ANSI |
| Reloj | La fecha del sistema |
| Ejecutor de comandos | La ejecución de un proceso hijo |

**Por qué el registro de paquetes se consulta con el gestor y no con un cliente propio.** El gestor ya resuelve la autenticación contra el feed con la configuración del usuario, descarga y extrae el paquete. Un cliente propio obligaría a leer credenciales dentro de la herramienta, que es exactamente lo que no debe ocurrir, y a implementar la extracción del formato de empaquetado.

**Por qué el ejecutor de comandos es un puerto, y por qué recibe el comando despiezado.** Solo lo usan las operaciones que terminan un producto: instalar sus dependencias e iniciar su repositorio. Como puerto, una prueba comprueba *con qué argumentos* se habría invocado al gestor o a git, sin ejecutar ninguno. Recibe el ejecutable y sus argumentos como elementos separados, nunca una línea de shell, de modo que nada de lo que una persona escribió pueda convertirse en otra cosa.

**Por qué el reloj es un puerto.** El registro de versiones del producto declara el momento de la derivación. Sin un puerto, dos ejecuciones de la misma prueba producirían archivos distintos y el determinismo exigido por RF-05 no sería verificable.

**La forma de la salida es del adaptador, no de la operación.** Una operación dice qué escribe y nada sobre su forma. El adaptador de consola es el único que conoce los códigos de color, el ancho de las columnas y la alineación; aplica color solo cuando la salida va a una terminal y el entorno no lo desactiva, de modo que una canalización reciba texto limpio, y muestra el banner solo al abrir una operación en terminal interactiva.

**Y la forma de una pregunta también.** El adaptador de preguntas decide tres cosas por el mismo criterio:

- **Ninguna lista se enrolla**, y se muestra entera cuando la terminal tiene lugar. Los defaults del paquete del ecosistema son los contrarios —siete opciones visibles y lista circular— y sobre las dos preguntas más densas del recorrido, la revisión de una derivación con hasta quince opciones y los behavior qualifiers de una capacidad con treinta, eso producía una lista sin primera ni última fila. Decidirlo en el adaptador corrige **todas** las preguntas del recorrido y no la pantalla donde apareció.
- **El rechazo ocurre en su sitio.** Una pregunta de texto viaja con la condición que su respuesta debe satisfacer y una selección múltiple con el mínimo que acepta, de modo que el adaptador refresca la pregunta en su lugar cuando la respuesta no sirve. Antes el valor se validaba después de cerrarla, y una respuesta que rompía su patrón en la pregunta doce terminaba el comando entero y perdía las once anteriores, que es lo contrario de lo que RNF-01 pide. La condición no se escribe acá: es la que el modelo declara.
- **Las dos teclas con que se abandona una pregunta son de la terminal.** La tecla de escape retrocede una pregunta y la interrupción sale; las dos se reportan al núcleo como señales y no como fallos, y el adaptador no escucha nada entre preguntas. La decodificación es de la plataforma, que ya distingue un escape solo del escape que abre la secuencia de una flecha.

## 5. Resolución de la entrada

Una operación con variabilidad recibe sus valores por tres vías, y las tres alimentan la misma tubería, de modo que la ejecución asistida y la automatizada producen la misma entrada resuelta.

| Vía | Forma | Para qué |
| :---- | :---- | :---- |
| Banderas | `--project-name term-deposit-api` | Una línea reproducible en un script, sin archivo intermedio |
| Archivo | `--input product.json`, con el documento del modelo de variabilidad | Automatización y repetición de una derivación |
| Preguntas | Sin nada declarado, o para completar lo que falta | Uso asistido en terminal |

**Precedencia**, de mayor a menor: bandera, archivo, valor por defecto del modelo, pregunta. Dos consecuencias: `--input product.json --project-name otro-nombre` deriva con todo lo del archivo salvo el nombre, y `--project-name x` en una terminal pregunta solo lo que falta.

**Por qué una sola tubería y no dos caminos.** La vía interactiva no es un modo aparte: es el último paso de la resolución, que se ejecuta solo para los puntos que siguen sin valor. Dos caminos de código habrían obligado a mantener dos veces la validación y las reglas, y habrían hecho posible que el modo interactivo admitiera algo que el no interactivo rechaza.

**La plantilla se decide antes de la primera pregunta del modelo**, de modo que un rechazo por plantilla inexistente o por catálogo ilegible llega antes de que nadie escriba nada. Cuando el catálogo ofrece más de una y la invocación no la nombra, se pregunta: una opción por plantilla ofrecida, con lo que cada una deriva como pista, y la lista no se enrolla.

![][cap1]

La captura es esa primera pantalla, con la herramienta instalada del feed. Es el camino que ningún circuito recorre, porque los dos corren con banderas: lo que se ve en ella —las dos opciones, la descripción de la que está bajo el cursor y la línea de teclas— no lo comprueba ninguna prueba automática.

**La resolución está partida en dos a propósito.** El recorrido delega cada punto en una función que resuelve *un* punto, y hay además una que vuelve a preguntar uno. No es una reorganización cosmética: la derivación cierra con una revisión enmendable, y corregir una sola respuesta sin descartar las demás exige poder resolver un punto otra vez. Volver a correr la resolución completa preguntaría todo dos veces.

**Qué hace cada pieza.** La validación aplica el patrón y la longitud máxima declarados, y cuando el valor no pasa, el mensaje no imprime la expresión regular: nombra la forma que el punto declara, da un ejemplo que la satisface y repite lo que llegó.

```
aggregateName must use PascalCase. Example: TermDeposit. Received: 'bolsillo'.
```

La regla que gobierna un punto se encuentra por su expresión de oferta, y un punto que no se ofrece se omite; solo se rechaza la invocación si traía un valor que lo contradice. Los registros de las opciones elegidas se comprueban contra las ofrecidas y se devuelven completos. Los valores por defecto resuelven tanto un literal como la lectura de un campo de una opción ya elegida. Y la pregunta se elige según el tipo del punto: texto, confirmación, selección simple o selección múltiple.

**Por qué la resolución devuelve respuestas y registros.** Una selección deja dos cosas: el valor elegido y el registro de la opción, con todos sus campos. Las reglas y las plantillas necesitan el segundo —`operations.some(o => o.mutates)` no se puede evaluar con el identificador de la operación—, así que la resolución devuelve ambos en lugar de obligar a la operación a volver a buscar la opción.

**Lo que la operación aporta.** El núcleo no sabe de dónde salen las opciones de un punto de selección: eso lo resuelve una función que la operación implementa. La derivación la implementa contra el espacio de selección de dominio, y la Fase 3 contra el catálogo de módulos.

## 6. Evaluador de las reglas del modelo

El modelo de variabilidad declara sus reglas como texto. El núcleo las evalúa con un intérprete de **gramática cerrada**, y es el mismo que lee la condición de un bloque dentro de una plantilla: no existe una segunda gramática.

| Forma admitida | Significado |
| :---- | :---- |
| `<id>` | La respuesta es verdadera o no está vacía |
| `!<expr>` | Negación |
| `<id>.length <op> <entero>` | Comparación de cardinalidad |
| `<id>.some(o => o.<campo>)` | Alguna opción seleccionada tiene ese campo en verdadero |
| `<expr> => <expr>` | Implicación |
| Igualdad y desigualdad contra un literal, igualdad entre dos nombres, `some` con igualdad, `includes` | Las cuatro formas que la condición de una plantilla agregó |

**Por qué no se evalúa como código.** Evaluar la expresión con el intérprete del lenguaje convertiría un archivo de datos en código ejecutable: cualquier cosa que llegara al modelo se ejecutaría con los permisos de quien deriva. El costo de la gramática cerrada es que una regla nueva puede exigir ampliarla; a cambio, el archivo declarativo sigue siendo datos.

**Cuándo falla una regla mal escrita.** No al derivar un producto, sino al verificar la herramienta: una prueba recorre todas las reglas del modelo real y comprueba que el evaluador las admita, de modo que una expresión no soportada rompe la verificación. El reparto es que el esquema valida la *forma* del archivo y la prueba valida la *gramática* de sus expresiones, porque un esquema no puede expresar una gramática.

## 7. Resolución de activos

El resolutor es genérico sobre el catálogo: recibe el identificador de una entrada y devuelve un directorio en disco y la versión resuelta, sin que le importe si el activo es una plantilla, el artefacto de contratos o un módulo.

**Por qué resolución en ejecución y no activos empaquetados con la herramienta.** Un módulo del catálogo no puede viajar dentro de la herramienta: el marco lo entrega como paquete más cableado generado, y la Fase 3 debe incorporar y actualizar módulos publicados después de ella. Si el núcleo resolviera solo lo que trae instalado, esa fase construiría un segundo mecanismo de obtención. El determinismo no lo da el empaquetado sino el pin, y el acceso al registro no agrega ninguna restricción nueva, porque el producto derivado ya depende del artefacto de contratos, que vive en el registro.

**Dirección del registro.** El núcleo la lee de la configuración del entorno para el espacio de nombres de la línea, y admite sobreescribirla. Si no está configurada, falla nombrando el dato que falta en lugar de derivar un producto que no se puede instalar. La consulta se pide sin espacios de trabajo, porque dentro de un paquete de un monorepo el gestor se niega a responderla y el adaptador leería esa negativa como un registro sin configurar: la dirección es una propiedad del entorno de quien ejecuta, no del directorio en el que está parado.

**Por qué del entorno y no de un archivo de configuración propio.** Quien deriva un producto necesita de todos modos resolver el artefacto de contratos desde el registro, así que su entorno ya tiene el espacio de nombres configurado; pedir el dato otra vez sería pedir lo que el entorno conoce. Además la dirección no queda escrita en el código de la herramienta, lo que mantiene la agnosticidad del registro que el marco exige.

**Los artefactos declarativos se cargan, no se leen.** El modelo, el espacio de selección y el pin son datos que la herramienta consulta en memoria, y la operación los necesita al declarar sus parámetros, antes de que exista contexto o puerto alguno. Por eso se cargan con el módulo y viajan compilados, mientras que las plantillas se leen del disco y viajan como archivos.

## 8. Contexto de proyecto

Toda operación posterior a la derivación opera sobre un producto ya derivado, y el núcleo aporta la lectura para que ninguna operación la reimplemente: localiza el registro desde un directorio hacia arriba, lo valida y lo entrega. No escribe.

**Por qué rechaza la plantilla explícitamente.** Sin esa comprobación, ejecutar una operación dentro del repositorio de la plantilla la aplicaría sobre el activo de la línea en lugar de sobre un producto. El campo `kind` del registro existe precisamente para distinguirlos, y este es su primer consumidor.

**Por qué dos campos del registro son opcionales.** El agregado y la entrada con que el producto se derivó se agregaron para que el registro diga con qué se derivó y no solo qué capacidad representa. Un producto derivado antes de esa decisión no los trae, y el lector no puede rechazarlo por eso.

**Un defecto latente que apareció al construirlo.** La comparación de la versión del esquema era por **igualdad exacta** mientras la prosa del archivo decía dos veces la regla contraria. No mordía solo porque nadie había subido el número: el día que alguien escribiera una menor nueva por un campo agregado, todo producto derivado hasta entonces habría quedado ilegible. Es ahora por versión mayor, en los tres lectores que la hacen.

## 9. Plan de cambios y escritura

Una operación no escribe en el disco: produce un plan y el núcleo lo aplica. El plan es la pieza que hace posibles la escritura transaccional, la vista previa y la prueba sin disco. El juego de clases de cambio es cerrado.

| Clase | Qué hace | Quién la introduce |
| :---- | :---- | :---- |
| `write` | Escribe un archivo nuevo con el contenido que la operación entrega | Fase 2 |
| `copy` | Copia los bytes del origen, sin leer el contenido | Fase 2 |
| `edit-at-marker` | Inserta texto en un marcador declarado de un archivo existente, o falla si el marcador no está | Fase 2 |
| `rewrite` | Reemplaza el contenido completo de un archivo que ya existe | Fase 3 |
| `replace-region` | Reemplaza lo que hay entre las marcas de apertura y cierre de una región | Fase 3 |

Una operación no elige cómo se escribe: declara qué cambio quiere. Eso es lo que permite que la vista previa muestre el plan sin tocar el disco, y que un rechazo ocurra antes de abrir un archivo.

**Por qué la tercera clase existe desde esta fase.** La plantilla lleva los marcadores del punto de composición desde su construcción, porque un punto de inserción agregado después obligaría a modificar todos los productos ya derivados. Por la misma razón el núcleo trae el mecanismo que los usa: la Fase 3 inserta el registro de un módulo sin construir infraestructura de escritura, y sin que el núcleo conozca ningún marcador concreto.

| Situación | Comportamiento del escritor |
| :---- | :---- |
| El plan solo crea archivos y el destino no existe o está vacío | Se materializa en un directorio temporal y se mueve al destino al terminar |
| El plan solo crea archivos y el destino tiene contenido | Falla antes de escribir, nombrando el destino. No sobrescribe ni fusiona |
| El plan edita un archivo existente | El archivo se lee del destino, se edita en el temporal y se reemplaza al final, cuando todas las ediciones tuvieron éxito |
| Falla cualquier cambio | No queda nada escrito en el destino |
| Vista previa | Se imprime el plan, ordenado por ruta, y no se escribe nada |

**Límite asumido.** Cuando un plan edita varios archivos existentes, el reemplazo final se hace archivo por archivo: un fallo del sistema de archivos en medio de esa secuencia podría dejar algunos reemplazados y otros no. El caso no se da en esta fase, donde la derivación solo crea archivos sobre un destino vacío; la Fase 3, que es la que edita productos existentes, resuelve la atomicidad con una copia de respaldo del conjunto de archivos tocados.

## 10. Errores y códigos de salida

Un comando que se usa en una canalización necesita que su código de salida distinga un error de quien lo usa de un fallo del entorno.

| Clase | Código | Qué agrupa |
| :---- | :---- | :---- |
| Éxito | 0 | La operación terminó |
| Error de uso | 1 | Bandera desconocida, valor que no cumple su patrón, regla del modelo incumplida, dato obligatorio ausente, directorio que no es un producto |
| Error de entorno | 2 | Registro sin configurar, activo inexistente o retirado, versión sin pin, destino con contenido, fallo al obtener un paquete |
| Cancelado | 130 | Quien corrió el comando pidió salir antes de que se escribiera algo |
| Error interno | 70 | Cualquier fallo no previsto. Se informa como defecto de la herramienta |

**Salir no es fallar.** La clase que representa la cancelación existe porque antes no existía: la interrupción de la terminal llegaba a la raíz de composición como un fallo no previsto, de modo que la herramienta respondía a quien cancelaba que eso era un defecto de la herramienta. Es la única clase que la raíz escribe como línea informativa y no como fallo —`Cancelled. Nothing was written.`—, y su código es el que un shell usa para un comando interrumpido, de modo que un script distinga «lo dejé yo» de «falló». Se produce por dos vías: la interrupción de la terminal, y la tecla de escape cuando no queda ninguna pregunta atrás.

**La versión del entorno se comprueba antes que nada.** El manifiesto declara el piso de Node, pero el gestor de paquetes solo advierte. El punto de entrada comprueba la versión mayor **antes de importar nada** de la herramienta —el fallo original ocurría al cargar una dependencia, de modo que cualquier comprobación posterior llegaba tarde— y, si es anterior, escribe qué versión necesita y cuál encontró, y termina con el código de error de entorno. El piso es 24 y no 22 porque el producto que la herramienta deriva necesita 24.9 para correr sus pruebas: aceptar menos sería entregar un producto que quien lo generó no puede verificar.

**Por qué el núcleo devuelve el código y no termina el proceso.** El despachador no llama a ninguna función que termine el proceso: devuelve, y la composición traduce. Así el núcleo se prueba invocándolo y leyendo su resultado, sin que la prueba muera con él. La traducción de *lo que no es un error previsto* vive en la frontera, no en el núcleo.

## 11. Ayuda generada y superficie de comandos

La ayuda se construye con la declaración de cada operación, de modo que una operación nueva aparece documentada sin escribir texto de ayuda.

```
$ bsl --help
 BACKEND SERVICE LINE · 0.33.0

Command-line tool of the backend service line.

Usage: bsl <command> [options]

Commands:
  new             Generates a product of the line from the base asset
  templates list  Lists the templates the organization offers
  templates show  Tells what a template offers and what a product of it is made of
  modules list    Lists the modules the line offers and what this product does with each one
  modules add     Incorporates a module of the catalog into a product
  modules update  Moves an incorporated module to another version
  modules remove  Takes an incorporated module out of a product
  status          Tells what a product carries and which of its modules are behind the catalog

Still working, use these instead:
  add             bsl modules add
  update          bsl modules update
  assets          bsl modules list

Global options:
  -h, --help                    Show this help, or the help of a command
  -v, --version                 Show the version of the tool
      --dry-run                 Show the change plan without writing anything
      --non-interactive         Never ask; fail naming what is missing
      --registry <url>          Override the registry address
      --asset-source <id=path>  Resolve an asset from a local path
```

**Qué declara cada operación para que la ayuda diga lo que dice**, todo dato: los argumentos sin bandera producen la línea de invocación y su propio bloque, con el argumento entre ángulos si es obligatorio y entre corchetes si no; `required` y `asked` producen la marca de lo obligatorio; `group` produce el título bajo el cual se lista un parámetro, y lo que no declara grupo va al final; y los ejemplos producen el bloque con que cierra la ayuda.

Antes de eso no había línea de invocación —la forma de invocar estaba documentada en el texto del error que se queja de su ausencia, que lo lee solo quien ya se equivocó— y la derivación no marcaba ninguno de sus **once** parámetros obligatorios, porque los declaraba desde el modelo de variabilidad sin copiar el campo que lo dice. Su ayuda queda además en cinco bloques, porque diecisiete banderas en una lista plana no se leen.

**Los alias se listan aparte, apuntando a su reemplazo.** Las operaciones de módulos se agruparon bajo un nombre común y los nombres anteriores siguen vivos en todo `0.x`, de modo que un guion escrito contra la superficie anterior no se rompe. Listarlos en su propio bloque es lo que distingue la superficie vigente de lo que se conserva por compatibilidad.

## 12. El motor de plantillas y la derivación

El activo de una plantilla contiene un agregado real con sus operaciones, y un producto puede pedir otro agregado con operaciones que el activo no tiene. Derivar no puede ser renombrar: hay que decidir de dónde sale el código de una operación que el activo no trae, y cómo se evita que esa fuente y el activo digan cosas distintas.

**El motor.** Una plantilla es un archivo de texto con marcadores, y sobre eso tiene las tres construcciones y las dos tablas cerradas que el doc 2 §3 enumera. La condición de un bloque la lee el evaluador de §6. Un marcador sin valor es un error y no se sustituye por vacío.

**Dos motores, por el alcance de cada uno.** La derivación usa el de las tres construcciones. La incorporación y la actualización de un módulo usan uno que **solo sustituye marcadores**: un módulo escribe líneas de cableado, no archivos con estructura condicional, y darle bloques sería darle una capacidad que ninguna regla de composición necesita.

*Archivo: `src/core/templates/render.ts`*

```ts
import { UsageError } from '../errors';

/** Values a template is rendered with, by marker name. */
export type RenderContext = Readonly<Record<string, string>>;

const TOKEN = /\{\{([a-zA-Z][a-zA-Z0-9]*)\}\}/g;

export function render(template: string, context: RenderContext): string {
  return template.replace(TOKEN, (_match, name: string) => {
    const value = context[name];
    if (value === undefined) {
      throw new UsageError(`Template marker '${name}' has no value.`);
    }
    return value;
  });
}
```

**La derivación es un intérprete.** No conoce la forma del producto que produce: lee el catálogo de archivos del manifiesto de la plantilla, arma el scope con las cuatro primitivas del vocabulario, y por cada entrada produce un cambio del plan según su clase. Su firma no nombra framework, estándar ni carpeta de un producto. Lo que antes era el catálogo de archivos del producto escrito en código pasó a ser dato: la derivación bajó de 919 a 586 líneas y el intérprete ocupa 203.

**Qué queda de lógica del estándar en la herramienta.** Los nombres que el término de acción impone sobre una operación —la clase del caso de uso, su archivo, la ruta, el método, el nombre del evento— y su límite de pluralización. Es el último trozo y queda declarado como punto de extensión.

| Elemento | Regla | Ejemplo |
| :---- | :---- | :---- |
| Directorio del agregado | `src/domain/<agregado en kebab>/` | `src/domain/term-deposit/` |
| Clase del caso de uso | `{ActionTerm}{Agregado}{Calificador}UseCase` | `ExecuteTermDepositInterestUseCase` |
| Archivo del caso de uso | kebab de la clase, sin el sufijo de rol | `execute-term-deposit-interest.use-case.ts` |
| Clase del evento | `{Agregado}{Calificador}{TérminoEnParticipio}` | `TermDepositInterestExecuted` |
| Base de la ruta | agregado en kebab, en plural | `/term-deposits` |

El calificador es lo que queda del identificador de la operación después de quitar el término de acción, y una operación de behavior qualifier lo toma del qualifier que la publica. **Límite asumido:** la pluralización cubre las terminaciones regulares del inglés y falla con un plural irregular. El producto es del equipo que lo recibe y el segmento de ruta se corrige con una edición, que RNF-02 admite expresamente; se descartó preguntar el plural al derivar porque agrega una pregunta a todos los casos para cubrir unos pocos.

![][image1]

## 13. Determinismo, y la plantilla como salida de sus propias plantillas

RF-05 exige que la misma entrada produzca el mismo resultado. Tres reglas lo sostienen.

| Regla | Qué evita |
| :---- | :---- |
| Las listas se ordenan por el orden declarado en el espacio de selección, no por el orden en que se escribieron las operaciones | Que `--operations retrieve,initiate` y `--operations initiate,retrieve` produzcan archivos distintos |
| Los fragmentos se componen en orden fijo y se unen con un separador fijo | Que el orden de los métodos dependa de la iteración |
| Nada consulta el reloj ni el sistema de archivos durante el renderizado | Que el contenido dependa del momento o del entorno |

**La única excepción declarada** es el momento de la derivación que el registro del producto guarda, de modo que dos ejecuciones difieren en ese valor. La comparación de determinismo se define sobre el árbol completo excluyendo ese campo. Se conserva porque es el dato que permite auditar cuándo se derivó un producto, y quitarlo trasladaría esa información a algo externo al proyecto.

**El oráculo.** Rendir las plantillas con la entrada del agregado de referencia y comparar el resultado con los archivos del activo, byte a byte, es lo que impide que el activo y las plantillas se separen. Esa prueba se conservó a través de toda la reescritura del motor y **se usó como oráculo de cada paso**: cada colapso de plantillas y el cambio al intérprete produjeron productos idénticos. Los únicos cambios deliberados de bytes fueron el documento OpenAPI, que dejó de imprimirse desde código y pasó a ser texto en su plantilla, y el módulo global, porque el formato por ancho de línea se eliminó en vez de expresarse como dato y la plantilla escribe siempre la forma multilínea, que comprueba el `prettier --check` del propio producto.

## 14. El reporte de la derivación

El comando no instala dependencias por defecto, porque instalar tarda y exige acceso al registro, y la derivación debe poder ejecutarse sin red cuando el activo ya está en caché. En su lugar imprime los pasos siguientes.

![][cap2]

La captura es la derivación completa de un producto de tres operaciones, con la herramienta instalada del feed. Se le retiró el bloque de previsualización, que repite ya aplicado el que sigue, y la elisión queda marcada. Lo que hay que mirar es el último tramo: los pasos llevan el comando que cada script corre, el copiado nombra el archivo que esta forma de producto tiene y no otro, y la línea de cierre apunta al readme.

**Todo paso se lee del plan aplicado, no de una forma sabida.** `npm install` solo si el producto trae un manifiesto de paquete; el copiado de un archivo creado cuyo nombre termina en `.example` al mismo nombre sin el sufijo —una convención que las dos plantillas ya seguían sin que nadie la hubiera escrito—; el arranque desde los scripts del producto, el de desarrollo si existe y si no el de arranque, y ninguna línea si no declara ninguno; y la verificación solo si declara ese script. Un paso que corre un script **muestra el comando que corre**, leído de los scripts del producto, porque el paso era cierto e incompleto: el arranque de un producto de Azure corre una herramienta externa que no es dependencia del producto a propósito, y la primera señal de que faltaba algo era el fallo.

**Por qué no se declaran en el manifiesto de la plantilla.** Era la salida que el plan de esa ronda había diseñado, y se descartó por escrito: un manifiesto puede **mentir** y el plan **es** el producto. Leer el producto funciona además para la plantilla de un tercero sin que declare nada. Lo que una forma necesita más allá de esos comandos lo escribe la plantilla en el README del producto, así que el reporte cierra apuntando al readme en vez de repetirlo.

**Repositorio del producto.** El comando inicializa el repositorio y deja un commit inicial con todo lo generado, salvo que se le pida omitirlo. Es lo que hacen las herramientas equivalentes del ecosistema, y hay una razón propia: el commit inicial es la línea de base contra la cual se ve qué modificó el equipo, que es lo que RNF-02 protege y lo que la actualización de la Fase 3 necesita distinguir. Si git no está instalado, la herramienta avisa y termina igual: el producto está generado y la ausencia de repositorio no lo invalida.

**El resumen de la derivación** nombra la capacidad y el agregado, las operaciones cuyo efecto de negocio queda al equipo, dónde persiste el producto y qué pasa con sus eventos. Hay un punto abierto: afirma algo sobre los eventos en un producto que nunca publica eventos, porque una plantilla no puede declarar qué puntos de variación honra.

## 15. Empaquetado de la herramienta

| Decisión | Contenido |
| :---- | :---- |
| Punto de entrada | Un envoltorio con shebang que invoca la composición compilada |
| Artefactos declarativos | Se cargan con el módulo y viajan compilados: una sola copia por paquete |
| Catálogo | Dependencia con versión exacta, como respaldo de la resolución en ejecución |
| Dependencias de ejecución | La librería de preguntas y la de color, nada más |
| Análisis de argumentos | La biblioteca estándar del entorno, sin dependencia |
| Tutorial | `TUTORIAL.md` viaja en el paquete publicado, junto al binario y al compilado |

**Por qué dos dependencias y no cero.** La selección múltiple con descripciones, los valores por defecto y el manejo de una terminal que se interrumpe son varios cientos de líneas que no aportan nada al trabajo, y el color se resuelve con una librería de un solo archivo. El análisis de argumentos, en cambio, está en la biblioteca estándar. La auditoría de dependencias que RNF-04 exige se satisface con que la herramienta la supere, no con no tener dependencias.

**Por qué la verificación de generación es un script aparte y no parte de `verify`.** Deriva productos reales e instala sus dependencias, de modo que tarda y necesita red la primera vez. Dejarlo dentro de `verify` haría que publicar o confirmar un cambio dependiera de eso. Corre en la puerta de `pre-push`, donde el costo se paga una vez y no en cada confirmación.

## 16. Qué queda abierto

| Punto de extensión | Condición para retomarlo |
| :---- | :---- |
| Descubrimiento dinámico de operaciones | Que operaciones de terceros tengan sentido en la línea |
| Salida estructurada para otros programas | Que una canalización necesite consumir el resultado y no solo su código de salida |
| Atomicidad del reemplazo de varios archivos existentes | La primera operación que edite un producto, en la Fase 3 |
| Ampliación de la gramática de reglas | Una regla del modelo que las formas admitidas no expresen |
| El modelo de variabilidad y los nombres del estándar como dato de cada plantilla | Transforms encadenados en el motor |

Lo diferido queda como punto de extensión del mecanismo y no como limitación de la solución.

[image1]: <../Insumos/Diagramas/MG-04_fig1_derivacion_de_una_operacion.svg>
[cap1]: <../Insumos/Evidencias/MG-04_cap1_recorrido_interactivo.png>
[cap2]: <../Insumos/Evidencias/MG-04_cap2_derivacion_de_un_producto.png>
