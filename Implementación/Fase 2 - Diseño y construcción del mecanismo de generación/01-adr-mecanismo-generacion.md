# Log de decisiones — Mecanismo de generación

Trabajo de grado: *Desarrollo de una herramienta CLI para la generación automatizada de proyectos backend e integración de módulos reutilizables*
Fase 2 — diseño y construcción del mecanismo de generación

Las decisiones que aparecieron al construir el código de la fase (`Codigo/bsl-assets`, `Codigo/bsl-catalog`): las que los documentos 1 a 4 no habían resuelto, y las que resolvían de una forma que el código, al escribirse, no pudo sostener sin ajuste. Cada una es trazable a un documento de la fase, a un requerimiento de la Fase 1 o a una decisión previa del marco.

## Convenciones

- **Terminología**: igual que en el log de Fase 1, los términos técnicos se mantienen en inglés dentro de prosa en español.
- **Estados**: Aceptada · Aceptada (provisional) · Diferida · Revisada · Sustituida.
- **Numeración**: continúa la numeración global del marco. Este log abre en ADR-042, siguiendo a ADR-041 de la Fase 1.

**Significado de los estados**

| Estado | Qué indica |
| :---- | :---- |
| Aceptada | Decisión firme, aplicada en el código construido |
| Aceptada (provisional) | Decisión tomada sin evidencia suficiente para cerrarla, con su condición de revisión declarada |
| Diferida | Corresponde a una fase posterior; se conserva como insumo |
| Revisada | Modifica una decisión previa de esta misma fase o de la Fase 1 |
| Sustituida | Reemplazada por otra; se conserva por trazabilidad |

## Índice de decisiones

| ID | Decisión | Documento | Estado | Revisada después por |
| :---- | :---- | :---- | :---- | :---- |
| ADR-042 | Criterio de madurez aplicado a todo el toolchain | Doc 2 | Aceptada | — |
| ADR-043 | Valor por defecto de `SERVICE_NAME` | Doc 2 | Aceptada | — |
| ADR-044 | Casos de uso construidos con fábricas en el punto de composición | Doc 2 | Aceptada | — |
| ADR-045 | Rango de dependencia `^0.1.0` para `@bsl/contracts` | Doc 2 / Doc 3 | Aceptada | **ADR-147** |
| ADR-046 | Identidad de los tokens de inyección bajo instalaciones duplicadas | Doc 2 | Aceptada (provisional) | — |
| ADR-047 | Inglés como idioma del contenido de los repositorios de código | Transversal | Aceptada | — |
| ADR-048 | Esquema JSON explícito para el manifiesto del catálogo | Doc 3 | Revisada | **ADR-171** |
| ADR-049 | Conventional Commits y hooks de git como estándar de confirmación | Transversal | Aceptada | **ADR-148** |
| ADR-050 | Resolución de los activos contra el registro, con pin de versiones en la herramienta | Doc 3 / Doc 4 | Aceptada | **ADR-162** |
| ADR-051 | Origen de la dirección del registro al derivar | Doc 3 / Doc 4 | Aceptada | — |
| ADR-052 | Contrato de operación declarativo y registro estático como punto de extensión | Doc 4 | Aceptada | **ADR-071** |
| ADR-053 | Núcleo sin efectos: la operación recibe puertos ya construidos | Doc 4 | Aceptada | — |
| ADR-054 | Organización del paquete de la herramienta por responsabilidad | Doc 4 | Aceptada | — |
| ADR-055 | Tres vías de entrada con precedencia y una sola tubería de resolución | Doc 4 | Aceptada | — |
| ADR-056 | Evaluador de reglas con gramática cerrada, sin evaluación de código | Doc 4 | Aceptada | — |
| ADR-057 | Plan de cambios de tres clases y escritura transaccional | Doc 4 | Aceptada | **ADR-103**, **ADR-117**, **ADR-118** |
| ADR-058 | Taxonomía de errores y códigos de salida | Doc 4 | Aceptada | — |
| ADR-059 | Dependencias de la herramienta | Doc 4 | Aceptada | — |
| ADR-060 | Operación de lectura `assets` como verificación del núcleo | Doc 4 | Aceptada | — |
| ADR-061 | Lectura del registro de versiones del producto en el núcleo | Doc 4 | Aceptada | — |
| ADR-062 | Presentación de la salida: banner, color condicionado y pasos siguientes | Doc 4 / Doc 5 | Aceptada | **ADR-129** |
| ADR-063 | Inicialización de repositorio git en el producto derivado | Doc 5 | Aceptada | — |
| ADR-064 | Forma del comando de generación y destino del producto | Doc 5 | Aceptada | — |
| ADR-065 | Plantillas en la herramienta y motor de sustitución sin lógica | Doc 5 | Aceptada | **ADR-172** |
| ADR-066 | El activo base es la salida de las plantillas, verificado por regeneración | Doc 5 | Aceptada | — |
| ADR-067 | Punto de composición generado y omisión de las piezas opcionales | Doc 5 | Aceptada | **ADR-134** |
| ADR-068 | Derivación por término de acción y recorte de los términos no usados | Doc 5 | Aceptada | — |
| ADR-069 | Determinismo definido sobre el árbol, excluyendo el momento de derivación | Doc 5 | Aceptada | — |
| ADR-070 | Rango del contrato en el producto y versión exacta en su registro | Doc 5 | Aceptada | — |
| ADR-071 | Registro de operaciones y despacho fuera del núcleo | Doc 4 | Aceptada · revisa ADR-052 | — |
| ADR-072 | Exclusión de RF-04 y su reasignación a la Fase 3 | Doc 5 / Transversal | Aceptada | — |
| ADR-073 | Versión mínima del entorno comprobada en el punto de entrada | Doc 4 | Aceptada | — |
| ADR-074 | La consulta del registro se hace sin workspaces | Doc 4 | Aceptada | — |
| ADR-075 | Una sola copia de cada artefacto declarativo en el paquete publicado | Doc 4 | Aceptada · revisa ADR-050 | — |
| ADR-076 | El arranque informa en qué dirección quedó escuchando el producto | Doc 2 | Aceptada | — |
| ADR-077 | Sondas de vida y de disponibilidad en el activo base | Doc 2 | Aceptada | — |
| ADR-078 | Carpeta propia para el rol que multiplica dentro de la capa | Doc 2 / Doc 5 | Aceptada · revisa ADR-020 | — |
| ADR-079 | Política de versión del framework: adoptar la estable vigente y permanecer en ella | Doc 2 | Aceptada · revisa ADR-042 | — |
| ADR-080 | El producto permanece en CommonJS sobre los paquetes ESM de NestJS 12 | Doc 2 | Aceptada · revisa ADR-073 | — |
| ADR-081 | El rechazo de un valor nombra su formato y da un ejemplo | Doc 1 / Doc 4 | Aceptada | **ADR-136** |
| ADR-082 | El producto declara su alcance | Doc 2 / Doc 5 | Aceptada | **ADR-136** |
| ADR-083 | El registro del producto guarda la entrada resuelta | Doc 5 | Aceptada | **ADR-132** |
| ADR-084 | El activo base registra cada request por el puerto de registro | Doc 2 | Aceptada | **ADR-152**, **ADR-153** |
| ADR-085 | El framework escribe sus propias entradas por el puerto de registro | Doc 2 | Aceptada | **ADR-128**, **ADR-133** |
| ADR-086 | La verificación no modifica lo verificado | Doc 6 | Aceptada | — |
| ADR-087 | Criterio de cobertura por lógica propia, con los exentos declarados | Doc 6 | Aceptada | — |
| ADR-088 | El arranque y las sondas se comprueban en ejecución dentro del verificador | Doc 6 | Aceptada | **ADR-150** |
| ADR-089 | La regla de dependencia se comprueba con una prueba negativa | Doc 6 | Aceptada | — |
| ADR-090 | La configurabilidad del producto se comprueba por barrido de su código | Doc 6 | Aceptada | — |
| ADR-091 | Forma de la evidencia: comando, resultado y fecha | Doc 6 | Aceptada | — |
| ADR-092 | Frontera entre el documento de pruebas y el de trazabilidad | Doc 6 | Aceptada | — |
| ADR-093 | Reparto documental: el README es dueño del cómo, el documento de fase del camino | `packages/cli/TUTORIAL.md` | Aceptada | — |
| ADR-094 | El registro de un producto no es un archivo de entrada | `packages/cli/TUTORIAL.md` | Aceptada | — |
| ADR-128 | El producto escribe su log en dos formas, una por entorno | Doc 2 | Revisada | **ADR-133**, **ADR-152** |
| ADR-129 | La forma de la salida de la herramienta vive en el adaptador, y la ayuda abre con el banner | Doc 4 / Doc 5 | Revisada | — |
| ADR-131 | El adaptador de repositorio declara al arrancar qué es y si el dato sobrevive al reinicio | Doc 2 | Aceptada | — |
| ADR-132 | El registro del producto declara el efecto de negocio de cada operación, y su lectura tolera la forma anterior | Doc 5 | Revisada | — |
| ADR-133 | Cada request tiene nombre dentro del servicio; la propagación entre servicios sigue siendo del módulo | Doc 2 | Revisada | **ADR-151** |
| ADR-134 | El producto trae una prueba de humo de su superficie HTTP, y no es una pieza opcional | Doc 5 | Revisada | — |
| ADR-135 | La Business Area de una entrada del espacio de selección es una de las cinco del estándar | Doc 1 | Aceptada | **ADR-137** |
| ADR-136 | El alcance del producto se declara antes de derivarlo, y el prompt nombra el formato que espera | Doc 5 | Revisada | — |
| ADR-137 | Ante una discrepancia sobre la jerarquía del estándar, manda el portal y no el documento del marco | Doc 1 | Revisada | — |
| ADR-138 | Una entrada del espacio de selección existe cuando sirve a un propósito escrito del proyecto | Doc 1 | Aceptada | — |
| ADR-139 | El dato de una capacidad se transcribe del documento oficial de su Service Domain | Doc 1 | Revisada | — |
| ADR-140 | El verbo y la ruta salen del action term; la forma de ruta es punto de variación | Doc 1 | Revisada | **ADR-154**, **ADR-155** |
| ADR-141 | Los behavior qualifiers entran al espacio de selección como segundo nivel | Doc 1 | Aceptada | — |
| ADR-142 | Una operación de behavior qualifier produce superficie y andamio, nunca una entidad inventada | Doc 5 | Aceptada | — |
| ADR-143 | Se admite declarar una capacidad fuera del catálogo, con la forma cerrada | Doc 1 | Revisada | — |
| ADR-144 | El espacio de selección se presenta en lenguaje de negocio, con el nombre del estándar al lado | Doc 1 | Aceptada | **ADR-149** |
| ADR-145 | La derivación cierra con una revisión enmendable, no con una confirmación | Doc 5 | Aceptada | — |
| ADR-147 | El punto de composición del activo son tres archivos, y ningún archivo de `src/` queda sin tipo de elemento | Doc 2 | Aceptada | — |
| ADR-148 | La configuración del analizador de la herramienta fija su raíz, porque los patrones no resolvían desde el paquete | Doc 4 | Aceptada | — |
| ADR-149 | `display` se retira del modelo y `fixed` pasa a estar comprobado | Doc 1 | Aceptada | — |
| ADR-150 | El circuito de generación compara la lista de archivos de cada producto contra un manifiesto, no un conteo | Doc 6 | Aceptada | — |
| ADR-151 | La traza del estándar W3C entra al activo; exportarla sigue siendo del módulo | Doc 2 | Revisada | **ADR-161** |
| ADR-152 | Un asiento dice de qué despliegue viene, iza lo que se consulta y nunca lleva un secreto | Doc 2 | Revisada | **ADR-153**, **ADR-161** |
| ADR-153 | Todo fallo del producto se responde y se explica en un solo lugar | Doc 2 | Revisada | — |
| ADR-154 | El estilo de ruta por defecto es el de recurso, no el que publica el estándar | Doc 1 | Sustituida por ADR-155 | **ADR-155** |
| ADR-155 | La herramienta sirve una sola forma de ruta, la del recurso | Doc 1 | Aceptada | — |
| ADR-161 | El producto reporta su telemetría donde la produce, a un puerto que puede no tener adaptador | Doc 2 | Revisada | — |
| ADR-162 | El catálogo se resuelve como un activo más; la copia instalada con la herramienta es el piso | Doc 3 / Doc 4 | Revisada | — |
| ADR-163 | Lo que declara una versión de la línea que el feed no sirve no se publica | Doc 3 / Doc 6 | Aceptada | — |
| ADR-166 | Una lista de opciones tiene principio y fin, y la acción que termina se nombra por lo que hace | Doc 4 / Doc 5 | Aceptada | — |
| ADR-169 | Una respuesta que no se acepta no termina el comando, y salir se declara en la pregunta | Doc 1 / Doc 4 | Aceptada | — |
| ADR-170 | Lo obligatorio se dice donde se pregunta y donde se documenta | Doc 4 / Doc 5 | Aceptada | — |
| ADR-171 | La plantilla es un activo del catálogo que se describe a sí mismo | el índice de la fase / Doc 3 | Aceptada | — |
| ADR-172 | Las plantillas viven en el activo que las usa, no en la herramienta | Doc 5 | Aceptada | — |
| ADR-173 | Motor con gramática cerrada: condición y repetición sin evaluar código | Doc 5 | Aceptada | — |
| ADR-174 | Lo que no es expresable como dato, y dónde queda | Doc 5 / Doc 7 | Aceptada | — |
| ADR-175 | La derivación es un intérprete del manifiesto, sin estándar ni framework dentro | Doc 5 / Doc 7 | Aceptada | — |
| ADR-176 | La forma del producto es un contrato declarado y comprobable | Doc 7 | Revisada | — |
| ADR-177 | El esquema del registro de un producto se compara por versión mayor | Doc 4 | Aceptada | — |
| ADR-178 | Los comandos se agrupan, y los nombres publicados quedan como alias | Doc 4 / `packages/cli/TUTORIAL.md` | Aceptada | — |
| ADR-179 | Una plantilla de otra familia como evidencia de que el intérprete es genérico | Doc 6 / Doc 7 | Aceptada | — |
| ADR-192 | Las plantillas viven juntas, con una convención de nombres y un procedimiento para agregar una | Doc 7 | Aceptada | — |
| ADR-193 | El producto registra la plantilla que lo derivó, y no un literal | Doc 2 / Doc 7 | Aceptada | — |
| ADR-194 | La segunda plantilla de la línea: Azure Functions, con sus límites declarados | Doc 7 | Aceptada | — |
| ADR-196 | Leer una plantilla no es derivar de ella, y publicar un activo no activa su entrada | Doc 3 / Doc 4 | Aceptada | — |
| ADR-197 | La plantilla se decide antes de la primera pregunta, y se pregunta si la invocación no la nombra | Doc 1 / Doc 5 | Aceptada | — |
| ADR-198 | El reporte de la derivación se lee del producto escrito | Doc 5 | Aceptada | — |

---

## ADR-042 · Criterio de madurez aplicado a todo el toolchain

**Estado:** Aceptada · 2026-10-19 · Doc 2

**Contexto.** El doc 2 §11 fija el criterio de versión solo para el framework destino: "descartando una versión mayor publicada en los últimos meses". Al construir, Node, TypeScript, ESLint, `eslint-plugin-boundaries` y Jest tenían también mayores recién publicadas (TypeScript 6/7, ESLint 10 recién salido de 9, boundaries 6/7).

**Decisión.** El criterio de madurez del doc 2 se aplica a todo el toolchain, no solo al framework: Node 24 LTS, TypeScript `~5.9`, NestJS `^11.2`, ESLint `~10.13` (9 quedó sin soporte), `typescript-eslint` `^8`, `eslint-plugin-boundaries` `~5.4` (la sintaxis del doc 2 §6 es de esa versión), Jest `^30`, Zod `^4`, ajv `^8`.

**Consecuencia.** El doc 2 §11 queda parcialmente desactualizado: su extracto de `package.json` fija `zod: "^3.0.0"` y no declara el resto de versiones. Se registra como ajuste pendiente al documento.

**Traza.** Doc 2 §11.

---

## ADR-043 · Valor por defecto de `SERVICE_NAME`

**Estado:** Aceptada · 2026-10-19 · Doc 2

**Contexto.** El doc 2 §7 declara `SERVICE_NAME` como obligatoria, sin valor por defecto. El el índice de la fase (Alcance) exige que el producto derivado arranque sin edición previa de archivos. Sin un valor por defecto, `npm start` falla apenas se clona el activo base o un producto derivado, porque nadie completó un `.env`.

**Decisión.** `SERVICE_NAME` toma por defecto `process.env.npm_package_name`, que npm define automáticamente al correr un script. Como el mecanismo de derivación reescribe `package.json#name` con el `projectName` resuelto, el nombre del servicio queda correcto sin que nadie lo configure.

**Límite asumido.** Si el proceso se arranca sin pasar por un script de npm (por ejemplo `node dist/main.js` directo, sin que la variable esté seteada), la validación falla y nombra la variable. Es el mismo comportamiento que tendría cualquier variable obligatoria sin configurar.

**Traza.** el índice de la fase (condición de llegada), Doc 2 §7, RNF-05.

---

## ADR-044 · Casos de uso construidos con fábricas en el punto de composición

**Estado:** Aceptada · 2026-10-19 · Doc 2

**Contexto.** El doc 2 §9 registra los casos de uso en `app.module.ts` como providers de clase (`useClass` implícito). Para que NestJS resuelva sus dependencias automáticamente, la clase necesitaría `@Injectable()` y `@Inject(TOKEN)` en su constructor. La capa `application` tiene prohibido depender de `@nestjs/*` (doc 2 §6, regla `boundaries/external`), así que esa anotación haría fallar el propio analizador que el documento exige.

**Decisión.** Los casos de uso quedan como clases TypeScript puras, sin decoradores. `app.module.ts` los construye con `useFactory` e `inject`, pasando las dependencias ya resueltas por posición. El orden de `inject` coincide con el de los parámetros de la fábrica.

**Consecuencia.** El código de `app.module.ts` en el doc 2 §9 queda desactualizado: muestra los casos de uso como entradas simples del arreglo `providers`, sin `useFactory`. Se registra como ajuste pendiente al documento.

**Traza.** Doc 2 §6, Doc 2 §9, MR-03 (regla de dependencia).

---

## ADR-045 · Rango de dependencia `^0.1.0` para `@bsl/contracts`

**Estado:** Aceptada · 2026-10-19 · Doc 2 / Doc 3

**Contexto.** El extracto de `package.json` del doc 2 §11 fija `"@bsl/contracts": "^1.0.0"`. El doc 3 §4 fija la política de versionado de la fase: `0.x` durante la construcción, `1.0.0` solo al cerrarla. Un rango `^1.0.0` no resuelve ninguna versión `0.x` publicada.

**Decisión.** Mientras la fase esté en construcción, el activo base depende de `@bsl/contracts` con `^0.1.0`, coherente con la política del doc 3 §4. El rango sube a `^1.0.0` cuando se publique la versión `1.0.0` del contrato, al cerrar la fase.

**Traza.** Doc 2 §11, Doc 3 §4.

---

## ADR-046 · Identidad de los tokens de inyección bajo instalaciones duplicadas

**Estado:** Aceptada (provisional) · 2026-10-19 · Doc 2

**Contexto.** Cada token de puerto se declara como `Symbol('NombreDelPuerto')`. Un `Symbol` creado así es único por cada evaluación del módulo. Si un producto derivado, al incorporar módulos en la Fase 3, terminara con dos copias instaladas de `@bsl/contracts` (por ejemplo, por rangos `^0.x` estrechos entre un módulo y el activo base), cada copia tendría su propio `LOGGER_PORT`, y la inyección fallaría en silencio: NestJS buscaría un token que el proveedor no usa.

**Decisión.** Se acepta el riesgo para esta fase, porque hoy solo existe un consumidor de los tokens (el activo base) y no hay módulos que puedan duplicar la dependencia todavía.

**Condición de revisión.** Antes de que la Fase 3 incorpore el primer módulo del catálogo, se revisa si cambiar a `Symbol.for('NombreDelPuerto')` (que sí es único globalmente, incluso entre copias distintas del paquete) resuelve el riesgo sin costo, o si el gestor de paquetes ya garantiza una sola copia por árbol de dependencias.

**Traza.** Doc 2 §3.

---

## ADR-047 · Inglés como idioma del contenido de los repositorios de código

**Estado:** Aceptada · 2026-10-19 · Transversal

**Contexto.** El código se escribió inicialmente siguiendo la regla general del proyecto (prosa en español, términos técnicos en inglés), incluido un locale de Zod en español. El autor determinó que mezclar español e inglés dentro del código resulta confuso, y que la regla de idioma del proyecto está pensada para los documentos de `Implementación/` y la tesis, no para el contenido de los repositorios.

**Decisión.** Dentro de `Codigo/bsl-assets` y `Codigo/bsl-catalog`, todo el contenido queda en inglés: identificadores, mensajes de error y de log, nombres de prueba, textos de los artefactos JSON, TSDoc y READMEs. Esta regla rige únicamente dentro de los repositorios; los documentos de fase, los ADR y las guías de `Codigo/` dirigidas a quien programa siguen en español.

**Consecuencia.** Los fragmentos de texto en español que los docs 2, 3 y 4 citan literalmente (`prompt`, `description`, mensajes de validación, `owner` del catálogo) no coinciden con el texto real del código, que está en inglés. Se registra como ajuste pendiente a esos documentos.

**Traza.** Doc 1 §5-6, Doc 2 (mensajes citados en §6-7), Doc 3 §6-7.

---

## ADR-048 · Esquema JSON explícito para el manifiesto del catálogo

**Estado:** Revisada · 2026-10-19 · Doc 3 · **revisada el 2026-11-09 por ADR-171**

**Contexto.** El doc 3 §6 describe los campos de una entrada del catálogo en una tabla de prosa, pero no define un esquema JSON que los haga cumplir mecánicamente. Sin un esquema, nada impide que una entrada incorporada por propuesta de cambio (doc 3 §7) tenga un campo con el nombre mal escrito, o que un módulo omita `contractVersion`.

**Decisión.** Se agrega `catalog.schema.json`, con `additionalProperties: false` y la regla condicional de que `contractVersion` es obligatorio solo para `type: "module"` y está prohibido para los demás tipos. `catalog.json` declara `"$schema": "./catalog.schema.json"`. La validación corre en `verify` con ajv.

**Qué cambió (2026-11-09, ADR-171).** El enumerado de tipos gana `template`, y la regla condicional de `contractVersion` se reescribió porque no sabía decir lo que hace falta ahora: es **obligatorio** para un módulo, **admitido** para una plantilla —que declara el contrato contra el que se construyó— y **prohibido** para un activo base o para el paquete del contrato. El `if/then/else` original solo distinguía módulo de no-módulo, así que una plantilla no habría podido declararlo; quedó como un `allOf` de tres cláusulas. `base-template` pasó de `type: base-asset` a `type: template`. La validación con ajv no cambia.

**Traza.** Doc 3 §6-7, ADR-171.

---

## ADR-049 · Conventional Commits y hooks de git como estándar de confirmación

**Estado:** Aceptada · 2026-10-19 · Transversal

**Contexto.** Ninguno de los documentos de la fase regula el formato de los mensajes de commit ni exige verificación automática antes de confirmar o de subir cambios. Sin una regla escrita, cada commit quedaría a criterio de quien lo escribe, y nada impediría subir código que no pasa el lint, las pruebas o la auditoría de dependencias.

**Decisión.** Los commits de `Codigo/bsl-assets` y `Codigo/bsl-catalog` siguen Conventional Commits en inglés, en una sola línea (`type(scope): subject`), sin cuerpo, sin trailers y sin mención a herramientas de IA. Husky instala hooks de git: `pre-commit` corre formato, lint, tipos, pruebas y validación de artefactos; `commit-msg` valida el mensaje con commitlint; `pre-push` corre la verificación completa y una auditoría de dependencias de producción. El detalle vive en `Codigo/ESTANDAR-DE-COMMITS.md`.

**Traza.** Transversal a todo commit de los dos repositorios.

---

## ADR-050 · Resolución de los activos contra el registro, con pin de versiones en la herramienta

**Estado:** Aceptada · 2026-10-19 · Doc 3 / Doc 4

**Contexto.** El doc 3 §8 resolvió cómo la herramienta obtiene el catálogo: como dependencia propia con versión fija, lo que sostiene el determinismo de RF-05. No resolvió cómo obtiene el contenido de un activo. Una entrada del catálogo declara el paquete, no su versión. A ello se suma que la Fase 3 debe incorporar y actualizar módulos publicados después que la herramienta (RF-11, RF-12), que por definición no pueden viajar dentro de ella.

**Decisión.** El núcleo resuelve cualquier activo del catálogo contra el registro en tiempo de ejecución, mediante el propio gestor de paquetes, con caché local por paquete y versión. La versión que esta versión de la herramienta ofrece se declara en un artefacto propio, `asset-pins.json`, con su esquema. Un segundo modo, de ruta local a un directorio o a un tarball, permite desarrollar y probar sin red y sin publicar.

**Alternativas.** Declarar `@bsl/base-template` como dependencia de la herramienta, de modo que el activo viajara instalado con ella. Se descarta porque la Fase 3 tendría que construir un segundo mecanismo de obtención para los módulos, que es el retrabajo que la frontera del índice de la fase busca evitar.

**Por qué.** El determinismo no lo da el empaquetado sino el pin: dos ejecuciones de la misma versión de la herramienta resuelven la misma versión del activo. El requisito de red no agrega ninguna restricción nueva, porque el producto derivado depende de `@bsl/contracts`, que vive en el registro: sin acceso al feed, RF-01 no se cumple con activo empaquetado ni sin él.

**Consecuencia.** El doc 3 §8 incorpora la nota del pin. El doc 4 construye el resolutor genérico con los dos modos, indiferente a si el activo es `base-asset` o `module`. La Fase 3 lo reutiliza sin modificarlo.

**Traza.** el índice de la fase (frontera con la Fase 3), Doc 3 §6 y §8, RF-05, RF-10, RF-11, RF-12, RF-15.

---

## ADR-051 · Origen de la dirección del registro al derivar

**Estado:** Aceptada · 2026-10-19 · Doc 3 / Doc 4

**Contexto.** El activo base almacena su configuración de registro con un marcador, `@bsl:registry=https://<direccion-del-feed>/`, y el doc 3 §3 establece que el mecanismo de derivación la reescribe con la dirección real. Ningún documento declara de dónde toma la herramienta esa dirección.

**Decisión.** El núcleo la lee de la configuración de npm del entorno donde se ejecuta, admite sobreescribirla por bandera, y cuando no está configurada falla nombrando el dato que falta en lugar de generar un producto que no instala.

**Por qué.** Quien deriva un producto ya necesita resolver `@bsl/contracts` desde el registro, de modo que su entorno tiene el espacio de nombres configurado. Pedir el dato otra vez sería pedir lo que el entorno ya conoce. La dirección no queda escrita en ningún documento ni en el código de la herramienta, lo que mantiene la agnosticidad del registro que el marco exige.

**Consecuencia.** El doc 4 construye la lectura y el fallo con nombre. El producto derivado queda instalable sin configuración previa en el entorno de quien lo derivó.

**Traza.** Doc 3 §3, RF-15, RNF-05.

---

## ADR-052 · Contrato de operación declarativo y registro estático como punto de extensión

**Estado:** Aceptada · 2026-10-20 · Doc 4 · **Revisada en ADR-071** (2026-10-22): el registro y el despacho no viven en el núcleo. Lo demás sigue firme.

**Contexto.** El alcance de la fase asignó al núcleo el contrato de una operación y el punto de extensión que la Fase 3 usará. Una operación puede declarar sus parámetros como datos y dejar que el núcleo construya el análisis de argumentos, la ayuda y la validación, o puede recibir `argv` y analizarlo por su cuenta.

**Decisión.** Una operación es un objeto declarativo: nombre, resumen, parámetros como datos y una función `execute(input, context)`. El núcleo construye con esa declaración el análisis de argumentos, la ayuda y la validación. El registro de operaciones es un arreglo estático que una operación nueva amplía con una línea; ADR-071 lo sitúa en `operations/registry.ts` y no en el núcleo, porque enumerar las operaciones obliga a importarlas.

**Alternativas.** Operación como clase que analiza sus argumentos: se descarta porque la Fase 3 duplicaría validación y ayuda en cada operación, sin garantía de que tres operaciones traten igual una bandera ausente. Descubrimiento dinámico de operaciones desde paquetes instalados: se descarta porque ningún requerimiento pide extensibilidad por terceros y haría que el comportamiento dependiera de lo instalado, lo que rompe RF-05.

**Consecuencia.** Agregar una operación no modifica ninguna otra pieza del núcleo. El descubrimiento dinámico queda como punto de extensión declarado.

**Traza.** el índice de la fase (frontera con la Fase 3), Doc 4 §4, RF-05, RNF-01.

---

## ADR-053 · Núcleo sin efectos: la operación recibe puertos ya construidos

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** El núcleo tiene que leer artefactos, obtener paquetes del registro, preguntar en la terminal, escribir archivos y registrar el momento de la derivación. Si cada pieza usa los módulos del entorno directamente, no hay forma de probarla sin disco, sin red y sin terminal.

**Decisión.** El núcleo declara cinco puertos —sistema de archivos, registro de paquetes, preguntas, reporte y reloj— y los recibe ya construidos en el contexto de la operación. Los adaptadores son el único lugar con efectos, y `src/core/**` no puede importar `node:fs`, `node:process`, `node:os`, `node:child_process` ni la librería de preguntas; la restricción la hace cumplir el analizador.

**Por qué.** Es la misma disciplina que el marco exige a los productos de la línea, aplicada a la herramienta que los produce. El reloj entra como puerto porque el registro de versiones del producto declara el momento de la derivación, y sin fijarlo el determinismo de RF-05 no sería verificable.

**Consecuencia.** Las pruebas del núcleo usan dobles escritos a mano y corren en cualquier entorno. `run` devuelve el código de salida en lugar de terminar el proceso, para poder invocarlo desde una prueba.

**Traza.** Doc 4 §5 y §14, RF-05, MR-04.

---

## ADR-054 · Organización del paquete de la herramienta por responsabilidad

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** La estructura canónica del marco está definida para un producto de la familia: capas de dominio, aplicación e infraestructura alrededor de un bounded context. La herramienta no es un producto de la familia: no expone API HTTP ni modela un dominio de negocio.

**Decisión.** El paquete se organiza en `core`, `operations`, `cli`, `adapters` y la composición en `main.ts`, con la regla de dependencia activa en el analizador. No se aplica la estructura canónica del producto generado.

**Por qué.** Aplicar la estructura canónica produciría una capa de dominio vacía y una clasificación que no corresponde a lo que la herramienta hace. La propiedad que el marco busca —que los efectos queden confinados y la regla sea verificable— se conserva con esta organización.

**Consecuencia.** La ausencia queda declarada en el documento para que no se lea como inconsistencia con el marco.

**Traza.** ADR-002 (alcance de la familia), Doc 4 §3.

---

## ADR-055 · Tres vías de entrada con precedencia y una sola tubería de resolución

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** El modelo de variabilidad fijó la entrada resuelta como documento JSON y declaró que la vía no interactiva lo admite. Faltaba decidir si existen banderas, qué ocurre al mezclar vías y qué hace la herramienta cuando falta un dato y no hay terminal.

**Decisión.** Tres vías —banderas, archivo y preguntas— con precedencia bandera sobre archivo sobre valor por defecto del modelo sobre pregunta. Las preguntas son el último paso de la misma tubería y solo alcanzan a los puntos que siguen sin valor. Sin terminal interactiva, o con `--non-interactive`, la resolución falla nombrando todos los puntos ausentes en lugar de quedar esperando una respuesta.

**Alternativas.** Dos vías excluyentes, todo interactivo o todo en archivo. Se descarta porque obligaría a escribir un JSON para cualquier uso automatizado y eliminaría la forma de una sola línea, que es la que se usa al probar.

**Consecuencia.** La validación y las reglas se aplican una sola vez, al final de la tubería, de modo que ninguna vía admite algo que otra rechace. El comando de generación declara `--input` como su parámetro; el núcleo aporta el mecanismo.

**Traza.** Doc 1 §11, Doc 4 §6, RF-02, RF-05, RNF-01.

---

## ADR-056 · Evaluador de reglas con gramática cerrada, sin evaluación de código

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** El modelo de variabilidad declara sus reglas como texto (`operations.length >= 1`, `domainEvents => operations.some(o => o.mutates)`) y promete que las reglas residen en el modelo y no en el código del generador. Evaluar esas expresiones con el intérprete del lenguaje sería trivial de implementar.

**Decisión.** El núcleo trae un evaluador propio con una gramática cerrada: identificador, negación, comparación de cardinalidad, `some` sobre un campo booleano de las opciones elegidas, e implicación. Una expresión fuera de esa gramática es un error de sintaxis, y la validación de artefactos del paquete evalúa la sintaxis de todas las reglas del modelo, de modo que el fallo ocurre al verificar la herramienta y no al derivar un producto.

**Por qué.** Evaluar la expresión como código convertiría un archivo de datos en código ejecutable con los permisos de quien deriva. La gramática cerrada mantiene el modelo como datos y conserva la promesa del doc 1.

**Consecuencia.** Una regla nueva puede exigir ampliar la gramática; queda declarado como punto de extensión.

**Traza.** Doc 1 §10, Doc 4 §7, RF-02, RNF-03.

---

## ADR-057 · Plan de cambios de tres clases y escritura transaccional

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** Hacía falta repartir la escritura entre el núcleo y las operaciones sin que el núcleo conociera plantillas ni marcadores concretos, y sin que un fallo a mitad de camino dejara un proyecto incompleto que alguien tenga que borrar a mano.

**Decisión.** Una operación no escribe: produce un plan de cambios con tres clases —`write` con el contenido que la operación entrega, `copy` de bytes sin leer el contenido, y `edit-at-marker` que inserta en un marcador declarado o falla si no está—. El núcleo materializa el plan en un directorio temporal y lo mueve al destino al terminar; si algo falla, no queda nada escrito. El destino debe no existir o estar vacío, sin sobrescritura ni fusión. `--dry-run` imprime el plan, ordenado por ruta, y no escribe.

**Por qué.** El criterio del reparto es que el núcleo decide cómo se aplica un cambio y la operación qué dice el cambio. La tercera clase existe desde esta fase porque el activo base ya lleva el marcador del punto de composición, y así la Fase 3 inserta el registro de un módulo sin construir infraestructura de escritura.

**Límite asumido.** Cuando un plan edita varios archivos existentes, el reemplazo final es archivo por archivo y un fallo del sistema de archivos en medio podría dejarlo a medias. No ocurre en esta fase, donde la generación solo crea archivos sobre un destino vacío. La Fase 3 lo resolverá con una copia de respaldo del conjunto tocado.

**Consecuencia.** El escritor no agrega marcas de tiempo ni rutas absolutas y aplica los cambios en el orden declarado, que es lo que hace comprobable el determinismo de RF-05.

**Traza.** Doc 2 §9 (marcador `bsl:modules`), Doc 4 §10, RF-05, RF-07.

---

## ADR-058 · Taxonomía de errores y códigos de salida

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** Un comando usado en una canalización necesita distinguir por su código de salida un error del usuario de un fallo del entorno. Ningún documento de la fase lo había fijado.

**Decisión.** Tres clases y cuatro códigos: 0 éxito; 1 error de uso o de validación de la entrada; 2 error de entorno o de activo; 70 error interno no previsto, informado como defecto de la herramienta. Todo mensaje nombra la causa y, cuando existe, la salida.

**Consecuencia.** Las operaciones no definen códigos propios: usan las dos clases de error del núcleo. El núcleo devuelve el código y la composición lo traduce, de modo que una prueba puede invocarlo sin terminar el proceso.

**Traza.** Doc 4 §11, RNF-01.

---

## ADR-059 · Dependencias de la herramienta

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** RNF-04 exige que la herramienta se someta a auditoría de dependencias, y cada dependencia es superficie que auditar. El análisis de argumentos y las preguntas interactivas podían resolverse con librerías o con código propio.

**Decisión.** El análisis de argumentos usa `parseArgs` de `node:util`, sin dependencia. La obtención de activos invoca al propio gestor de paquetes, sin cliente HTTP ni librería de empaquetado. Las preguntas interactivas usan `@inquirer/prompts`, única dependencia nueva de ejecución, junto al catálogo, que ya era dependencia por decisión del doc 3.

**Por qué.** La selección múltiple con descripciones y el manejo de una terminal interrumpida son varios cientos de líneas sin valor para el trabajo. Invocar al gestor de paquetes deja además la credencial del registro fuera de la herramienta. RNF-04 se satisface con que la auditoría corra y pase, no con no tener dependencias.

**Traza.** Doc 4 §5 y §15, RNF-04, RF-15.

---

## ADR-060 · Operación de lectura `assets` como verificación del núcleo

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** El documento del núcleo podía entregar solo piezas verificadas por pruebas unitarias, sin ningún comando ejecutable hasta el documento siguiente.

**Decisión.** El documento entrega además una operación de lectura, `bsl assets`, que lista las entradas del catálogo con su versión fijada y, con `--resolve <id>`, resuelve el activo e imprime el directorio y el origen.

**Por qué.** El resolutor de activos es la pieza con más probabilidad de fallar por causas ajenas al diseño: autenticación contra el feed, nombre del paquete, extracción, caché y rutas. Sin una operación que lo ejercite desde la terminal, el primer fallo aparecería al derivar el primer proyecto y habría que depurar resolución y derivación a la vez.

**Alcance declarado.** No es RF-08: ese requerimiento lista módulos del catálogo y los incorporados en un proyecto, y pertenece a la Fase 3.

**Traza.** Doc 4 §13, RF-14, RF-15.

---

## ADR-061 · Lectura del registro de versiones del producto en el núcleo

**Estado:** Aceptada · 2026-10-20 · Doc 4

**Contexto.** Toda operación posterior a la generación opera sobre un producto ya derivado: necesita localizar su raíz, leer su registro de versiones y rechazar un directorio que no sea un producto de la línea.

**Decisión.** El núcleo localiza el registro buscando hacia arriba desde el directorio de trabajo, valida su versión de esquema y rechaza con error de uso un directorio cuyo registro declare `kind: "template"`. La escritura del registro inicial pertenece al comando de generación y la de entradas de módulo a la Fase 3.

**Por qué.** Sin esto, cada operación de la Fase 3 reimplementaría la misma lectura. El campo `kind` del registro existe para distinguir plantilla y producto, y este es su primer consumidor.

**Traza.** el índice de la fase, Doc 2 §10, Doc 4 §9, RF-10.

---

## ADR-062 · Presentación de la salida: banner, color condicionado y pasos siguientes

**Estado:** Aceptada · 2026-10-20 · Doc 4 / Doc 5 · **Revisada en ADR-129** (2026-11-01): el banner entra también en la ayuda y la alineación pasa al adaptador. El reparto de responsabilidades que esta decisión fijó es el que ADR-129 lleva hasta el final.

**Contexto.** El núcleo declaraba un puerto de reporte con `info`, `warn`, `error` y `table`, suficiente para informar pero no para acompañar una operación larga. Una herramienta que crea un proyecto y termina en silencio deja al desarrollador sin saber qué sigue.

**Decisión.** El puerto de reporte gana `heading`, `step` y `success`. El adaptador de consola es el único que conoce los códigos de color, y lo aplica solo cuando la salida va a una terminal y el entorno no declara `NO_COLOR`. La herramienta abre con un banner, que se omite cuando la salida está redirigida, y toda operación que crea algo termina imprimiendo los pasos siguientes. Se agrega `picocolors` como dependencia.

**Por qué.** Los pasos siguientes son lo que evita que alguien tenga que leer la documentación para saber que hay que instalar antes de arrancar; es la práctica de las herramientas equivalentes del ecosistema. Condicionar el color preserva la salida limpia en una canalización, que es donde el código de salida y el texto se consumen por programa.

**Consecuencia.** El doc 4 §5 y §15 se ajustan: puerto, adaptador y dependencias.

**Traza.** Doc 4 §5, Doc 5 §2, RNF-01.

---

## ADR-063 · Inicialización de repositorio git en el producto derivado

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** Ningún documento decidía si el producto nace con repositorio. Las herramientas equivalentes del ecosistema lo inicializan por defecto: `nest new` salvo `--skip-git`, y `create-next-app` salvo `--disable-git`.

**Decisión.** El comando ejecuta `git init` y deja un commit inicial con todo lo generado. `--skip-git` lo omite. Si git no está instalado, la herramienta avisa y termina con éxito: el producto está generado y la ausencia de repositorio no lo invalida.

**Por qué.** Además de la convención del ecosistema, el commit inicial es la línea de base contra la cual se distingue qué modificó el desarrollador, que es lo que RNF-02 protege y lo que la operación de actualización de la Fase 3 necesita diferenciar.

**Traza.** Doc 5 §2, RNF-02.

---

## ADR-064 · Forma del comando de generación y destino del producto

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** El alcance de la fase asignó al núcleo la forma en que una operación recibe sus parámetros, pero no la forma del comando que deriva.

**Decisión.** `bsl new <nombre-del-proyecto>`, con el nombre como argumento posicional, destino por defecto `./<nombre-del-proyecto>` y `--output` para cambiarlo. El comando no instala dependencias: imprime los pasos siguientes, y `--install` las instala cuando se pide.

**Por qué.** El nombre es el mismo `projectName` del modelo; pedirlo como posicional y como bandera sería redundante. No instalar por defecto mantiene la generación rápida y utilizable sin red cuando el activo ya está en caché, y la instalación obligatoria habría atado el comando al acceso al registro en cada ejecución.

**Traza.** el índice de la fase, Doc 5 §2, RF-01, RNF-01.

---

## ADR-065 · Plantillas en la herramienta y motor de sustitución sin lógica

**Estado:** Sustituida · 2026-10-20 · Doc 5 · **sustituida el 2026-11-09 por ADR-172 y ADR-173**

**Contexto.** El activo base contiene un agregado real con dos operaciones. Un producto puede pedir cinco, entre ellas términos de acción que el activo no demuestra. Derivar por renombrado del activo no puede producir lo que el activo no tiene.

**Decisión.** Todo lo que depende del agregado o de las operaciones se rinde desde plantillas que viven en la herramienta, bajo `src/operations/generate/templates/`. La infraestructura técnica, la configuración y el entorno de trabajo se copian del activo, y `package.json` se reescribe campo a campo sobre el del activo. El motor sustituye marcadores `{{nombre}}` y no tiene condicionales ni bucles: lo opcional se resuelve eligiendo qué plantilla se rinde, y lo repetido componiendo fragmentos en el código de la operación. Un marcador sin valor es un error.

**Alternativas.** Renombrado de identificadores sobre el activo: no produce operaciones ausentes. Transformación por árbol sintáctico: dependencia grande y mucho código para un beneficio que el renombrado ya daba.

**Por qué.** Las plantillas pertenecen al mecanismo de derivación, no al producto, por lo que viven con la herramienta, igual que el modelo de variabilidad. Un motor sin lógica mantiene todas las decisiones en el código de la operación, de modo que leer las plantillas no es necesario para saber qué genera la herramienta, y cabe en quince líneas sin agregar dependencia.

**Consecuencia.** Existen dos fuentes del mismo código, el agregado del activo y las plantillas, lo que obliga a la verificación de ADR-066. `package.json` conserva una sola fuente para las versiones de dependencias.

**Qué se sustituyó y qué sobrevive (2026-11-09).** Las dos mitades de esta decisión cayeron por la misma razón, que es que el catálogo pasó a admitir más de una plantilla (ADR-171). La **ubicación** la sustituye **ADR-172**: las plantillas pertenecen al mecanismo, sí, pero a una plantilla del mecanismo, y no al programa que las interpreta, así que viven en el paquete del activo que las usa. El **motor** lo revisa **ADR-173**: gana condición y repetición, con una gramática cerrada y sin `eval`, porque una plantilla que no puede decir «esto va solo si el producto publica eventos» obliga a que la herramienta lo sepa, y entonces la herramienta conoce la plantilla. Sobrevive intacto lo que esta decisión protegía: la cirugía campo a campo sobre `package.json`, que conserva una sola fuente para las versiones de dependencias y hoy es una clase declarativa del catálogo del manifiesto (ADR-174); que un marcador sin valor es un error; y la verificación de ADR-066, que se conservó a través de toda la reescritura y sirvió como oráculo de cada paso.

**Traza.** Doc 2 §5, Doc 5 §3 a §8, RF-02, ADR-171, ADR-172, ADR-173, ADR-174.

---

## ADR-066 · El activo base es la salida de las plantillas, verificado por regeneración

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** Con plantillas en la herramienta, el agregado de referencia del activo y las plantillas describen el mismo código y pueden divergir en silencio.

**Decisión.** Una prueba rinde las plantillas con la entrada de Party Reference Data Directory —agregado `PartyReference`, operaciones `initiate` y `retrieve`, con eventos y pruebas— y compara el resultado con los archivos del activo base, falla mostrando la diferencia y corre con `verify`.

**Consecuencia.** El activo base deja de ser un proyecto parecido a lo que la herramienta genera y pasa a ser exactamente eso. Para que la igualdad se cumpla hay que uniformar tres textos del activo: la documentación de la entidad, los mensajes de invariante y la documentación del puerto de repositorio. Quedan anotados en el doc 5 §12 y se aplican al construir la operación.

**Traza.** Doc 2 §5, Doc 5 §12, RF-05.

---

## ADR-067 · Punto de composición generado y omisión de las piezas opcionales

**Estado:** Aceptada · 2026-10-20 · Doc 5 · **Revisada en ADR-134** (2026-11-02): `sampleTests` decide las pruebas de ejemplo del dominio; la prueba de humo de la superficie HTTP y su arranque se generan siempre.

**Contexto.** `app.module.ts` depende de todo lo que el producto eligió, y las piezas opcionales del modelo —eventos de dominio y pruebas de ejemplo— podían generarse e ignorarse o no generarse.

**Decisión.** El punto de composición se rinde desde plantilla, conservando literal el marcador `bsl:modules`. Cuando `domainEvents` es falso no se generan la clase base de evento, los eventos, el adaptador de publicación ni la dependencia del publicador en los casos de uso, y el punto de composición no registra ese puerto. Cuando `sampleTests` es falso no se genera el directorio de pruebas, pero sí su configuración.

**Por qué.** Un producto que declarara el puerto de publicación sin emisor tendría una declaración sin realización, que el marco prohíbe, y generar archivos inertes invita a editar el producto apenas se recibe, que es lo contrario de la condición de llegada de la fase.

**Traza.** Doc 1 §9, Doc 2 §9, Doc 5 §9, RF-01, RF-03.

---

## ADR-068 · Derivación por término de acción y recorte de los términos no usados

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** El modelo de variabilidad fijó la tabla de rutas para cinco operaciones de un Service Domain, pero no la regla general que las produce ni qué ocurre con los términos de acción que el espacio de selección todavía no usa.

**Decisión.** La forma de cada operación se deriva de su término de acción —`Initiate`, `Update`, `Retrieve`, `Execute`, `Control`— y la emisión de evento, de `mutates`. Los términos `Request`, `Exchange`, `Notify` y `Evaluate` no se derivan: una entrada que los declare hace fallar la resolución nombrando el término, en lugar de generar un producto incompleto. El contrato del repositorio declara la unión de los métodos que las operaciones seleccionadas necesitan. La pluralización del segmento de ruta usa una heurística de terminaciones regulares del inglés.

**Consecuencia.** Precisa dos filas del doc 1: la de normalización del identificador de operación, porque el nombre del caso de uso intercala el agregado, y la de multiplicidad del método del repositorio, que enunciaba uno por operación. Ambas quedaron ajustadas.

**Límite asumido.** La heurística de plural falla con un irregular como `person`; el segmento se corrige con una edición del producto, que RNF-02 admite.

**Traza.** Doc 1 §7, §8 y §10, Doc 5 §6 y §7, RF-02.

---

## ADR-069 · Determinismo definido sobre el árbol, excluyendo el momento de derivación

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** RF-05 exige que la misma entrada produzca el mismo resultado, y el registro de versiones del producto lleva el momento de la derivación, que cambia entre ejecuciones.

**Decisión.** El determinismo se define sobre el árbol completo del producto, byte a byte, excluyendo el campo `derivedAt` del registro. Lo sostienen tres reglas: las listas se ordenan por el orden declarado en el espacio de selección y no por el orden en que el usuario escribió las operaciones; los fragmentos se componen en orden fijo; y el renderizado no consulta el reloj ni el sistema de archivos.

**Por qué.** El campo es el dato que permite auditar cuándo se derivó un producto y ya forma parte del formato fijado en el doc 2. Quitarlo trasladaría esa información fuera del proyecto.

**Traza.** Doc 2 §10, Doc 5 §11, RF-05.

---

## ADR-070 · Rango del contrato en el producto y versión exacta en su registro

**Estado:** Aceptada · 2026-10-20 · Doc 5

**Contexto.** El producto derivado depende del artefacto de contratos. Fijar la versión exacta lo congela; un rango lo deja recibir correcciones compatibles.

**Decisión.** El `package.json` del producto declara el rango que el manifiesto del activo trae, hoy `^0.1.0`. La versión exacta resuelta al derivar queda registrada en `project.json`, junto con la del activo base.

**Por qué.** El rango es lo que la política de versionado del marco prevé y lo que RNF-06 necesita para que dos proyectos convivan con versiones distintas de un mismo activo. La trazabilidad no se pierde porque vive en el registro del producto, que es su lugar.

**Traza.** Doc 2 §10 y §11, Doc 3 §4, Doc 5 §10, RNF-06, RF-10.

---

## ADR-071 · Registro de operaciones y despacho fuera del núcleo

**Estado:** Aceptada · 2026-10-22 · Doc 4 · Revisa ADR-052

**Contexto.** ADR-052 y el doc 4 §4 situaban el registro de operaciones en `src/core/operation-registry.ts` y el despacho en `src/core/runner.ts`. Al construirlo, las dos piezas resultaron imposibles en ese lugar: enumerar las operaciones obliga a importar `operations`, y despachar obliga a importar `cli/argv` y `cli/help`. Ambas importaciones van de `core` hacia fuera, y la regla de dependencia que el propio doc 4 §3 declara y el analizador hace cumplir (`from: ['core'], allow: ['core']`) las rechaza. El diseño documentado no compilaba contra su propia regla.

**Decisión.** El registro pasa a `src/operations/registry.ts` y el despacho a `src/cli/runner.ts`. El runner recibe las operaciones en `RunnerServices.operations` en lugar de importarlas, y `main.ts` le pasa `OPERATIONS`. El núcleo conserva el contrato de operación (`core/operation.ts`); no la lista de las que existen. Se elimina `findOperation`: el runner busca sobre el arreglo que recibe.

**Por qué.** La regla de dependencia es la propiedad que el documento quería proteger, y el lugar de las dos piezas era un error de redacción del documento, no una decisión. Resolverlo moviéndolas mantiene intacto lo que ADR-052 decide de fondo —operación declarativa, registro estático, una línea por operación nueva— y añade una ventaja no buscada: con las operaciones inyectadas, `runner.spec.ts` despacha contra un registro propio sin tocar el real.

**Consecuencia.** El punto de extensión sigue siendo un arreglo de una línea, pero vive en `operations/` y no en el núcleo. ADR-052 queda revisada en ese punto y firme en todo lo demás. El doc 4 §3, §4 y §11 quedaron alineados con el código el 2026-10-22.

**Traza.** ADR-052, ADR-054, Doc 4 §3 y §4, RF-05.

---

## ADR-072 · Exclusión de RF-04 y su reasignación a la Fase 3

**Estado:** Aceptada · 2026-10-22 · Doc 5 · Transversal

**Contexto.** RF-04 pide que el proyecto generado produzca su documentación OpenAPI de forma automática, con prioridad `S`. El walkthrough del marco lo difirió a la Fase 2. El el índice de la fase y el doc 5 §15 de esta fase lo dejan fuera, cada uno con su razón, pero solo en prosa: al cerrar la fase el requerimiento quedaba sin cubrir y sin fase asignada, lo que lo convertía en una omisión y no en una decisión.

**Decisión.** RF-04 queda fuera del alcance de la Fase 2 y se reasigna a la Fase 3. El criterio es el que el índice de la fase enuncia: la documentación de API es una capacidad del producto, no una condición del mecanismo que lo produce. El marco ya habilita la fuente de la que se deriva —la separación entre tipos expuestos y objetos de dominio, ADR-022— de modo que lo diferido es el mecanismo que la genera, no su fundamento.

**Por qué la Fase 3 y no la Fase 4.** La Fase 3 construye operaciones nuevas sobre el núcleo y es la primera que vuelve a tocar un producto ya derivado. Generar la documentación de API cabe ahí, sea como módulo del catálogo o como pieza del activo base, sin abrir una fase nueva. La Fase 4 evalúa; no construye.

**Consecuencia.** El el índice de la fase de esta fase debe registrar RF-04 como requerimiento no satisfecho por decisión de alcance, con esta referencia, y no como hueco. El índice de la Fase 3 lo recoge como entrada propia al abrirse.

**Límite asumido.** Un producto derivado en esta fase no publica su contrato de API. El equipo que lo recibe lo documenta por su cuenta hasta que la Fase 3 lo resuelva.

**Traza.** RF-04, T-07, T-08, ADR-007 (criterio de exclusión documentada), ADR-022, el índice de la fase, Doc 5 §15.

---

## ADR-073 · Versión mínima del entorno comprobada en el punto de entrada

**Estado:** Aceptada · 2026-10-22 · Doc 4

**Contexto.** La herramienta declara `engines: >=22` en su manifiesto, pero el gestor de paquetes solo advierte y deja instalar igual. Al ejecutarla sobre Node 18 durante la primera demostración, falló al cargar la librería de preguntas con `The requested module 'node:util' does not provide an export named 'styleText'`, y la composición lo informó como defecto de la herramienta con el código 70. El mensaje no nombra la causa y el código de salida atribuye el fallo al lugar equivocado.

**Decisión.** El punto de entrada comprueba la versión mayor del entorno antes de importar nada de la herramienta. Si es anterior a 22, escribe en la salida de error qué versión necesita y cuál encontró, y termina con el código 2, el de error de entorno.

**Por qué.** El fallo original ocurría al cargar una dependencia, de modo que cualquier comprobación posterior a las importaciones llegaba tarde. Y es un error del entorno, no de la herramienta: el código de salida y el texto tienen que decirlo, que es lo que ADR-058 establece para las tres clases de error.

**Consecuencia.** El requisito deja de estar solo en el manifiesto y en el README: la herramienta lo hace cumplir. Se comprobó ejecutando el punto de entrada con Node 18 y con Node 22.

**Traza.** ADR-058, ADR-059, ADR-080, Doc 4 §11 y §15, RNF-01.

---

## ADR-074 · La consulta del registro se hace sin workspaces

**Estado:** Aceptada · 2026-10-22 · Doc 4

**Contexto.** El adaptador del registro pregunta al gestor de paquetes la dirección configurada para el espacio de nombres de la línea. Ese comando se niega a responder cuando se ejecuta dentro de un paquete de un monorepo, y el adaptador, que trata cualquier fallo como ausencia de configuración, devolvía indefinido. El efecto era que derivar un producto desde dentro de un monorepo fallaba con "No registry configured" aunque el registro estuviera configurado.

**Decisión.** La consulta de la dirección y la descarga de un activo se piden sin workspaces, de modo que el directorio desde el que se invoca la herramienta no cambie la respuesta.

**Por qué.** La dirección del registro es una propiedad del entorno de quien ejecuta, no del proyecto en el que está parado. Que el resultado dependiera del directorio contradecía el origen de la dirección que ADR-051 fijó.

**Traza.** ADR-050, ADR-051, Doc 4 §8.

---

## ADR-075 · Una sola copia de cada artefacto declarativo en el paquete publicado

**Estado:** Aceptada · 2026-10-22 · Doc 4 · Revisa ADR-050

**Contexto.** El doc 4 §15 publica los artefactos declarativos bajo `src`, para que la herramienta los lea del disco por su puerto de archivos. La operación de generación los necesita antes de eso: declara sus parámetros a partir del modelo de variabilidad, y esa declaración se resuelve al cargar el módulo, cuando todavía no hay contexto ni puertos. Al importarlos, el compilador los copió también a `dist`, y el paquete terminó llevando dos copias de la misma verdad.

**Decisión.** Una sola regla para todo lo que la herramienta lee de sí misma: **lo que es dato se carga con el módulo y viaja compilado; lo que es plantilla se lee del disco y viaja como archivo.** El manifiesto publica `bin`, `dist` y las plantillas. Los pines dejan de leerse por el puerto de archivos: el núcleo recibe la lista y solo la convierte en consulta por identificador, con `pinsById`. `toolDirectory` queda como el directorio de las plantillas.

**Por qué.** La duplicación no era un desperdicio de espacio sino dos fuentes de verdad para el mismo archivo, y nada garantizaba que un cambio alcanzara a las dos. La regla elegida se apoya en una distinción real: el modelo, el espacio de selección y los pines son datos que la herramienta consulta en memoria; las plantillas son archivos que se rinden.

**Consecuencia.** `readPins` desaparece del núcleo y el puerto de archivos pierde un consumidor. El doc 4 §5, §8 y §15 quedan por ajustar, y el README del paquete ya lo declara.

**Traza.** ADR-050, ADR-053, ADR-065, Doc 4 §5, §8 y §15.

---

## ADR-076 · El arranque informa en qué dirección quedó escuchando el producto

**Estado:** Aceptada · 2026-10-28 · Doc 2

**Contexto.** El arranque del activo base llamaba a `listen` con el puerto de la configuración y no escribía nada. En la primera demostración, quien levantó el producto no supo en qué puerto respondía: tuvo que abrir `.env` o el esquema de configuración para averiguarlo. El producto cumplía su condición de llegada —arranca sin editar un archivo— y aun así no era usable sin leer su código.

**Decisión.** Después de `listen`, el arranque escribe por el puerto de registro la dirección en la que responde, con el entorno de ejecución y la ruta de la sonda de vida como contexto. El nombre del servicio no se repite: el adaptador de registro ya lo pone en cada entrada.

**Por qué.** Es información que solo el proceso conoce en ese momento, porque el puerto puede venir del entorno. Y se escribe por el puerto de registro, no por la salida estándar: el activo no puede exigir puertos a los productos y saltárselos en su propio arranque.

**Consecuencia.** `main.ts` viaja tal cual a cada producto derivado, de modo que el cambio alcanza a todos sin tocar ninguna plantilla. El doc 2 §4 y §11 describen ese archivo y quedan por ajustar.

**Traza.** el índice de la fase (condición de llegada), Doc 2 §4, MR-04, RNF-01.

---

## ADR-077 · Sondas de vida y de disponibilidad en el activo base

**Estado:** Aceptada · 2026-10-28 · Doc 2

**Contexto.** El producto derivado no ofrecía forma de preguntar por su estado. Un servicio de una entidad regulada se opera con sondas: el orquestador necesita saber si reiniciar un proceso o sacarlo de rotación, y son dos preguntas distintas. El alcance de la fase excluye el despliegue y la infraestructura, pero la superficie que el producto expone para ser operado es del producto, no del despliegue.

**Decisión.** El activo base incorpora un adaptador de entrada montado en `health`, fuera de la ruta del agregado, con dos rutas. `GET /health/live` responde `200` con el estado, el nombre del servicio y los segundos en marcha, y no comprueba nada fuera del proceso. `GET /health/ready` responde `200` con la lista de comprobaciones, o `503` en cuanto una falla.

**Qué no responde, y por qué.** Ni variables de entorno, ni versiones de dependencias, ni direcciones internas, ni trazas de error. Una sonda es alcanzable antes de que se pida credencial alguna, de modo que lo que dice lo lee cualquiera que llegue al servicio; en un entorno regulado, revelar versiones es facilitarle el trabajo a quien busca una vulnerabilidad conocida.

**Por qué dos rutas y no una.** Responder ambas preguntas con la misma sonda convierte una dependencia caída en un ciclo de reinicios: el proceso está vivo y se lo reinicia por algo que el reinicio no arregla.

**Límite asumido.** La lista de comprobaciones nace vacía, porque el producto de esta fase persiste en memoria y no tiene dependencia externa que comprobar. El lugar donde un módulo de persistencia de la Fase 3 registra la suya queda marcado en el archivo, igual que el efecto de negocio de `Execute` en su caso de uso.

**Traza.** el índice de la fase (fuera de alcance), Doc 2 §8, ADR-068, RNF-03.

---

## ADR-078 · Carpeta propia para el rol que multiplica dentro de la capa

**Estado:** Aceptada · 2026-10-28 · Doc 2 / Doc 5 · Revisa ADR-020

**Contexto.** ADR-020 fijó la estructura del producto: capas arriba y, dentro del dominio, agrupación por agregado. Con las dos operaciones del agregado de referencia la forma es legible. Con cinco operaciones, `application/` acumula cinco archivos hermanos, `domain/<agregado>/` mezcla la entidad, su puerto y tres eventos, y `infrastructure/http/` junta el controlador, la respuesta y un tipo de entrada por operación. El producto nace así y el equipo que lo recibe le agrega las suyas: la forma se aplana justo donde más crece.

**Decisión.** Se agrega un nivel, y solo donde un rol se repite:

| Rol | Ubicación |
| :---- | :---- |
| Evento de dominio | `domain/<agregado>/events/` |
| Caso de uso | `application/<operación>/` |
| Tipo expuesto de entrada | `infrastructure/http/requests/` |

La entidad y el puerto de repositorio siguen en la raíz de la carpeta del agregado, a la vista. Las capas no se mueven, y el dominio se sigue agrupando por agregado.

**Por qué no contradice a ADR-020.** Esa decisión descartó agrupar el dominio **por tipo de patrón**, es decir sustituir la carpeta del agregado por `entities/`, `repositories/` y `events/`, y su argumento fue que obliga a tocar varias carpetas ante un cambio. Lo que se adopta aquí no sustituye la agrupación por agregado: la conserva y le agrega un nivel interno para lo que se repite. Un cambio en el agregado sigue ocurriendo dentro de su carpeta.

**Por qué no hay nivel de agregado en `application/` ni en `http/`.** ADR-004 fija un bounded context por producto: esa carpeta sería siempre una sola.

**Por qué `test/` no se reorganiza.** El producto nace con tres archivos de prueba de ejemplo. Imponer una jerarquía a tres archivos es ruido, y las pruebas que el equipo escriba son suyas.

**Consecuencia.** Cambia la forma de todo producto derivado, de modo que el activo base sube a `0.2.0` y la herramienta a `0.3.0`. El analizador no necesita cambios: sus patrones ya cubren cualquier profundidad. Quedan desalineados el árbol canónico de MR-03 §1 en la Fase 1, el doc 2 §4 y el doc 5 §3, §5, §8 y §13, con sus figuras.

**Traza.** ADR-004, ADR-020, ADR-025, Doc 2 §4, Doc 5 §3, RNF-02.

---

## ADR-079 · Política de versión del framework: adoptar la estable vigente y permanecer en ella

**Estado:** Aceptada · 2026-10-28 · Doc 2 · Revisa ADR-042

**Contexto.** ADR-042 fijó un criterio de madurez: descartar una versión mayor publicada en los últimos meses. Por eso el activo base quedó en NestJS `^11.2`. El 2026-10-28 la verificación de la plantilla empezó a fallar por un aviso de severidad alta sobre `multer` 2.0.0 a 2.4.0, que llega como dependencia transitiva de `@nestjs/platform-express`. La plantilla no versiona lockfile —se instala aparte en cada verificación—, de modo que resuelve siempre lo último que satisface sus rangos, y `^11.2.0` resuelve a 11.2.8, que fija `multer` 2.4.0. La versión parchada es `multer` 2.5.0 y la única línea de NestJS que la trae es la 12. La 11 sigue recibiendo parches —11.2.8 es de cinco días antes— pero no movió esa dependencia.

**Decisión.** El criterio de madurez se reemplaza por dos reglas:

1. **Al construir o al reconstruir el activo se adopta la versión estable vigente del framework.** Hoy NestJS `^12.3`.
2. **La línea permanece en ese major.** Una mayor nueva no se adopta por ser nueva: los avisos de seguridad y los defectos se resuelven dentro del major vigente, con la versión de parche que los corrija o, si no existe, con un `overrides` que fije la versión parchada de la dependencia transitiva.

**Por qué se abandona el criterio anterior.** Quedarse en una mayor anterior no es la opción conservadora que parecía. Un major viejo deja de recibir las actualizaciones de sus propias dependencias antes de quedar sin soporte, y entonces un aviso de severidad alta no tiene salida dentro de ese major: la línea queda sin poder publicar, que es exactamente lo que ocurrió. El riesgo que el criterio de madurez buscaba evitar —adoptar algo inmaduro— se controla mejor exigiendo que el activo pase su propia verificación completa con la versión nueva, que es una comprobación y no un pronóstico.

**Consecuencia.** El activo base pasa a NestJS `^12.3.2` y a `@nestjs/cli` `^12.0.11`, lo que resuelve el aviso: la auditoría de las dependencias de producción de la plantilla vuelve a dar cero vulnerabilidades. El activo sube a `0.3.0` y la herramienta a `0.4.0`. El `overrides` sobre `multer` queda descartado para este caso y registrado como el mecanismo de la regla 2. La tabla de versiones de `ESTANDAR-DE-CODIGO.md` y el doc 2 §11 y §12 quedan por ajustar, igual que la nota de ADR-042.

**Traza.** ADR-042, Doc 2 §11, Doc 2 §12, RNF-04, P-20.

---

## ADR-080 · El producto permanece en CommonJS sobre los paquetes ESM de NestJS 12

**Estado:** Aceptada · 2026-10-28 · Doc 2 · Revisa ADR-073

**Contexto.** NestJS 12 publica todos sus paquetes como ESM. El producto de la línea es CommonJS: ningún `package.json` declara `"type": "module"` y la salida compilada se consume con `require`. La pregunta que abre ADR-079 es si adoptar la 12 obliga a convertir el producto.

**Decisión.** El producto permanece en CommonJS. Las notas de la versión 12 son explícitas en que las aplicaciones CommonJS siguen funcionando, porque Node hace `require()` de un módulo ESM sin bandera desde la 22.12, y en que `nest upgrade` no convierte el proyecto a ESM ni a Vitest. De ahí tres ajustes, y solo tres:

| Ajuste | Por qué |
| :---- | :---- |
| `module` y `moduleResolution` del producto pasan de `node16` a `nodenext` | `node16` es anterior a `require(esm)` y el compilador rechaza con TS1479 cualquier importación de un paquete ESM desde un archivo CommonJS. `nodenext` la admite y sigue emitiendo CommonJS, porque el manifiesto no declara `"type": "module"` |
| El script de pruebas invoca `node --experimental-vm-modules node_modules/jest/bin/jest.js` | Jest necesita esa bandera para hacer `require()` de un paquete ESM. El soporte existe desde Jest 30.4 sobre Node 24.9, así que el piso de Jest sube a `^30.5` |
| `engines.node` del producto pasa a `>=24.9.0`, y a `>=24` en la herramienta y sus paquetes | Es el piso real: por debajo de 24.9 las pruebas del producto no corren. La herramienta sube a 24 para no entregar un producto que quien lo generó no pueda verificar, lo que **revisa la constante de ADR-073**, que la fijaba en 22 |

**Por qué no se invoca Jest con `NODE_OPTIONS`.** Un prefijo de variable de entorno en un script de npm no corre en Windows. Invocar el binario con `node` funciona en los tres sistemas.

**Por qué no ESM.** ESM con Vitest es la forma que `nest new` genera hoy, y es la dirección del ecosistema, pero costaba la extensión `.js` explícita en toda importación relativa del activo, de las diecinueve plantillas que llevan importaciones relativas y de las importaciones que `derive.ts` compone, más reemplazar el runner de pruebas de la línea. ESM con Jest cargaba con esa misma disciplina y además seguía necesitando la bandera experimental, porque Jest la exige también para ejecutar módulos ESM. Ninguna de las dos aporta una propiedad que el producto necesite hoy, y las dos cambian la forma de todo producto derivado.

**Consecuencia.** El producto generado lleva una bandera experimental de Node en su script de pruebas. Es experimental la implementación de Jest, no `require(esm)`, que es estable en Node desde la 22.12; no afecta al arranque ni a la compilación, solo a la ejecución de las pruebas. Se retira cuando Jest deje de exigirla. La evaluación de ESM con Vitest queda abierta para cuando la 12 tenga recorrido, sin fecha.

**Verificación.** Con NestJS 12.3.2, la plantilla instalada aparte supera su lint, sus tres suites con siete pruebas y su compilación; la auditoría de producción da cero vulnerabilidades; y `verify:generation` deriva `term-deposit-api` con 39 archivos y `party-directory-api` con 25, cada uno superando su propia verificación. Un producto derivado con dependencias instaladas arranca, informa por el puerto de registro en qué dirección escucha, y sus dos sondas responden `200`: resuelve `@nestjs/core` 12.3.2 y `multer` 2.5.0.

**Traza.** ADR-042, ADR-073, ADR-079, Doc 2 §11, Doc 4 §11, RNF-02, RNF-06.

---

## ADR-081 · El rechazo de un valor nombra su formato y da un ejemplo

**Estado:** Aceptada · 2026-10-28 · Doc 1 / Doc 4 · **Revisada en ADR-136** (2026-11-02): el formato y el ejemplo entran también en la pregunta, no solo en el rechazo y en la ayuda.

**Contexto.** Una revisión externa de la herramienta, hecha por un desarrollador ajeno a su construcción, se topó con que `--aggregate-name bolsillo` responde `aggregateName must match ^[A-Z][A-Za-z0-9]*$.` La condición que el modelo declara es una expresión regular, y el mensaje la imprime tal cual. Quien la lee tiene que interpretarla para saber qué escribir, y el intento se repite.

**Decisión.** La validación de un punto de variación puede declarar dos campos más, ambos opcionales: `format`, el nombre de la forma que el valor debe tener, y `example`, un valor que la satisface. Cuando existen, el rechazo dice la forma, el ejemplo y el valor recibido:

```
aggregateName must use PascalCase. Example: TermDeposit. Received: 'bolsillo'.
```

El ejemplo viaja además con la pregunta, de modo que `--help` y el prompt lo muestran antes del intento: `--aggregate-name <value>  Name of the root aggregate (e.g. TermDeposit)`. Un punto que no declara `format` conserva el mensaje anterior, que sigue siendo correcto.

**Por qué no se corrige el valor en silencio.** La revisión propone normalizar el valor automáticamente. Un identificador de agregado nombra carpetas, clases, rutas y eventos: cambiarlo sin decirlo esconde una decisión que es del desarrollador, y la primera vez que el nombre aparezca distinto en el código, nadie sabrá por qué.

**Consecuencia.** El esquema del modelo de variabilidad admite los dos campos y la validación de artefactos los acepta. El doc 1 debe sumarlos a la tabla de la validación y el doc 4 recoge el mensaje nuevo en su §5.

**Traza.** RNF-01, T-14, Doc 1, Doc 4 §5.

---

## ADR-082 · El producto declara su alcance

**Estado:** Aceptada · 2026-10-28 · Doc 2 / Doc 5 · **Revisada en ADR-136** (2026-11-02): el alcance se declara además **antes** de derivar, que es cuando todavía puede cambiar una decisión.

**Contexto.** La misma revisión externa llega a una observación que ninguno de sus catorce hallazgos agota: **elegir una capability del estándar puede hacer creer que lo generado es un producto de negocio, cuando es un habilitador técnico.** Lo generado no miente —las operaciones `Execute` y `Control` marcan en su TSDoc y con un comentario dónde va el efecto de negocio, la persistencia es un `Map` a la vista, el publicador de eventos es in-process— pero nada de eso está dicho **fuera del código**. Ni el resumen de la generación, ni el README del producto, ni su registro. Quien no lee el código asume que lo que hay es lo que parece.

**Decisión.** El producto declara su alcance en los dos lugares donde se lo lee sin abrir un archivo de código.

El **resumen de la generación** gana cuatro líneas: cuántas de las operaciones elegidas llevan su efecto de negocio y cuáles son andamios, que la persistencia es en memoria y los datos se pierden al detener el proceso, que los eventos se publican in-process y sin consumidores, y —solo cuando difieren— el agregado local frente al que la capability de referencia sugiere.

El **README del producto** gana: un párrafo de apertura que dice que es un punto de partida ejecutable y no un producto terminado, y que el agregado es una semilla cuyos atributos de negocio define el equipo; una columna `Business effect` con `implemented` o `scaffold` por operación; una sección de persistencia con el aviso de volatilidad y qué hay que implementar para cambiarla; una sección de eventos con lo mismo; y una sección `Trying it out` con un `curl` por operación.

**Por qué los ejemplos ejecutables y no OpenAPI.** La necesidad que la revisión enuncia en su punto 8 es poder probar un endpoint sin leer el código. Los ejemplos la resuelven con lo que ya se conoce al derivar —método, ruta y el cuerpo que el tipo de entrada valida— sin dependencias nuevas. RF-04 sigue reasignado a la Fase 3 por **ADR-072**: la documentación OpenAPI es una capacidad del producto, y esa decisión no se reabre.

**Por qué no `501 Not Implemented` en las operaciones de andamio.** La revisión lo propone para que el andamio no simule una respuesta funcional. Se descarta: la operación no está sin implementar —carga el agregado, lo persiste, publica su evento y registra el resultado—, lo que falta es el efecto de negocio, que por diseño pertenece al equipo del producto. Un `501` habría que borrarlo a mano en cada producto, contra RNF-02, y haría que una prueba de humo diera por buena una respuesta de error. Lo que faltaba no era un código de estado: era decirlo.

**Por qué tampoco un wizard de atributos.** El punto 5 de la revisión propone generar atributos de negocio o preguntarlos. Convertiría la herramienta en una de modelado de dominio e impondría supuestos a cada producto. La semilla se mantiene y se declara como tal, que es lo que la hacía confusa.

**Consecuencia.** Cambia lo que el producto dice de sí mismo, no lo que hace: ningún archivo de código del producto cambia por esta decisión. El doc 5 debe recoger el README nuevo y su composición.

**Traza.** T-02, T-10, T-07, T-08, RNF-02, ADR-072, Doc 2 §12, Doc 5 §9, Doc 5 §12.

---

## ADR-083 · El registro del producto guarda la entrada resuelta

**Estado:** Aceptada · 2026-10-28 · Doc 5

**Contexto.** `project.json` declara identidad, capability y activos incorporados, pero no el agregado ni las operaciones con que el producto fue derivado. La revisión externa lo encontró por su síntoma: un producto cuyo registro dice `Term Deposit` y cuyo código dice `Bolsillo`, sin nada que conecte los dos nombres, se lee como una contradicción.

**Decisión.** El registro gana dos campos, ambos opcionales en el tipo que lo lee: `aggregate`, el nombre del agregado raíz, y `derivation`, con las operaciones elegidas y las banderas de eventos y de pruebas de ejemplo. El nombre local y el de la capability quedan los dos en el registro, de modo que la diferencia es un dato y no una contradicción.

**Por qué ahora y no en la Fase 3.** Es aditivo y no mueve `schemaVersion`, así que un registro anterior se sigue leyendo. Hacerlo después obliga a migrar productos ya derivados, y es el dato que la Fase 3 necesita para operar sobre uno: saber qué agregado y qué operaciones tiene sin inferirlo del árbol de archivos.

**Consecuencia.** `ProjectRecord` declara los dos campos como opcionales por esa misma razón. El doc 2 §10 y el doc 5 deben recoger los campos nuevos.

**Traza.** RF-02, RF-05, RF-10, ADR-025, Doc 2 §10, Doc 5 §9.

---

## ADR-084 · El activo base registra cada request por el puerto de registro

**Estado:** Aceptada · 2026-10-28 · Doc 2

**Contexto.** El producto trae un logger estructurado y, desde ADR-076, informa en qué dirección quedó escuchando. Lo que no hace es registrar lo que se le pide: la revisión externa lo nombra como falta de visibilidad al consumir el servicio. Operar un servicio en un entorno regulado exige poder responder qué se le pidió, qué respondió y cuánto tardó.

**Decisión.** El activo base trae un interceptor que escribe una entrada por request, por `LoggerPort`, con el método, la ruta, el código de estado y la duración. Se registra con `APP_INTERCEPTOR` en el punto de composición, que es lo que permite inyectarle el puerto. Escribe tanto cuando el manejador responde como cuando falla —un request fallido no puede ser un silencio— y toma el estado del error cuando el error lo declara.

**Qué no registra.** El cuerpo de la petición ni el de la respuesta: es donde un producto de esta línea lleva datos de una persona. Y deja fuera las rutas bajo `health`: una plataforma las consulta cada pocos segundos y enterrarían todo lo demás; de su estado responde la sonda misma (ADR-077).

**Límite asumido.** No hay identificador de correlación ni métricas. Propagar un identificador entre servicios y exponer métricas son capacidades de un módulo transversal de observabilidad, que es lo que T-09 nombra y lo que la Fase 3 construye. Esta decisión cubre el mínimo que no puede faltar el primer día.

**Consecuencia.** El activo sube a `0.4.0` y la herramienta a `0.5.0`. El interceptor viaja copiado, igual que las sondas, y su prueba viaja con las de ejemplo: los conteos del producto de referencia pasan de 39 y 25 a 41 y 26. El doc 2 §4, §8 y §12 y el doc 5 §3 y §13 quedan por ajustar.

**Verificación.** Un producto en ejecución escribe `POST /bolsillos 201`, `GET /bolsillos/<id> 200` y `GET /bolsillos/no-existe 404` con su duración, y ninguna entrada para `/health/live` ni `/health/ready`.

**Traza.** T-09, ADR-076, ADR-077, RNF-02, Doc 2 §8, Doc 2 §9.

---

## ADR-085 · El framework escribe sus propias entradas por el puerto de registro

**Estado:** Aceptada · 2026-10-28 · Doc 2 · **Revisada en ADR-128** (2026-11-01): la forma del asiento la decide el entorno. Un solo idioma en producción sigue firme. · **Revisada en ADR-133** (2026-11-02): de las tres cosas que esta decisión difirió al módulo de observabilidad, nombrar la request dentro del servicio se adelanta; la propagación entre servicios y las métricas siguen diferidas.

**Contexto.** El producto escribe por `LoggerPort` una línea JSON por evento, y desde ADR-084 también una por request. NestJS, en cambio, escribe sus propias entradas de arranque —módulos cargados, rutas montadas— con su logger interno y su formato humano, con colores y alineación. El arranque de un producto quedaba así:

```
[Nest] 6827  - 10/28/2026, 4:12:10 PM     LOG [RouterExplorer] Mapped {/bolsillos, POST} route +0ms
{"timestamp":"...","level":"info","service":"bolsillos-w","message":"Listening on http://localhost:3000", ...}
```

Dos formatos en el mismo flujo de salida. Un colector de logs puede interpretar uno y no el otro, de modo que las once primeras líneas de todo producto de la línea quedan fuera de cualquier consulta. Y el activo predica un puerto de registro mientras arranca salteándoselo.

**Decisión.** El activo base trae un adaptador que implementa la interfaz `LoggerService` del framework y delega en `LoggerPort`. La aplicación se crea con `bufferLogs`, que retiene las entradas del arranque, y se le entrega el adaptador en cuanto el contenedor existe: el framework vuelca entonces todo lo que escribió, por el puerto. El nombre de la parte que escribe —`RouterExplorer`, `NestApplication`— se conserva como `scope` en el contexto, y el detalle que el framework adjunta a un error, como `detail`, en lugar de concatenarlos al mensaje, de modo que se pueda filtrar por ellos.

**Por qué no silenciar el logger del framework.** `logger: false` es una línea y borra el problema, pero también borra el mapa de rutas del arranque, que es lo único de esas entradas que sirve para diagnosticar por qué un endpoint responde `404`. El objetivo no era tener menos líneas: era tener un solo idioma.

**Por qué no Winston ni Pino.** Son realizaciones del mismo puerto, no una capacidad nueva: el contrato que el dominio usa no cambia. Sustituir `ConsoleLoggerAdapter` por un adaptador que venga del catálogo es la demostración que la Fase 3 debe dar —un adaptador externo reemplaza al propio sin que el dominio cambie— y adelantarla aquí agregaría una dependencia al activo sin agregar una propiedad. Con ese módulo llegan además el identificador de correlación, las métricas y el formato legible en desarrollo.

**Consecuencia.** El activo sube a `0.5.0` y la herramienta a `0.6.0`. El adaptador viaja copiado y su prueba viaja con las de ejemplo: los conteos del producto de referencia pasan de 41 y 26 a 43 y 27. El doc 2 §4, §8 y §9 y el doc 5 §3 y §13 quedan por ajustar.

**Verificación.** El arranque de un producto derivado escribe doce líneas JSON seguidas, de `Starting Nest application...` con `scope: NestFactory` hasta `Listening on http://localhost:3125`, sin una sola línea en el formato del framework.

**Traza.** ADR-076, ADR-084, T-09, RNF-02, Doc 2 §8, Doc 2 §9.

---

## ADR-086 · La verificación no modifica lo verificado

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** El Bloque C completa las pruebas de un código ya construido, verificado y publicado. Al enumerar lo que faltaba comprobar aparecieron dos comprobaciones que solo eran posibles cambiando algo que ya estaba decidido: hacer viajar la prueba del interceptor de registro con todo producto, incluso el mínimo, y declarar obligatoria una prueba por cada archivo de `src/`. La primera cambia el reparto de archivos de la generación, o sea el producto; la segunda cambia el estándar de código. Las dos abaratan la verificación a costa de lo verificado.

**Decisión.** La verificación no modifica lo verificado. Este bloque no cambia el producto, los activos de la línea, la interfaz de la herramienta, los estándares de código ni una decisión aceptada. Cuando una comprobación solo es posible cambiando algo de eso, se detiene, se declara como límite en el doc 6 §12, y el cambio se decide aparte, fuera del bloque.

**Por qué como principio y no caso por caso.** Una prueba que exige cambiar el objeto probado se justifica siempre con el mismo argumento —sería más fácil de comprobar—, y ese argumento no tiene fondo. Declararlo una vez evita discutirlo en cada comprobación y deja por escrito por qué dos recomendaciones razonables se retiraron.

**Consecuencia.** La propuesta de hacer viajar la prueba del interceptor se retiró: el comportamiento se comprueba en ejecución (doc 6 §9.1), que además es evidencia más fuerte porque mira al producto tal como se entrega. El estándar de código no se modifica (ADR-087). El doc 2, el doc 5 y ADR-084 quedan intactos. La interfaz de la herramienta no cambia en nada: ningún comando, parámetro, mensaje ni salida.

**Traza.** ADR-084, RNF-02, Doc 6 §1, Doc 6 §9.1, Doc 6 §12.

---

## ADR-087 · Criterio de cobertura por lógica propia, con los exentos declarados

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** `ESTANDAR-DE-CODIGO.md` §9 dice "Un archivo `.spec.ts` por archivo probado". Leído como obligación de probar todo archivo de `src/`, exige suites para `SystemClockAdapter` —trece líneas que devuelven `new Date()`— y para `NodeCommandRunnerAdapter` —veinte que envuelven `execFile`—. Ninguna de esas pruebas puede fallar por culpa de este proyecto.

**Decisión.** Se prueba toda unidad con lógica propia. Un archivo sin lógica propia queda exento y la exención se declara en el doc 6 §3 con su razón. El estándar de código no cambia: su regla es de organización y de nombre, no una obligación de cobertura, y la tabla de exentos vive en el documento de fase.

**Lo que el criterio no permite.** Declarar exento un archivo con lógica para evitar escribirle la prueba. Los dos archivos que tienen lógica propia y no reciben suite en esta fase quedan como cobertura indirecta declarada, con el medio por el que hoy se verifican y el límite de ese medio: el reporter de terminal y el adaptador del registro de paquetes.

**Dos reglas que se desprenden.** Un límite conocido se fija como aserción, con el nombre de la prueba diciendo que es un límite —así nadie lo "arregla" sin decidirlo—; es el caso de la pluralización del doc 5 §7. Y cuando dos archivos de `src/` comparten nombre base, la prueba del segundo lleva su carpeta como prefijo: `generate-naming.spec.ts` para `operations/generate/naming.ts`, porque `naming.spec.ts` ya es de `core/input/naming.ts`.

**Consecuencia.** Cuatro suites nuevas: las dos operaciones de la herramienta, los nombres de la derivación y el análisis de la invocación. Cierra el hueco que el doc 5 §14 declaraba (P-09). `ESTANDAR-DE-CODIGO.md` queda sin tocar.

**Traza.** ESTANDAR-DE-CODIGO §9, Doc 5 §7, Doc 5 §14, P-09, Doc 6 §3, Doc 6 §4.

---

## ADR-088 · El arranque y las sondas se comprueban en ejecución dentro del verificador

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** La condición de llegada de la fase es un producto que arranca sin que nadie edite un archivo (el índice de la fase). `verify:generation` corría el lint, las pruebas y la compilación del producto derivado, pero no lo arrancaba: el arranque, la dirección en que escucha y las dos sondas se comprobaban a mano y quedaban anotados en el apartado "Verificado" de ADR-076, ADR-077 y ADR-084. Una afirmación que solo una persona puede reproducir caduca con el primer cambio del activo base.

**Decisión.** El verificador arranca el producto derivado con `npm run start`, espera `/health/live` y `/health/ready`, le pide una ruta de su capacidad y lo apaga. No escribe ningún `.env`, no exporta variables del servicio y no edita un archivo: solo fija `PORT`, porque la corrida necesita un puerto propio. Eso es lo que convierte la comprobación en evidencia de RF-01 y no en un trámite.

**Sobre un solo producto.** Corre sobre `term-deposit-api`. Los dos productos derivan del mismo activo base, así que arrancar el segundo no agrega evidencia y sí duplica el costo. Es además el producto que ya se deriva dos veces para la comprobación de equivalencia.

**Decisiones de implementación.** El puerto se pide al sistema operativo en lugar de fijarse, para que dos corridas simultáneas no se estorben. La espera está acotada y, al vencerse, falla con el log capturado en el mensaje en lugar de colgar la puerta. El proceso se lanza en su propio grupo, porque `npm` lanza a su vez el servidor y apagar solo a `npm` dejaría el servidor escuchando.

**Límite asumido.** La comprobación necesita un puerto libre y poder señalar al grupo de procesos. En una máquina donde eso no sea posible falla aunque el producto esté bien. Es el costo de verificar un proceso real en lugar de su descripción.

**Consecuencia.** `verify:generation` suma el arranque y queda donde ya estaba, en `check:push`, no en `check:commit`: una puerta de commit que tarda minutos se empieza a saltar. El "Verificado" manual de ADR-076, ADR-084 y ADR-085 pasa a ser automático.

**Traza.** RF-01, ADR-076, ADR-077, ADR-084, ADR-085, el índice de la fase, Doc 6 §6, Doc 6 §7.

---

## ADR-089 · La regla de dependencia se comprueba con una prueba negativa

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** La condición de llegada exige que el producto supere su análisis estático "con la regla de dependencia activa", y RNF-03 pide que lo generado pueda analizarse sin adaptación previa. Que el lint del producto pase demuestra que el lint corre; no demuestra que la regla esté activa. Una configuración de `boundaries` con un patrón de capa que no coincide con el árbol, o un `ignores` de más, deja el lint verde y la regla muerta.

**Decisión.** Sobre la copia temporal del producto, el verificador escribe en la entidad raíz una importación que la regla prohíbe —dominio hacia infraestructura—, corre el lint esperando que falle, exige que la salida nombre `boundaries/element-types` y restaura el archivo. Un fallo cualquiera no alcanza: si el lint falla por otra razón, la comprobación falla también, con la salida en el mensaje.

**Dónde se escribe la violación.** En la copia temporal que el verificador borra al terminar, nunca en las plantillas ni en el activo base. El principio de ADR-086 rige también para una prueba negativa.

**Traza.** RF-03, RNF-03, el índice de la fase, Doc 6 §6, Doc 6 §8, ADR-086.

---

## ADR-090 · La configurabilidad del producto se comprueba por barrido de su código

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** RNF-05 pide que el producto no contenga valores fijos susceptibles de cambio, en particular direcciones de servicios y parámetros de negocio. Era la única comprobación de conformidad que se hacía leyendo el código, sin nada que la sostuviera entre una lectura y la siguiente.

**Decisión.** El verificador barre los archivos de `src/` del producto derivado con dos reglas: `process.env` se lee únicamente bajo `src/config/`, que es donde el esquema valida el entorno, y ningún archivo lleva una dirección absoluta cuyo host tenga un punto.

**Por qué el host con punto.** La regla admite a propósito `http://localhost:${port}`, que el arranque compone con el puerto configurado y que no es un valor fijo, y atrapa tanto un dominio como una dirección IP, que es la forma que toma una dirección de servicio en un producto de esta línea.

**Límite asumido.** No atrapa un número de puerto escrito a mano ni un parámetro de negocio en una constante. El juicio completo de RNF-05 sigue siendo de revisión; esta comprobación cubre el caso que el requerimiento nombra y que puede automatizarse sin falsos positivos.

**Traza.** RNF-05, Doc 6 §6, Doc 6 §9.2, Doc 6 §12.

---

## ADR-091 · Forma de la evidencia: comando, resultado y fecha

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** La evidencia de la fase estaba repartida entre el tablero y los pies de otros documentos, producida en fechas distintas. El el índice de la fase tiene que citarla sin volver a producirla, y la revisión del 2026-10-28 ya mostró que un bloque transcrito envejece sin que nadie lo note (P-21).

**Decisión.** La evidencia se registra en una tabla con el comando, el resultado y la fecha de la corrida. Se transcribe un extracto corto por comprobación —la línea que prueba el resultado—, no la salida completa. Los números de pruebas van solo en esa tabla, donde son una medición fechada, y no en la prosa de la estrategia, donde quedarían obsoletos con la primera prueba que se agregue.

**Consecuencia.** Al cerrar la fase hay que recorrer la tabla una vez más, porque cada fila afirma una corrida concreta.

**Traza.** P-21, Doc 6 §11.

---

## ADR-092 · Frontera entre el documento de pruebas y el de trazabilidad

**Estado:** Aceptada · 2026-10-31 · Doc 6

**Contexto.** El doc 6 produce la evidencia y el índice de la fase cierra la fase trazando lo construido hasta su origen. Si los dos arman su propia correspondencia con los requerimientos, hay dos matrices que pueden contradecirse; si el 7 no nombra ningún requerimiento, el 9 tiene que reconstruir la correspondencia desde cero.

**Decisión.** El doc 6 lleva la etiqueta del requerimiento junto a cada comprobación. La matriz completa y el juicio de cobertura son del índice de la fase, incluido RF-04 como no satisfecho por decisión de alcance (ADR-072). Una etiqueta no es una traza.

**Lo que el doc 6 declara como límite.** RNF-02 y RNF-06 no son verificables en esta fase: el primero necesita operaciones que la Fase 3 construye, el segundo más de una versión publicada de un activo consumido. Se declaran en el doc 6 §12 porque una ausencia muda se lee como olvido.

**Sin sección de desviaciones.** Cuando la verificación encuentra que un documento anterior declara algo que el código no sostiene, se corrige el documento anterior y la corrección se registra como ADR. El doc 6 no guarda una lista de desviaciones: sería un cementerio que nadie lee y dejaría al documento anterior afirmando algo falso.

**Traza.** ADR-072, RF-04, RNF-02, RNF-06, Doc 6 §1, Doc 6 §6, Doc 6 §12, el índice de la fase.

---

## ADR-093 · Reparto documental: el README es dueño del cómo, el documento de fase del camino

**Estado:** Aceptada · 2026-10-31 · `packages/cli/TUTORIAL.md`

**Contexto.** Al abrir el documento de instalación y uso ya existían seis READMEs en los dos repositorios, 491 líneas que resuelven cada uno su parte: acceso al feed y token, instalación global y comandos, el activo como paquete, el producto y sus rutas, los puertos, y el catálogo con su procedimiento de incorporación. Un documento de fase que los transcribiera duplicaría todo eso en un lugar que nadie lee al usar la herramienta, y los dos textos envejecerían por separado. Es el problema que P-21 dejó abierto.

**Decisión.** El README de cada paquete es dueño del **cómo**: el comando que se escribe, la opción que se pasa, la ruta que responde. El documento de fase es dueño del **camino y del por qué**: el orden de los pasos, qué prueba cada uno, qué falla si falta un prerrequisito y qué decisión de la fase explica cada exigencia. Lo que el documento agrega o corrige a un README se transcribe literal en su §9, y lo que ya está bien dicho se referencia.

**Consecuencia.** El `packages/cli/TUTORIAL.md` encontró dos huecos y los cerró en el README de la herramienta: la forma del archivo de entrada, que estaba nombrada como opción y no documentada, y lo que la herramienta dice cuando algo falla, que no existía en ningún README. El resto de los READMEs no se tocó. El README del producto en particular no documenta la herramienta: un producto derivado no la necesita para compilar, correr ni desplegarse, y es código del equipo que lo recibe desde el primer commit (RNF-02).

**Traza.** RNF-01, RNF-02, ADR-047, P-21, Doc 3 §9, `packages/cli/TUTORIAL.md`, `packages/cli/TUTORIAL.md`.

---

## ADR-094 · El registro de un producto no es un archivo de entrada

**Estado:** Aceptada · 2026-10-31 · `packages/cli/TUTORIAL.md`

**Contexto.** `--input` toma los valores de un archivo JSON, y ADR-083 hizo que el `project.json` de un producto guarde la entrada resuelta con que fue derivado. Las dos cosas juntas sugieren que el registro de un producto sirve para derivar otro igual, y al documentar el formato se comprobó que no: el registro agrupa sus campos por tema —`project`, `domain`, `aggregate`, `derivation`— y el lector de entrada espera los identificadores del modelo en la raíz. La invocación falla nombrando los valores que no encontró.

**Decisión.** El archivo de entrada conserva su formato plano, un campo por punto de variación, y el registro del producto conserva el suyo, agrupado por tema y pensado para leerse. No se agrega una traducción entre los dos. El límite queda declarado en `packages/cli/TUTORIAL.md` y en el README de la herramienta.

**Por qué no se unifican.** Son dos artefactos con dos propósitos. El registro responde de dónde viene un producto y qué versión de cada activo lleva, y lo va a leer la Fase 3 para saber qué incorporar; el archivo de entrada responde qué se quiere derivar. Hacer que uno sirva de otro obligaría a que el registro cargara los identificadores del modelo en su raíz, o a que el lector de entrada conociera la forma del registro: en los dos casos se acoplan dos formatos que evolucionan por razones distintas.

**Límite asumido.** Derivar un producto a partir del registro de otro no se puede en esta release. No es un detalle de formato: supone leer un producto existente, que es lo que la Fase 3 construye con las operaciones de consulta y composición. Quien quiera repetir una derivación escribe el archivo de entrada o guarda el que usó.

**Traza.** RF-02, RF-05, ADR-083, Doc 5 §5, `packages/cli/TUTORIAL.md`, `packages/cli/TUTORIAL.md`, Fase 3.

---

## ADR-128 · El producto escribe su log en dos formas, una por entorno

**Estado:** Revisada · 2026-11-01 · Doc 2 · revisa ADR-085 · revisada en ADR-133

**Contexto.** ADR-085 llevó todo lo que el proceso escribe al puerto de registro y dejó **una sola
forma** para el asiento: una línea JSON por evento, en todo entorno. El motivo era correcto —dos
formatos en el mismo flujo dejan a un colector interpretando la mitad— y difirió al módulo de
observabilidad «el identificador de correlación, las métricas y el formato legible en desarrollo».

Al usar los productos derivados, ese costo resultó el que se paga todos los días: un arranque son doce
líneas JSON seguidas y un circuito de requests una más por request, donde el logger nativo del
framework daba columnas alineadas, con color y con el `+Nms` entre entradas. La causa no es el puerto
ni el ruteo: es que la forma del asiento se decidió una sola vez para todos los entornos, y
desarrollar y operar no leen lo mismo.

**Decisión.** La forma la decide el entorno. `LOG_FORMAT` toma `json`, `pretty` o `auto`, y vale `auto`
por defecto: resuelve a `pretty` solo mientras `NODE_ENV` sea `development` **y** la salida sea un
terminal, y a `json` en todo lo demás. Un contenedor, una canalización o una salida redirigida nunca
degradan lo que el colector consume, y nadie configura nada para desarrollar.

La forma salió del adaptador: `log-formatter.ts` expone dos funciones puras, el adaptador resuelve la
forma una vez al construirse y ya no arma texto. El color se escribe solo contra un terminal.

**Qué trae la forma legible.** Columnas fijas de hora con milisegundos, nivel, parte que escribe y
mensaje, sin repetir lo que el mensaje ya dice: `scope` es la tercera columna, `durationMs` la derecha,
`statusCode` el color del mensaje, y un valor del contexto que aparezca literal en el mensaje se omite.
Dos excepciones a una línea por entrada: un error baja su stack debajo, porque plegado no se lee, y una
pausa de más de un segundo abre una línea en blanco, que es lo que separa el arranque del primer
request.

**Por qué no esperar al módulo de observabilidad.** ADR-085 difirió tres cosas en una frase. El
identificador de correlación y las métricas son capacidad nueva: amplían el puerto y dependen de la
plataforma de la organización, que es como C-02 las clasifica. El formato legible no es capacidad: es
presentación del mismo asiento, sin puerto nuevo, sin dependencia y sin servicio institucional. Se
adelanta solo esa tercera parte.

**Alternativas.** Una librería de formato legible agregaría una dependencia de ejecución al activo base
para escribir texto con códigos de escape. Se escriben a mano, como `@bsl/persistence`, que no trae
ninguna (ADR-107).

**Lo que no cambia.** El puerto `LoggerPort`, que es el contrato que el dominio usa. `LOG_LEVEL` y el
descarte por severidad. El ruteo de warnings y errores a la salida de error. Y, en producción, el JSON
asiento por asiento con sus mismas claves, de modo que la evidencia de ADR-085 sigue válida.

**Límite asumido.** La primera versión honraba `NO_COLOR` y `FORCE_COLOR` leyendo el entorno dentro del
adaptador, y `verify:generation` lo rechazó: ADR-090 comprueba por barrido que ningún archivo del
producto lea `process.env` fuera de `src/config`, y la regla es anterior y más importante que la
convención. El color se decide por el TTY, que no es configuración.

**Consecuencia.** Activo base en `0.7.0` y herramienta en `0.8.0`. El formateador y su prueba viajan
copiados, así que el producto de referencia pasa de 46 a 48 archivos y su suite de 19 a 25 pruebas.

**Verificación (2026-11-01).** `check:push` en verde con 195 pruebas y cero vulnerabilidades. Los dos
productos arrancan, sirven su documento OpenAPI y pasan el barrido de configurabilidad. Con
`LOG_FORMAT=pretty` y `NODE_ENV=development`:

```
19:01:31.524  INFO   [app]               Listening on http://localhost:3132              +1ms  environment=development
19:01:33.568  INFO   [app]               Party reference initiated                     id=9df953da-57ea-4928-9ffe-7b00c0373a72
19:01:33.568  INFO   [http]              POST /party-references 201                       1ms
```

Con `NODE_ENV=production` y sin variable, el mismo producto escribe catorce líneas JSON y ninguna en la
otra forma.

**Traza.** ADR-076, ADR-084, ADR-085, ADR-090, ADR-107, T-09, RNF-02, Doc 2 §8, Doc 2 §9, Doc 5 §13,
Fase 3 doc 1 C-02.

---

## ADR-129 · La forma de la salida de la herramienta vive en el adaptador, y la ayuda abre con el banner

**Estado:** Revisada · 2026-11-01 · Doc 4 / Doc 5 · revisa ADR-062

**Contexto.** ADR-062 fijó la presentación de la salida: el puerto de reporte con `heading`, `step` y `success`, el color conocido solo por el adaptador, el banner al abrir y los pasos siguientes al terminar. El código lo cumplió a medias y de dos maneras.

El banner se escribía solo al ejecutar una operación en un terminal, de modo que `bsl --help` —la página que se lee primero y a la que se vuelve— abría con una línea de texto plano, sin las letras de la línea. Y la alineación de los bloques de datos quedó escrita dentro de cada mensaje: `'  Product          '` con su relleno a mano en `add`, otro ancho en `update`, otro en `generate`. Tres operaciones con tres anchos, las marcas de paso, éxito, aviso y falla sin columna común, y ninguna señal de duración en los pasos que tardan —resolver un activo contra el registro, instalar dependencias—, que es justo donde la salida parece congelada.

**Decisión.** Tres cosas, todas del lado del adaptador.

La ayuda de la herramienta y la de cada operación abren con el banner, con las letras en bold y la firma de la línea en gris debajo. `--version` sigue imprimiendo el número pelado, porque eso lo lee un script.

`ReporterPort` gana `pairs(rows)`, que recibe etiquetas y valores y los alinea contra la etiqueta más larga, y `success` acepta una duración opcional. Una operación dice qué está escribiendo —una sección, un hecho, un par, un paso, un éxito— y nada sobre su forma. El ancho, el color, la indentación y la unidad de la duración son del adaptador.

La forma: una sección abre con línea en blanco, título en bold y una regla debajo, acotada para que un título largo no la empuje fuera del terminal; `>`, `ok`, `!` y `x` comparten una columna de dos caracteres; y la tabla gana una regla bajo su encabezado.

**Por qué en el puerto y no en cada operación.** El relleno a mano es una decisión de presentación tomada en el lugar donde se redacta el mensaje, y por eso divergía: tres operaciones ya tenían tres anchos, y la cuarta que se escriba tendrá el suyo. Con `pairs`, la forma se decide una vez y toda operación futura la hereda sin saber que existe. Es la misma razón por la que el adaptador es el único que conoce los códigos de color.

**Lo que no cambia.** Ningún comando, ningún parámetro, ningún texto de error y ningún artefacto escrito. La salida cambia de forma, no de contenido, y ninguna operación cambió lo que decide.

**Consecuencia.** Los documentos que transcriben salida de la herramienta quedan desalineados y se re-transcriben leyendo una corrida real: doc 5 §2 y `packages/cli/TUTORIAL.md` de esta fase, y doc 5 y doc 6 de la Fase 3. El doc 6 §4 queda por ajustar en dos filas de su tabla de líneas por archivo (`cli/banner.ts` y `adapters/console-reporter.adapter.ts` crecieron) y en el doble `RecordingReporter`, que implementa el método nuevo. Dos pruebas de `generate` afirmaban el relleno a mano y ahora afirman el contenido.

**Verificación (2026-11-01).** `bsl --help` abre con las letras y la firma `BACKEND SERVICE LINE · 0.8.0`, y `bsl status --help` también. Una derivación real escribe lo siguiente, con el activo resuelto por ruta local —de ahí `@local` y los `0ms`— y la ruta del destino abreviada:

```
  >   Resolving the base asset of the line
  ok  @bsl/base-template@local resolved  0ms

Product created at /tmp/run/term-deposit-api
────────────────────────────────────────────────────────────
  Service domain   Term Deposit (Products / Loans and Deposits)
  Aggregate        TermDeposit
  Operations       initiate, retrieve
  Business effect  2 of 2 operations carry one
  Persistence      in-memory, data is lost when the process stops
  Events           in-process, no external consumers configured
  Base asset       @bsl/base-template@local
  ok  42 files written

Next steps:
───────────
  cd term-deposit-api
  npm install
  cp .env.example .env
  npm run start:dev
```

`verify:composition` corre el circuito completo con la salida nueva, con sus cinco rechazos comprobados.

**Traza.** ADR-062, ADR-086, RNF-01, Doc 4 §5, Doc 5 §2, Doc 6 §4, Fase 3 doc 5, Fase 3 doc 6.

---

## ADR-131 · El adaptador de repositorio declara al arrancar qué es y si el dato sobrevive al reinicio

**Estado:** Aceptada · 2026-11-02 · Doc 2

**Contexto.** **ADR-082** hizo que el producto declare su persistencia fuera del código: el README avisa que guarda en memoria y que los registros se pierden al detenerse el proceso. El criterio de aceptación que la revisión externa del 2026-10-28 escribió para esa área pide dos cosas, y la segunda no estaba: «el README **y el log de arranque** indican el adapter y si los datos sobreviven al reinicio». `main.ts` escribe el puerto, el entorno y la URL de la sonda, y nada sobre dónde queda el dato. Quien arranca el servicio tiene que abrir `app.module.ts` para saberlo.

Hay una razón más fuerte que el criterio. Desde **ADR-130**, incorporar el módulo de persistencia corrige el README. Si la línea de arranque la escribiera el arranque, habría que corregirla también al componer, y sería el tercer lugar donde una afirmación puede quedar desactualizada respecto del cableado.

**Decisión.** La escribe el adaptador, al inicializarse. `InMemory<Agregado>Repository` implementa `OnModuleInit` y declara que guarda en proceso y que los registros se pierden al detenerse; el adaptador relacional que genera el módulo declara lo suyo. La entrada va por `LoggerPort` con `scope: 'persistence'`, `adapter` y `durable`, de modo que es legible por una persona y consultable sobre el log recolectado.

**Por qué el adaptador y no el arranque.** Queda correcta por construcción. El que está ligado es el que habla: no hay forma de que la línea mienta sin que el adaptador que la escribe sea el que no está ligado, lo que no puede pasar. La alternativa —que `main.ts` resuelva del contenedor qué clase quedó ligada y la nombre— es reflexiva, frágil ante un renombre, y deja la decisión de qué significa esa clase en el lugar que menos sabe de ella.

**Por qué no rompe la regla de capas.** Es un adaptador de infraestructura, y `LOGGER_PORT` lo provee `PlatformModule`, que es global desde **ADR-110** de la Fase 3. No cruza ninguna frontera: el dominio y la aplicación siguen sin saber que la persistencia registra algo. El analizador con la regla de dependencia activa pasa sin excepciones agregadas.

**Consecuencia.** El activo base sube a `0.8.0` y el módulo a `0.2.0`. El adaptador de memoria recibe el puerto por constructor, lo que agrega tres pruebas al activo base. `verify:generation` comprueba que un producto recién derivado declara `in-memory` y `durable: false`; `verify:composition` comprueba que, con el módulo incorporado, la línea cambió y la anterior no aparece. El doc 2 §8 queda por ajustar con la entrada nueva del arranque.

**Verificación (2026-11-02).** `check:push` en verde, código de salida 0, cero vulnerabilidades. Comprobado rompiéndolo, como pide **ADR-126**: cambiado `scope: 'persistence'` por `scope: 'store'` en la plantilla del adaptador, `verify:generation` falla con `The product did not declare which persistence adapter is bound.`

**Traza.** RF-02, RNF-02, T-09, ADR-076, ADR-082, ADR-084, ADR-090, ADR-126, ADR-130, Fase 3 ADR-110, Doc 2 §8, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G1-b.

---

## ADR-132 · El registro del producto declara el efecto de negocio de cada operación, y su lectura tolera la forma anterior

**Estado:** Revisada · 2026-11-02 · Doc 5 · revisa ADR-083

**Contexto.** **ADR-082** hizo que el README del producto marque cada operación como `implemented` o `scaffold`, y **ADR-129** lo llevó al resumen de la derivación. El dato vive en prosa y en una línea de salida, y no en el registro: `derivation.operations` de **ADR-083** es una lista de identificadores. La consecuencia práctica es que `bsl status` no puede decir cuántas operaciones del producto siguen sin su efecto de negocio, y que la Fase 4 no puede contarlo sin leer un README.

**Decisión.** Cada entrada de `derivation.operations` pasa a ser un objeto con `id` y `businessEffect`, que vale `implemented` o `scaffold`. `bsl status` abre informando cuántas operaciones llevan su efecto y nombrando las que no.

La lectura tolera las dos formas. `derivedOperations` normaliza la lista: un identificador suelto da una entrada sin `businessEffect`, que es el único caso en que la respuesta es desconocida y no uno de los dos valores. La consulta lo dice con esas palabras en lugar de contar un cero que no significa cero.

**Por qué no se sube `schemaVersion`.** Es el criterio que **ADR-083** ya aplicó al agregar estos mismos campos: un cambio aditivo no migra productos. Subir la versión del formato dejaría ilegible todo producto derivado hasta hoy —la herramienta rechaza un registro cuya versión no reconoce— para ganar un campo que no cambia nada de lo que ya se leía. Tolerar las dos formas en un solo lugar cuesta una función y deja a `add`, `update` y `status` sin saber que existen dos formas.

**Por qué en el registro y no solo en el README.** El README lo lee una persona; el registro lo lee la herramienta, y es lo que **ADR-094** dejó claro que es: el lugar donde el producto declara de dónde viene y qué tiene. Lo que queda por implementar es parte de eso.

**Consecuencia.** La herramienta sube a `0.9.0`. `verify:generation` comprueba, en los dos productos que deriva, que el registro declara el efecto de cada operación y que no declara ninguno desconocido. Quedan por ajustar con la forma nueva el doc 2 §10, que transcribe el registro del activo base, y del doc 5 el §8 —donde está `project.json.tpl`—, el §10 y el §13, que transcribe el registro de los dos productos derivados.

**Verificación (2026-11-02).** `check:push` en verde. Tres pruebas nuevas en `status.operation.spec.ts`: una cuenta e informa, una comprueba que un producto sin `derivation` no dice nada de operaciones, y una lee un registro con la forma anterior y lo declara como tal.

**Traza.** RF-02, RF-05, RF-08, RF-10, ADR-070, ADR-082, ADR-083, ADR-094, ADR-129, Fase 3 ADR-123, Doc 2 §10, Doc 5 §8, Doc 5 §10, Doc 5 §13, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G1-c.

---

## ADR-133 · Cada request tiene nombre dentro del servicio; la propagación entre servicios sigue siendo del módulo

**Estado:** Revisada · 2026-11-02 · Doc 2 · revisa ADR-085 y ADR-128 · revisada en ADR-151

**Contexto.** ADR-085 difirió tres cosas al módulo de observabilidad en una frase, y ADR-128 tomó la
tercera clasificando las otras dos como «capacidad nueva que depende de la plataforma de la
organización». Esa clasificación es la que esta decisión corrige, y solo en una mitad.

El criterio que la revisión externa escribió para observabilidad es «cada request registra método,
ruta, status, duración **y request ID**». Los cuatro primeros los da ADR-084; el quinto no existía —un
`grep` de `requestId`, `correlation` y `x-request-id` sobre los dos repositorios daba cero—. Y el costo
real no es incumplir un criterio: es que en un servicio con tráfico, el asiento del caso de uso y el
del request que lo causó **no se pueden juntar**.

**Decisión.** El identificador se parte en dos, y solo la primera mitad entra.

**Entra: nombrar la request dentro del servicio.** El interceptor toma `x-request-id` cuando el llamador
la manda y, si no, acuña uno con `randomUUID`. Lo devuelve en la respuesta bajo la misma cabecera, lo
escribe en su asiento, y corre el resto del manejo dentro de un `AsyncLocalStorage`. El adaptador de
registro lee ese contexto y adjunta `requestId` a **toda** entrada escrita mientras la request se
atiende, incluidas las del caso de uso, que no saben que existe.

**Sigue fuera, en el módulo:** llevar la traza al servicio siguiente —la cabecera que la organización
use, el formato de contexto, la propagación saliente, el muestreo y las métricas—. Eso sí amplía el
puerto y sí depende de la plataforma institucional, que es como C-02 lo clasifica.

**Por qué esta mitad no es capacidad nueva.** No amplía `LoggerPort`, porque `LogContext` ya es
`Record<string, unknown>`. No agrega dependencia, porque `node:async_hooks` es de Node. Y no necesita
servicio institucional: lo que se ata son las entradas de **un** servicio consigo mismo. Es el corte de
ADR-128 aplicado al identificador.

**Alternativas.** Pasar el identificador del controlador al caso de uso y de ahí al repositorio. Se
descarta: mete una preocupación de registro en la firma del dominio, que es exactamente lo que el puerto
existe para evitar. Con el contexto, ninguna capa fuera de `infrastructure/logging` sabe que existe.

**Por qué se honra el valor que llega.** Una request ya identificada aguas arriba conserva un solo
nombre de punta a punta. Como viene de afuera, se acota a 200 caracteres y se le quitan los que no son
seguros en una línea de log ni en una cabecera; si no queda nada usable, se acuña uno.

**Límite asumido.** La columna del identificador en la forma legible se resolvió dos veces. La primera
cortaba a ocho caracteres, y al correrla `edge-7781` salió como `edge-778`: un identificador corto
mostrado como si estuviera completo, y distinto del real. Ahora tiene nueve, muestra entero lo que entra
y marca con elipsis lo que tuvo que cortar.

**Consecuencia.** Activo base en `0.9.0` y herramienta en `0.10.0`. `request-context.ts` viaja copiado y
el producto de referencia pasa a 49 archivos. No hay variable nueva: la cabecera no es configuración
del servicio, de modo que el barrido de ADR-090 sigue pasando.

**Verificación (2026-11-02).** `check:push` en verde con 214 pruebas y cero vulnerabilidades.
`verify:generation` comprueba que ninguna entrada de request queda sin identificador, que la request que
llega nombrada vuelve con su nombre en la cabecera, y que al menos una entrada del dominio lleva el
identificador de la request que la causó:

```json
{"level":"info","service":"term-deposit-api","message":"Term deposit initiated","context":{"requestId":"edge-7781","id":"c08b2122-3275-4c95-aba3-bbba52b01d34"}}
{"level":"info","service":"term-deposit-api","message":"POST /term-deposits 201","context":{"scope":"http","requestId":"edge-7781","method":"POST","route":"/term-deposits","statusCode":201,"durationMs":1}}
```

**Verificación, rompiéndolo (ADR-126), con dos redes.** Quitado el envoltorio del contexto asíncrono,
falla la prueba que viaja con el producto, con `Received: undefined`. Cambiada la clave que el adaptador
adjunta por `traceId` —lo que pasa el lint y el typecheck—, falla el circuito: `No entry of the domain
carried the request that caused it`. La primera red está en el producto, la segunda en la línea.

**Traza.** T-09, RNF-02, RF-02, ADR-076, ADR-084, ADR-085, ADR-090, ADR-126, ADR-128, Doc 2 §8,
Fase 3 doc 1 C-02, seguimiento de mejoras G2.

---

## ADR-134 · El producto trae una prueba de humo de su superficie HTTP, y no es una pieza opcional

**Estado:** Revisada · 2026-11-02 · Doc 5 · revisa ADR-067

**Contexto.** El informe externo pidió, en su hallazgo 14, «cada endpoint generado tiene al menos un
smoke test HTTP». El el índice de la Fase 3 lo admitió como candidato solo si la verificación de esa fase lo
necesitaba, y `packages/cli/TUTORIAL.md` concluyó que no: el circuito ejerce la API real en ejecución.

Ese razonamiento sigue siendo correcto para verificar **la línea**, y es insuficiente para lo que la
Fase 4 va a medir. El tercer criterio del objetivo 4 es el inicio de lógica de negocio en el producto
generado, y quien lo empieza necesita una prueba que falle antes y pase después. Hoy el producto cubre
su entidad y su caso de uso con dobles escritos a mano, y **nada ejerce el camino completo** de un
request. El circuito lo ejerce, pero vive en el repositorio de los activos y no en las manos del equipo
que recibe el producto.

**Decisión.** Todo producto derivado trae `test/http-smoke.spec.ts`: arranca la aplicación con
`Test.createTestingModule({ imports: [AppModule] })` y pide a cada ruta una respuesta por HTTP.

**Qué asegura y qué no.** Asegura el estado que la ruta declara en su contrato y el rechazo de un cuerpo
que su esquema no acepta. **No asegura ningún efecto de negocio**: eso pertenece al equipo dueño del
producto. Es la frontera que ADR-082 fijó para el README y ADR-132 para el registro, ahora en las
pruebas.

**Qué casos se generan.** Uno por operación, sin que ninguno dependa de que otro haya corrido:
`Initiate` responde `201` con un cuerpo válido y `400` con uno que el esquema rechaza; toda ruta con
`:id` responde `404` sobre un identificador que no existe; `Update` suma su propio `400`. Un producto
que a la vez inicia y consulta recibe un caso más, que almacena un agregado y lo lee de vuelta, porque
es el único camino que cruza el repositorio.

**Por qué no es opcional.** `--no-sample-tests` existe para no entregar pruebas de ejemplo que el equipo
va a borrar. Una prueba que afirma que las rutas del propio producto responden no es un ejemplo: es cómo
el producto dice de sí mismo que está cableado, y por eso entra en `npm run verify`. Si viajara con las
de ejemplo, un producto derivado con esa bandera no tendría ninguna y el criterio quedaría incumplido
justo en el caso más austero. **Esto revisa ADR-067:** lo que la bandera decide son las pruebas de
ejemplo del dominio, no las del producto.

**Alternativas.** Pruebas e2e. Se descartan: un circuito con base de datos y datos de prueba tarda, se
rompe por razones ajenas al cambio que se prueba y es trabajo del equipo. Lo que la línea entrega es el
humo: barato, estable, y suficiente para que un cableado roto no pase la puerta.

**Por qué el `AppModule` real, contra la regla de que las pruebas no importan `config.ts`.** La regla de
`ESTANDAR-DE-CODIGO.md` §9 existe para que una prueba unitaria no dependa del entorno; esta no es
unitaria y lo que verifica es precisamente la composición, así que importarlo es el punto. `test/setup.ts`
fija el entorno antes de que se importe cualquier módulo.

**Consecuencia.** Activo base en `0.10.0` y herramienta en `0.11.0`. Siete plantillas nuevas y
`test/setup.ts` copiado; el producto de referencia pasa a 51 archivos y el segundo deja de nacer sin
carpeta `test/`. **Cuesta tres dependencias de desarrollo** —`@nestjs/testing`, `supertest` y sus
tipos— que **no mueven la superficie que RNF-04 audita**, porque la auditoría del producto corre con
`--omit=dev`: comprobado, `check:push` informa cero vulnerabilidades con las tres instaladas.

**Verificación (2026-11-02).** Los dos productos del circuito corren su prueba de humo dentro de su
propia verificación: `term-deposit-api` con ocho casos y `party-directory-api` con uno, que es el único
endpoint que tiene. El producto compuesto también la pasa, con el adaptador relacional ligado, antes y
después de actualizar el módulo.

**Verificación, rompiéndolo (ADR-126).** `verify:generation` compara las rutas que el README declara
contra lo que la prueba nombra. Apuntada la plantilla del caso de consulta a otra ruta, falla con
`/party-references/:id is a route of party-directory-api and its smoke test does not name it.` Es la
comprobación que atraparía un action term nuevo agregado sin su fragmento.

**Límite asumido.** `npx jest` invocado a mano sigue fallando sobre los paquetes ESM de NestJS, que es
**P-22** y no cambia con esta decisión: la suite se corre por `npm test`, que pasa la bandera que Jest
todavía exige.

**Traza.** RF-03, RNF-02, RNF-03, RNF-04, ADR-067, ADR-080, ADR-082, ADR-086, ADR-126, ADR-132,
Doc 5 §5, §9 y §13, Doc 6, P-22, el índice de la Fase 3, Fase 3 doc 7 §9, seguimiento de mejoras G3.

---

## ADR-135 · La Business Area de una entrada del espacio de selección es una de las cinco del estándar

**Estado:** Aceptada · 2026-11-02 · Doc 1 · **Revisada en ADR-137** (2026-11-02): el Business Domain de `Party Reference Data Directory` quedó mal por razonar desde el documento del marco en lugar del portal. La regla general que esta decisión fija se conserva.

**Contexto.** El hallazgo 3 de la revisión externa del 2026-10-28 dice que el catálogo parece servir solo para dos productos, y su causa está en los datos: `service-landscape.json` trae dos Service Domains de un subconjunto de cuarenta y seis (P-06). Al abrir ese trabajo y cruzar el archivo con el insumo del marco que declara el subconjunto, apareció algo anterior: **las dos entradas que ya existían declaraban una Business Area que el estándar no tiene.**

`MR-00_Teoria_BIAN.md` §3 enumera las cinco Business Areas de la versión 14.0 —Sales and Service, Reference Data, Operations and Execution, Risk and Compliance y Business Support— y dice qué Business Domains contiene cada una. El archivo decía `Products` para Term Deposit, cuyo Business Domain `Loans and Deposits` pertenece a `Operations and Execution`; y `Party` para Party Reference Data Directory, donde `Party` es el Business Domain y su área es `Reference Data`. Ninguno de los dos valores existe como Business Area.

No es cosmético. El valor viaja al `project.json` y al README de todo producto derivado, y la alineación con el estándar es el objetivo general del proyecto: un producto que declara pertenecer a un área que el estándar no define no está alineado, lo afirme o no.

**Decisión.** La Business Area de una entrada es una de las cinco que el estándar define, y se resuelve por el Business Domain de la entrada, no por el producto ni por el nombre del Service Domain. Las dos entradas quedan en `Operations and Execution / Loans and Deposits` y `Reference Data / Party`, y el ejemplo del esquema deja de sugerir un valor inválido.

**Por qué el Business Domain manda.** La jerarquía del estándar es de contención: el Service Domain está dentro de un Business Domain y ese dentro de un Business Area. Teniendo el Business Domain, el área no se elige: se lee de la tabla. Así la transcripción de las cuarenta y cuatro entradas que faltan no necesita el portal para ese campo.

**Una inconsistencia que esta decisión no resuelve.** MR-00 §8 ubica `Party Reference Data Directory` bajo el Business Domain `Customer Management`, y §3 lo sitúa en `Party`. El conteo del propio documento resuelve cuál vale: §3 dice que diez Business Domains corresponden al contexto de aplicación y la tabla de §8 trae nueve filas, que son diez con `Party` como fila propia. El código ya declaraba `Party`, así que se conserva. **Corregir MR-00 es trabajo de la Fase 1** y queda anotado en el insumo de P-06, no se hace al paso.

**Consecuencia.** Un producto derivado antes de hoy conserva en su registro el valor con que nació, que es procedencia y no error que haya que migrar. Los documentos que transcriben el archivo quedan por ajustar: el doc 1 §5, donde está la entrada y su esquema, y §11, con la entrada resuelta; el doc 2 §10, con el registro del producto; y `packages/cli/TUTORIAL.md`. Es un caso más de **P-21**. El activo base también declaraba `Party` en su propio `project.json` y quedó corregido.

**Verificación (2026-11-02).** `npm run verify:artifacts -w @bsl/cli` valida el archivo contra su esquema y la unicidad de sus identificadores; `check:commit` en verde con 220 pruebas. Ninguna prueba afirmaba los valores anteriores, lo que es parte del problema: el espacio de selección no tiene comprobación de que su Business Area sea una de las cinco. Agregarla exige que el archivo declare las cinco áreas, que es trabajo de la transcripción.

**Traza.** RF-01, RF-02, ADR-083, Doc 1 §5, Doc 1 §11, Doc 2 §10, `packages/cli/TUTORIAL.md`, P-06, P-21, MR-00 §3, MR-00 §8, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G4.

---

## ADR-136 · El alcance del producto se declara antes de derivarlo, y el prompt nombra el formato que espera

**Estado:** Revisada · 2026-11-02 · Doc 5 · revisa ADR-081 y ADR-082

**Contexto.** Al retirar el triage de la revisión externa y auditar el informe **propuesta por propuesta** —catorce hallazgos por tres propuestas, cuarenta y dos— aparecieron dos que nunca se adoptaron ni se descartaron. El triage resolvía por hallazgo, así que un hallazgo quedaba cerrado cuando una de sus tres propuestas lo estaba.

Las dos son de la misma clase y una de ellas toca el diagnóstico central del informe. **ADR-082** hizo que el producto declare su alcance, y **ADR-129** lo llevó al resumen de la derivación: los dos se leen cuando el producto ya está escrito. La propuesta 6.1 pedía decirlo **antes de generar**, que es el único momento en que todavía puede cambiar una decisión. Y la propuesta 4.1 pedía confirmar cuando el agregado local difiere del que sugiere la capability; lo que existe —el registro con los dos nombres y la nota del README (ADR-082, ADR-083)— explica la diferencia después de haberla escrito.

La tercera, la propuesta 2.2, es del mismo tipo un nivel más abajo: **ADR-081** llevó el formato y el ejemplo al rechazo y a la ayuda, y el prompt interactivo siguió mostrando solo su pregunta. El punto de variación ya declara su `format` y su `example`; nadie los usaba hasta que la respuesta fallaba.

**Decisión.** Tres cosas.

**Una declaración antes de derivar.** Resuelta la entrada y calculado el destino, la operación escribe qué va a producir —que es un bootstrap técnico y no un producto de negocio terminado, cuántas operaciones llevan su efecto y cuáles son andamios, qué persistencia y qué eventos— y, en un terminal, pide confirmación. Fuera de un terminal declara y sigue.

**La diferencia de nombre va en esa misma declaración**, como una fila más, y solo cuando los dos nombres difieren. No es una confirmación aparte.

**El prompt nombra la forma que espera**: `Name of the root aggregate (PascalCase, e.g. TermDeposit)`.

**Por qué una sola confirmación y no dos.** La evaluación adversarial del propio informe lo anticipó para el hallazgo 4: «advertir protege coherencia, pero añade fricción». Dos preguntas seguidas antes de generar se responden sin leerlas. Una declaración que incluye la diferencia de nombre cumple las dos propuestas con una sola interrupción, y la pone donde el desarrollador ya está decidiendo si seguir.

**Por qué no detiene una corrida sin terminal.** Una invocación por banderas —un script, la verificación de la línea, integración continua— no tiene a quién preguntar. Pedir confirmación ahí convertiría una declaración en un fallo. Declara y sigue, que es lo que `--dry-run` ya hacía con el plan de archivos.

**Lo que no cambia.** El resumen posterior de ADR-129 se queda: declara el alcance esperado, el otro declara lo que quedó escrito, y la diferencia entre los dos es lo que importa cuando algo salió distinto de lo pedido. Ningún comando, ninguna bandera y ningún archivo generado cambian.

**Consecuencia.** El activo base sube a `0.11.0` y la herramienta a `0.12.0`. Cuatro pruebas nuevas en la operación y cuatro guiones de prueba del resolvedor actualizados, porque la pregunta del agregado cambió de texto. El doc 5 §2 queda por ajustar con la declaración y la confirmación, y el doc 4 §5 con el texto del prompt.

**Verificación (2026-11-02).** `check:push` en verde, código de salida 0, 224 pruebas. Una derivación real escribe, antes de tocar el disco:

```
What this derivation produces
─────────────────────────────
  Result           a technical bootstrap of the line, not a finished business product
  Business effect  3 of 5 operations carry one; execute-interest-settlement, control are scaffolds
  Persistence      in-memory, data is lost when the process stops
  Events           in-process, no external consumers configured
```

Con un agregado nombrado de otro modo aparece además la fila `Bolsillo  (reference capability names it TermDeposit)`, y con el nombre sugerido esa fila no está. Respondida la confirmación con `no`, la operación informa `Nothing was written.` y el directorio del producto queda vacío, comprobado por prueba.

**Traza.** RF-01, RF-02, RNF-01, RNF-02, T-14, ADR-081, ADR-082, ADR-083, ADR-129, Doc 4 §5, Doc 5 §2, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G5.

---

## ADR-137 · Ante una discrepancia sobre la jerarquía del estándar, manda el portal y no el documento del marco

**Estado:** Revisada · 2026-11-02 · Doc 1 · revisa ADR-135

**Contexto.** **ADR-135**, tomada horas antes, corrigió la Business Area de las dos entradas del espacio de selección porque declaraban áreas que el estándar no tiene. La mitad de esa corrección estaba mal.

El caso de `Term Deposit` era directo: su Business Domain `Loans and Deposits` pertenece a `Operations and Execution`, y así quedó. El de `Party Reference Data Directory` no: el código declaraba `businessDomain: "Party"`, ADR-135 lo tomó por bueno y solo le cambió el área a `Reference Data`, apoyándose en la tabla de `MR-00_Teoria_BIAN.md` §3, que sitúa el Business Domain `Party` en esa área. Para descartar lo que §8 decía —que ese Service Domain está en `Customer Management`— usé un argumento de conteo: §3 afirma que diez Business Domains corresponden al contexto de aplicación y la tabla de §8 trae nueve filas, de donde concluí que faltaba `Party` como fila propia.

**El conteo era una inferencia, no una fuente.** Consultada la vista matriz del Service Landscape v14.0 en el portal público, la jerarquía es inequívoca: el Business Domain `Party`, del área `Reference Data`, contiene exactamente dos Service Domains —`Party Routing Profile` y `Legal Entity Directory`—, y `Party Reference Data Directory` figura bajo `Sales and Service / Customer Management`. **MR-00 §8 tenía razón desde el principio, y el `businessDomain: "Party"` del código estaba mal desde antes de ADR-135.**

**Decisión.** Dos cosas, y la segunda importa más que la primera.

**El dato.** `Party Reference Data Directory` queda en `Sales and Service / Customer Management`, en el espacio de selección y en el registro del activo base.

**La regla.** Cuando un documento del marco y el portal del estándar discrepan sobre la jerarquía, **manda el portal**, y la discrepancia se anota contra el documento del marco. Un documento del marco es una transcripción, y una transcripción no gana una discusión contra su fuente. Ningún razonamiento interno a los documentos —un conteo, una simetría, una tabla que parece incompleta— sustituye la consulta.

**Por qué esto se registra y no se corrige en silencio.** ADR-135 argumentó explícitamente a favor del valor equivocado y dejó ese argumento escrito. Borrarlo dejaría el log diciendo que la decisión fue correcta. Queda la decisión, queda su error, y queda la regla que lo evita.

**Lo que ADR-135 conserva.** Su parte sustantiva: que la Business Area de una entrada es una de las cinco del estándar y se resuelve por el Business Domain. Era correcta y es la que hizo visible el problema; lo que falló fue la fuente consultada para aplicarla a un caso.

**Consecuencia.** El activo base sube a `0.12.0` y la herramienta a `0.13.0`. **P-33 se cierra**: no era una inconsistencia por resolver entre §3 y §8, era el código contradiciendo a §8 con razón de más. Queda en cambio por corregir la frase de §3 que afirma diez Business Domains, que es la que no se sostiene (P-06 lo anota). Un producto derivado antes de hoy conserva en su registro el valor con que nació, que es procedencia.

**Verificación (2026-11-02).** `npm run verify:artifacts -w @bsl/cli` valida el espacio de selección; `check:push` en verde con 224 pruebas y cero vulnerabilidades. La consulta quedó registrada en el insumo de P-06, con la URL de la vista y qué da y qué no da el portal.

**Traza.** RF-01, RF-02, ADR-135, Doc 1 §5, Doc 1 §11, Doc 2 §10, P-06, P-33, MR-00 §3, MR-00 §8, `Fase 4 .../Insumos/seguimiento-de-mejoras.md` G4.

---

## ADR-138 · Una entrada del espacio de selección existe cuando sirve a un propósito escrito del proyecto

**Estado:** Aceptada · 2026-11-02 · Doc 1

**Contexto.** P-06 pedía completar `service-landscape.json` «con el resto del subconjunto», y el log de ADR de la Fase 1 lo registraba como «falta extraer los Service Domains del portal». Resuelto el acceso al dato del estándar —la extracción quedó en `Fase 1 .../Insumos/Teoria/BIAN/MR-00_BIAN_service-domains-extraidos.md`—, lo que apareció no fue el final del pendiente sino una pregunta que nadie había hecho: **cuántas entradas debe tener el espacio de selección.**

La respuesta por defecto era «todas las del subconjunto», cuarenta y seis. Es la equivocada, y el propio marco lo dice: la tabla de `MR-00_Teoria_BIAN.md` §8 se declara «un subconjunto orientativo del Service Landscape, no una asignación definitiva», cuya función es acotar el espacio «y puede ampliarse conforme el laboratorio construya productos en áreas no contempladas aquí». Transcribir las cuarenta y seis convertiría una lista orientativa en una asignación, y pondría a elegir entre capacidades que el laboratorio no va a construir.

**Decisión.** Una entrada del espacio de selección existe cuando sirve a un **propósito escrito** del proyecto, y la entrada se agrega junto con ese propósito. No se agrega para poblar un catálogo ni para cubrir un Business Domain.

El criterio no es nuevo: es el que el doc 1 §5 ya había aplicado sin enunciarlo, cuando declaró que el archivo trae «Term Deposit, que aporta el caso de selección con cinco operaciones, y Party Reference Data Directory, que es la del agregado de referencia del activo base». Esta decisión lo vuelve explícito y lo aplica a lo que faltaba.

**Las cinco entradas, con su propósito.**

| Service Domain | Propósito | Dónde está escrito |
| :-- | :-- | :-- |
| Term Deposit | El caso de selección con cinco operaciones | Doc 1 §5 |
| Party Reference Data Directory | El agregado de referencia del activo base | Doc 1 §5, Doc 2 |
| Consumer Loan | El ejemplo de derivación con el que el marco explica su propio mecanismo | MR-02 §6 y su figura 4 |
| Savings Account | Una capacidad que ningún producto derivó todavía, para que el caso de estudio de la Fase 4 parta de cero y no de un producto ya documentado | el índice de la Fase 3 |
| Current Account | Completa `Loans and Deposits` con las capacidades que el contexto construye, de modo que la línea cubra un Business Domain coherente y no una colección de ejemplos | MR-00 §8 |

**Por qué Consumer Loan no podía faltar.** El marco ilustra su mecanismo completo con esa capacidad —bounded context `consumer-loan`, agregado `ConsumerLoan`, rutas derivadas de sus operaciones— y la herramienta no permitía seleccionarla. Un marco que explica su artefacto con un caso que el artefacto no admite no es un ejemplo: es una contradicción.

**Qué se hizo con las otras cuarenta y una.** Quedan extraídas y listas en el insumo de la Fase 1, con su control record, sus operaciones derivables y las que quedan fuera del alcance de esta release. Agregar una después es copiar una fila, no volver al portal.

**El límite del dato.** De las cuarenta y seis, **cinco no tienen operaciones de nivel control record en v14.0** —Customer Consent, Payment Orchestration, Payment Settlement, Payment Confirmation y Party Asset Directory—. Tienen control record, pero el estándar no les modela operaciones sobre él. Entrar al espacio de selección les exigiría decidir qué operaciones publicar, que es una decisión de diseño y no una transcripción.

**Una forma de capacidad que el espacio no ejercita.** Las cinco entradas crean su propio control record: todas tienen `initiate`. El subconjunto tiene capacidades que no lo tienen, porque su control record lo crea otra capacidad. Incorporar una ejercitaría una variabilidad que ninguna entrada cubre y podría destapar un supuesto del activo base, que genera la fábrica `initiate` del agregado en todos los casos. Queda anotado en el insumo, sin decidir.

**Consecuencia.** El espacio pasa de dos entradas a cinco, en dos Business Areas y dos Business Domains. La herramienta sube a `0.14.0` y el activo base queda donde está, porque no cambió. **P-06 se cierra**: lo que pedía —extraer del portal— está hecho y guardado, y cuántas entradas van es esta decisión y no un pendiente. El doc 1 §5 queda por ajustar con las cinco entradas y con este criterio.

**Verificación (2026-11-02).** `npm run verify:artifacts -w @bsl/cli` valida el archivo y la unicidad de sus identificadores; `check:push` en verde con 224 pruebas. Ninguna entrada nueva cambia el comportamiento de la herramienta: el modelo de variabilidad y las plantillas son los mismos, que es lo que el doc 1 anticipaba al decir que el resto del subconjunto se incorpora «sin cambio en el formato ni en la herramienta».

**Traza.** RF-01, RF-02, ADR-135, ADR-137, Doc 1 §5, Doc 2, MR-00 §8, MR-02 §6, el índice de la Fase 3, P-06, `Fase 1 .../Insumos/Teoria/BIAN/MR-00_BIAN_service-domains-extraidos.md`.

---

## ADR-139 · El dato de una capacidad se transcribe del documento oficial de su Service Domain

**Estado:** Revisada · 2026-11-03 · Doc 1

**Contexto.** ADR-138 cerró P-06 dando por resuelto el acceso al dato del estándar, y el insumo de la transcripción declaraba un límite: las vistas del portal dan nombres y jerarquía, el detalle de cada Service Domain se arma con JavaScript y «hay que abrirla en un navegador». Bajo ese límite, la descripción, el control record y las operaciones de `Term Deposit` se habían escrito como paráfrasis de lo que se suponía que el estándar decía.

El 2026-11-03 el autor consiguió el **documento OpenAPI oficial de `Term Deposit` v14.0**, que es la publicación del Service Domain y no una vista del landscape. Contra ese documento, la entrada tenía tres errores:

| Lo que la entrada decía | Lo que el documento publica |
| :-- | :-- |
| Una descripción que incluye los «master agreements que fijan las condiciones estándar con el cliente» | Esa cláusula pertenece a `Term Deposit Framework Agreement`, que es **otro** Service Domain. La definición omitía además el `maturity processing` |
| Cinco operaciones de nivel control record, una de ellas `execute-interest-settlement` | **Cuatro**: `Initiate`, `Update`, `Control`, `Retrieve`. No existe un `Execute` de nivel control record |
| `control` con `mutates: false` | `PUT` con `requestBody: TermDepositFacility`: cambia el estado del control record |

El tercero era además una inconsistencia interna: las otras cuatro entradas declaraban `control` con `mutates: true`, de modo que la misma operación del estándar producía dos formas distintas según la capacidad, y eso no estaba escrito en ninguna parte.

**Decisión.** El dato de una capacidad se transcribe del **documento oficial de su Service Domain**, no de una vista del landscape ni de una paráfrasis. La jerarquía sigue bajo ADR-137 —ante una discrepancia manda el portal—; lo que esta decisión fija es la fuente del resto: definición, control record, operaciones y behavior qualifiers salen del documento publicado de esa capacidad.

Una entrada cuya fuente oficial no se tenga a la vista queda marcada como paráfrasis en el insumo, en lugar de pasar por transcripción.

**Consecuencia.** `Term Deposit` queda corregido en los tres puntos. `execute-interest-settlement` sale del nivel control record y reaparece como operación del behavior qualifier `Interest` (ADR-141). `control.mutates` pasa a `true`, con lo que la operación publica evento de dominio y la entrada queda consistente con las otras cuatro. El ejemplo del esquema para `controlRecord` deja de nombrar `Term Deposit Arrangement`, que es un valor que el estándar no usa.

Las otras cuatro entradas —`Consumer Loan`, `Current Account`, `Savings Account`, `Party Reference Data Directory`— **siguen siendo paráfrasis** y quedan anotadas como tales en **P-38**. No se inventó ninguna descripción para reemplazarlas.

**Verificación (2026-11-03).** `npm run verify:artifacts -w @bsl/cli` valida el archivo; `check:push` en verde. El producto de referencia pasa de 51 a 50 archivos con las cuatro operaciones: pierde el caso de uso y el evento de la operación retirada, y gana el evento de `control`.

**Traza.** RF-01, RF-02, ADR-135, ADR-137, ADR-138, ADR-141, Doc 1 §5, P-06, P-38, documento OpenAPI de `Term Deposit` v14.0.

---

## ADR-140 · El verbo y la ruta salen del action term; la forma de ruta es punto de variación

**Estado:** Revisada · 2026-11-03 · Doc 1

**Contexto.** El documento oficial publica sus rutas así: `POST /TermDeposit/Initiate`, `PUT /TermDeposit/{termdepositid}/Update`, `GET /TermDeposit/{termdepositid}/Retrieve`, `PUT /TermDeposit/{termdepositid}/Control`. El producto derivado servía `POST /term-deposits`, `PATCH /term-deposits/:id`, `GET /term-deposits/:id`, `POST /term-deposits/:id/control`. Las dos diferencias no son de estilo:

- **La base de la ruta.** El estándar la toma del Service Domain; la herramienta la tomaba del agregado en plural. Son nombres distintos cuando el equipo renombra su agregado, que es un caso que el producto ya admite y documenta.
- **El verbo.** El estándar usa `PUT` para `Update`, `Control` y `Execute`; la herramienta usaba `PATCH` para `Update` y `POST` para el resto. Y responde `200` a una iniciación, donde la herramienta respondía `201`.

Lo anterior se había armado sin el documento, así que no era una divergencia decidida: era un supuesto. Pero adoptar la forma del estándar sin más sube la curva de adopción, que es el hallazgo central de la revisión externa.

**Decisión.** El verbo y la última porción de la ruta se derivan del **action term**, y la forma de la ruta es un **punto de variación** con dos valores, `bian` por defecto y `rest` como opción. Los dos salen del mismo descriptor de operación: el estilo cambia la superficie del producto y nunca lo que el producto incorpora.

| | `bian` | `rest` |
| :-- | :-- | :-- |
| Base | el Service Domain sin espacios (`TermDeposit`) | el agregado en plural (`term-deposits`) |
| `Initiate` | `POST /TermDeposit/Initiate`, responde `200` | `POST /term-deposits`, responde `201` |
| `Update` | `PUT /TermDeposit/{id}/Update` | `PATCH /term-deposits/{id}` |
| `Retrieve` | `GET /TermDeposit/{id}/Retrieve` | `GET /term-deposits/{id}` |
| `Control` | `PUT /TermDeposit/{id}/Control` | `POST /term-deposits/{id}/control` |

El código de respuesta de una iniciación lo declara el estilo y no el action term: el estándar publica `200`, y una superficie de recurso responde `201` porque la operación crea uno. El artefacto `route-styles.json` lo declara en `initiateStatus`, de modo que no vive escrito en una plantilla.

**El protocolo sigue fijo.** `fixed: { inboundProtocol: rest }` **se conserva**: las dos formas son HTTP sobre REST, y lo que varía es la forma de las rutas dentro de ese protocolo. El doc 1 §2 queda por ajustar en ese punto: dice que el protocolo «no es punto de variación en esta versión», lo que sigue siendo cierto, pero ya no alcanza para describir la variabilidad de la superficie.

**Consecuencia, y es la más cara del cambio.** Con `bian` por defecto, el **activo base cambió**: `reference-aggregate.spec.ts` exige igualdad byte a byte entre lo que derivan las plantillas y `packages/base-template/template/`, de modo que hubo que regenerar el activo con las rutas nuevas —`/PartyReferenceDataDirectory/Initiate` y `/PartyReferenceDataDirectory/{id}/Retrieve`— y con ellas su controlador, su documento OpenAPI, su tipo de entrada y su prueba de humo. Arrastró también la ruta del circuito de composición y la lista exacta de rutas del circuito de generación.

Las plantillas dejan de llevar el decorador escrito: el verbo, la ruta y el código de respuesta llegan como marcadores, porque el motor de plantillas no tiene condicionales (ADR-065).

**Una divergencia declarada.** El estándar nombra el parámetro de ruta `{termdepositid}`; el producto lo nombra `{id}`. Se conserva `{id}`: la estructura y los action terms son los del estándar, y el nombre del parámetro es local al producto. Queda dicho acá para que no se lea como un descuido.

**Consecuencia asumida sobre el formato.** La prueba de humo generada pasa de los 100 caracteres en varias líneas cuando las rutas son las del estándar, así que entra a `.prettierignore` junto al documento OpenAPI, que ya estaba ahí por la misma razón: es un archivo generado y su estilo es el que escribe el generador. La verificación del producto —lint, pruebas y compilación— no comprueba formato.

**Verificación (2026-11-03).** `verify:generation` deriva `term-deposit-api` en forma `bian` y `deposit-rest-api` en forma `rest`, y los dos pasan su propia verificación. `generate-naming.spec.ts` fija las dos matrices de verbo y ruta, una por estilo.

**Traza.** RF-01, RF-02, RF-05, RNF-02, ADR-065, ADR-078, ADR-134, ADR-139, ADR-146, Doc 1 §2 §4 §6, Doc 5 §7, documento OpenAPI de `Term Deposit` v14.0.

---

## ADR-141 · Los behavior qualifiers entran al espacio de selección como segundo nivel

**Estado:** Aceptada · 2026-11-03 · Doc 1

**Contexto.** El estándar modela cada Service Domain en dos niveles: el control record y sus **behavior qualifiers**, que son subdivisiones de ese control record sobre las que publica operaciones propias. `Term Deposit` tiene diez —`Interest`, `Charge`, `Sweep`, `Deposit`, `DebitAndCredit`, `Payments`, `AmountBlock`, `IssuedDevice`, `Rollover`, `Booking`— con treinta operaciones entre todas. El espacio de selección conocía un solo nivel, y por eso `execute-interest-settlement` había terminado declarada donde no va (ADR-139).

**Decisión.** El descriptor de una capacidad gana `behaviorQualifiers`, con el nombre del qualifier y las operaciones que el estándar publica sobre él. Se ofrecen **en una sola pregunta, aplanada**: cada opción es `<Qualifier>.<operación>`.

**Por qué aplanada y no una pregunta por qualifier.** Una pregunta anidada no es declarable en el modelo de variabilidad, que resuelve una lista de puntos y no un árbol; y con diez qualifiers obligaría a diez preguntas para llegar a una respuesta. El aplanado conserva el qualifier en el registro de la opción, que es lo único que la derivación necesita.

**Una capacidad sin qualifiers no se pregunta.** `Party Reference Data Directory`, `Consumer Loan`, `Current Account` y `Savings Account` no declaran el arreglo. Para que la pregunta no aparezca vacía se agregó una regla al núcleo de la resolución: **una pregunta sin opciones no tiene respuesta que dar y no se hace**, siempre que el punto no sea obligatorio. Vale para cualquier punto cuyas opciones vengan de una respuesta anterior.

**El límite del dato.** Se transcribieron los diez qualifiers de `Term Deposit` del documento oficial, con el texto del `summary` sin el código de nivel de dos letras que el documento le pone delante. **Queda fuera `Payments/Exchange`**, porque `Exchange` no es uno de los cinco action terms que esta release deriva; es la misma regla que el insumo de la transcripción ya declaraba.

**Consecuencia.** El espacio de selección pasa a describir los dos niveles del estándar para la capacidad que tiene su documento oficial a la vista. Las otras cuarenta y una capacidades extraídas en el insumo de la Fase 1 **no traen qualifiers**: la extracción se hizo de las vistas del landscape, que no los dan. Queda en **P-35**.

El script de validación gana tres comprobaciones que el esquema no puede expresar: nombres de qualifier únicos dentro de la entrada, identificadores de operación únicos dentro del qualifier, y que ninguna operación de qualifier derive el mismo nombre que una operación del control record.

**Verificación (2026-11-03).** Las tres reglas se rompieron a propósito y cada una falló con su mensaje. `verify:generation` deriva `term-deposit-api` con cuatro operaciones de qualifier y diez rutas en su documento OpenAPI.

**Traza.** RF-01, RF-02, ADR-139, ADR-142, ADR-146, Doc 1 §5, P-35, documento OpenAPI de `Term Deposit` v14.0.

---

## ADR-142 · Una operación de behavior qualifier produce superficie y andamio, nunca una entidad inventada

**Estado:** Aceptada · 2026-11-03 · Doc 5

**Contexto.** Decidido que los behavior qualifiers entran al espacio de selección (ADR-141), queda qué produce en el producto una operación de qualifier. La respuesta por defecto era generar una sub-entidad por qualifier —un `Charge`, un `Interest`— con su identidad y sus atributos, sostenida por el agregado.

Dos cosas lo desaconsejan. El agregado generado es inmutable, con constructor privado y fábrica estática, así que sostener una colección de hijos exige reescribirlo. Y los atributos de un qualifier son tan desconocidos para la línea como los del agregado: generar un `Charge` con campos inventados es el **wizard de atributos** que ADR-082 ya descartó.

**Decisión.** Una operación de behavior qualifier produce **la superficie y el andamio**, y ninguna entidad nueva:

| Pieza | Qué se genera |
| :-- | :-- |
| Caso de uso | Uno por operación, en `src/application/<operación>/`. Carga el agregado, marca dónde va el efecto, persiste, publica su evento y registra el resultado |
| Ruta | Anidada bajo la instancia del qualifier, en el mismo controlador del agregado |
| Evento de dominio | Cuando la operación cambia estado y el producto se derivó con eventos |
| Caso de humo | Uno por operación |
| Registro | La operación queda en `derivation.operations` con su `qualifier` y su `businessEffect` |

**Un solo controlador y un solo repositorio.** El producto aloja un bounded context (MR-02 §3) y el qualifier es una subdivisión de su control record, no otro agregado: sus operaciones actúan a través del mismo agregado raíz y del mismo puerto de repositorio.

**Ninguna recibe cuerpo.** La línea genera los atributos del agregado como semilla y los valida; no tiene semilla equivalente para un qualifier, así que pedir un cuerpo sería validar una forma que nadie declaró.

**Todas son andamio.** `businessEffect` es `scaffold` en todas, cualquiera sea su action term. La línea no sabe qué significa aplicar interés, y decirlo en el registro es lo que evita que el producto parezca más terminado de lo que está.

**La forma de las rutas, por estilo.** En `bian` la operación nombra la instancia del qualifier como el estándar: `PUT /TermDeposit/{id}/Interest/{interestId}/Execute`. Una operación que inicia crea esa instancia y por eso no la nombra: `POST /TermDeposit/{id}/Charge/Initiate`. En `rest` la forma es de recurso: `GET /term-deposits/{id}/interests/{interestId}`.

**Consecuencia.** Cuatro plantillas nuevas: tres de caso de uso —consulta, con evento y sin evento— y una de método de controlador, más una de caso de humo. El documento OpenAPI declara los **dos** parámetros de ruta de una operación de qualifier; declarar solo uno habría dejado un documento con el que no se puede llamar a la operación.

Una consulta sobre un qualifier responde con el agregado que lo contiene, porque la línea no modela el qualifier. El caso de uso lo dice en su `@remarks`: estrechar la respuesta al qualifier es lo primero que agrega la capacidad.

**Verificación (2026-11-03).** `term-deposit-api` deriva 57 archivos con cuatro operaciones de qualifier y pasa su lint, sus pruebas y su compilación. `deposit-rest-api` ejercita la forma de recurso y el caso de uso sin eventos. Se apuntó la plantilla del caso de humo a otra ruta y el circuito lo rechazó.

**Traza.** RF-01, RF-02, RF-03, RNF-02, ADR-078, ADR-082, ADR-141, ADR-146, MR-02 §3, Doc 5 §6 §8.

---

## ADR-143 · Se admite declarar una capacidad fuera del catálogo, con la forma cerrada

**Estado:** Revisada · 2026-11-03 · Doc 1

**Contexto.** La revisión externa del 2026-10-28 proponía «mantener BIAN como referencia avanzada, no como única entrada visible» (propuesta 3.3). El seguimiento de mejoras la había dejado **excluida con argumento**: «debilita la alineación con el estándar, que es el objetivo general del proyecto».

Ese argumento se cae contra el propio marco. **MR-02 §3 ya admite el caso**, textual: «Si el producto corresponde a una capacidad que no figura en el espacio de selección por defecto, **se permite declarar un Service Domain fuera de ese subconjunto**, registrando el Business Domain que lo contiene. Lo que no se admite es omitir el metadato». La tesis lo dice igual en `3-fundamentacion.tex`. Estaba **declarado y no implementado**: el resolvedor rechazaba cualquier valor fuera de las opciones ofrecidas.

Y el caso es real. El laboratorio no construye el core del banco: construye backends para capacidades de negocio que no siempre tienen un Service Domain publicado. Hoy, si la capacidad no está en las cinco entradas, la herramienta frena.

**Decisión.** Se admite declarar una capacidad fuera del catálogo. **La forma queda cerrada y solo los valores hoja quedan abiertos.**

| Campo | Capacidad del catálogo | Capacidad declarada |
| :-- | :-- | :-- |
| Business domain | de la entrada | **elegido entre los nueve** del marco |
| Business area | de la entrada | **derivado del grupo, nunca preguntado** |
| Nombre de la capacidad | de la entrada | escrito, validado como nombre |
| Control record | de la entrada | escrito, validado como nombre |
| Operaciones | de la entrada | **elegidas entre los cinco** action terms derivables |

El Business Area no se pregunta a propósito: un producto que pudiera responder las dos cosas por separado podría contradecir al estándar.

**Por qué sigue siendo una línea de producto.** El «conjunto cerrado» del doc 1 §3 está acotado a una clase de variabilidad, y su justificación es estrecha y verificable: «la escritura libre dejaría el metadato de dominio sin validación posible». Una capacidad declarada **exige** su Business Domain y su control record, así que el metadato sigue validado: se cumple la justificación y cae la forma, no la razón. La derivación sigue siendo sistemática —misma estructura, mismas plantillas, mismos action terms— y no hay un camino de código que solo la capacidad declarada recorra.

Queda como **desviación declarada**, en el estilo de MR-01 §6: la familia admite un producto cuya capacidad no está en el espacio por defecto, y el registro lo marca.

**Lo que esto habilita, y vale más que el atajo.** El registro escribe `declaredOutsideCatalog: true`, de modo que se puede preguntar al conjunto de productos del laboratorio **qué capacidades propias se repiten**. Tres productos declarando la misma es la evidencia que justifica una entrada nueva del catálogo. Es el flujo de retorno del dominio que MR-01 §4 declara y que hasta ahora no tenía por dónde ocurrir.

**Consecuencia.** Artefacto nuevo `business-domains.json` con los nueve Business Domains y su área. La opción centinela `(declared)` lleva `declared: true` y su propio arreglo de operaciones, con lo que la condición `serviceDomain.some(s => s.declared)` ofrece las tres preguntas extra **sin tocar la gramática de reglas** y la pregunta de operaciones no se duplica. El registro y el README del producto dicen que la capacidad fue declarada.

El doc 1 §3 queda por ajustar: su fila «Selección» dice «un subconjunto de un conjunto cerrado», y pasa a nombrar la forma cerrada con valores hoja abiertos.

**Un defecto latente que esto activaba.** Una operación `Execute` sin calificador enrutaba a `:id/s` en forma de recurso, porque pluralizar una cadena vacía da `s`. Ninguna entrada del catálogo lo alcanzaba, porque todas califican sus ejecuciones; una capacidad declarada sí. Corregido a `:id/execute`.

**Sobre el tag del documento OpenAPI.** Las operaciones de una capacidad declarada se agrupan bajo `CR - <control record declarado>`. El tag nombra el **nivel** —control record frente a behavior qualifier— y no la procedencia; lo que dice que el estándar no la publica es `declaredOutsideCatalog` en el registro.

**Verificación (2026-11-03).** `verify:generation` deriva `pocket-api` para la capacidad declarada `Savings Pocket`, comprueba que el registro trae los cuatro campos con el área derivada del grupo, y el producto pasa su propia verificación. Tres roturas: sin Business Domain, con un Business Domain fuera de los nueve, y con un nombre en minúsculas. Y la inversa también se rechaza: declarar un Business Domain para una capacidad del catálogo falla.

**Traza.** RF-01, RF-02, RNF-02, ADR-083, ADR-138, MR-01 §4 §6, MR-02 §3, Doc 1 §3 §5, `3-fundamentacion.tex` §espacio de selección, revisión externa 2026-10-28 propuesta 3.3.

---

## ADR-144 · El espacio de selección se presenta en lenguaje de negocio, con el nombre del estándar al lado

**Estado:** Aceptada · 2026-11-03 · Doc 1

**Contexto.** Dos propuestas de la revisión externa —3.1, separar en la presentación estándar, capability, producto y agregado; y 3.2, lenguaje natural en la pregunta de operaciones— habían quedado en «se decide con lo que muestre la medición». El argumento era razonable: construirlas antes de medir es inventar el requisito.

Pero el hallazgo que las motiva no es de preferencia, es de adopción: entender BIAN da ventaja a quien ya lo conoce y sube la curva para el resto, y eso no lo baja medirlo primero. La pregunta de operaciones mostraba `Execute Term Deposit Interest Settlement` con `Execute` de pista, que no dice qué endpoint sale.

**Decisión.** El espacio de selección gana una **capa de lenguaje llano**, y es dato del artefacto y no código: `plainName` y `plainDescription` por capacidad, `plainDescription` por operación, `plainName` por behavior qualifier. La lista se lee primero en lenguaje de negocio y el nombre del estándar queda alineado al lado, de modo que los dos se aprenden juntos en lugar de sustituirse.

La pregunta de operaciones muestra además **la ruta que va a salir**. El estilo de ruta y el agregado ya están contestados cuando esa pregunta llega, así que la ruta mostrada es la real y no un ejemplo.

**Es glosa propia, no transcripción.** El esquema lo dice en la descripción de los campos: es la redacción de esta línea y no texto del estándar. Por eso convive con `description`, que sí es del estándar (ADR-139) y que ahora viaja al README del producto.

**Los campos son obligatorios.** Se declararon opcionales al principio y el código pasó a depender de ellos, lo que dejaba una caída latente: una entrada sin glosa habría roto la presentación en ejecución. El esquema los exige.

**Las etapas.** Las catorce preguntas se reordenaron en cuatro bloques declarados en el modelo —`Capability`, `Surface`, `Project`, `Options`— y el bloque se nombra una sola vez, **solo cuando una pregunta se hace de verdad**: un valor pasado por bandera no anuncia nada. El modelo gana `stage` como campo obligatorio de cada punto, y la resolución avisa por un callback, porque el núcleo no escribe en la terminal.

**Consecuencia.** La descripción oficial de la capacidad deja de morir en la pista de la pregunta: el README del producto gana la fila `What it is` con la definición del estándar. Hasta ahora lo que viajaba al producto era el texto libre del proyecto, que es otra cosa.

Las propuestas 3.1 y 3.2 salen de «se decide midiendo» a hechas, y **G6 se reabre y se cierra construido**.

**Verificación (2026-11-03).** Tres roturas: una capacidad sin su glosa, una operación de qualifier sin la suya y una pregunta sin su etapa; las tres fallan en `verify:artifacts` con su mensaje.

**Traza.** RF-02, RNF-01, ADR-081, ADR-136, ADR-139, ADR-145, Doc 1 §5 §6, revisión externa 2026-10-28 propuestas 3.1 y 3.2.

---

## ADR-145 · La derivación cierra con una revisión enmendable, no con una confirmación

**Estado:** Aceptada · 2026-11-03 · Doc 5

**Contexto.** ADR-136 puso una declaración de alcance antes de escribir, con una confirmación sí o no. Resolvió la mitad del problema: quien deriva ve qué va a producir antes de que exista. La otra mitad quedó abierta: una pregunta del estándar contestada mal costaba **el comando entero de nuevo**, y es esa fricción la que hace que un desarrollador deje de leer las preguntas.

**Decisión.** La derivación cierra con una **revisión enmendable**. Muestra cada respuesta —capacidad, agregado, operaciones, qualifiers, forma de las rutas, eventos, pruebas de ejemplo y destino— y ofrece corregir cualquiera de ellas, derivar, o cancelar.

**Qué se vuelve a preguntar al corregir.** Solo lo que depende de la respuesta corregida. Corregir el agregado cuesta una pregunta. Corregir la capacidad vuelve a preguntar lo que le pertenece —sus operaciones, sus qualifiers, su agregado y los campos de una capacidad declarada— y deja en pie el resto: el proyecto, su descripción, su responsable y su correo no dependen de la capacidad y no se preguntan otra vez.

Las dependencias se declaran de forma explícita en la operación, no se infieren. Conservar una operación elegida para otra capacidad dejaría un producto cuyo registro dice una capacidad y cuyo código responde por otra.

**Una bandera no es una respuesta al corregir.** Al volver a preguntar se descarta lo que la invocación había dado para ese punto: honrarlo otra vez mostraría la pregunta y conservaría el valor viejo.

**Fuera de una terminal declara y sigue**, como hacía ADR-136: una corrida por banderas —un script, la verificación de la línea— no tiene a quién preguntar, y detenerla convertiría una declaración en una falla.

**Consecuencia.** Se extrajo de `resolveInput` la resolución de **un punto suelto**, que es lo que una revisión necesita y que volver a correr la resolución completa no da: preguntaría todo dos veces. El cambio es de forma y no de comportamiento: la resolución completa quedó como el bucle que llama a esa función.

Si la revisión deja una respuesta que rompe una regla del modelo, la regla se avisa y la opción de derivar no se ofrece hasta que se corrija. Antes el mismo caso terminaba en un error al final de la resolución.

Los dos valores de la revisión que no son respuestas —derivar y cancelar— se escriben `(derive)` y `(cancel)`: el identificador de un punto de variación no admite paréntesis, así que no pueden colisionar con una respuesta enmendable.

**Verificación (2026-11-03).** Dos pruebas nuevas en `generate.operation.spec.ts`: corregir el agregado conserva las demás respuestas, y corregir la capacidad vuelve a preguntar sus dependientes y **no** pregunta la descripción ni el responsable. El doble de preguntas admite ahora una respuesta distinta por vez, porque la revisión pregunta `What now` una vez por ronda.

**Traza.** RF-02, RNF-01, RNF-02, ADR-081, ADR-136, ADR-144, Doc 5 §2, revisión externa 2026-10-28 hallazgos 2, 4 y 6.

---

## ADR-147 · El punto de composición del activo son tres archivos, y ningún archivo de `src/` queda sin tipo de elemento

**Estado:** Aceptada · 2026-11-04 · Doc 2 · revisa ADR-045

**Contexto.** El analizador del activo base declara un tipo de elemento por capa y uno más, `composition`, con el patrón `src/(app.module|main).ts`. Esos dos archivos eran, al cerrar esta fase, los únicos que conocen todas las capas a la vez. **ADR-110** de la Fase 3 agregó un tercero, `platform.module.ts`, para servir los puertos técnicos de la línea a cualquier módulo incorporado, y nadie lo agregó al patrón.

La consecuencia no es que la regla lo rechace: es que **no lo examina**. `boundaries/element-types` solo evalúa archivos que corresponden a un tipo declarado, y un archivo que no corresponde a ninguno se omite en silencio. Comprobado el 2026-11-04 activando `boundaries/no-unknown-files` sobre una copia del activo: señala `platform.module.ts` y ningún otro archivo.

**Decisión.** Dos cambios en la configuración del activo, que viaja copiada a todo producto derivado.

El patrón de `composition` pasa a `src/(app.module|platform.module|main).ts`, que es lo que el activo tiene hoy. Y se activa `boundaries/no-unknown-files` como error, de modo que un archivo nuevo en `src/` que no corresponda a ninguna capa **falla** en lugar de quedar fuera del análisis.

**Por qué la segunda mitad importa más que la primera.** Nombrar el archivo que falta corrige el caso de hoy. Activar la regla corrige la clase: el modo de fallar era silencioso, y un análisis que omite lo que no reconoce da la misma salida —en verde— cuando todo está bien y cuando algo se le escapó. Ese es el peor de los dos resultados posibles, porque nada lo dice.

**Qué no cambia, y por eso no hay violación que haya escapado.** Las direcciones que la regla prohíbe son dominio hacia cualquier otra capa, aplicación hacia infraestructura o configuración, y configuración hacia fuera de sí misma. Lo que `platform.module.ts` hace —importar adaptadores de infraestructura y el artefacto de contratos— es legítimo bajo cualquier clasificación que le corresponda. El hueco era de cobertura del análisis, no de conformidad del activo.

**Verificación, rompiéndolo.** Un archivo nuevo en la raíz de `src/` sin capa declarada hace fallar el lint nombrándolo. Un import de la capa de aplicación desde `platform.module.ts` **no** falla, y es correcto: ese archivo ahora es composición, y la composición puede importar todo. La sonda válida para él es la primera.

**Consecuencia.** El activo base cambia su `eslint.config.mjs`, que se copia literal al producto, así que todo producto derivado desde ahora nace con la regla cubriendo sus tres archivos de composición. Los productos ya derivados no la reciben: les llega al actualizarse. **Aplicado al expediente el mismo día:** el doc 2 §6 lleva el bloque del analizador retranscrito y la nota de los dos cambios, y §9 los dos bloques reales del punto de composición con el hallazgo ya corregido.

**Traza.** RNF-03, ADR-045, ADR-066, ADR-110, Doc 2 §6 y §9, P-46.

---

## ADR-148 · La configuración del analizador de la herramienta fija su raíz, porque los patrones no resolvían desde el paquete

**Estado:** Aceptada · 2026-11-04 · Doc 4 · revisa ADR-049

**Contexto.** Este hallazgo salió de aplicar **ADR-147**. Al activar `boundaries/no-unknown-files` en la configuración de la raíz del monorepo, el lint de `@bsl/cli` empezó a señalar **todos** sus archivos como sin tipo de elemento. La causa es que sus patrones están escritos desde la raíz —`packages/cli/src/core/**`— y el script `lint` del paquete ejecuta el analizador **desde el paquete**, donde ese mismo archivo es `src/core/...`.

Lo que eso significa hacia atrás es lo grave: en `npm run verify -w @bsl/cli`, que es la puerta que el paquete corre sobre sí mismo, **ningún archivo correspondía a un tipo y la regla de dependencia de la herramienta no comprobaba nada**. No fallaba: se omitía. Solo el `npm run lint` de la raíz, que ejecuta el analizador desde la raíz, la estaba aplicando de verdad.

**Decisión.** La configuración declara `'boundaries/root-path': import.meta.dirname`, con lo que el plugin resuelve las rutas contra el directorio de la configuración y no contra el directorio de trabajo. Los patrones quedan como estaban y pasan a coincidir desde los dos lugares.

**Por qué no se cambiaron los patrones.** Reescribirlos relativos al paquete los rompería desde la raíz, que es el problema simétrico. Fijar la raíz resuelve los dos a la vez y deja una sola verdad sobre dónde empieza una ruta.

**Comprobado rompiéndolo, desde el paquete.** Un import de `operations` dentro de `core` ahora falla con `The core group cannot import from operations`. Antes del cambio, esa misma violación pasaba el lint del paquete en verde.

**Por qué no se había notado.** Porque los dos modos de fallar de este plugin son distintos: un archivo con tipo que importa lo que no debe **falla**, y un archivo sin tipo se **omite**. Con todos los archivos sin tipo, la regla no tenía a quién aplicarse y su silencio era indistinguible de su aprobación. Es el mismo modo de fallar que ADR-147 corrige en el activo, y aparece aquí porque la corrección de allá obligó a mirar.

**Consecuencia.** La regla de dependencia de la herramienta queda comprobada por las dos puertas, la del paquete y la de la raíz. **Aplicado al expediente el mismo día:** el doc 4 §3 lleva la nota de por qué la configuración fija su raíz y qué significaba hacia atrás, y su bloque quedó retranscrito como el extracto del paquete de la herramienta que su etiqueta declara.

**Traza.** RNF-03, ADR-049, ADR-147, Doc 4 §3, P-46.

---

## ADR-149 · `display` se retira del modelo y `fixed` pasa a estar comprobado

**Estado:** Aceptada · 2026-11-04 · Doc 1 · revisa ADR-144

**Contexto.** El modelo de variabilidad llevaba dos declaraciones que **ningún código leía**. `display` nombraba, en tres puntos de selección, qué campos de cada opción mostrar al elegir. `fixed` declara los tres invariantes de la familia: `language`, `packageManager` e `inboundProtocol`. Un `grep` sobre el paquete daba cero consumidores del primero, y del segundo solo su propio tipo.

Los dos casos parecen el mismo y no lo son, y por eso la decisión es distinta para cada uno.

**Decisión para `display`: se retira.** Del modelo, de su esquema y del tipo. **ADR-144** construyó la presentación de las opciones en el adaptador de terminal, con el nombre del estándar al lado y la ruta que va a salir, y esa presentación no consulta `display` ni podría: decide por etapa y por punto, no por una lista de campos. La declaración quedó superada y mantenerla invita a que alguien la edite esperando un efecto que no ocurre.

**Decisión para `fixed`: se queda y se le exige.** No se retira por dos razones. Es la declaración de qué **no** varía en la familia, que el doc 1 §2 usa como punto de partida de todo el modelo; y un invariante no se consulta en ejecución, porque si se consultara sería una variable. Lo que le faltaba no era un consumidor en la derivación sino que alguien comprobara que es cierto. Entra por dos lados.

**El validador de artefactos exige que lo fijo y lo variable sean disjuntos.** Una decisión declarada en los dos lugares se lee como cerrada y se pregunta igual, y la pregunta gana en silencio porque el resolutor solo lee `variationPoints`. El riesgo no es teórico: **ADR-140** convirtió la **forma de la ruta** en punto de variación mientras el **protocolo de entrada** seguía fijo, y las dos cosas se nombran casi igual.

**Tres pruebas leen el activo real y comprueban cada invariante.** Que todo archivo de `src/` del activo sea TypeScript; que el activo lleve configuración de npm y ninguna de otro gestor; que exponga su superficie con controladores HTTP. Es el patrón que esta fase ya usa con el activo base como validación ejecutable del marco, aplicado a lo que hasta ahora solo estaba escrito.

**Dónde se tropezó al construirlas.** La primera versión de la prueba del gestor de paquetes recorría el activo en profundidad y encontraba dos `yarn.lock` **dentro de `node_modules`**, de dependencias suyas. El invariante es sobre el activo, no sobre lo que el activo instala, así que el recorrido excluye `node_modules` y la comprobación de la raíz no desciende.

**Verificación, rompiéndolo.** Declarar `inboundProtocol` también como punto de variación hace fallar el validador nombrándolo. Cambiar el valor fijo de `packageManager` a otro gestor, o dejar un archivo que no sea TypeScript en `src/` del activo, hacen fallar su prueba.

**Consecuencia.** El esquema pierde una propiedad opcional, lo que no invalida ningún modelo existente. **Aplicado al expediente el mismo día:** el doc 1 §2 gana la nota de que los tres invariantes están comprobados y dónde, y los bloques del modelo y de su esquema quedaron retranscritos del archivo real. En prosa no había que corregir nada: un `grep` sobre todo el expediente confirma que `display` solo aparecía dentro de esos bloques, nunca en el texto. El doc 6 §10 ajusta la fila de `verify:artifacts` con la regla nueva.

**Traza.** RF-02, RF-05, ADR-140, ADR-144, Doc 1 §2 y §5, P-37.

---

## ADR-150 · El circuito de generación compara la lista de archivos de cada producto contra un manifiesto, no un conteo

**Estado:** Aceptada · 2026-11-04 · Doc 6 · revisa ADR-088

**Contexto.** `verify-generation.mjs` declaraba, por producto, cuántos archivos debía escribir la derivación: 57, 34, 38 y 37. Cada grupo de mejoras movió esos números a mano, y el único aviso de que había que moverlos era el mensaje de error del propio script.

El conteo tiene un defecto peor que el costo de mantenerlo: dice **cuántos** y nunca **cuáles**. Una plantilla agregada y otra retirada se cancelan y la comprobación sigue en verde.

**Decisión.** Cada producto del circuito tiene un manifiesto en `scripts/manifests/<producto>.txt`: la lista ordenada de las rutas relativas que su derivación escribe. La comprobación compara la lista real contra la declarada y, al diferir, imprime los dos lados —qué ruta apareció y qué ruta desapareció— y nombra el comando que acepta el cambio. `npm run verify:generation -- --update-manifests` los reescribe.

**Por qué un manifiesto regenerable y no un rango.** Un rango de archivos admitidos convierte la comprobación en una tolerancia: deja de decir qué derivó el mecanismo y empieza a decir que derivó una cantidad plausible. El manifiesto conserva un oráculo exacto y traslada el costo a donde se puede revisar: aceptar un cambio deja un diff en un archivo de texto con nombres de archivo, en lugar de una edición a un número que nadie puede juzgar.

**Lo que no se derivó, y a propósito.** La lista de rutas del documento OpenAPI sigue escrita a mano en el script. Derivarla de los argumentos del producto, con las mismas reglas que la herramienta usa para producirla, haría que un error en esas reglas pasara la comprobación: un oráculo que recalcula lo que verifica no verifica nada. Esa lista cambia solo cuando alguien cambia deliberadamente la definición de un producto del circuito, que es un acto consciente; el conteo de archivos cambiaba al agregar cualquier plantilla en cualquier parte, que es lo que lo volvía frágil.

**Verificación, rompiéndolo.** Quitar una ruta de un manifiesto hace fallar el circuito con `appeared: src/main.ts` y con el comando que lo acepta. Los cuatro manifiestos iniciales se generaron con la bandera y dieron 57, 34, 38 y 37: los mismos números que la tabla declaraba, lo que confirma que el manifiesto no cambió el oráculo, solo su forma.

**Consecuencia.** La tabla `PRODUCTS` pierde su campo `files`. Los manifiestos **no viajan en el paquete publicado**: la lista blanca de `files` declara `bin`, `dist` y las plantillas, y no `scripts/`. Es lo correcto, porque el circuito se corre desde el repositorio y no desde el paquete instalado; se anota porque la primera redacción de esta decisión afirmaba lo contrario. **Aplicado al expediente el mismo día:** el doc 6 §10 ajusta la fila de `verify:generation` y lleva la nota de las dos puertas que cambiaron. No es §9, como esta decisión decía primero: §9 es el registro de requests y no tiene que ver. La tabla de evidencia de §11 conserva sus conteos de 43 y 27 porque ya declara, con nota fechada, que es la del cierre de la fase.

**Traza.** RF-05, RNF-03, ADR-088, Doc 6 §9, P-34, P-21.

---

## ADR-151 · La traza del estándar W3C entra al activo; exportarla sigue siendo del módulo

**Estado:** Revisada · 2026-11-05 · Doc 2 · revisa ADR-133

**Contexto.** ADR-133 partió el identificador de correlación en dos y tomó la primera mitad: cada request tiene nombre dentro del servicio. Dejó fuera, en el módulo de observabilidad, «la cabecera que la organización use, el formato de contexto de traza, la propagación saliente, el muestreo y las métricas», con el argumento de que eso depende de la plataforma institucional.

Al mirar esa frase con el log en la mano aparece que mezcla dos cosas distintas. El muestreo, las métricas y el exportador sí dependen de la plataforma: alguien tiene que decidir a qué servicio se mandan los spans y con qué proporción. El **formato** no: W3C Trace Context es un estándar publicado, es lo que leen Azure Monitor, la distribución de AWS de OpenTelemetry y cualquier colector de esa familia, y leerlo no requiere ningún servicio institucional. Es el mismo criterio con el que ADR-139 resolvió que el dato de una capacidad se transcribe del documento oficial del estándar y no de una paráfrasis: cuando hay estándar publicado, la línea no inventa una cabecera propia ni espera a que la organización elija una.

Y el costo de no tenerlo es concreto: con solo `requestId`, el log de un producto se puede leer una request a la vez, pero no se puede juntar con el log del servicio que lo llamó. En un entorno donde un producto de la línea atiende a otro producto de la línea, eso es justo la pregunta que hay que responder cuando algo falla.

**Decisión.** El activo base lee `traceparent` cuando el llamador lo manda y abre la traza cuando no llega. Mantiene el `traceId`, conserva el span del llamador como `parentSpanId`, y **siempre acuña su propio span**, porque el trabajo que hace este servicio no es el que hacía quien llamó. Devuelve en la respuesta un `traceparent` que nombra su span, que es lo que el siguiente servicio de la cadena recoge. Los tres valores viajan en el contexto asíncrono junto al `requestId`, de modo que toda entrada escrita mientras se atiende la request los lleva.

Un valor malformado no es motivo para fallar una request: se trata como si no hubiera llegado traza y el servicio abre la suya. Los identificadores que el estándar reserva como vacíos —todo ceros— y la versión `ff` se rechazan igual.

**Sigue fuera, en el módulo de observabilidad.** Exportar spans a la plataforma de la organización, el muestreo, las métricas y la propagación saliente hacia un cliente HTTP. La propagación saliente además no tiene hoy a qué engancharse: el activo base no trae cliente HTTP, así que lo único que se podía hacer —dejar el valor listo para quien lo pase— es lo que hace `traceparentOf`.

**Por qué el span propio y no el que llegó.** Reusar el span del llamador haría que dos servicios reportaran el mismo tramo de trabajo, y la traza dejaría de poder decir cuánto tardó cada uno. El verificador comprueba exactamente eso: que el producto no responda bajo el span de su llamador.

**Consecuencia.** `trace-context.ts` viaja copiado con el activo. El asiento del request lleva los identificadores él mismo en lugar de dejarlos al adaptador, para que la única entrada que responde por una request no dependa de que el contexto asíncrono esté intacto. En la forma legible la traza se muestra solo cuando llegó de otro servicio: una traza que abrió este servicio no agrega nada en pantalla, porque es la request, que ya tiene su columna.

**Traza.** ADR-085, ADR-128, ADR-133, ADR-139, T-09, RNF-02, Doc 2 §8, Fase 3 doc 1 C-02.

---

## ADR-152 · Un asiento dice de qué despliegue viene, iza lo que se consulta y nunca lleva un secreto

**Estado:** Revisada · 2026-11-05 · Doc 2 · revisa ADR-128 y ADR-084 · revisada en ADR-153

**Contexto.** El asiento que ADR-128 fijó tiene cinco claves y todo lo operativo dentro de `context`.
Contra lo que hace falta para operar, eso deja tres huecos. No dice **de qué despliegue viene**, así que
un stream donde conviven dos réplicas o dos releases no se puede separar. Los campos que un tablero
consulta —`route`, `statusCode`— viven como `context.route`, y hay que nombrarlos así en cada consulta.
Y `LogContext` es `Record<string, unknown>`, así que nada impide que un caso de uso adjunte un token o
el documento de una persona: ADR-084 prohibió registrar el body, que es por donde llegan, y no cubrió
el camino por el que alguien los pone a mano.

**Decisión.** Tres cosas, en el activo base y sin dependencia nueva.

**Todo asiento dice de qué despliegue viene.** `service`, `serviceVersion`, `environment`, `host`, `pid`
y `severityNumber`. El número de severidad es el del modelo de datos de logs de OpenTelemetry, que es lo
que permite a un colector ordenar severidades sin conocer las palabras de esta línea.

**Lo que se consulta se iza al nivel superior**, en un conjunto cerrado: nombre del evento, `scope`,
identificadores de request y de traza, y después del mensaje el método, la ruta, el estado, la duración,
el agente y el error. Lo que un caso de uso adjunta se queda en `context`, donde no choca con un campo
de la línea. Un asiento declara además `event`, un nombre estable de máquina —`http.request.served`,
`service.started`— que permite consultar por tipo sin hacer coincidir texto.

**Un asiento nunca lleva un secreto.** Lo que un llamador adjunta pasa por una redacción por nombre de
clave —`password`, `token`, `authorization`, `cardNumber`, `documentNumber`, `email`, `phone` y su
familia— acotada en profundidad, en largo de texto y en cantidad de elementos.

**El ciclo de vida del proceso se registra**: qué es al arrancar, que le pidieron parar con `SIGTERM` o
`SIGINT`, y por qué se muere ante una excepción o un rechazo sin manejar. Sin la última, una caída y un
reinicio ordenado se leen igual en un stream. Las sondas pasan a `debug` en lugar de excluirse: al nivel
`info` de un servicio desplegado no se ve ninguna, y se gana poder subir el nivel un rato.
`LOG_DESTINATION` queda en `split` por defecto, con `stdout` para la plataforma que lee el stream del
que viene una línea como su severidad.

**Alternativas.** Renombrar las claves a ECS o al modelo de OpenTelemetry era lo más interoperable y se
descartó: cambia toda clave de todo asiento, obliga a retranscribir la evidencia de tres decisiones en
cuatro documentos, y no compra nada que las plataformas destino no resuelvan consultando el campo por su
nombre. De ahí se tomó solo `severityNumber`, que es donde la falta de estándar sí dolía.

**Por qué la redacción no distingue dato de negocio.** La clave no alcanza: el nombre de una persona
llega como `partyName` y el de un servicio como `serviceName`, así que redactar por `name` vaciaría
medio log. La lista cubre credenciales e identificadores fuertes; de no adjuntar dato de negocio
responde quien escribe la entrada, y el README del producto lo dice.

**Límite asumido.** El asiento iba a declarar el tamaño de la respuesta. Al correrlo nunca apareció:
cuando el interceptor escribe, el cuerpo todavía no se serializó, así que `content-length` no existe.
Escribirlo en el evento `finish` lo resolvería y rompería la garantía de ADR-084, porque una request
abortada no dispara `finish` y quedaría en silencio. El campo se retiró: uno que casi nunca está es peor
que no tenerlo.

**Consecuencia.** Activo base en `0.15.0` y herramienta en `0.19.0`. `redaction.ts` viaja copiado con
tres pruebas, así que el producto de referencia pasa de 57 a 62 archivos. La suite del activo pasa de 46
a 78 pruebas.

**Verificación (2026-11-05).** `check:push` en verde con 288 pruebas y cero vulnerabilidades.
`verify:generation` comprueba en ejecución, sobre un producto arrancado sin editarle un archivo, que
ninguna entrada deja de decir de qué despliegue viene, que el arranque y el apagado están nombrados, y
que la traza que llegó se conserva. Un asiento de request en `production`:

```json
{"timestamp":"2026-11-05T20:08:11.081Z","level":"info","severityNumber":9,"service":"bsl-base-template","serviceVersion":"1.4.2","environment":"production","host":"…","pid":10069,"event":"http.request.served","scope":"http","requestId":"edge-7781","traceId":"4bf92f3577b34da6a3ce929d0e0e4736","spanId":"eda7a011b5e5a1a5","parentSpanId":"00f067aa0ba902b7","traceFlags":"01","message":"POST /PartyReferenceDataDirectory/Initiate 200","method":"POST","route":"/PartyReferenceDataDirectory/Initiate","statusCode":200,"durationMs":1,"userAgent":"curl/8.7.1"}
```

**Traza.** ADR-084, ADR-085, ADR-128, ADR-131, ADR-133, ADR-151, T-08, T-09, RNF-02, Doc 2 §8, Doc 2 §9,
Doc 5 §13.

---

## ADR-153 · Todo fallo del producto se responde y se explica en un solo lugar

**Estado:** Revisada · 2026-11-05 · Doc 2 · revisa ADR-084 y ADR-152

**Contexto.** La pregunta que abrió la decisión fue si el log debía llevar el body. La respuesta era no,
y al medir qué quedaba registrado cuando algo fallaba apareció algo peor, comprobado arrancando un
producto y provocando los dos fallos. Un `400` dejaba **solo el estado**, en nivel `info`, sin una
palabra sobre qué campo estaba mal: la lista de problemas llegaba al cliente y no al log. Un `500`
dejaba dos asientos y ninguno servía: el del request también en `info`, de modo que no se distinguía de
un `200` filtrando por severidad, y el único en `error` lo escribía el manejador del framework con el
mensaje `{"code":"ECONNREFUSED"}` —`JSON.stringify` de un `Error` solo devuelve sus propiedades propias—
y **sin `requestId` ni traza**, porque ese manejador corre fuera del contexto del interceptor. Una ruta
que el servicio no tiene no quedaba registrada en absoluto.

**Decisión.** Tres piezas, con una frontera clara entre lo que ve el llamador y lo que ve el log.

**Un middleware nombra la request antes que nada.** El contexto se abre con `app.use` y no en el
interceptor, porque un interceptor corre **después de los guards**: una request rechazada por el guard
que agrega un módulo de autenticación quedaría rechazada antes de que nada la nombrara. El middleware
envuelve la tubería entera, así que todo lo que se escriba mientras se atiende esa request lleva sus
identificadores, incluido lo que el filtro escribe después de que el manejador falló.

**Un filtro `@Catch()` responde por todo fallo**, registrado con `APP_FILTER` para toda ruta. Clasifica
tres casos: una `HttpException` levantada a propósito, un `Error` que nadie esperaba, y un valor lanzado
que no es ni un error.

**El reparto es deliberadamente opuesto.** Al llamador, siempre la misma forma —`statusCode`, `error`,
`message`, `problems` cuando lo que está mal es el request, y `requestId` para que pueda citarlo— y un
`5xx` responde una línea genérica, porque el mensaje de un error interno nombra tablas, hosts y
librerías. Al log, todo: un `4xx` como `warn` con `invalid` —una entrada por campo y regla— y un `5xx`
como `error` con el nombre, el mensaje, el `code`, el stack y la cadena de causas.

**Por qué no el body, ni cuando falla.** Tres razones en orden de peso. Es donde viajan los datos de la
persona, y un log se envía, se indexa y se conserva. No es lo que responde la pregunta: para saber qué
entró hace falta **qué campo y qué regla**, no el valor. Y un body por request multiplica la factura del
colector y entierra lo demás. La redacción de ADR-152 ayuda y no es garantía: un campo anidado con
nombre inocente la pasa.

**Consecuencia sobre lo anterior.** ADR-084 pedía una entrada por request, responda o falle: se
conserva, y ahora la escribe el interceptor cuando el servicio respondió y el filtro cuando falló, que
es la pieza que sabe por qué. Siguen siendo **dos piezas y una entrada**, y ahora también la hay para
una ruta que no existe.

**Consecuencia.** Activo base en `0.16.0` y herramienta en `0.20.0`. Dos archivos nuevos viajan copiados
y el producto de referencia pasa de 62 a 66 archivos. El esquema `Problem` del documento OpenAPI gana
`problems` y `requestId` y queda tipado, lo que **cambia la forma del cuerpo de error de todo producto
derivado**: es el costo declarado de esta decisión.

**Verificación (2026-11-05).** `check:push` en verde con 296 pruebas y cero vulnerabilidades.
`verify:generation` comprueba en ejecución que un request que el llamador erró se reporte como `warn` y
que uno fallido diga cuánto tardó antes de fallar. Tres de los seis casos:

```json
{"level":"warn","event":"http.request.failed","requestId":"mal-2","message":"POST /PartyReferenceDataDirectory/Initiate 400","statusCode":400,"durationMs":1,"context":{"invalid":["name: Invalid input: expected string, received undefined","Unrecognized keys: \"nombre\", \"password\""]}}
{"level":"error","event":"http.request.failed","requestId":"err-4","message":"GET /PartyReferenceDataDirectory/boom/Retrieve 500","statusCode":500,"error":{"name":"Error","message":"Could not reach the store","stack":"…","cause":{"name":"Error","message":"connection refused","code":"ECONNREFUSED","stack":"…"}}}
{"level":"warn","event":"http.request.failed","requestId":"ruta-6","message":"GET /no-existe 404","statusCode":404,"durationMs":0}
```

**La contraseña que el segundo caso mandó en el body no aparece en ninguna parte del log**: solo el
nombre de la clave que la validación rechazó. Y lo que recibió ese llamador:

```json
{"statusCode":400,"error":"Bad Request","message":"The request is not valid.","problems":["name: Invalid input: expected string, received undefined","Unrecognized keys: \"nombre\", \"password\""],"requestId":"mal-2"}
```

**Límite asumido.** Al formatear se corrigieron dos archivos que `.prettierignore` excluye a propósito
—`openapi.ts` y `http-smoke.spec.ts`, que los genera la herramienta— y `reference-aggregate.spec.ts` lo
detectó: el activo tiene que tener el estilo del generador y no el de Prettier. Se restauraron desde el
render.

**Traza.** ADR-066, ADR-084, ADR-085, ADR-128, ADR-133, ADR-151, ADR-152, T-08, T-09, RNF-02, Doc 2 §8,
Doc 2 §9, Doc 5 §13.

---

## ADR-154 · El estilo de ruta por defecto es el de recurso, no el que publica el estándar

**Estado:** Aceptada · 2026-11-05 · Doc 1 · revisa ADR-140

**Contexto.** **ADR-140** convirtió la forma de la ruta en punto de variación con dos valores y dejó `bian` como defecto, con el argumento de que el documento publicado de un Service Domain expone esas rutas y que servirlas hace al producto comparable con el estándar. Lo que no se midió entonces es qué recibe quien no elige: un producto derivado sin bandera sirve `POST /ConsumerLoan/Initiate`, con los segmentos capitalizados y el término de acción como último segmento.

Eso **no es la convención con la que el equipo escribe y lee URLs**. El autor lo encontró usando la herramienta, que es como aparecen estas cosas: no leyendo el modelo sino abriendo el navegador en una ruta del producto.

**Decisión.** El valor por defecto de `routeStyle` pasa a `rest`. Un producto derivado sin elegir forma sirve `POST /consumer-loans`, `GET /consumer-loans/{id}`, `POST /consumer-loans/{id}/control`.

**Qué no cambia.** El estilo `bian` sigue existiendo, sin modificaciones, bajo `--route-style bian`. ADR-140 no se revierte: la forma que el estándar publica se sigue derivando del mismo descriptor, el documento OpenAPI sigue llevando el `operationId` y los tags del estándar en las dos formas (**ADR-146**), y el anidamiento de un behavior qualifier se conserva en las dos —en forma de recurso, `GET /term-deposits/{id}/interests/{interestId}` y `POST /term-deposits/{id}/interests/{interestId}/execute`—. Lo que se revisa es cuál manda cuando nadie elige, no qué formas existen.

**Por qué el defecto y no la existencia de la forma.** Una línea de producto impone convenciones, y cada una que impone tiene que pagarse con una razón que el equipo acepte. La comparabilidad con el documento publicado es una razón válida **para quien la necesita**, y por eso la forma se conserva; pero no es la necesidad del caso común, que es un equipo construyendo un servicio con las convenciones de su organización. Un defecto que sorprende es un defecto que se cambia a mano en cada producto, y entonces la línea deja de gobernarlo.

**Había dos valores por defecto, y solo uno se veía.** Al aplicarlo apareció que `derive.ts` llevaba un `?? 'bian'` incrustado, además del `default` del modelo. El del modelo gobierna lo que la herramienta pregunta; el literal gobierna lo que toma una derivación que no pasa por la resolución de la entrada, que es como se produce el activo base. Separados, el activo habría quedado en una forma y todo producto derivado en la otra. Ahora el literal es la constante `DEFAULT_ROUTE_STYLE`, y una prueba exige que coincida con el `default` del modelo.

**Consecuencia.** El activo base se regeneró y sirve `/party-references`; su prueba del documento OpenAPI se alineó. El circuito de generación mantiene las dos formas cubiertas: el primer producto toma el defecto **sin bandera**, de modo que lo que se verifica es lo que un usuario recibe, y el segundo pasa a fijar `bian` explícitamente y se llama `deposit-bian-api`. El circuito de composición toma también el defecto, porque lo que verifica es el módulo y no la forma. Dos comprobaciones dejaron de llevar un valor escrito a mano: el estado que responde un `initiate` se lee de `route-styles.json`, y el estilo del primer producto se lee del modelo. Activo base en `0.17.0` y herramienta en `0.21.0`.

**Traza.** RF-02, RNF-02, ADR-140, ADR-146, Doc 1 §6, Doc 4 §5 de la Fase 3, P-50.

---

## ADR-155 · La herramienta sirve una sola forma de ruta, la del recurso

**Estado:** Aceptada · 2026-11-05 · Doc 1 · sustituye a ADR-140 y revisa ADR-154

**Contexto.** **ADR-140** hizo de la forma de la ruta un punto de variación con dos valores, y **ADR-154** movió el defecto a `rest` al ver que un producto sin bandera servía `POST /ConsumerLoan/Initiate`. Eso dejó el problema de fondo sin tocar: la línea mantenía **dos superficies** que verificar, documentar y narrar, y ningún equipo había pedido la segunda.

El costo de un punto de variación no es el código que lo implementa. Es que cada documento gana una columna, cada tabla de rutas se escribe dos veces, el circuito deriva un producto más, y quien adopta la herramienta tiene que decidir algo que no sabe decidir en su primera semana.

**Decisión.** La herramienta sirve **una sola forma**: la del recurso. Se retiran el punto de variación `routeStyle`, el artefacto `route-styles.json` con su esquema, y la rama `bian` de la derivación. La base de toda ruta es el agregado en plural y en kebab, el término de acción vive en el método HTTP y en el documento de la API, y una operación de behavior qualifier anida su ruta bajo el recurso de su control record.

**Por qué esto no contradice el estándar.** Porque el estándar nunca gobernó la URL en este marco: **ADR-006** fija que gobierna **el dominio** del proyecto. Y el dominio sobrevive entero, comprobado sobre un producto derivado el 2026-11-05:

| Dónde | Qué conserva del estándar |
| :---- | :---- |
| El agregado | Sale del control record del Service Domain |
| Los casos de uso y los eventos | Se nombran con el action term |
| El documento OpenAPI | `operationId` del término —`Initiate`, `RetrieveInterest`, `ExecuteInterest`— y tags de los dos niveles, `CR - TermDepositFacility` y `BQ - Interest` |
| `project.json` | `serviceDomain`, `controlRecord`, `businessDomain`, `businessArea` |

Un producto en forma de recurso sigue siendo trazable al estándar operación por operación. **La trazabilidad vivía en el documento de la API, no en la URL**, y eso es lo que vuelve barata esta decisión.

**Qué se pierde, dicho sin suavizar.** La posibilidad de comparar las URLs carácter a carácter con el documento publicado del Service Domain. Eso lo necesita quien implemente el estándar como contrato de interoperabilidad **entre entidades**; no quien construye un servicio interno, que es el caso de aplicación declarado. Si algún día hace falta, lo resuelve un gateway mapeando rutas, no el generador duplicando su superficie.

**Por qué se retira en lugar de dejarse como opción no ofrecida.** El doc 1 §5 fija que una entrada del espacio de selección existe cuando sirve a un propósito escrito. Una forma que nadie elige no es una opción: es una rama que hay que mantener verde sin que nadie la mire, y la línea ya pagó ese costo durante dos días.

**Consecuencia.** El modelo pasa de catorce puntos de variación a **trece**. `naming.ts` pierde el tipo `RouteStyle`, la lista, el defecto y el parámetro de estilo de sus cinco funciones; `routeBaseFor` recibe solo el agregado. El circuito de generación pierde el producto `deposit-bian-api` y deriva **tres**: 66, 38 y 41 archivos. El activo base no cambió, porque ya servía la forma de recurso desde ADR-154. Activo base en `0.18.0` y herramienta en `0.22.0`, 294 pruebas.

**Lo que queda por hacer fuera del código.** El **capítulo 4 de la tesis** narra la forma de la ruta como ejemplo de punto de variación, y hay que rehacer ese pasaje. Queda anotado como pendiente y no se toca aquí, porque la tesis se escribe al cerrar una fase y no al paso.

**Traza.** RF-02, RNF-02, ADR-006, ADR-140, ADR-146, ADR-154, Doc 1 §5 y §6, Doc 4 §5 de la Fase 3, P-51.

---

## ADR-161 · El producto reporta su telemetría donde la produce, a un puerto que puede no tener adaptador

**Estado:** Revisada · 2026-11-05 · Doc 2 · revisa ADR-151 y ADR-152

**Contexto.** ADR-151 dejó dicho qué le falta al activo base para que su traza sirva fuera del proceso: exportarla, muestrearla y acompañarla de métricas, todo del lado de un módulo de observabilidad. Ese módulo existe desde **ADR-156**, y recibe lo que el producto le entregue por `TelemetryPort` (**ADR-157**). Faltaba decidir **desde dónde** se lo entrega.

La pregunta no es de detalle. El producto escribe una entrada por request y una sola, por el reparto que **ADR-153** fijó: la escribe el interceptor si respondió y el filtro si falló. Un span de request que se reportara en un solo lugar perdería la mitad de las requests, y justo la mitad que importa.

**Decisión.** El producto reporta en los tres lugares donde produce telemetría, y en ningún otro:

| Dónde | Qué reporta | Por qué ahí |
| :-- | :-- | :-- |
| El adaptador del logger | Cada entrada que **escribió**, tal como la escribió | Es el único lugar por el que pasa toda entrada: las del arranque, las del dominio y las de la request. Reportar después de escribir es lo que impide que el stream y el colector digan cosas distintas |
| El interceptor | El span de la request que respondió, y su duración | Es donde una request termina bien |
| El filtro de errores | El span de la request que falló, y su duración | Es donde una request termina mal, y ya es el lugar que sabe por qué |

Lo que arma cada señal vive en una pieza propia del activo, `src/infrastructure/logging/telemetry.ts`, para que el interceptor y el filtro no la dupliquen. El puerto se inyecta **opcional** en los tres: sin módulo, no hay adaptador, y el producto responde igual.

Dos reglas quedan fijadas con su razón:

- **Lo que el nivel descartó no se exporta.** Una entrada por debajo de `LOG_LEVEL` no se escribe y tampoco se reporta. El producto no exporta lo que no está dispuesto a escribir.
- **El span de un `4xx` no dice que el servicio falló.** Una request que el llamador mandó mal no es un fallo de quien la respondió, y contarla como tal esconde las que sí lo son. Es el mismo criterio con el que ADR-153 reparte `warn` y `error`.

**Por qué las sondas también se reportan.** Dejarlas afuera escondería una sonda que se puso lenta, que es exactamente lo que hace que una plataforma reinicie un servicio sano. `http.route` las separa en cualquier consulta, igual que `debug` las separa en el log (ADR-152).

**Consecuencia.** La duración de una request sale como `http.server.request.duration` en **segundos** y con los atributos que las convenciones semánticas del estándar nombran —`http.request.method`, `http.route`, `http.response.status_code`—, y no en milisegundos como el asiento del log: el asiento lo lee una persona y la medición la agrega un backend que ya sabe leer esa unidad. Un valor del contexto que no es primitivo viaja como su texto JSON, porque el puerto lleva atributos planos y perder la cadena de causas de un error sería perder lo único que explica el fallo.

**Verificación (2026-11-05).** 98 pruebas del activo base, con la entrada reportada y la descartada, el span de un `4xx` y el de un `5xx`, y el caso sin módulo. En ejecución, el circuito de composición: el producto compuesto exportó sus entradas, los spans de sus requests y su histograma de duración a un colector, continuando la traza que el llamador mandó.

**Traza.** T-08, T-09, RNF-02, ADR-128, ADR-151, ADR-152, ADR-153, ADR-156, ADR-157, ADR-159, Doc 2 §8, Doc 2 §9, Fase 3 doc 1 C-02, Fase 3 doc 2 §12.

---

## ADR-162 · El catálogo se resuelve como un activo más; la copia instalada con la herramienta es el piso

**Estado:** Revisada · 2026-11-06 · Doc 3 / Doc 4 · revisa ADR-050 y el doc 3 §8

**Contexto.** El doc 3 §8 decidió que la herramienta declara `@bsl/catalog` como dependencia con versión
fija, y dejó escrita la salida con su condición: «la resolución dinámica se registra como punto de
extensión, **aplicable si en operación el costo de publicar pesa más que el beneficio del
determinismo**».

Ese costo se midió al ofrecer el segundo módulo. Para que `bsl add observability` funcionara con la
herramienta del feed hubo que publicar **dos** paquetes: el catálogo con la entrada en `active`, y una
versión de `@bsl/cli` cuyo **único cambio sustantivo era el número del pin**. Antes de eso, quien
instalaba la herramienta veía tres entradas y no podía incorporar un módulo ya publicado.

**Decisión.** El catálogo se resuelve en ejecución, con tres fuentes en este orden:

| Orden | Fuente | Para qué |
| :-- | :-- | :-- |
| 1 | La ruta que dé la invocación | Congelar una ejecución, y es cómo corren los dos circuitos sin feed |
| 2 | La última versión que sirve el registro, cacheada por versión | Que un activo agregado se ofrezca sin publicar la herramienta |
| 3 | La copia instalada con la herramienta | Que siga funcionando sin red, con las entradas con que se instaló |

Cuál respondió **se informa en la salida** —`Catalog 0.3.0 from the registry`—, porque una ejecución que
resuelve un conjunto de activos distinto al de la anterior tiene que poder decirlo.

**Por qué RF-05 no se toca.** RF-05 pide que dos ejecuciones con parámetros idénticos produzcan
estructuras equivalentes, y lo que determina la estructura es el **contenido** del activo base, que
sigue fijado por `asset-pins.json`. Lo que el catálogo decide es **qué activos existen**, que por
definición cambia cuando el gobierno agrega uno, y que **ya era dinámico para los módulos**: un módulo
nunca tuvo pin. La tabla del doc 3 §8 trataba las dos cosas como una sola.

**Las otras tres filas de esa tabla.** La operación sin red la resuelve el piso, y la salida lo dice. El
alcance de una entrada publicada por error lo cubren tres cosas que no existían cuando esa tabla se
escribió: una entrada nace en `proposed` (ADR-100), una `deprecated` se rechaza, y el repositorio del
catálogo tiene su revisión y su `CODEOWNERS`. El control de gobierno vive donde el marco lo pone, no en
la cadencia de publicación de la herramienta.

**Alternativas.** Un rango `^0.3.0` en lugar de la versión exacta. No funciona: en `0.x` el operador `^`
pinea la menor, así que no acepta `0.4.0` y la entrada nueva seguiría invisible. Es el mismo error de
rango que **ADR-160** registró para el contrato.

**Consecuencia.** La herramienta mantiene la dependencia con versión exacta y cambia lo que significa:
**ya no es la fuente, es el respaldo**, así que no hay que moverla cuando el catálogo gana una entrada.
Una entrada nueva cuesta desde ahora **una** publicación.

**Verificación (2026-11-06).** Contra el feed real: sin `--asset-source`, `bsl assets` informa
`Catalog 0.3.0 from the registry` y lista las cuatro entradas; la segunda ejecución informa
`from the cache` y no vuelve a bajar nada; y con el registro apuntado a una dirección inalcanzable
informa `from the copy installed with the tool` y lista lo mismo. Seis pruebas nuevas cubren las tres
fuentes, el reuso del caché y los dos rechazos.

**Traza.** RF-05, RF-10, RF-11, RF-12, RF-14, RF-15, ADR-050, ADR-100, ADR-104, ADR-120, ADR-156,
ADR-160, P-30, Doc 3 §8, Doc 4, Fase 3 doc 2 §11.

---

## ADR-163 · Lo que declara una versión de la línea que el feed no sirve no se publica

**Estado:** Aceptada · 2026-11-06 · Doc 3 / Doc 6

**Contexto.** El 2026-11-06 se publicaron `@bsl/base-template` `0.19.0` y `@bsl/cli` `0.23.0` **antes** que el `@bsl/contracts` `0.3.0` que los dos declaran. Durante ese rato el feed sirvió un artefacto que **no se podía instalar**: la plantilla publicada pedía `@bsl/contracts: ^0.3.0` y el feed servía `0.2.0`. Nada lo impidió, porque `prepublishOnly` comprueba que el paquete es válido —lint, pruebas, compilación— y no que lo que declara exista.

Es la cara operativa de **ADR-160**: en `0.x` un cambio menor del contrato obliga a mover el rango en el activo base y en cada módulo, y entonces el orden de publicación deja de ser un detalle. La regla que el episodio dejó escrita era correcta y no tenía dientes: vivía en una ficha de pendientes.

**Decisión.** Antes de publicar, cada activo publicable comprueba que **todo rango que declara sobre un paquete `@bsl/*` lo satisface algo ya publicado en el feed**. Si no, el `publish` se rechaza nombrando qué falta publicar primero. La comprobación entra en el `prepublishOnly` de los cinco activos, junto a `verify`.

Quién decide si un rango está satisfecho es el gestor de paquetes —se le pregunta por `<paquete>@<rango>`— y no una reimplementación de la semántica de rangos. Un rango que apunta a una ruta (`file:`) se omite: es desarrollo, no publicación.

**Por qué en `prepublishOnly` y no en la puerta de push.** Al empujar, el contrato legítimamente puede no estar publicado todavía: subir el código y publicar son dos actos distintos y en ese orden. La condición que importa es la del momento de publicar, y es exactamente ahí donde se comprueba.

**Por qué no basta con documentar el orden.** Ya estaba documentado, en el propio doc 3 §5, que la condición de validez «no se delega en la memoria de quien publica: se aplica automáticamente». El episodio mostró que esa frase cubría la validez del paquete y no la de sus dependencias. Esta decisión extiende la misma idea al único hueco que quedaba.

**Consecuencia.** Publicar sin red deja de ser posible, que ya no lo era: publicar necesita el feed. La comprobación añade una consulta por rango declarado, que son entre cero y dos por activo. El `package.json` de los cinco activos cambia su `prepublishOnly`, y eso no mueve ninguna versión: el script no viaja en el paquete y lo que hace no cambia para quien instala.

**Verificación (2026-11-06).** Los cinco activos pasan la comprobación con el feed de hoy, nombrando qué satisface cada rango. Comprobado rompiéndolo, como pide **ADR-126**: apuntado el rango de la plantilla a `^0.9.0`, el `publish` se rechaza con `@bsl/base-template@0.19.0 cannot be published yet: nothing in the registry satisfies what it declares on the line.` y nombra el rango; restaurado, vuelve a pasar.

**Traza.** RF-15, RNF-06, ADR-126, ADR-160, ADR-162, P-50, P-52, Doc 3 §5, Doc 6.

---

## ADR-166 · Una lista de opciones tiene principio y fin, y la acción que termina se nombra por lo que hace

**Estado:** Aceptada · 2026-11-06 · Doc 4 / Doc 5

**Contexto.** El autor usó la revisión de **ADR-145** y no pudo navegarla: bajando por la lista «da
vueltas infinitamente», y la opción que termina el comando no se entendía como tal. El adaptador
llamaba a `select` y a `checkbox` **sin configurarlos**, así que tomaba los defaults del paquete del
ecosistema: siete opciones visibles y lista circular, que su propio paginador declara como
`loop = true`. Sobre una lista más larga que la ventana eso produce un carrusel: no hay primera ni
última fila, y bajar nunca llega a ningún borde.

No es un caso de borde de la revisión. El modelo declara **trece puntos de variación**, así que la
revisión ofrece hasta quince opciones, y la pregunta de los behavior qualifiers de una capacidad ofrece
**treinta** en un solo `checkbox` (ADR-141). Las dos preguntas más densas eran las dos peor presentadas.

A eso se sumaba el nombre de la acción que cierra: `Derive it at <ruta>` empieza por el vocabulario de
la línea —*derivar*, correcto en el expediente y no lo que alguien espera leer en una terminal— y sigue
con una ruta larga que empuja el verbo fuera de la vista. La ruta ya estaba en pantalla, en el resumen
que la revisión imprime arriba.

**Decisión.** Dos cosas, en dos lugares distintos.

1. **Ninguna lista se enrolla, y se muestra entera cuando la terminal tiene lugar.** El adaptador pasa
   `loop: false` y un `pageSize` calculado: las filas de la terminal menos las que reserva la pregunta,
   con piso en las siete del default —nunca peor que antes— y un valor fijo cuando el entorno no informa
   su tamaño.
2. **La acción que termina se nombra por lo que hace.** `Derive it at <ruta>` pasa a
   `Create the project`, con la ruta como pista bajo la lista, y `What now` pasa a
   `What do you want to do`.

**Por qué en el adaptador y no en la revisión.** El defecto no es de la revisión: es de cómo se dibuja
cualquier lista. **ADR-129** ya puso la forma de la salida en el adaptador, y arreglarlo ahí corrige de
una vez **todas** las preguntas del recorrido —hasta trece según la capacidad—, incluida la de los
treinta calificadores, en lugar de parchear la pantalla donde apareció. La elección de palabras, en
cambio, pertenece a la operación, porque nombra lo que esa operación hace.

**Alternativas.** Separar las dos acciones de los trece cambios con un separador visual. Se descarta por
ahora: exigiría agregar un campo a `Choice` en `PrompterPort`, y un puerto no se cambia por
presentación. Con la lista completa y con tope la estructura ya se lee, porque cada corrección entra con
su prefijo `Change:`.

**Consecuencia.** Cambian el adaptador de preguntas y la operación de generación. Cuatro pruebas que
guionaban la pregunta por su texto quedaron actualizadas. Nada cambia fuera de una terminal. El
`pageSize` queda sin prueba unitaria, coherente con que este adaptador no tenga suite propia: es el que
posee la terminal, y lo que decide solo se observa en una.

**Verificación (2026-11-06).** `npm run verify` en verde en todo el monorepo con 354 pruebas, y
prettier limpio. La causa quedó confirmada leyendo el paginador del paquete, que declara `loop = true`
por defecto. **Falta el render**, que exige una terminal real y lo confirma el autor.

**Traza.** T-14, RNF-01, ADR-129, ADR-141, ADR-144, ADR-145, Doc 4 §5, Doc 5.

---

## ADR-169 · Una respuesta que no se acepta no termina el comando, y salir se declara en la pregunta

**Estado:** Aceptada · 2026-11-07 · Doc 1 / Doc 4

**Contexto.** El autor reportó que en `bsl new` «si se me daña algo se me sale todo». Aparecieron cuatro
defectos, los cuatro en el camino de la entrada y ninguno declarado en ningún documento:

1. **Una respuesta se validaba después de preguntarla, fuera de la pregunta.** El valor pasaba a
   `validate`, que lanzaba `UsageError` hasta la raíz de composición. Cinco de los trece puntos declaran
   patrón, así que un correo mal escrito en la pregunta doce tiraba las once anteriores. El mensaje de
   rechazo era bueno y llegaba cuando ya no servía para corregir nada.
2. **Desmarcar todas las operaciones terminaba el comando.** La restricción se evalúa al final de la
   resolución y lanza antes de que exista la revisión enmendable de ADR-145. El `minItems: 1` del modelo
   no llegaba nunca al `checkbox`.
3. **La interrupción de la terminal se reportaba como defecto de la herramienta.** Ctrl+C lanza
   `ExitPromptError`, que no es `CliError`, así que la herramienta respondía a quien cancelaba con
   `This is a defect of the tool. Report it with the command that produced it.`
4. **No había salida declarada.** La tecla de escape no hacía nada, y la única salida ordenada estaba en
   la última pantalla del recorrido.

El defecto 1 rompe **RNF-01** en su propio criterio —«cada operación se completa con un único comando»—,
que estaba contado como cumplido leyéndolo como «no hay que encadenar comandos». La lectura estricta es
la que vale.

**Decisión.** Tres cosas.

1. **La pregunta rechaza en su sitio y queda abierta.** La condición que el punto de variación declara
   viaja con la pregunta: `PrompterPort.text` recibe un `TextQuestion` con `required` y con la función
   que lee el rechazo. Lo mismo para una selección múltiple, con el mínimo que el punto declara.
2. **La regla se comprueba en un solo lugar.** `validate` se partió en `reasonToReject`, que devuelve el
   motivo, y el `validate` que lo lanza. La pregunta lee el motivo y vuelve a preguntar; la resolución lo
   lanza cuando el valor llegó por bandera o por archivo y no hay a quién preguntarle.
3. **Las dos teclas significan algo, y lo dice la pregunta.** La escape **retrocede una pregunta** y, sin
   ninguna atrás, sale; la interrupción sale directo. Las dos por `CancelledError`, que la raíz escribe
   como línea informativa con código 130.

**Por qué.** Retroceder vuelve al último punto **realmente preguntado**, no al anterior del modelo: a un
valor que vino por bandera no hay pregunta a la que volver. Se olvida todo desde ese punto en adelante,
porque una pregunta posterior puede haberse ofrecido o poblado desde una respuesta anterior. Y qué tecla
significa qué lo decide el adaptador, igual que la forma de la salida (ADR-129) y el dibujo de una lista
(ADR-166): el núcleo solo conoce el significado del paso, `SteppedBack` es una señal del puerto y no un
fallo, y `readline` ya distingue un escape solo del que abre la secuencia de una flecha.

**Alternativas.** Envolver cada pregunta en un ciclo dentro de la resolución, dejando la validación donde
estaba. Se descarta: el rechazo se dibujaría bajo una pregunta ya cerrada, con la respuesta mala en el
historial y dos preguntas iguales una debajo de otra. El prompt del ecosistema ya sabe refrescar en su
lugar, y el único motivo por el que no lo hacía era que nadie le pasaba la condición.

**Consecuencia.** El puerto de preguntas cambia de firma, que es lo primero que le cambia desde que se
escribió, y el doc 4 §5 queda retranscrito. Cambian el núcleo de la resolución, el adaptador, la raíz de
composición, la operación de generación y el doble de pruebas, que ahora honra el contrato completo.
**Nada cambia fuera de una terminal:** una corrida por banderas no pregunta y los dos circuitos corren
con `--non-interactive`.

**Verificación (2026-11-07).** Dieciséis pruebas nuevas, siete de ellas en `input-resolver.spec.ts`.
`check:push` en verde con 378 pruebas y cero vulnerabilidades. **Falta el render y la captura de la
tecla**, que exigen una terminal real y las confirma el autor: el doble cubre el significado de las dos
teclas, no su decodificación, que es la mitad que vive en la plataforma.

**Traza.** T-14, RNF-01, RNF-02, ADR-081, ADR-129, ADR-136, ADR-145, ADR-166, ADR-170, Doc 1,
Doc 4 §5, §6 y §11.

---

## ADR-170 · Lo obligatorio se dice donde se pregunta y donde se documenta

**Estado:** Aceptada · 2026-11-07 · Doc 4 / Doc 5

**Contexto.** Segundo reporte del autor sobre el mismo recorrido: no se ve qué campo es obligatorio. No
lo decía ninguna de las dos superficies.

- **En la ayuda.** `renderOperationHelp` sabe escribir `(required)`, pero `bsl new` arma sus parámetros
  desde el modelo **sin copiar el campo que lo dice**: de los once puntos obligatorios, la ayuda no
  marcaba ninguno, y los diecisiete parámetros se listaban como una sola lista plana.
- **En la pregunta.** Las trece se veían iguales. `description` y `owner` son obligatorios y no declaran
  patrón, así que `validate` no tenía nada que comprobar: Enter en vacío los aceptaba y el producto
  quedaba con descripción vacía.
- **En la invocación.** Ninguna ayuda nombraba los argumentos sin bandera. `bsl new <name>` existía solo
  dentro de la operación que lo leía, documentado en el texto del error que se queja de su ausencia, que
  lo lee únicamente quien ya se equivocó.

**Lo que había que separar primero.** `ParameterDeclaration.required` lo usa el parseo para rechazar una
invocación a la que le falta una bandera. Marcar con ese campo los once puntos del modelo habría dejado
`bsl new` inservible sin banderas: habría exigido trece antes de preguntar nada. Son dos cosas y ahora
se dicen por separado: **`required`** es que la operación no puede correr sin el valor, y **`asked`** es
que en una terminal se pregunta por él.

**Decisión.** Cinco cambios, todos de declaración.

1. **`bsl new` copia del modelo lo que ya sabía.** Cada punto obligatorio queda `required` y `asked`, y
   la ayuda escribe `(required; asked when omitted)`. Un parámetro opcional muestra su valor por defecto.
2. **Los argumentos sin bandera se declaran como dato.** `Operation` gana `positionals`, y la ayuda abre
   con su línea de invocación, con la convención del ecosistema: obligatorio entre ángulos, opcional
   entre corchetes.
3. **Los parámetros se agrupan por donde pertenecen**, usando la etapa que el modelo ya declara:
   `Capability`, `Surface`, `Project`, `Options`, y al final los propios del comando.
4. **La pregunta dice su condición.** Un punto de texto se pregunta como obligatorio u opcional; una
   selección múltiple dice su mínimo. Una simple no se marca, porque elegir de una lista cerrada siempre
   produce respuesta.
5. **Lo obligatorio se comprueba de verdad.** `reasonToReject` rechaza una respuesta vacía en un punto
   obligatorio, venga de la pregunta, de una bandera o de un archivo.

**Alternativas.** Marcarlo solo en la ayuda. Se descarta porque la ayuda es la superficie que menos se
lee de las dos: quien corre `bsl new` sin banderas nunca la ve, y es justo el caso del reporte.

**Tres hallazgos al construir.** Dos de la agrupación: la etapa `Options` del modelo chocaba con el
título que la ayuda usa para lo que no declara grupo, así que ese bloque quedaba empujado al final
—corregido indexando por grupo y no por título—; y al corregirlo, un grupo llamado `Options` más
parámetros sin grupo producía **dos bloques con el mismo título**, de modo que ahora lo sin grupo se
suma a ese bloque. El tercero: un booleano que viene en sí no se pide con su propia bandera, sino con la
que lo apaga. El parseo acepta `--no-<bandera>` desde que se escribió y ninguna ayuda lo mencionaba, así
que `--domain-events` se leía como la forma de incluir algo que ya estaba incluido.

**Consecuencia.** Cambian el contrato de operación, el parseo, la ayuda y las cinco operaciones. Las dos
ayudas cierran con ejemplos, porque la forma de un comando se lee más rápido de un caso que de la lista
de lo que acepta. Ningún requerimiento cambia de veredicto: RF-02 y RNF-01 ya estaban cumplidos y
quedan mejor sostenidos.

**Verificación (2026-11-07).** Ocho pruebas nuevas en `help.spec.ts`, la primera suite propia de la
ayuda. Los dos circuitos siguen en verde y **ninguno pasó a exigir una bandera que antes no exigía**,
que es el riesgo que la separación de `required` y `asked` tenía.

**Traza.** T-14, RF-02, RNF-01, ADR-052, ADR-081, ADR-136, ADR-169, Doc 4 §4, §6 y §12, Doc 5 §2.

---

## ADR-171 · La plantilla es un activo del catálogo que se describe a sí mismo

**Estado:** Aceptada · 2026-11-09 · el índice de la fase / Doc 3 · revisa ADR-017 y ADR-048

**Contexto.** El alcance del anteproyecto compromete el «desarrollo de un sistema de almacenamiento de
plantillas, asegurando su disponibilidad para los equipos»; el objetivo específico 2 habla de
«plantillas configurables», en plural; RF-14 y RF-15, del «catálogo de plantillas y módulos». Lo
construido tenía **una** plantilla y no tenía dónde poner una segunda: los 51 archivos `.tpl` vivían
dentro de `@bsl/cli`, el catálogo la describía como `base-asset` sin decir que era una plantilla, y la
herramienta sabía por su nombre cuál era. No es una mejora: es cerrar algo que el anteproyecto prometió
y que la Fase 2 cerró sin construir, y lo vuelve exigible el orden de ejecución, porque la Fase 4
evalúa contra los objetivos del anteproyecto y no contra los del expediente.

**Lo que el marco ya permitía, y por eso esto no rompe nada.** **ADR-017**, «una sola plantilla base
canónica», estaba **Diferida** y nunca se aceptó: su propio motivo dice que «qué es una plantilla y qué
contiene pertenece al diseño del mecanismo de derivación». Esta decisión es ese diseño, y con ella
ADR-017 pasa a **Revisada**. **MR-01 §5** dice que la superficie común «hace **viable**» una plantilla
única, que habilita y no obliga; **MR-05** define validez y propiedad **por tipo de activo, sin
cardinalidad**. Lo único que no se toca es el alcance de la familia, que MR-01 §7 declara estable: lo
que cambia es dejar de deducir «una sola plantilla» de él.

**Decisión.** Una plantilla es un activo del catálogo del mismo rango que un módulo, y **se describe a
sí misma** en un `bsl-template.json` dentro de su paquete, con su esquema al lado. Es ADR-101 aplicado
donde faltaba.

| Pieza | Qué queda |
| :---- | :---- |
| `bsl-template.json` | Identidad, contrato contra el que se construyó, forma del producto que deriva, dónde viven sus archivos, el vocabulario con que arma su scope y el catálogo de lo que el producto está hecho |
| Esquema del catálogo | Gana el tipo `template`. `contractVersion` queda **obligatorio** para un módulo, **admitido** para una plantilla y **prohibido** para el paquete del contrato, que es lo que el `if/then/else` anterior no sabía decir |
| `bsl templates list` | El almacén: identificador, paquete, versión publicada, responsable y estado |
| `bsl templates show <id>` | Lo que deriva, el contrato, la forma del producto con sus puntos y sus puertos, y cuántos archivos copia y renderiza |
| `bsl new --template <id>` | Deriva de la plantilla nombrada. Con dos o más ofrecidas la herramienta **se niega a adivinar** |

**Por qué el manifiesto en el paquete y no en el catálogo.** El argumento de ADR-101, palabra por
palabra: lo que la plantilla declara de sí misma cambia con ella, y ponerlo en el catálogo obligaría a
cambiar dos repositorios de forma coordinada. Una desincronización dejaría a la herramienta derivando
con el catálogo de archivos de otra versión.

**Alternativas.** Dejarla como un `base-asset` más y resolver la pluralidad con un segundo
`base-asset`. Se descarta porque no resuelve nada: los archivos seguirían en la herramienta, el
catálogo de lo que el producto está hecho seguiría siendo código, y una plantilla de otro equipo
seguiría costando una versión de `@bsl/cli`.

**Consecuencia.** El catálogo deja de describir un activo base y pasa a describir **un almacén**. El día
que un equipo publique su plantilla, aparece en `bsl templates list` **sin una versión de la
herramienta** (RF-14, RF-16). RF-05 no se toca: lo que determina la estructura de un producto sigue
siendo el contenido del activo, fijado en `asset-pins.json`. El cambio de tipo cuesta publicar el
catálogo y **no** una versión de la herramienta, que es la propiedad que **ADR-162** persigue: el piso
instalado queda en `0.3.0` y no rompe nada porque `templateEntries` lee los dos tipos durante todo
`0.x`, la cláusula escrita para este tránsito.

**Un hallazgo propio.** El manifiesto se llamaba a sí mismo `bian-sync-api` y su entrada del catálogo
`base-template`. Para un módulo la herramienta rechaza exactamente eso desde que se escribió; para una
plantilla nadie lo miraba. Ahora lo mira, con la misma comprobación, al derivar y al mostrar.

**Verificación (2026-11-09).** `bsl templates list` y `bsl templates show` corridos en terminal real
contra el catálogo del repositorio; `bsl new --template base-template` deriva el producto de referencia
y `verify:generation` los tres productos de la fase. Once pruebas nuevas, dos para la comprobación de
identificadores y nueve para la elección de plantilla y el rechazo a adivinar.

**Traza.** Alcance del anteproyecto, OE2, RF-01, RF-02, RF-05, RF-14, RF-15, RF-16, ADR-002, ADR-017,
ADR-035, ADR-048, ADR-101, ADR-162, MR-01 §5, MR-05 §1, MR-01 §7, el índice de la fase, Doc 3 §6 y §7.

---

## ADR-172 · Las plantillas viven en el activo que las usa, no en la herramienta

**Estado:** Aceptada · 2026-11-09 · Doc 5 · sustituye la parte de ubicación de ADR-065

**Contexto.** **ADR-065** puso los archivos `.tpl` bajo `src/operations/generate/templates/` con un argumento correcto para lo que entonces se sabía: «las plantillas pertenecen al mecanismo de derivación, no al producto, por lo que viven con la herramienta, igual que el modelo de variabilidad». El argumento se cae en cuanto hay más de una plantilla: pertenecen al mecanismo, sí, pero **a una plantilla del mecanismo**, y no al programa que las interpreta. Con 51 archivos dentro de `@bsl/cli`, una plantilla de otro equipo no tenía dónde vivir y una versión de la plantilla costaba una versión de la herramienta.

**Decisión.** Los archivos de una plantilla viven en el paquete de esa plantilla, y el manifiesto dice dónde: `files.assetRoot` es el directorio de lo que el producto recibe tal cual, y `files.templates` el de lo que se renderiza. Los 29 archivos `.tpl` que quedan pasaron a `packages/base-template/templates/`, y `@bsl/cli` dejó de distribuirlos: su `files` del `package.json` quedó en `bin` y `dist`, y el de la plantilla ganó `bsl-template.json`, `bsl-template.schema.json` y `templates`.

**Por qué 29 y no 51.** No es esta decisión: es ADR-173, que colapsó 22 fragmentos en los bloques de la plantilla que los usaba. Se dicen juntos porque se construyeron juntos, pero son dos cosas: una es dónde viven y la otra cuántos son.

**Consecuencia.** La dependencia de dirección queda como el marco la pide: la herramienta depende del contrato del manifiesto, y la plantilla de nada de la herramienta. Lo que ADR-065 declaraba como consecuencia asumida —«existen dos fuentes del mismo código, el agregado del activo y las plantillas»— **sigue existiendo y sigue verificándose igual**: las dos fuentes están ahora en el mismo paquete, que es lo único que mejora. `reference-aggregate.spec.ts` se conservó a través de toda la reescritura y es lo que sostiene que cada paso produjo el mismo producto byte a byte.

**Un cambio deliberado de bytes.** `src/infrastructure/http/openapi.ts` del activo base pasó de 147 a 161 líneas. El documento OpenAPI dejó de imprimirse desde código y pasó a ser texto en `openapi.ts.tpl` (ADR-174), lo que cambia el formato del archivo sin cambiar el documento que sirve. Fue posible porque `.prettierignore` ya excluía ese archivo; el activo se regeneró y el oráculo volvió a pasar.

**Un hallazgo al empaquetar.** El manifiesto **no se estaba publicando**: el `files` del `package.json` de la plantilla seguía listando solo lo de antes, así que el tarball salía sin `bsl-template.json` y una instalación desde el feed no habría podido derivar nada. Lo encontró el punto 5 de la lista de verificación del estándar de código, `npm pack --dry-run`, y no lo habría encontrado ninguna prueba: las dos corren contra el directorio del repositorio.

**Traza.** RF-02, RF-14, ADR-050, ADR-065, ADR-066, ADR-171, Doc 5 §3 a §8.

---

## ADR-173 · Motor con gramática cerrada: condición y repetición sin evaluar código

**Estado:** Aceptada · 2026-11-09 · Doc 5 · revisa la parte de motor de ADR-065

**Contexto.** **ADR-065** eligió un motor sin condicionales ni bucles, con una justificación que era verdadera: «un motor sin lógica mantiene todas las decisiones en el código de la operación, de modo que leer las plantillas no es necesario para saber qué genera la herramienta». El precio estaba a la vista en el conteo: lo opcional se resolvía **eligiendo qué archivo renderizar** —siete plantillas de método de controlador, siete de caso de humo, once de caso de uso— y lo repetido **componiendo fragmentos en el código de la operación**, que es la razón por la que `derive.ts` llegó a 919 líneas. Con las plantillas fuera de la herramienta ese precio deja de ser pagable: una plantilla que no puede decir «esto va solo si el producto publica eventos» obliga a que la herramienta lo sepa, y entonces la herramienta conoce la plantilla.

**Decisión.** Tres construcciones más, y ninguna más que esas tres:

```
{{nombre}}  {{nombre|transform}}
{{#when <expresión>}} … {{:else}} … {{/when}}
{{#each <lista>}} … {{/each}}        {{#each <lista> between="\n\n"}} … {{/each}}
```

- **La condición se lee con el evaluador que ya existía.** `core/input/rule-evaluator.ts` es una gramática cerrada desde la Fase 2 —identificador, `!`, `.length <op> n`, `.some(x => x.f)`, implicación—, validada en `verify:artifacts` y **sin `eval`**. Entró con cuatro formas más: igualdad y desigualdad contra un literal, igualdad entre dos nombres, `some` con igualdad, e `includes`. Una condición dentro de una plantilla la lee **el mismo evaluador** que lee una restricción del modelo, así que no existe una segunda gramática.
- **Los transforms son un vocabulario cerrado** de doce nombres: `pascal camel kebab words snake upperSnake title plural lowerFirst compact tsLiteral`. Un nombre que no está en esa tabla es un `TemplateSyntaxError`, que es un defecto de la plantilla y aparece en la verificación del activo que la posee.
- **El cuerpo de un `each` aplana el ítem sobre el scope padre.** Es exactamente lo que el contexto de una operación ya producía, y es lo que permitió que los 22 fragmentos se volvieran bloques dentro de la plantilla que los usaba **sin renombrar un solo marcador**.
- **`between` en vez de `@first`/`@last`.** Los únicos usos reales eran separadores, y no introduce estado.

**La propiedad que ADR-065 protegía se reemplaza por una más fuerte.** No es ya «las plantillas no deciden nada», que con una sola plantilla era sostenible y con dos no. Es: **todo lo que una plantilla puede decidir está enumerado** —en el esquema del manifiesto, en esas tres construcciones y en esas dos tablas— y `--dry-run` sigue mostrando el plan entero, porque la evaluación ocurre al construir el plan y no al escribirlo.

**Por qué esta sintaxis y no otra.** El `TOKEN` que ADR-065 escribió **no reconoce `#`**, así que ninguna plantilla existente contenía un bloque por accidente: no hubo que cambiar un marcador, ni en los 29 `.tpl` ni en los `{{aggregateKebab}}` de los dos `bsl-module.json`. La migración fue cortar y pegar, verificable paso a paso contra el oráculo de bytes.

**Efecto medido.** 51 archivos `.tpl` pasaron a **29**: los siete métodos de controlador a uno, los siete casos de humo a uno, los once casos de uso a los que quedan, los tres proveedores de la aplicación a uno y los seis métodos de repositorio a tres. `derive.ts` bajó de 919 a 586 líneas, y lo que la plantilla no puede decir quedó en 203 líneas de intérprete (ADR-175).

**Tres hallazgos de semántica, al escribir las pruebas.** El primero fue mío y no del motor: una etiqueta sola en su línea se lleva esa línea, **y el cuerpo conserva el salto de línea que termina su última línea**, así que `between="\n"` producía líneas en blanco. El motor tenía razón y mis expectativas no; la semántica quedó documentada y fijada con una prueba. El segundo: `title` en esta línea capitaliza solo la primera palabra —`Term deposit`, que es como el producto lo escribe en su README y en su log—, y mi transform capitalizaba todas; se alineó al significado del proyecto en vez de agregar un nombre casi duplicado. El tercero: al admitir comparación entre dos nombres, `x == true` sin comillas habría devuelto `false` en silencio; `true` y `false` sin comillas ahora levantan `RuleSyntaxError`.

**Traza.** RF-02, ADR-065, ADR-066, ADR-081, ADR-172, ADR-175, Doc 1 §4, Doc 5 §3 a §8.

---

## ADR-174 · Lo que no es expresable como dato, y dónde queda

**Estado:** Aceptada · 2026-11-09 · Doc 5 / Doc 7

**Contexto.** Si una plantilla declara lo que el producto está hecho de, hay que decir **hasta dónde**. Sin esa frontera escrita, el manifiesto crece hasta volverse un lenguaje de programación en JSON, que es la forma conocida de llegar a lo que ADR-101 prohibió para un módulo: código del activo corriendo dentro de la herramienta.

**Decisión.** La frontera es esta lista, y es cerrada.

| No expresable como dato | Dónde queda, y por qué |
| :---- | :---- |
| `toPascalCase`, `toKebabCase`, `pluralize` con sus terminaciones irregulares | Es morfología del idioma, no variabilidad del producto. Queda en `core/input/naming.ts` y se expone como el vocabulario cerrado de transforms de ADR-173 |
| Cirugía JSON sobre `package.json` | Preserva la única fuente de las versiones de dependencias, que es lo que ADR-065 protegía. Queda como una clase del catálogo —`json`, con `set` y `unset`— y el `parse`/`stringify` lo hace la herramienta |
| Unión con deduplicación y orden | Queda como la primitiva `derived` del vocabulario, con `collect`, `with`, `plusWhen`, `unique`, `sort`, `prefix` y `join` |
| Elegir el primer ítem que cumple una condición | Primitiva `pick`, con `where` sobre la misma gramática |
| Reagrupar una lista por una clave de sus ítems | Primitiva `group`. **No es opcional:** el documento OpenAPI tiene un objeto `paths` donde dos operaciones comparten ruta, y un `each` sobre operaciones habría escrito la clave dos veces y **perdido operaciones** |
| Declarar una lista cuyos ítems dependen de lo elegido | Primitiva `lists`, con `when` por ítem |
| Huellas `sha256`, reloj, `git init`, `npm install`, respaldo, preguntas, registro, catálogo, códigos de salida | Son el mecanismo y no el producto. Quedan en la herramienta |

**Dos cosas se eliminaron en vez de expresarse.**

- **El formato por ancho de línea.** `platformFor` escribía los proveedores de la plataforma en una línea cuando cabía en cien columnas y en varias cuando no. No es variabilidad: es formato, y el producto ya tiene `prettier --check` en su propia verificación. La plantilla escribe siempre la forma multilínea. **Costo asumido y deliberado: cambian los bytes de `src/platform.module.ts` en todo producto derivado.**
- **El impresor de literales del documento OpenAPI.** `openapi.ts` eran 334 líneas que armaban un documento imprimiendo literales de TypeScript desde estructuras de datos. El documento pasa a ser texto en `openapi.ts.tpl`, que es lo que es. Sobrevive una sola pieza, `stringLiteral`, como el transform `|tsLiteral`, porque una plantilla tiene que poder meter texto que alguien escribió dentro de un literal sin romper el archivo.

**Lo que no se eliminó, contra lo que esta ronda había planeado.** `operations/generate/naming.ts` **sigue existiendo**, con sus 229 líneas: son los nombres que el estándar BIAN impone sobre una operación —su término de acción, su ruta, su método HTTP, su evento— y son el último trozo de lógica del estándar que queda dentro de la herramienta. Mover eso al vocabulario del manifiesto exige transforms encadenados, que el motor de hoy no tiene. Queda declarado como punto de extensión y no como limitación, con su pendiente.

**Traza.** RF-02, ADR-065, ADR-101, ADR-146, ADR-173, ADR-175, Doc 5 §3, Doc 7.

---

## ADR-175 · La derivación es un intérprete del manifiesto, sin estándar ni framework dentro

**Estado:** Aceptada · 2026-11-09 · Doc 5 / Doc 7 · consecuencia de ADR-171 y ADR-172

**Contexto.** `derive.ts` tenía 919 líneas y **era** el catálogo de archivos del producto escrito en código: dos tablas de archivos copiados, la convención `<paquete>/template/` como literal, unas cuarenta y cinco inserciones de cambios al plan, los nombres de NestJS, los decoradores, los textos de estado, el tiempo pasado de los verbos y la composición de 29 fragmentos. Mientras eso fuera código, una plantilla de otra familia era otra versión de la herramienta.

**Decisión.** Entra `operations/generate/interpret.ts`, de 203 líneas, con una firma que **no nombra ningún framework, ningún estándar y ninguna carpeta de un producto**:

```ts
export async function interpret(request: InterpretRequest): Promise<ChangePlan>;
```

Hace tres cosas y nada más: aplica el vocabulario que el manifiesto declara, recorre el catálogo —copiar, reescribir campos de un JSON, renderizar— y produce un plan. El orden del vocabulario es el que las cuatro primitivas necesitan: una lista se declara primero, un grupo lee una lista, un pliegue lee cualquiera de las dos, y un ítem se elige al final para que todo contra lo que pueda comparar ya esté ahí.

`derive.ts` queda en 586 líneas y hace **una** cosa: armar el scope desde la entrada resuelta —las operaciones elegidas, los nombres del estándar, la capacidad— y llamar al intérprete. Eso es lo que todavía es de este estándar y de esta familia, y es donde vive el pendiente de ADR-174.

**Lo único que el intérprete agrega al scope por su cuenta** es la forma del producto que el manifiesto declara (ADR-176), y no es variabilidad: es la plantilla diciendo qué hace, que todo producto tiene que llevar porque la compatibilidad de un módulo se decide contra el producto y nunca contra la plantilla que lo derivó.

**La propiedad de seguridad de la migración.** `reference-aggregate.spec.ts` —la prueba que ADR-066 escribió para vigilar que el activo base y las plantillas no se separen— **se conservó a través de toda la reescritura y se usó como oráculo de cada paso**. Cada colapso de familia de plantillas y el cambio al intérprete produjeron productos idénticos byte a byte: 68, 40 y 43 archivos. El único cambio deliberado de bytes fue el de ADR-172.

**Dos errores al reescribir, los dos atrapados por el oráculo o por el compilador.** Un script recortó `derive.ts` por la mitad porque el corte se apoyó en texto y no en anclas precisas; se restauró con `git checkout` y se rehízo. Otro borró la llave de cierre de una interfaz y una tabla vecina, porque el bloque `/**` que precedía al recorte pertenecía a la declaración de al lado; lo atraparon `tsc` y el lint en el acto.

**Y un error de método que conviene dejar escrito.** La tabla de términos de acción del plan aprobado para esta ronda estaba **mal en tres de sus cinco filas**. El código real enruta `Retrieve` a `GET`, **`Update` a `PATCH`** y todo lo demás a `POST`; transcribir la tabla del plan habría cambiado el método HTTP de toda ruta de todo producto. Lo encontró una prueba nueva sobre dos operaciones que comparten ruta. Un plan es una propuesta, y el código es la fuente.

**Traza.** RF-02, RF-05, ADR-065, ADR-066, ADR-146, ADR-171, ADR-172, ADR-173, ADR-174, Doc 5, Doc 7.

---

## ADR-176 · La forma del producto es un contrato declarado y comprobable

**Estado:** Aceptada · 2026-11-09 · Doc 7 · revisa ADR-102

**Contexto.** **ADR-102** fijó los puntos de inserción del producto y los describió en prosa; hoy son ocho, después de ADR-130 y de la ronda del segundo módulo. La herramienta los conocía como **constantes de su propio código**: `PRODUCT_FILES` daba el archivo, `MARKERS` el nombre de la marca y una tabla `COMMENT` decidía el estilo de comentario **por ruta literal del archivo**. Con eso, una plantilla que pusiera su punto de composición en otro archivo era inservible, y el supuesto que ADR-102 dejaba implícito —«el producto derivó del activo base que escribió esas marcas»— no lo comprobaba nadie.

**Decisión.** La forma de un producto es un dato con nombre y versión, declarada en tres lugares que se comparan entre sí:

| Quién | Dónde | Qué dice |
| :---- | :---- | :---- |
| La plantilla | `productShape` de su `bsl-template.json` | Qué forma derivan sus productos: sus puntos de inserción con archivo, clase y estilo de comentario; sus puertos con quién los liga y si un módulo puede reemplazarlos; y lo que la forma supone del producto |
| El producto | `shape` de su `project.json` | **La misma forma, copiada al derivar.** Es lo que permite decidir la compatibilidad de un módulo sin leer la plantilla que lo derivó, que puede no estar instalada ni existir |
| El módulo | `serves` de su `bsl-module.json` | A qué formas sirve (ADR-180) |

La forma de esta línea es `nestjs-hexagonal@1`: cuatro marcas —`bsl:module-imports`, `bsl:modules`, `bsl:module-config`, `bsl:module-env`, cada una con el rol que cumple en la composición— y cuatro regiones —`bsl:repository-import`, `bsl:repository-binding`, `bsl:persistence` y `bsl:telemetry`—, con los puertos `DATABASE_PORT`, ligado por la plantilla en `bsl:repository-binding`, y `TELEMETRY_PORT`, que **ninguna ligadura del activo base satisface** (ADR-157) y que el producto inyecta opcional.

**Los supuestos tácitos quedan repartidos.** Siete pasan a `insertionPoints` con su archivo, su clase y su comentario, y dejan de decidirse por ruta literal. Cuatro pasan a `requires`, declarados como hechos: `npm-package-manifest`, `project-record-1.0`, `single-aggregate` y `zod-config-schema`, que `bsl templates show` imprime. Y el que nadie comprobaba pasa a comprobable por partida doble: la composición rechaza un módulo que reemplaza una región **que la forma del producto no declara**, y rechaza un producto al que le falta un punto que su propia forma declara.

**La cláusula de lectura, con su fecha y su fin.** Un registro sin `shape` se lee como `nestjs-hexagonal@1`, porque hasta esta ronda existía **una** forma y todo producto derivado la tenía. Es una cláusula fechada y no un valor por defecto: una segunda forma vuelve ambiguo el silencio, y por eso todo producto derivado desde aquí la escribe. Se retira en `1.0.0`.

**Lo que esa duplicación cuesta, y cómo se paga.** La forma implícita vive en el código de la herramienta **y** en el manifiesto de la plantilla, y las dos tienen que decir lo mismo. Una prueba las compara: lee `bsl-template.json` del paquete de la plantilla y exige igualdad con la constante. Sin esa comparación la cláusula valdría lo que vale una esperanza.

**Lo que no cambia.** `schemaVersion` del registro **no sube**: `shape` es un campo agregado, y el registro ya tolera campos agregados para `aggregate` y `derivation`. Lo que sí tuvo que cambiar es cómo se compara esa versión, que es ADR-177.

**Traza.** RF-06, RF-07, RF-14, ADR-057, ADR-101, ADR-102, ADR-130, ADR-157, ADR-171, ADR-180, MR-04 §4, Doc 7, Doc 2 §6 de la Fase 3.

---

## ADR-177 · El esquema del registro de un producto se compara por versión mayor

**Estado:** Aceptada · 2026-11-09 · Doc 4 · corrige un defecto latente

**Contexto.** Al agregar `shape` al registro apareció algo que no tenía que ver con esta ronda. `project-context.ts` comparaba `record.schemaVersion !== SUPPORTED_SCHEMA` **por igualdad exacta**, mientras el propio TSDoc del registro decía, en prosa y dos veces, que subir la versión por un campo agregado «haría ilegible a todo producto derivado hasta ahora, sin ganancia». Las dos cosas no pueden ser verdad a la vez. No mordía todavía porque nadie había subido el número; el día que alguien escribiera `1.1` por un campo nuevo, **todo producto derivado hasta entonces habría quedado ilegible**, con un mensaje sobre un esquema que no se lee.

**Decisión.** La comparación es por versión mayor, en los tres lectores que la hacían: el registro del producto, el manifiesto de un módulo y el manifiesto de una plantilla. Una mayor distinta significa que el archivo dice **algo distinto**; una menor mayor significa que dice **más**, y más se lee.

**Consecuencia.** El registro queda en `1.0` con `shape` dentro, y el manifiesto de un módulo pasa a `1.1` con `serves` y `composition` (ADR-180, ADR-181) **sin dejar de leer** los dos manifiestos `1.0` que están publicados. Entra con tres pruebas: una menor posterior se lee, una mayor distinta se rechaza nombrando las dos, y un registro con `shape` se lee completo.

**Por qué esto es un ADR y no una corrección silenciosa.** Porque cambia qué acepta la herramienta, y porque la razón por la que el defecto existió está escrita: la prosa del registro decía la regla correcta y nadie la comparó con el código que la aplicaba. Es el mismo tipo de hallazgo que ADR-169 dejó registrado —una condición declarada en un lugar y comprobada en otro— y el expediente gana más teniéndolo escrito que teniéndolo arreglado.

**Traza.** RF-12, RF-13, ADR-057, ADR-176, ADR-180, Doc 4 §8.

---

## ADR-178 · Los comandos se agrupan, y los nombres publicados quedan como alias

**Estado:** Aceptada · 2026-11-09 · Doc 4 / `packages/cli/TUTORIAL.md` · cierra P-59

**Contexto.** El autor reportó la superficie de comandos como «confusa y poco útil», con tres quejas concretas: `bsl assets` no dice qué hace, para ver los módulos de un producto hay que correr `bsl status` que tampoco es diciente, y `bsl update` se leía como actualizar el proyecto y no un módulo de él. La superficie era `new · add · update · status · assets`: cinco comandos sin ninguna relación visible entre ellos, donde tres son operaciones sobre los módulos de un producto y uno es un diagnóstico del entorno.

**Decisión.** La superficie se agrupa por el sujeto sobre el que cada comando actúa:

```
new · templates list|show · modules list|add|update|remove · status
```

`runner.ts` pasa a buscar **el nombre más largo que los tokens iniciales deletrean**, así una operación puede llamarse `modules add` sin tocar la interfaz `Operation` ni la resolución de entrada. La primera palabra sola de un grupo contesta con los comandos que el grupo tiene, en vez de leerse como un comando desconocido: un comando a medio escribir no es un error de quien escribe.

**Lo que se hace con los nombres ya publicados.** `bsl add`, `bsl update` y `bsl assets` **siguen funcionando en todo `0.x`** y se retiran en `1.0.0`. Un comando publicado no se puede renombrar sin más: alguien lo tiene escrito en un script. `Operation` gana un campo que declara qué comando lo reemplazó, y con eso la ayuda describe **una** superficie: los tres quedan listados aparte, al lado del comando que los reemplaza, en vez de mezclados entre los comandos —donde describirían dos superficies— o en ninguna parte, donde quien los tiene en un script no tendría cómo averiguar en qué se convirtieron.

Hay dos razones distintas para estar en esa lista, y se tratan distinto. `add` y `update` son **renombres**: el trabajo es el mismo y solo se movió el nombre, así que el alias delega y escribe una línea en el stream de error diciendo cómo se llama ahora. `assets` **no es un renombre**: sus dos mitades útiles las tomaron `templates list` y `modules list`, cada una diciendo algo que ese listado nunca dijo, y lo que queda —resolver un activo a un directorio— es un diagnóstico del entorno que no tiene otro lugar donde pedirse. No dice nada al correr, porque el comando nuevo no es el mismo comando.

**`bsl modules list`, que es el comando que no existía.** Contesta la pregunta que hacía falta dos comandos y una comparación a mano: qué puede tomar este producto y qué tiene ya. `bsl assets` listaba el catálogo sin conocer ningún producto; `bsl status` listaba los módulos de un producto sin conocer el catálogo; **ninguno de los dos decía si un módulo cabe**, que es lo que necesita quien decide. Corrido fuera de un producto lista el catálogo solo, porque el catálogo no depende de dónde se invocó.

**`bsl status` conserva su nombre.** No es una operación sobre módulos: es lo que el producto es y en qué estado está. Lo que ganó es la respuesta a «qué es este producto»: de qué plantilla se derivó, qué forma tiene y qué clase de módulo acepta.

**Qué queda fuera, y quién lo decide.** El reporte del autor incluía quitar un módulo, que **ningún requerimiento pide**: RF-06 a RF-13 cubren incorporar, consultar y actualizar. Construirlo es ampliar el alcance de la línea, y esa decisión es del autor; la tomó, y está en ADR-183.

**Traza.** T-14, RF-14, RF-16, RNF-01, ADR-052, ADR-129, ADR-170, P-59, Doc 4 §5, `packages/cli/TUTORIAL.md`.

---

## ADR-179 · Una plantilla de otra familia como evidencia de que el intérprete es genérico

**Estado:** Aceptada · 2026-11-09 · Doc 6 / Doc 7

**Contexto.** Todo lo que esta ronda afirma descansa en una sola proposición: que lo que queda en la herramienta es un **mecanismo** y no la descripción de un ejemplo. Con una sola plantilla en el repositorio esa proposición no es comprobable: un intérprete que solo ha interpretado su propio caso y una función escrita para ese caso se comportan igual.

**Decisión.** Entra una segunda plantilla **como fixture de prueba**, en `packages/cli/test/fixtures/batch-pipeline/`, de una familia que la herramienta no conoce: un trabajo por lotes agendado, en Python, con comentarios `#`, forma de producto `python-batch@3`, un puerto `SINK_PORT` y un contrato que **no es** el de esta línea. Once pruebas derivan un producto de ella y recorren las cuatro primitivas del vocabulario, la condición, la repetición por lista, la repetición por grupo, el ítem elegido, la reescritura de un JSON del activo, los archivos copiados y la forma del producto escrita en su propio registro.

**Por qué un fixture y no una plantilla publicada.** Las dos dan la misma evidencia **sobre el mecanismo**, y solo una de las dos revierte una exclusión de alcance. El el índice de la fase de esta fase excluyó deliberadamente un segundo activo del alcance de la Fase 2 y lo declaró como punto de extensión; publicar una segunda plantilla sería revertir esa exclusión, lo que es una decisión del autor sobre el alcance del proyecto y no una consecuencia de esta ronda. El fixture prueba que el mecanismo es genérico sin tocar lo publicado, y deja la decisión de alcance donde corresponde.

**Lo que el fixture no prueba.** No prueba que una plantilla de otro equipo pase la verificación de su propio paquete, ni que se publique bien, ni que un módulo de otra forma se incorpore a un producto de ella. La primera y la segunda son las mismas comprobaciones que esta plantilla ya pasa; la tercera queda cubierta por el rechazo de ADR-180, que se comprueba en el circuito rompiéndolo.

**Traza.** RF-02, RF-14, ADR-171, ADR-173, ADR-174, ADR-175, el índice de la fase, Doc 6 §4, Doc 7.

---

## ADR-192 · Las plantillas viven juntas, con una convención de nombres y un procedimiento para agregar una

**Estado:** Aceptada · 2026-11-09 · Doc 7 · completa ADR-171 y ADR-172

**Contexto.** **ADR-171** abrió el almacén y **ADR-172** sacó los archivos de una plantilla de la herramienta, pero ninguna de las dos dijo **dónde** vive una plantilla en el repositorio ni cómo se llama. Con una sola, la pregunta no existía: vivía en `packages/base-template` y se llamaba como el concepto que entonces era, *el activo base*. Con dos, la estructura empezó a mentir en tres cosas a la vez:

- `packages/base-template` y `packages/templates/azure-functions-api` son dos plantillas en dos lugares sin relación visible, y un equipo que busca «las plantillas» no encuentra un lugar.
- El nombre `base-template` dice **el papel que tenía** —ser la única— y no **qué deriva**. Al lado de `azure-functions-api` se lee como si una fuera la base de la otra, que es falso: son hermanas.
- El validador de manifiesto vivía dentro de la plantilla, así que la segunda tendría que copiarlo, y un chequeo que cada plantilla copia es un chequeo que se desincroniza: el día que una gane una regla, las otras siguen pasando sin ella.

**Decisión.** Cuatro cosas, y las cuatro son de organización y no de mecanismo.

**1. Un solo lugar.** Toda plantilla vive bajo `packages/templates/`, una carpeta por plantilla, igual que los módulos bajo `packages/modules/`. El workspace `packages/templates/*` entra a la raíz.

**2. El nombre dice qué deriva.** `@bsl/base-template` pasa a **`@bsl/nestjs-hexagonal-api`**, con su carpeta, su entrada del catálogo y su scope de commit renombrados. La convención queda escrita:

| Cosa | Cómo se nombra | Ejemplo |
| :---- | :---- | :---- |
| Carpeta | Como su entrada del catálogo | `azure-functions-api` |
| Paquete | `@bsl/` más ese identificador | `@bsl/azure-functions-api` |
| Identificador | `<stack-o-host>-<tipo>`, en kebab-case | `nestjs-hexagonal-api` |
| Forma del producto | `<stack-o-host>-<estilo>`, con versión entera | `nestjs-hexagonal@1` |

**3. El validador de manifiesto es uno y es compartido**, en `scripts/validate-template-manifest.mjs`. Toma el directorio de trabajo como el paquete a validar, así que cada plantilla lo corre desde su propio `verify`.

**4. El procedimiento de agregar una plantilla se escribe donde un equipo lo va a encontrar**, que es `packages/templates/README.md`: el índice del almacén, la convención, los seis pasos, qué le da el scope a una plantilla y **qué no le da hoy**, con el pendiente que lo sigue. Eso último es lo que lo hace útil: un equipo que no sabe qué no puede hacer descubre el límite a mitad del trabajo.

**Por qué renombrar un paquete publicado, que no es gratis.** `@bsl/base-template` está publicado en `0.21.0`, así que el renombre es una **primera publicación** de `@bsl/nestjs-hexagonal-api` y el paquete anterior queda en el feed sin recibir versiones nuevas. Se acepta porque el costo es de una vez y el nombre viejo iba a mentir para siempre; porque ningún producto derivado se rompe —el registro de un producto guarda el nombre con que fue derivado, que es dato histórico y nada lo lee para decidir—; y porque era **P-60**, ya declarado como lo que había que hacer de una vez cuando se decidiera.

**Lo que el renombre descubrió, y vale la pena por sí solo.** Al mover la carpeta fallaron cuatro rutas que se calculaban por posición relativa y que ninguna prueba cubría: el `contractsDir` del script de verificación de la plantilla, sus dos rutas a `scripts/` de la raíz, el `assetDir` de los dos circuitos, y las rutas de tres pruebas y un doble. Las atrapó `check:push` una por una, lo que dice dos cosas: que la puerta vale, y que **una ruta relativa por posición es una dependencia que nadie declara**. Quedan como están, porque convertirlas en resolución por nombre de workspace es trabajo de otra ronda.

**Traza.** RF-14, RF-16, RNF-01, ADR-035, ADR-171, ADR-172, ADR-191, ADR-194, MR-05 §1, P-60, Doc 3 §7, Doc 7 §3 y §8.

---

## ADR-193 · El producto registra la plantilla que lo derivó, y no un literal

**Estado:** Aceptada · 2026-11-09 · Doc 2 / Doc 7 · corrige un defecto de ADR-171

**Contexto.** El registro de todo producto declara los activos que incorporó, que es lo que **RF-10** exige y lo que **ADR-040** fijó. La plantilla del registro lo escribía así:

```json
{ "name": "@bsl/base-template", "version": "{{baseTemplateVersion}}", "role": "base" }
```

El nombre es un **literal**. Mientras la línea tuvo una plantilla fue verdad por casualidad; el día que tuvo dos, **todo producto afirmaba venir de la misma**, cualquiera fuera la que lo derivó. El scope no tenía marcador para el paquete de la plantilla: tenía `baseTemplateVersion`, que llevaba la versión del activo resuelto con un nombre que ya nombraba al papel y no a la cosa.

Es un defecto de **ADR-171**: esa decisión abrió el almacén y no revisó qué escribía el registro sobre la procedencia. Lo encontré al escribir la segunda plantilla, que es el momento en que un literal de este tipo se vuelve visible.

**Decisión.** La procedencia la escribe la plantilla **desde el manifiesto**. El scope gana dos marcadores, y los dos salen de lo que el intérprete ya tenía en la mano:

| Marcador | De dónde sale |
| :---- | :---- |
| `templatePackage` | El `package` del `bsl-template.json` de la plantilla resuelta |
| `templateVersion` | La versión del activo resuelto, igual que `baseTemplateVersion` |

`baseTemplateVersion` se conserva durante `0.x` como alias, porque es un marcador que una plantilla de otro equipo pudo haber usado, y se retira en `1.0.0` con las demás cláusulas de lectura. Y el `role` del activo pasa de `base` a **`template`**, que es lo que es; el lector lo acepta desde que se escribió, porque `status` compara contra los dos valores.

**Lo que esto hace comprobable.** La verificación de una plantilla ahora exige que el producto que deriva **registre ese paquete y esa forma**: si el manifiesto dice una cosa y el registro otra, la puerta falla. Sin eso, un módulo podría comparar su `serves` contra la forma de un producto cuya procedencia es falsa.

**Completado el 2026-11-09, después de ADR-196.** Un `grep` de `base-template` sobre `Codigo/` encontró que los **tres archivos de identidad del producto de referencia** —`template/package.json`, `template/README.md` y `template/project.json`— seguían nombrando `@bsl/base-template`, que es exactamente la afirmación falsa que esta decisión corrigió en todo producto derivado. La razón de que nada lo viera es la misma que vuelve el caso instructivo: **son los tres archivos que `reference-aggregate.spec.ts` excluye a propósito** de la comparación byte a byte, porque son la identidad privada del activo y no la de un producto, y el oráculo que vigila todo lo demás no los mira. Quedaron en `bsl-nestjs-hexagonal-api` / `@bsl/nestjs-hexagonal-api`, y `npx jest reference-aggregate` sigue en verde, que es lo que prueba que el renombre no mueve un byte de lo comparado. En el mismo pase se alinearon la tabla de scopes de `Codigo/ESTANDAR-DE-COMMITS.md` —declaraba un `scope-enum` de tres entradas cuando el real tiene seis— y los dos `examples` del esquema del catálogo.

**Traza.** RF-10, RF-12, ADR-040, ADR-171, ADR-176, ADR-192, Doc 2 §10, Doc 7 §4 y §8.

---

## ADR-194 · La segunda plantilla de la línea: Azure Functions, con sus límites declarados

**Estado:** Aceptada · 2026-11-09 · Doc 7 · revisa el alcance del índice de la fase y la elección de ADR-179

**Contexto.** El el índice de la fase excluyó «la construcción de más de un activo base» y lo declaró punto de
extensión. **ADR-179** eligió una plantilla ficticia como fixture en lugar de publicar una segunda,
dejando dicho que revertir la exclusión es decisión del autor. El autor la tomó.

**Decisión.** Entra `@bsl/azure-functions-api`, que deriva un API HTTP de un Service Domain sobre Azure
Functions, con forma de producto `azure-functions@1`. El fixture se conserva: prueba que el intérprete
deriva una familia de entrada distinta, y esta prueba que una plantilla publicable de otra forma pasa
las puertas de la línea.

**Por qué es evidencia y no un segundo caso del mismo.** Tres cosas difieren de verdad:

| | `nestjs-hexagonal-api` | `azure-functions-api` |
| :---- | :---- | :---- |
| Punto de composición | Un módulo de NestJS con contenedor de inyección | **No hay contenedor.** Se compone en `composition.ts` y cada función importa lo que necesita |
| Servidor | Propio, arrancado por `main.ts` | **Ninguno.** El host invoca una función por ruta |
| Puntos de inserción | Ocho | **Cinco**, y uno de los roles **no existe** |

**El punto que no existe, y es el hallazgo del contrato de forma.** Esta forma no declara punto de
inserción de entorno, y la razón es del formato: los settings de una function app viven en
`local.settings.json`, que es **JSON estricto**, y un marcador es una línea de comentario, que ahí
deja el archivo inválido. Una forma cuyo archivo de settings es JSON **no puede tener punto de
entorno**, y el contrato de **ADR-176** lo expresa sin inventar nada: la forma declara los puntos que
tiene y `pointOf` rechaza nombrando el rol que falta. Ningún módulo la sirve todavía, así que el costo
hoy es nulo.

**No trae producto de referencia, y es deliberado.** `nestjs-hexagonal-api` lo trae por historia y lo
paga con la prueba de igualdad byte a byte de **ADR-066**; esta no, así que no hay dos fuentes del
mismo código. Su verificación deriva un producto, comprueba que registre este paquete y esta forma, lo
instala y corre el `verify` que el producto trae.

**Límite asumido.** Tres:

| Límite | Por qué |
| :---- | :---- |
| Deriva **solo las operaciones del control record** | La ruta de un behavior qualifier necesita el calificador en kebab-case **y** en plural: dos transforms encadenados que el motor no tiene (**P-60**). El manifiesto las filtra con una condición en vez de servir una ruta inventada |
| Nunca publica eventos de dominio | El producto no liga un puerto de publicación, y el registro declara `domainEvents: false` cualquiera sea lo elegido. El reporte de la derivación todavía afirma lo contrario, porque una plantilla no puede declarar qué puntos de variación honra (**P-60**) |
| Su verificación **nunca arranca el producto** | Correrlo exige las Azure Functions Core Tools, que ninguna puerta puede dar por instaladas. La superficie la ejercitan las pruebas del producto, que invocan el handler directamente |

**Cuatro defectos propios, los cuatro atrapados por el producto derivado y no por una prueba de la
herramienta.** Una línea en blanco de más en la lista de imports, el `tsconfig.json` sin incluir `test`,
y el de fondo: `Control` y `Execute` **no reciben body** y la plantilla usaba `body` igual, así que el
producto no compilaba. Esas operaciones actúan sobre un registro que ya existe, de modo que ahora lo
cargan, lo mueven de estado y lo guardan, con `404` si no está.

**Un defecto que encontró el documento oficial del host.** El `local.settings.json.example` declaraba
`AzureWebJobsStorage: UseDevelopmentStorage=true`, que la guía de Microsoft exige **solo para triggers
que no son HTTP** y que obliga a tener Azurite instalado y corriendo. Este producto tiene tres
`app.http` y persiste en memoria, así que la línea le agregaba un emulador como requisito de arranque:
una segunda pared después de instalar `func`. Retirada, con el README del producto declarando por qué
no está y cuándo agregarla. El dato venía del scaffold genérico de `func init` y no del documento de
esta forma, que es el patrón de **ADR-139** en otro estándar.

**Consecuencia.** Ninguna de las cuatro primitivas del vocabulario **filtra una lista en otra lista**, y
el rodeo de hoy es agrupar por el calificador y quedarse con un grupo. Queda como candidato a quinta
primitiva en el doc 7. La entrada del catálogo nace `proposed`, que es la verdad mientras el paquete no
esté publicado, y su verificación trabaja sobre una copia con las plantillas en `active`.

**Traza.** Alcance del anteproyecto, objetivo específico 2, RF-01, RF-02, RF-04, RF-14, RF-15, ADR-066,
ADR-100, ADR-139, ADR-171, ADR-173, ADR-176, ADR-179, ADR-180, ADR-191, ADR-192, ADR-193, P-60,
el índice de la fase, Doc 7.

---

## ADR-196 · Leer una plantilla no es derivar de ella, y publicar un activo no activa su entrada

**Estado:** Aceptada · 2026-11-09 · Doc 3 / Doc 4 · precisa ADR-100 y ADR-171

**Contexto.** El autor publicó los seis activos y usó la herramienta del feed. Escribió
`bsl templates show azure-function-api` —en singular, un typo— y recibió
`No template 'azure-function-api' in the catalog. The catalog offers: nestjs-hexagonal-api.` Tres cosas
estaban mal en ese episodio:

1. **El rechazo nombraba lo ofrecido y no lo que el catálogo tiene.** Con la entrada de la plantilla de
   Azure en `proposed`, el mensaje la omitía, así que un typo se leía como «esa plantilla nunca se
   agregó». Peor: **contradecía a `bsl templates list`**, que la lista.
2. **`bsl templates show` se negaba a leer una plantilla propuesta.** Con el nombre bien escrito el
   mensaje era correcto y la negativa no: **leer qué deriva una plantilla no cambia nada**, y la que
   todavía no se publica es justo la que alguien necesita mirar para decidir si la adopta. La causa es
   que `show` y `new` compartían la resolución, y esa función se escribió para **derivar**.
3. **Publicar un activo no activa su entrada.** `@bsl/azure-functions-api` estaba servido y su entrada
   seguía en `proposed`. **ADR-100** fija la convención y no dice **quién** la mueve.

**Decisión.** Tres, una por cada cosa. **La resolución se parte según el acto:** `chosenTemplate` sigue
siendo la de derivar y rechaza una plantilla que no se ofrece, porque derivar de un activo que el
registro no sirve produce un producto que nadie puede instalar; entra `templateToInspect`, que es la de
leer y acepta cualquier estado. **Un rechazo por un nombre que no existe nombra lo que el catálogo
tiene, con el estado de cada uno:** `The catalog holds: nestjs-hexagonal-api, azure-functions-api
(proposed).` **Y activar la entrada es un paso explícito** del procedimiento de publicación del doc 3 §7.

**Alternativas.** Que el `prepublishOnly` moviera la entrada. Se descarta: el catálogo vive en otro
repositorio y es la pieza que **ADR-035** pone bajo revisión del gobierno de la línea, así que un
`prepublishOnly` que lo escriba convierte una publicación en un cambio no revisado de un repositorio
ajeno. El costo de la publicación aparte es el que ADR-162 midió y aceptó.

**Un cuarto hallazgo, que lo produjo activar la entrada.** Al pasar la entrada a `active`,
**`verify:generation` dejó de pasar**: derivaba sin `--template`, y la omisión era admisible mientras
exactamente una plantilla estuviera ofrecida. Con dos, la herramienta se niega a adivinar, que es lo
que ADR-171 decidió. Los dos circuitos nombran ahora la plantilla, lo que además es lo honesto de un
circuito: lo que verifica es **esa**. Lo encontró `check:push` y nada antes, porque el estado del
catálogo no es insumo de ninguna prueba unitaria y activar una entrada es un cambio de **un** campo en
otro repositorio que cambió el comportamiento de un comando.

**Consecuencia.** Ningún requerimiento cambia de veredicto. RF-15 y RNF-06 se miden contra el feed de
hoy y pasan a cumplidos con las seis publicaciones; lo que queda sin publicar es el catálogo `0.6.0`
(**P-63**), y hasta entonces la segunda plantilla **se lista y no se puede usar** desde el feed.

**Verificación (2026-11-09).** `check:push` en verde, código 0: 494 pruebas más las 4 del producto que
deriva la plantilla de Azure, cero vulnerabilidades, los tres productos de la generación nombrando su
plantilla, y los 22 pasos y 8 rechazos de la composición. `npm view` confirma los seis paquetes
servidos.

**Traza.** RF-14, RF-15, RF-16, RNF-06, ADR-035, ADR-100, ADR-162, ADR-163, ADR-171, ADR-195, P-63,
Doc 3 §7, Doc 4 §5, Doc 6 §10.

---

## ADR-197 · La plantilla se decide antes de la primera pregunta, y se pregunta si la invocación no la nombra

**Estado:** Aceptada · 2026-11-09 · Doc 1 / Doc 5 · revisa ADR-171 en su alcance

**Contexto.** Un reporte de uso: el autor corrió `bsl new` sin `--template`, respondió las nueve
preguntas del recorrido y recién al final leyó que con dos plantillas ofrecidas hay que nombrar una.
El defecto es más grande que la pregunta que falta. En `generate.operation.ts`, el cuestionario corría
**antes** de leer el catálogo, así que una condición que la invocación no satisfacía se comprobaba
después de cerrar las nueve preguntas y costaba perderlas todas. Es el defecto que **ADR-169** quitó de
los puntos de variación, sobreviviendo un nivel más arriba, en una condición que el modelo de
variabilidad no declara y que por eso ninguna de sus correcciones alcanzaba. El mismo orden tenía un
segundo costo igual: un catálogo ilegible también se cobraba las nueve respuestas.

**Decisión.** Dos, y el orden es la primera.

1. **La plantilla se decide antes de la primera pregunta del modelo.** Leer el catálogo y resolver la
   plantilla se mueven delante del cuestionario. Lo que se deriva decide qué es el producto, así que es
   lo primero que hay que saber, y un rechazo —por plantilla o por catálogo— llega antes de que nadie
   escriba nada.
2. **Si la invocación no la nombra, se pregunta.** Una opción por plantilla ofrecida, con el id como
   etiqueta y la descripción del catálogo como pista. Con una sola ofrecida no se pregunta. Una
   `proposed` no se ofrece, porque la derivación la rechazaría. La lista hereda ADR-166 y no se enrolla.

**Por qué.** Preguntar no es adivinar, así que ADR-171 se revisa en su alcance y no en su criterio: lo
que se agrega no es una conjetura de la herramienta sino la persona. `templateToDeriveFrom` delega en
`chosenTemplate` **todos** los rechazos y la respuesta de la pregunta vuelve a pasar por ahí, de modo
que cada rechazo sigue viviendo en un solo lugar y no hay una segunda lectura de lo que el catálogo
ofrece.

**Límite asumido.** La pregunta es su propio acto, antes del cuestionario, así que la tecla de escape
en la primera pregunta del modelo no vuelve a ella: sale del comando. Se evaluó meterla a la cadena de
navegación del resolvedor y se descartó, porque el resolvedor conoce solo el modelo de variabilidad y
hacerle aceptar una pregunta que no es un punto de variación acopla el núcleo al catálogo para ganar una
tecla. El día que una plantilla traiga su propio modelo —el punto de **P-60**— el límite se va solo.

**Consecuencia.** Ningún requerimiento cambia de veredicto, y se cierra el último lugar donde el
criterio de RNF-01 se incumplía: ninguna condición del recorrido se comprueba después de cerrar una
pregunta.

**Verificación.** Comprobado rompiéndolo (ADR-126): con el orden anterior el error que sale es
`No value given for: projectName` y no el de la plantilla. Comprobado además con la herramienta real
sin terminal. Falta el render de la pregunta, que exige terminal y lo confirma el autor.

**Traza.** RF-02, RF-05, RNF-01, ADR-126, ADR-166, ADR-169, ADR-171, ADR-196, P-60, Doc 1 §11,
Doc 5 §2.

---

## ADR-198 · El reporte de la derivación se lee del producto escrito

**Estado:** Aceptada · 2026-11-09 · Doc 5

**Contexto.** Los cuatro pasos que la herramienta imprime al terminar —`cd`, `npm install`,
`cp .env.example .env`, `npm run start:dev`— estaban escritos en su código. Con una sola forma de
producto eran verdad por casualidad. Con la segunda **fallan al ejecutarlos**: el producto de Azure
Functions se configura con `local.settings.json.example` y se arranca con `npm start`. La instrucción
correcta ya existía, textual, en el `README.md` que la plantilla escribe en el producto: la plantilla
sabía los pasos y la herramienta los afirmaba por su cuenta.

**Decisión.** Todo paso del reporte se lee del `ChangePlan` aplicado, y ninguno se afirma.

| Paso | De dónde sale |
| :---- | :---- |
| `npm install` | Solo si el plan escribe un `package.json` |
| `cp <archivo> <destino>` | Un archivo creado que termina en `.example`, al mismo nombre sin el sufijo. Es una convención que las dos plantillas ya seguían |
| El arranque | Los `scripts` del producto: `start:dev`, si no `start`, si no ninguna línea |
| `npm run verify` | Solo si el producto declara ese script |
| El cierre | `Read README.md for what else this product needs`, solo si el plan escribe uno |

Un paso que corre un script **muestra el comando que corre**, leído de los mismos `scripts`:
`npm start  # func start`. Así una herramienta externa se nombra antes de que el paso falle.

**Por qué leer el producto y no declararlo en el manifiesto.** Se evaluó darle a `bsl-template.json`
una sección `report`, que es lo que el plan de la sexta ronda había diseñado. Un manifiesto puede
mentir y el plan **es** el producto. Leer el producto funciona además para la plantilla de un tercero
que no declara nada, con solo seguir la convención del `.example`.

**Consecuencia.** La rama que no imprime `npm install` ni arranque —un producto sin `package.json`— no
la ejercita ninguna prueba: el modelo no puede producir tal producto, y el fixture que sí puede se
ejercita al nivel de `interpret`. Queda como hueco de cobertura conocido, sin taparlo exportando una
función privada.

**Verificación.** Comprobado rompiéndolo, como pide ADR-126: con los pasos escritos de nuevo en el
código, la prueba de la segunda forma falla. Y derivando los dos productos de verdad, donde el
hexagonal imprime exactamente los pasos de antes.

**Traza.** RF-02, RNF-01, ADR-126, ADR-179, ADR-193, ADR-194, P-60, Doc 5 §2.

## Decisiones pendientes de esta fase

Los ajustes que ADR-042, 044, 045, 047 y 048 declaraban pendientes se aplicaron a los documentos 1 a 4 el 2026-10-19: árbol y código real del activo base, configuración del analizador, configuración validada, punto de composición con fábricas, versiones del toolchain, esquemas JSON de los tres artefactos declarativos, textos en inglés, `npmrc` en las tablas de empaquetado y frontera, y asignación de decisiones del índice de la fase.

El código de los docs 5 y 6 se construyó y verificó, y los dos documentos quedaron alineados con él el 2026-10-22: árbol real del paquete, registro y despacho en su lugar (ADR-071), sexto puerto, composición, ayuda, catálogo de 37 plantillas, tabla de pruebas y empaquetado. Los tres ajustes de texto al activo base que ADR-066 declaraba están aplicados. Queda lo siguiente.

| Documento | Qué falta |
| :---- | :---- |
| Doc 1 / Doc 2 | Completar `service-landscape.json` con el resto del subconjunto de Service Domains que el contexto construye, transcrito del portal del estándar. Hoy el archivo trae dos entradas y ambos documentos lo declaran así |
| Doc 4 | Ajustar §5, §8, §11 y §15 según ADR-073, 074 y 075: comprobación de la versión del entorno, consulta del registro sin workspaces, y artefactos declarativos cargados con el módulo en lugar de leídos del disco |
| Doc 5 | ~~Corregir `repository.ts.tpl`~~. **Hecho el 2026-11-04.** Decía `The base template binds it to an in-memory adapter` y ahora dice `The product binds it...`, corregido a la vez en la plantilla y en el activo base, que es su salida (ADR-066). Verificado con `check:commit` y `verify:generation`. El bloque que el doc 5 §5 transcribe quedó retranscrito del archivo real |
| — | **Nada pendiente de los documentos de la fase.** El Bloque C se cerró el 2026-10-31: doc 6 (ADR-086 a 092), `packages/cli/TUTORIAL.md` (ADR-093, 094) y el índice de la fase, que registra RF-04 como no satisfecho por alcance según ADR-072 |
| Doc 4 / Doc 5 | Ajustados el 2026-10-31 con el doc 6. Doc 4 §14: entra `argv.spec.ts`, y la tabla de dobles se corrige —nombraba un `FixedClock` que nunca se escribió y omitía `FakeCommandRunner`—. Doc 5 §14: entra `generate.operation.spec.ts` como tercer archivo de prueba de la operación, y el "hueco de cobertura declarado" de `operations/generate/naming.ts` pasa a cerrado |
