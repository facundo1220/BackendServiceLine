# Fase 1 — Fundamentación y definición del marco de referencia

Demuestra con evidencia que el problema existe y entiende en qué consiste, y define cómo debe
estructurarse la solución antes de escribir código. Al terminar se sabe qué debe hacer la herramienta y
qué forma deben tener los proyectos que produzca.

**Capítulo de tesis:** `src/3-fundamentacion.tex` · **Código:** ninguno, la fase no construye ·
**Estado: completa.**

Estado posible por documento: `hecho` · `en curso` · `falta`

---

## Bloque A. Comprensión del problema y especificación

Reúne la evidencia del problema y la convierte en requerimientos con criterio de aceptación. Ninguna
afirmación del proyecto queda sin respaldo en estas fuentes.
Carpeta: `1 - Comprensión del problema y especificación/Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 1 | Caracterización organizacional y tecnológica | Describe el entorno por propiedades transferibles y separa lo que el equipo decide de lo impuesto | `01-caracterizacion-organizacional-y-tecnologica.md` | hecho |
| 2 | Identificación de stakeholders | Qué roles entrevistar y qué aporta cada perspectiva, con el modelo de capas de Alexander | `02-identificacion-de-stakeholders.md` | hecho |
| 3 | Protocolo de entrevistas y guiones por rol | Método de las entrevistas y los guiones por rol, con la cobertura de qué cierra cada uno | `03-protocolo-de-entrevistas.md` | hecho |
| 4 | Informe de análisis cualitativo | Convierte las entrevistas en temas (T-xx) respaldados en citas, agrupados en cinco grupos temáticos | `04-informe-de-analisis-cualitativo.md` | hecho |
| 5 | Estudio comparativo de soluciones existentes | Evalúa 8 herramientas contra los temas y extrae las brechas (B-xx) que justifican construir | `05-estudio-comparativo-de-soluciones-existentes.md` | hecho |
| 6 | Especificación de requerimientos | Traduce los temas y las brechas en RF/RNF con origen, prioridad MoSCoW y criterio de aceptación | `06-especificacion-de-requerimientos.md` | hecho |

## Bloque B. Definición del marco de referencia

Encuadra la solución y adopta los fundamentos sobre los que se modela la **familia de proyectos** que
la herramienta genera. Es el diseño de alto nivel: cómo se modela la línea como línea de producto de
software, con Domain-Driven Design, BIAN y arquitectura hexagonal.
Carpeta: `2 - Definición del marco de referencia/Documentos/`

**Log de decisiones del marco:** las decisiones estructurales viven en
`01-adr-marco-referencia.md` (en la raíz de esta fase). Los dos documentos de abajo las desarrollan;
el ADR es su registro.

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 7 | Caracterización como línea de producto de software | Encuadra la solución como LPS, declara sus cuatro elementos constitutivos, el alcance de la familia, las dos desviaciones del modelo de referencia y el mecanismo de evolución del marco | `01-caracterizacion-como-linea-de-producto-de-software.md` | hecho |
| 8 | Fundamentos adoptados (BIAN, DDD, arquitectura hexagonal) | Qué se toma y qué queda fuera de cada uno; la unidad de derivación y su criterio de granularidad; la exclusión razonada de ISO 20022 | `02-fundamentos-adoptados.md` | hecho |

**Dónde viven las reglas concretas del marco.** Las que gobiernan la forma de lo que la línea produce
—la estructura canónica y las reglas de dependencia, el contract package y las dos clases de puerto, y
el gobierno de los activos con su catálogo— viven en el documento de la fase que las construye y las
verifica: los documentos 1, 2 y 3 de la Fase 2, y el documento 2 de la Fase 3 para lo que hace válido a
un módulo. MR-01 §7 lo declara y clasifica un cambio sobre cualquiera de ellas. Una regla escrita en
abstracto y vuelta a escribir en concreto son dos fuentes de la misma verdad.

---

## Cierre de la fase

Está completa cuando los ocho documentos están en `hecho`, cada tema y cada brecha tienen su
origen en una fuente citable, y los veintidós requerimientos tienen criterio de aceptación.

**Cumplida el 2026-11-06.** Los documentos están en `hecho`, las decisiones del marco tienen su
origen declarado y comprobado por cierre transitivo.

**Dónde quedó la línea base.** Este índice advertía que convenía tomarla durante la fase, «porque el dato
es más creíble si se recoge antes de que exista la herramienta», y no se tomó a tiempo. Quedó constituida
el 2026-11-06 con la ventana cerrada, y **vive en la Fase 4**, que es donde se compara: es evidencia del
problema y la referencia de la medición, no una regla del marco ni materia prima de la especificación.

---

## Qué narra el capítulo 3 de la tesis

Esta sección existe para que el capítulo tenga una regla y no un criterio del momento. Se escribió después de que el capítulo saliera **transpuesto en lugar de destilado** —12.961 palabras y 34 tablas, el 51% de la tesis escrita— y fue la única de las cuatro fases que no la tenía, que es lo que explica aquel resultado. Con ella, y con el traslado de tres de sus secciones a la fase que las construye, el capítulo quedó en 7.344 palabras y nueve tablas.

El capítulo presenta una síntesis de dos bloques y una verificación. No reproduce los documentos de
la fase, los remite al repositorio del proyecto, que es la forma que fija `ESTANDAR-DE-REDACCION.md`
regla 1.3 desde el 15 de noviembre de 2026. **La tesis dejó de llevar anexos ese mismo día**, de modo
que lo que antes se citaba como Anexo A, B o C se remite ahora al documento de fase que lo contiene.

| Sección del capítulo | De dónde se destila |
| :---- | :---- |
| Caracterización del contexto de aplicación | Bloque A, doc 01, por propiedades transferibles |
| Identificación y justificación de stakeholders | Bloque A, doc 02, con el modelo de capas y el criterio de selección |
| Protocolo de recolección de información | Bloque A, doc 03, resumido a tipo de entrevista y cobertura alcanzada. El consentimiento y las reglas de tratamiento del material salieron del capítulo el 15 de noviembre de 2026, porque el capítulo 1 ya los declara como delimitación de confidencialidad |
| Análisis cualitativo y temas derivados | Bloque A, doc 04. Los quince temas se nombran por lo que dicen y conservan su identificador; los cinco grupos son la unidad de la que salen los requerimientos, y la tabla del capítulo muestra qué temas componen cada grupo |
| Estudio comparativo de soluciones existentes | Bloque A, doc 05. En el cuerpo, el marco de evaluación en una tabla y las tres brechas; la matriz celda por celda se remite al doc 05. Los patrones de referencia salieron del capítulo el 15 de noviembre de 2026 |
| Especificación de requerimientos | Bloque A, doc 06. En el cuerpo, el conteo de los veintidós, el criterio de priorización y qué exige cada capacidad; la ficha de cada uno se remite al doc 06. El alcance de la solución salió del capítulo el 15 de noviembre de 2026, porque el capítulo 1 ya lo transcribe del anteproyecto |
| La solución como línea de producto de software | Bloque B, MR-01, con los cuatro elementos constitutivos y las dos desviaciones declaradas. Desde el 15 de noviembre de 2026 la tabla de los cuatro elementos **contrasta tres estados** —lo que el enfoque exige, cómo estaba en el contexto y cómo se materializa en la línea—, porque la pertinencia del encuadre está en que los cuatro ya existían sin declarar |
| Fundamentos adoptados | Bloque B, MR-02, con el alcance de adopción de cada uno y la exclusión razonada de ISO 20022 |
| El cierre del marco | **No tiene sección propia.** «Qué queda acotado y qué queda abierto» salió del capítulo el 15 de noviembre de 2026 por decisión del autor, porque el `Resumen del capítulo` ya dice qué queda abierto y a qué fase va cada una de las tres reglas concretas. Lo que esa sección declaraba y no estaba en otro lugar —el modelo de características asignado a la Fase 2, y la relación entre bounded contexts como punto de extensión— lo dicen las subsecciones de la organización de la línea y de la adopción de Domain-Driven Design |
| La línea base | **No tiene sección propia.** La subsección que la anunciaba salió del capítulo el 15 de noviembre de 2026; lo que queda es la frase del protocolo que dice que las preguntas cerradas la sostienen, apuntando al capítulo 6, que es donde se narra |

**Tres secciones del capítulo cambian de capítulo.** La organización del código del proyecto generado,
los puertos y contratos de integración, y el gobierno de los core assets dejaron de ser documentos del
marco y se fundieron en la fase que las construye. Lo que el capítulo 3 narraba de ellas se narra en el
capítulo 4 —la forma del producto, el contract package y las dos clases de puerto, el catálogo y su
gobierno— y en el capítulo 5 lo que hace válido a un módulo. Los capítulos no se reescribieron en el
pase que movió los documentos, que es la regla: el mapeo se actualiza y la deuda queda anotada.
**Hecho el 12 de noviembre de 2026**, en el mismo pase que les dio su sección de hitos.

**Qué no narra el capítulo, que es la parte que faltaba.**

| Qué queda fuera | Por qué | Dónde vive |
| :---- | :---- | :---- |
| El catálogo completo de los veintidós requerimientos | El cuerpo necesita el conteo y el criterio, no la ficha de cada uno | Doc 06 del Bloque A |
| La matriz comparativa de las ocho soluciones, celda por celda | El argumento son las brechas, no la evaluación de cada eje | Doc 05 del Bloque A |
| Los patrones de referencia que cuatro soluciones aportaron al marco | El argumento del capítulo son las brechas; de dónde salió cada mecanismo es historia del diseño | Doc 05 §4 del Bloque A |
| Las tablas de reglas del marco: nomenclatura, campos y estados del catálogo, condiciones de validez | Son especificación verificable, no argumento | Los documentos 1, 2 y 3 de la Fase 2 |
| El alcance de la solución, con lo que entra y lo que queda fuera | El capítulo 1 lo transcribe del anteproyecto, y decirlo dos veces es decirlo con dos redacciones | Doc 06 §1 del Bloque A, y el capítulo 1 |
| Los guiones de entrevista por rol, el formato de consentimiento y las reglas de tratamiento del material | Es el instrumento y su protocolo ético, no el hallazgo, y el capítulo 1 ya declara la confidencialidad | Doc 03 del Bloque A |
| Las citas textuales tema por tema | El capítulo cita lo que sostiene un hallazgo, no el corpus | Doc 04 del Bloque A |
| La matriz de cada decisión hacia su origen | Es trazabilidad del expediente sobre sí mismo, y se construye al cerrar el proyecto | El documento de trazabilidad del cierre |
| El mecanismo de evolución del marco | Es una regla de mantenimiento, no un argumento del capítulo | MR-01 §7 |
| Las cuarenta y un capacidades extraídas del estándar | Es material de referencia, y cuatro de cinco entradas siguen siendo paráfrasis | El insumo de BIAN |
| La línea base medida, con su banda y su inventario de tareas | Es la referencia contra la que se compara, y se narra donde se compara | Doc 1 de la Fase 4, y el capítulo 6 |
| Los números de decisión y de documento | La tesis nombra lo que se decidió, no el registro que lo guarda | Los logs de cada fase |

**El presupuesto del capítulo.** Siete mil quinientas palabras y nueve tablas en el cuerpo, según
`Estandares/ESTANDAR-DE-REDACCION.md` Parte II.6. Lo que exceda ese techo es material de anexo o de
expediente, y esta sección dice cuál de los dos. El techo bajó de 9.500 cuando las tres reglas
concretas del marco pasaron a la fase que las construye.

**Una precisión sobre el reparto entre los capítulos 2 y 3.** El capítulo 2 **describe** las ocho
soluciones, una por una, y el 3 las **evalúa** contra un marco derivado de los temas. Son dos
actos distintos sobre el mismo objeto y ninguno de los dos repite al otro. El capítulo 3 no vuelve a
describir ninguna herramienta: la nombra y la mide.

**Lo que las rondas posteriores agregaron al capítulo**, registrado en MR-01 §7 y todavía no narrado:
**MR-01 §5** quedó refinado, porque la superficie común hace viable una plantilla única sin obligarla, y
cuántas plantillas tiene la línea es del mecanismo de derivación; la tabla de tipos de activo ganó la
plantilla con sus condiciones verificables; y la exclusión de la familia pasó de «aplicaciones
serverless» a «aplicaciones sin API HTTP expuesta». Los tres entran al capítulo cuando se reescriba.

**Las figuras del capítulo.** El marco conserva cinco: el enfoque y los mecanismos de reutilización, el
modelo de referencia instanciado, los tres fundamentos, la cadena del Service Domain al proyecto y la
arquitectura de referencia. Las de la estructura canónica, el contract package, las dos clases de puerto
y la escala de adaptación viajaron con su contenido a la Fase 2.
