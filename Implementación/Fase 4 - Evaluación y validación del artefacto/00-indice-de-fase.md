# Fase 4 — Evaluación y validación del artefacto

Establece si el artefacto resuelve el problema que la Fase 1 documentó, midiendo los tres criterios del
objetivo específico 4 contra la línea base, y declara con qué evidencia y con qué límites. **No se
construye nada nuevo:** se mide lo construido, y lo que la medición encuentre se registra como hallazgo
y no como trabajo pendiente. El orden de los documentos sigue una dependencia real: primero se declara
quién mide y cómo, después se mide, y al final se interpreta.

| | |
| :-- | :-- |
| **Capítulo de tesis** | `src/6-evaluacion-validacion.tex`, que se narra al cerrar la fase |
| **Log de decisiones** | `01-adr-evaluacion-y-validacion.md` |
| **Código** | Ninguno nuevo. La fase ejerce lo publicado en el feed, no el repositorio de trabajo |
| **Estado** | **abierta el 2026-11-06**. Los cuatro documentos existen: los dos del Bloque A en `hecho`, y el de las mediciones y el informe escritos y listos para recibir el insumo de las llamadas |

Estado posible por documento: `hecho` · `en curso` · `falta`

---

## Condición de llegada

Comprobable, parte por parte. La fase está completa cuando:

1. Existe un **informe de evaluación** que, para cada uno de los tres criterios del objetivo específico 4,
   declara su medición con la fecha y el comando o el registro que la produjo, comparada contra la línea base
   del doc 1.
2. Los **veintidós requerimientos** de la Fase 1 tienen veredicto final, cada uno con su evidencia o con su
   límite declarado.
3. La **rúbrica de nueve criterios** del informe externo del 2026-10-28 está medida sobre la versión publicada,
   con su «antes» y su «después», aplicada por quien escribió esos criterios. Los nueve entran: el noveno lo
   responde la mirada de negocio.
6. El informe declara **oportunidades de mejora y recomendaciones de adopción**, y no solo qué funcionó. Un
   resultado adverso está reportado con el mismo peso que uno favorable.
4. Cada **participante** de la evaluación está caracterizado con su rol, lo que su participación sostiene y lo
   que la sesga, y cada sesión que ejecutó está registrada.
5. Toda **desviación respecto del anteproyecto** está declarada con su ADR, y ninguna se presenta como si no
   hubiera ocurrido.

## Lo que esta fase hereda, y por eso no construye

| Qué hereda | De dónde | Para qué le sirve |
| :-- | :-- | :-- |
| El veredicto de los 22 requerimientos | Los campos `Traza` de los logs, y la bitácora del seguimiento de mejoras | Al 2026-11-06 estaban cerrados veinte con evidencia. Esta fase cierra los que faltan; el veredicto de los veintidós se levanta una sola vez, al cerrar el proyecto, en el documento de trazabilidad |
| La rúbrica de nueve criterios, escrita por alguien ajeno **antes** de que la Fase 3 construyera | `Insumos/revision-externa-2026-10-28-original.md` y `Insumos/seguimiento-de-mejoras.md` | Es el instrumento de medición del juicio externo, y su primera aplicación es el «antes» |
| Los circuitos reproducibles: `verify:generation` y `verify:composition` | Fases 2 y 3 | La evaluación parte de un estado verificado y no de una demostración |
| Los activos publicados en el feed | El registro de paquetes privado | Lo que se evalúa se instala como lo instalaría cualquiera, no se compila del repositorio. La evaluación corre sobre lo que el feed sirve el día de cada llamada, y el doc 3 declara qué versión fue |

## Bloque A. La referencia y el diseño de la evaluación

Contra qué se compara, quién mide, con qué instrumento y qué va a contar como evidencia. Nada se mide antes
de que las tres cosas estén escritas.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 1 | Línea base de proyectos existentes | Cuánto cuesta hoy, sin la herramienta, llevar un proyecto nuevo hasta que corre y queda desplegable; la definición operacional con que se mide el otro lado; el inventario de tareas con sus tres cubetas; y sus límites declarados | `01-linea-base-de-proyectos-existentes.md` | hecho |
| 2 | Participantes y diseño de la evaluación | Los cuatro `PE-xx` con su distancia respecto del artefacto, qué sostiene cada participación y qué la sesga; y **el instrumento completo** con el plan de las tres llamadas: qué se le pide a cada uno, qué se cronometra, qué cuenta como evidencia, qué superficie usa la sesión y qué se hace si la tercera llamada no ocurre. Es la actividad 1 del anteproyecto, y **está escrito antes de la primera llamada** | `02-participantes-y-diseno-de-la-evaluacion.md` | hecho |

**Por qué la línea base es el documento 1 de esta fase y no de la Fase 1.** Es evidencia del problema, no
materia prima de la especificación ni una regla del marco, y es la referencia contra la que esta fase compara:
vive donde se usa. Quedó constituida el 2026-11-06, con la ventana de medición ya vencida y los sustitutos
descartados por escrito, que es el límite que su §9 declara.

**Por qué los participantes y el instrumento son un solo documento.** El protocolo de una medición depende de
quién la ejecuta: un tiempo que cronometra quien construyó la herramienta y un tiempo observado sobre alguien
que no la conoce no se miden igual ni valen lo mismo. Quién mide y con qué instrumento es una sola decisión, y
separarla en dos documentos obligaba a leer los dos para entender cualquiera de los dos.

## Bloque B. Ejecución

Un documento con los tres criterios y la rúbrica, cada uno contra su referencia y con su veredicto. Lo que
aparezca al ejecutar se registra donde aparece.
Carpeta: `Documentos/`

| # | Documento | Qué mide | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 3 | Las mediciones | El criterio 1 contra la banda de la línea base, sobre la cubeta de lo cubierto y sobre el total; el criterio 2 contra la copia de carpetas sin vínculo, con lo que significa «correcta» fijado antes; el criterio 3 contra el andamio que el producto entrega y lo que el participante esperaba encontrar; y la rúbrica externa contra su propia primera aplicación. Más RNF-03, RF-16, dónde se trabó cada participante y los seis veredictos | `03-las-mediciones.md` | **listo para recibir el insumo** |

**Por qué las cuatro mediciones son un solo documento.** Son una sesión, un instrumento y un mismo conjunto de
participantes, y cada una repetía el mismo esqueleto: su referencia, su procedimiento, lo que no dice y su
veredicto. Lo que cambia entre ellas es qué se mide, y eso son cuatro secciones.

## Bloque C. Cierre

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 4 | Informe de evaluación | Los hallazgos, las recomendaciones y la pertinencia del artefacto. Es el resultado esperado 4 del anteproyecto | `04-informe-de-evaluacion.md` | **listo para recibir el insumo** |

## Insumos que abren la fase

| Insumo | Qué aporta |
| :-- | :-- |
| `Insumos/revision-externa-2026-10-28-original.md` | El informe externo tal como se recibió, con sus nueve criterios. Es el «antes» |
| `Insumos/seguimiento-de-mejoras.md` | Qué se hizo con cada hallazgo, en diecisiete grupos, con el comando que lo prueba, y el estado de la rúbrica: ocho de nueve cumplidos |
| `Insumos/Linea base/01-inventario-de-tareas-de-arranque.md` y `02-datos-autoreportados.md` | Las dos fuentes del doc 1: el inventario de las 31 tareas de arranque con su cubeta, y el autoreporte recogido en las entrevistas de agosto de 2026, que es la única fuente anterior al artefacto |
| `Insumos/auditoria-de-cierre-2026-11-07.md` | **Instantánea del 2026-11-07, superada por la siguiente.** La revisión de punta a punta antes de evaluar: 168 ADR sin huecos, la cadena de trazabilidad completa, y las siete afirmaciones del expediente sobre el código comprobadas por ejecución. Seis hallazgos, cuatro corregidos en el pase |
| `Insumos/auditoria-de-alineacion-2026-11-09.md` | **Instantánea del 2026-11-09, la más reciente de las dos.** El barrido de las cuatro fases más `Codigo/` después de las ocho rondas del día: 198 ADR, 505 pruebas, los dos circuitos y el cruce de los cuatro conceptos que las rondas movieron. **Cinco hallazgos, todos de estado y todos corregidos en el pase**; ninguna contradicción de fondo |
| `Insumos/bitacora-de-sesiones.md` | Nace vacío. Una entrada por sesión: fecha, participante, qué se le pidió, qué hizo, **dónde se trabó** y qué quedó registrado |

## Decisiones abiertas al abrir la fase

Se enumeran para que su ausencia no se lea como olvido. Ninguna se resuelve en este índice.

| Decisión | Dónde se toma |
| :-- | :-- |
| Cómo se evalúa sin el caso de estudio del laboratorio, y qué se pierde con ello | este índice, con su ADR |
| Qué sostiene la medición hecha por quien construyó el artefacto, y cómo se acota su sesgo | Doc 2 §2 |
| Si el tiempo se mide cronometrando una ejecución o reconstruyéndolo por tareas, y con qué unidad | Doc 2 §7 |
| **RF-16**: qué cuenta como evidencia de que el procedimiento de incorporación al catálogo es suficiente | Doc 2 §11 y doc 3 §2.5. El custodio natural del catálogo participa en la evaluación |
| **RNF-03**: con qué herramientas se analiza el producto generado | Doc 2 §11 y doc 3 §1.6 |
| El noveno criterio de la rúbrica, que pide un rol no técnico | Lo sostiene la mirada de negocio del líder técnico, que no usa la herramienta sino que observa y reacciona. Se mide en el doc 3 §4.4 |
| El hito `1.0.0` de la línea, que retira las tres cláusulas de lectura | este índice, al cerrar |

## Frontera con lo ya cerrado

El paso que más problemas evita, y acá no mira hacia adelante sino hacia atrás: no hay fase siguiente.

- **No se construye.** Si la evaluación encuentra un defecto, se registra como hallazgo con su severidad. Si se
  corrige, la corrección es una ronda de mejora con su propio ADR en el log de la fase cuyo artefacto toca, y
  esta fase registra que la medición se hizo sobre la versión anterior. Lo contrario —corregir y volver a
  medir en silencio— convierte la evaluación en una demostración.
- **No se reabren las fases 2 y 3.** Sus documentos de trazabilidad están cerrados. Esta fase los cita.
- **No se mide lo ya medido.** Que los 22 requerimientos estén construidos es trabajo del insumo de medición,
  anterior a la evaluación. Esta fase mide **uso**, no construcción.
- **Lo que quede sin cerrar no se esconde**: va al índice de la Fase 4 como trabajo futuro, con el motivo.

## Convenciones de la fase

- **Diagramas:** prefijo `EV-`, patrón `EV-0N_figM_...`, donde `N` es el documento al que la figura pertenece, con `Estandares/ESTANDAR-DE-DIAGRAMACION.md`.
- **Participantes:** identificador `PE-xx`, estable y citable desde cualquier documento o ADR.
- **Confidencialidad:** la bitácora puede nombrar a la persona; los documentos de la fase la citan por su
  `PE-xx` y su rol; la tesis, solo por su rol. Ningún dato privado de la organización entra al expediente.
- **Evidencia:** toda medición se reporta con su fecha y con el comando o el registro que la produjo. Una
  medición sin forma de repetirla no es evidencia.

---

## Qué queda fuera, y por qué

| Qué | Por qué |
| :---- | :---- |
| **Construir** | La fase evalúa. Si encuentra un defecto, lo registra como hallazgo con su severidad; corregirlo es otra ronda, con su ADR en el log de la fase cuyo artefacto toca, y esta fase declara que midió la versión anterior. Corregir y volver a medir en silencio convertiría la evaluación en una demostración |
| **Reabrir las fases 2 y 3** | Sus documentos de trazabilidad están cerrados. Esta fase los cita |
| **Medir construcción** | Que los 22 requerimientos estén construidos lo mide el seguimiento de mejoras, que es anterior a la evaluación. Esta fase mide **uso** |
| **Adopción en el tiempo** | Tres llamadas de una hora no la miden. Es lo que el caso de estudio habría dado, y queda declarado como límite |
| **La narración en la tesis** | Se escribe al cerrar la fase, en `src/6-evaluacion-validacion.tex` |
| **Publicar** | Es del autor. La evaluación corre sobre lo que el feed sirve el día de cada llamada, y el doc 3 declara qué versión fue |

---

## Qué narra el capítulo 6 de la tesis

El mapeo con que se narra el capítulo. Destila; no reproduce evidencia, la cita con su fecha y su comando.

| Sección del capítulo | De qué documento sale |
| :---- | :---- |
| Diseño de la evaluación: criterios, participantes e instrumento | Doc 2 |
| La desviación respecto del caso de estudio comprometido | este índice y el doc 2 |
| La línea base contra la que se compara | Doc 1 |
| Resultados del criterio 1 | Doc 3 §1 |
| Resultados del criterio 2 | Doc 3 §2 |
| Resultados del criterio 3 | Doc 3 §3 |
| El antes y el después de la rúbrica externa | Doc 3 §4 |
| Hallazgos y recomendaciones | Doc 4 §4 y §5 |
| Pertinencia del artefacto | Doc 4 §8 |
| Límites de la evaluación | Doc 4 §9 |
| Cobertura de requerimientos y brechas | El documento de trazabilidad del cierre |
| Trabajos futuros, para el capítulo 7 | Doc 4 §6 |
| Lecciones aprendidas, para el capítulo 7 | La §9 del doc 1 —la ventana de medición que se venció— y los hallazgos de método del doc 4 |
