# Auditoría de cierre del proyecto

> **Instantánea del 2026-11-07.** Todas las cifras son las de ese día. **La superan las mediciones de la auditoría de alineación del 2026-11-09** y las del pase de reescritura del 2026-11-10.
> Lo que vale de forma permanente son los hallazgos y su veredicto; los conteos se vuelven a medir
> corriendo las herramientas de `Estandares/herramientas/`.

La revisión de punta a punta del proyecto —expediente y código— hecha el 2026-11-07,
antes de ejecutar la evaluación. Comprueba que la línea lógica se sostiene: que la cadena de trazabilidad no
tiene eslabones huérfanos, que lo que el expediente afirma del código es lo que el código hace, que el encuadre
como línea de producto sigue siendo el correcto, y que no hay contradicciones entre documentos.

**Método.** Comprobación mecánica donde se puede comprobar —scripts sobre los archivos y ejecución de los dos
circuitos— y lectura cruzada donde hay que juzgar. Cada afirmación de abajo se comprobó; ninguna se da por
buena porque un documento la declare.

**Por qué ahora.** Porque es el momento en que todavía sirve: una auditoría al final, con la tesis escrita,
solo documenta lo que ya no se puede arreglar.

---

## 1. Integridad del sistema de decisiones

| Qué se comprobó | Resultado |
| :---- | :---- |
| Total de decisiones | **168 entradas**, numeradas de forma continua |
| Huecos en la numeración | **Ninguno.** La secuencia 1 a 168 está completa |
| Números duplicados | **Ninguno.** Cada número existe en un solo log |
| Reparto por log | 42 en la Fase 1, 83 en la Fase 2, 41 en la Fase 3, 2 en la Fase 4 |
| Índice contra entradas, log por log | **Coinciden exactamente**: 42/42, 83/83, 41/41, 2/2. Ninguna decisión está indexada sin entrada ni escrita sin índice |

Los rangos no son contiguos a propósito: cada decisión vive en el log de la fase cuyo artefacto toca, que es la
regla del proyecto. La numeración global continua es lo que permite que eso no rompa ninguna referencia, y la
comprobación confirma que no la rompió.

## 2. Integridad del expediente

| Qué se comprobó | Resultado |
| :---- | :---- |
| Documentos citados por los cuatro índices de fase | 45 citas: 14 en la Fase 1, 10 en la Fase 2, 11 en la Fase 3, 10 en la Fase 4 |
| Citas que apuntan a un archivo inexistente | **Ninguna** |
| Fases con documentos en `falta` | Ninguna. La Fase 1 quedó completa el 2026-11-06; las 2 y 3 cerraron el 2026-10-31; los nueve de la Fase 4 existen |

## 3. La cadena de trazabilidad

Se comprobó eslabón por eslabón que ningún identificador queda sin consumidor.

| Eslabón | Comprobación | Resultado |
| :---- | :---- | :---- |
| `T-xx` → `N-xx` | Los quince temas tienen una necesidad que los cita como origen | **Completo.** T-11, T-12, T-13 y T-15 aparecen solo en el doc 04 de la Fase 1, y es correcto: ahí los consume T-11, T-12, T-13 y T-15 respectivamente |
| `T-xx` → downstream | Los quince temas se citan en dos o más documentos | **Completo** |
| `B-xx` → downstream | B-01 en 8 documentos, B-02 en 9, B-03 en 8 | **Completo** |
| `RF/RNF` → downstream | Los veintidós requerimientos se citan en dos o más documentos | **Completo.** Ninguno queda enunciado y sin desarrollar |
| Requerimientos abiertos | Se buscó si algún documento declara RF-16 o RNF-03 como cumplidos | **Ninguno lo hace.** Los dos están declarados como abiertos, y la Fase 4 los cierra |

## 4. Lo que el expediente afirma del código, contra el código

Comprobado ejecutando, no leyendo.

| Afirmación del expediente | Comprobación | Resultado |
| :---- | :---- | :---- |
| Cinco activos con sus versiones | `package.json` de cada uno | Contrato `0.3.0`, activo base `0.20.0`, herramienta `0.27.0`, persistencia `0.3.0`, observabilidad `0.1.0`, catálogo `0.3.0`. **Coincide** *(la herramienta pasó a `0.28.0` ese mismo día, después de esta auditoría, con la ronda del recorrido de creación)* |
| 354 pruebas | Ejecutadas | **354 exactas**: 105 del activo base, 199 de la herramienta, 36 de observabilidad, 12 de persistencia, 2 del contrato |
| El activo base entrega 62 archivos sin contar la compilación | Contados | **62**: 31 en `src`, 18 en `test`, 13 en la raíz |
| El circuito de generación deriva tres productos de 68, 40 y 43 archivos | `verify:generation` | **Verde, y los tres conteos exactos.** Cada producto pasa su propia verificación, arranca, responde sus sondas, sirve su documento OpenAPI —nueve rutas en `term-deposit-api`— y sirve `/docs` con el visor instalado en el producto |
| El circuito de composición tiene diecinueve pasos y seis rechazos | `verify:composition`, y el conteo de los pasos que enumera el doc 7 §4 de la Fase 3 | **Verde.** Los seis rechazos aparecen uno por uno, y la enumeración del documento tiene exactamente diecinueve pasos |
| Un producto admite los dos módulos a la vez | El circuito | **Comprobado**: declara los dos, persiste un registro, sobrevive al reinicio, pasa su verificación y **exporta tres spans continuando la traza del llamador** |
| El modelo declara trece puntos de variación | `variability-model.json` | **Trece**, más tres invariantes en `fixed` |

## 5. El encuadre como línea de producto, revisado

La Fase 1 adoptó línea de producto de software como encuadre. La pregunta de la auditoría no es si fue acertado,
sino **si el artefacto construido sigue siendo eso**.

| Elemento constitutivo de una LPS | Qué lo materializa hoy | Estado |
| :---- | :---- | :---- |
| *Core assets* | Cinco paquetes publicados: el contrato, el activo base, la herramienta y dos módulos, más el manifiesto del catálogo | Presente |
| Mecanismo de derivación | `@bsl/cli`, con cinco operaciones | Presente |
| Familia de productos | El alcance declarado por el marco, y tres productos de referencia derivados y verificados | Presente |
| *Domain* y *application engineering* | La correspondencia con las fases que el marco declara: las fases 2 y 3 construyen los activos, la 4 ejerce la derivación | Presente |

**Las dos desviaciones que el encuadre declaró siguen siendo exactas**, y conviene registrarlo porque son lo que
distingue a esta línea de una clásica:

1. *Los productos quedan bajo control autónomo del equipo que los recibe* (RNF-02). Sigue siendo así: la
   actualización compara una huella para no pisar lo que el equipo cambió, en lugar de gobernar el producto.
2. *La derivación no ocurre en un solo acto, sino por configuración por etapas.* Es más cierto hoy que cuando
   se escribió: incorporar un módulo a un producto ya derivado y actualizarlo después son exactamente eso.

Y la práctica que el encuadre explicaba —*clone-and-own*, la copia de carpetas que T-04 documentó— sigue siendo
la referencia contra la que el doc 4 de la Fase 4 va a comparar. El encuadre no quedó decorativo: es lo que
nombra el problema y lo que ordena la comparación final.

## 6. Coherencia con la metodología

El anteproyecto declara Design Science Research en cuatro fases. La correspondencia se sostiene: la Fase 1
caracteriza el problema y especifica, la 2 y la 3 construyen el artefacto, la 4 lo evalúa. Las cuatro tienen
índice, log de decisiones y documento de trazabilidad, y cada una declara su condición de llegada comprobable.

**La única divergencia metodológica del proyecto está declarada**, y es la del diseño de la evaluación: no es el
caso de estudio en el laboratorio que el anteproyecto compromete, sino una evaluación con las personas de ese
contexto. No hay otra divergencia respecto del método declarado, y esta no se presenta como si no hubiera
ocurrido.

## 7. Hallazgos

Seis. Cuatro se corrigieron en el mismo pase; dos quedan como recomendación.

| ID | Hallazgo | Severidad | Estado |
| :-- | :---- | :---- | :---- |
| **A-01** | El doc 4 de la Fase 2, su log y el mapa raíz afirmaban que la herramienta hace «once preguntas» en su recorrido. **El modelo declara trece puntos de variación**, y cuántos se preguntan depende de la capacidad y de si se declara fuera del catálogo. El número era una invención de quien lo escribió | Dato falso en documento normativo | **Corregido** el 2026-11-07 en los tres lugares: ahora dice «todas las preguntas del recorrido, hasta trece según la capacidad» |
| **A-02** | El mapa raíz seguía diciendo «lo que sigue es abrir la Fase 4» con la fase ya abierta | Dato vencido | **Corregido** |
| **A-03** | El mapeo fase ↔ código del mapa raíz atribuía a la Fase 3 solo `persistence`, con `observability` construido desde el 2026-11-05 | Dato vencido | **Corregido** |
| **A-04** | El capítulo 3 de la tesis narra la Fase 1, que desde el 2026-11-06 tiene un documento 7 —la línea base— que **ningún capítulo menciona todavía**. La decisión fue narrarla en el capítulo 6, dentro de P-42, pero la narración de la Fase 1 queda incompleta sin al menos una referencia cruzada | Hueco de narración, no de contenido | **Anotado en la ficha de P-42** |
| **A-05** | *Reescrito el 2026-11-07 por la ronda del recorrido de creación: la versión vigente pasó a `0.28.0`, con el recorrido de creación corregido, y es esa la que hay que publicar. El hallazgo no cambia de naturaleza ni deja de bloquear.* **El feed sirve `@bsl/cli` `0.26.0` y la versión vigente es `0.28.0`** (P-56). La evaluación instala del feed, de modo que, si se hacen las llamadas antes de publicar, el participante se va a topar con la lista que gira infinitamente —el defecto que la ronda anterior acaba de corregir— y la medición registrará un problema ya resuelto | **Bloquea la evaluación**, por orden de ejecución | **Recomendación: publicar antes de la primera llamada.** Es el mismo error que el informe externo del 2026-10-28 documentó, cuando el evaluador midió una versión anterior a la del repositorio y tres hallazgos ya estaban resueltos sin que pudiera verlos |
| **A-06** | El documento 7 de la Fase 1 vive en la carpeta del Bloque B —`2 - Definición del marco de referencia/Documentos/`— aunque por naturaleza sea evidencia del problema, más cercana al Bloque A | Rareza declarada, no defecto | Es dónde el índice de la fase lo declaró, y se mantuvo por decisión del autor. Queda registrado para que un lector no lo lea como un error de archivo |

## 8. Lo que la auditoría no encontró

Vale decirlo, porque es el resultado principal:

- **Ningún requerimiento huérfano.** Los veintidós se desarrollan y se miden.
- **Ninguna necesidad ni brecha sin respuesta** en el expediente.
- **Ninguna decisión sin traza** a evidencia, requisito, encuadre o decisión previa.
- **Ninguna contradicción entre dos documentos** sobre el mismo hecho. Las afirmaciones vencidas que quedan en
  documentos cerrados tienen su nota fechada, que es la práctica del proyecto: el texto de cierre se conserva y
  la corrección se anota, en lugar de reescribir la historia.
- **Ninguna afirmación del expediente sobre el código resultó falsa** al ejecutarla. Las siete que se
  comprobaron coincidieron, conteos incluidos.

## 9. Estado de la tesis, que es lo que queda

El expediente está completo; la narración no. Al 2026-11-07:

| Capítulo | Líneas | Estado | Pendiente |
| :---- | :--: | :---- | :---- |
| 1, introducción | 229 | Narrado, con tres marcas `PENDIENTE` | P-25 |
| 2, marco | 223 | Narrado, con una marca | P-25 |
| 3, fundamentación | 1696 | Narrado; **19 marcas** de figura por insertar, y sin la línea base | P-13, y A-04 de esta auditoría |
| 4, generación | 696 | Narrado, sin marcas. Un pasaje quedó vencido por una ronda posterior | P-51 |
| 5, gestor de módulos | 367 | Narrado, sin marcas. No narra el segundo módulo | P-53 |
| 6, evaluación | 9 | **Vacío**, se narra al cerrar la fase | P-42 |
| 7, conclusiones | 21 | **Vacío** | P-43 |
| Riesgos éticos | 17 | Texto de la plantilla | P-44 |
| Preliminares | — | Sin escribir | P-45 |

**Ningún hueco de la tesis queda sin pendiente que lo siga**, que es justo lo que la auditoría del 2026-11-03
había encontrado mal: entonces el capítulo 5 estaba vacío y nadie lo seguía.

## 10. Conclusión de la auditoría

El proyecto se sostiene de punta a punta: la evidencia lleva a los temas, los temas y las brechas a
los requerimientos, los requerimientos a las decisiones, las decisiones a los documentos, los documentos al
código, y el código a la evaluación que esta fase va a ejecutar. Lo comprobado por ejecución coincide con lo
declarado, y el encuadre como línea de producto no quedó como adorno teórico: es lo que nombra el problema y lo
que ordena la comparación final.

Lo que falta es de dos clases, y ninguna es un hueco oculto: **el insumo de las llamadas**, que es lo que los
documentos 4 a 9 esperan, y **la narración en la tesis**, que por regla del proyecto se escribe al cerrar.

Y una cosa hay que hacer **antes** de la primera llamada: publicar `@bsl/cli` `0.28.0`. Es el hallazgo A-05, y
es el único que bloquea.

*Nota del 2026-11-07, después de esta auditoría.* La versión por publicar pasó de `0.27.0` a `0.28.0`: el autor
abrió la quinta ronda de mejoras sobre el recorrido de creación y decidió que entre
antes de la sesión, porque la sesión mide usabilidad y el defecto más grave que esa ronda corrige —una respuesta
mal escrita que termina el comando— está justo en el camino que el desarrollador interno va a recorrer. La ronda
aporta además algo que esta auditoría no había notado: **ningún camino automático de la línea pasa por una
pregunta**, porque los dos circuitos corren con banderas y con `--non-interactive`. Es la misma clase de hueco
que A-05 describe, un paso antes.
