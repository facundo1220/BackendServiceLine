# Fase 3 — Diseño y construcción del gestor de módulos reutilizables

Convierte el mecanismo de derivación en un mecanismo de composición. Al terminar, un producto ya
derivado incorpora una capacidad transversal del catálogo con un comando, la declara en su registro, y
puede consultarla, actualizarla y quitarla sin que nadie edite archivos a mano ni pierda el código propio
del equipo. El orden de los documentos sigue las dependencias reales: primero existe el activo que se
compone, después las operaciones que lo componen, después la verificación.

| | |
| :-- | :-- |
| **Capítulo de tesis** | `src/5-gestor-modulos.tex` |
| **Log de decisiones** | `01-adr-gestor-de-modulos.md` |
| **Código** | `Codigo/bsl-assets` y `Codigo/bsl-catalog` |
| **Estado** | **completa el 2026-10-31**, con sus documentos en `hecho`. El `packages/cli/TUTORIAL.md` se agregó el 2026-11-09 |

Estado posible por documento: `hecho` · `en curso` · `falta`

---

## Bloque A. El activo que se compone

Qué capacidad se construye y qué forma tiene un módulo. Verificable sin la operación: si el marco falla
al construir un módulo real, se descubre acá, antes de que exista el comando que lo incorpora.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Requisitos | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | Capacidades transversales y la capacidad elegida | Identifica y categoriza las doce capacidades transversales, fija su relación con BIAN y su límite, y **elige la que esta fase construye** con sus alternativas descartadas y el orden de crecimiento del catálogo | RF-09 | `01-capacidades-transversales.md` | hecho |
| 2 | El módulo: anatomía, reglas de composición y construcción | El módulo como artefacto —paquete, manifiesto, frontera entre lo empaquetado y lo generado, puntos de inserción, las nueve reglas y la entrada del registro del producto— y el módulo real construido, con su puerto técnico, su adaptador y su plantilla | RF-07, RF-09, RF-10, RF-14, RF-16 | `02-el-modulo-anatomia-composicion-y-construccion.md` | hecho |

## Bloque B. Las operaciones del gestor

Se montan sobre el núcleo de la Fase 2 sin modificarlo, que es la razón por la que ese núcleo se
construyó aparte.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Requisitos | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- | :-- |
| 3 | Las operaciones del gestor | Incorporar, consultar, actualizar y quitar: resolución del activo, análisis del producto, plan de cambios, ediciones que no sobrescriben código propio, escritura en el registro, criterio de preservación y mensajes de rechazo | RF-06, RF-07, RF-08, RF-10, RF-11, RF-12, RF-13 | `03-las-operaciones-del-gestor.md` | hecho |

## Bloque C. Verificación y cierre de la fase

No agrega funcionalidad: produce la evidencia de que lo construido funciona y es conforme. Rige el mismo
principio del Bloque C de la Fase 2: la verificación no modifica lo verificado.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 4 | Verificación de la composición | El circuito completo sobre un producto real, los ocho rechazos comprobados rompiéndolos, qué significa que el producto compuesto es conforme, las puertas y la evidencia fechada | `04-verificacion-de-la-composicion.md` | hecho |

**Qué se movió a la Fase 2.** La documentación OpenAPI del producto fue el documento 4 de este bloque A
mientras RF-04 estaba reasignado acá. Es una pieza de la plantilla y no del gestor —un documento de API
describe la superficie de entrada del producto, y un módulo no aporta adaptadores de entrada—, así que
vive en el doc 2 §12 de la Fase 2, con la decisión que lo resolvió.

---

## Qué abre la fase

Cuatro insumos, todos existentes. Ninguno se vuelve a producir acá.

| Insumo | Dónde | Qué aporta |
| :-- | :-- | :-- |
| Frontera funcional entre las fases | El índice de la Fase 2 | El núcleo y el punto de extensión son de la Fase 2; las operaciones de composición, consulta, actualización y remoción son de acá |
| Puntos de extensión construidos y verificados | Los documentos de la Fase 2 | Contrato de operación y registro estático, los seis puertos del núcleo, los puertos técnicos del producto, el arreglo de módulos del registro, el tipo de activo del catálogo y la resolución de activos por identificador |
| Revisión externa del artefacto | `Fase 4 .../Insumos/seguimiento-de-mejoras.md` | Nueve temas con su triage, separados en comprometidos y candidatos. No es un backlog: un candidato entra solo si un requisito lo sostiene |
| Requerimientos diferidos a esta fase | Fase 1, doc 06 | RF-06 a RF-09 y RF-11 a RF-13, más la mitad pendiente de RF-10, RNF-02 y RNF-06 |

---

## Frontera con la Fase 4

La Fase 4 evalúa; no construye. La frontera se traza antes para que la evaluación no termine completando
el artefacto.

| Elemento | Fase | Criterio |
| :-- | :-- | :-- |
| Operaciones de composición, consulta, actualización y remoción | 3 | Son el objeto de la fase |
| El módulo de RF-09 y el crecimiento del contract package | 3 | Sin un módulo real la composición no es verificable |
| Evidencia ejecutable de que la composición funciona | 3 | Es la condición de llegada, no un resultado de la evaluación |
| Línea base medida de proyectos existentes | 4 | Es evidencia del problema y la referencia contra la que se compara, no del artefacto: vive donde se usa, como doc 1 de la Fase 4 |
| Medición del tiempo de incorporación de un módulo | 4 | Requiere el gestor terminado |
| Catálogo poblado con las demás capacidades identificadas | Trabajo futuro | RF-09 exige un módulo, no el catálogo completo, y está declarado así en su criterio de aceptación |

---

## Convenciones de esta fase

- **Diagramas:** prefijo `GM-`, en `Insumos/Diagramas/`, con el patrón `GM-0N_figM_descripcion_corta.svg`,
  donde `N` es el número del documento al que la figura pertenece. Identidad visual según
  `Estandares/ESTANDAR-DE-DIAGRAMACION.md`.
- **Uso del gestor:** sin documento propio. Lo que alguien necesita saber para operar las operaciones
  nuevas vive en el README de `@bsl/cli` y en `packages/cli/TUTORIAL.md`. El reparto está decidido: el
  README es dueño del cómo, el documento de fase del camino y del por qué.
- **Código sin commits:** el código se construye y se verifica en `Codigo/`; confirmar y publicar es del
  autor, no de la asistencia.

---

## Cierre de la fase

**Condición de llegada.** Un producto ya derivado incorpora un módulo del catálogo con un comando, sigue
arrancando sin que nadie edite un archivo y superando su propia verificación, su registro declara el
módulo y la versión incorporada, y publicada una versión posterior del módulo la herramienta la detecta,
la aplica y deja intacto el código propio del equipo. Cada parte se comprueba por comando en el doc 4.

**Lo que la fase deja probado sobre el marco.** Tres afirmaciones del marco dejaron de ser declaraciones
y pasaron a ser hechos comprobables por comando:

- **El contract package sostiene el desacoplamiento.** Producto y módulo dependen de él y ninguno del
  otro, y cambiar el motor de persistencia no altera ninguna declaración de la capa de dominio.
- **La frontera entre lo empaquetado y lo generado es operable.** La implementación viaja en el paquete,
  el cableado se genera, y la herramienta puede distinguir uno de otro meses después gracias a la huella
  y a las regiones nombradas.
- **La escala de adaptación tiene consecuencia.** Editar el adaptador generado es sustituir el adaptador:
  el equipo conserva su código y el módulo sigue propagándose.

La cuarta —la convivencia de versiones distintas del mismo módulo entre productos, que es el criterio
literal de RNF-06— no quedó probada al cerrar la fase, y no por una falla del mecanismo sino porque
exigía publicar. Se comprobó después, por ejecución, con el paso del circuito que incorpora el mismo
módulo a un segundo producto.

---

## Fuera del alcance

| Queda fuera | Razón |
| :-- | :-- |
| Construir el resto del catálogo de capacidades transversales | RF-09 pide un módulo y declara el resto como crecimiento. El doc 1 deja la categorización escrita, que es lo que permite construirlas después sin volver a decidir |
| Un módulo de dominio alineado a BIAN | Declarado trabajo futuro en la Fase 1. El catálogo de esta línea agrupa capacidades técnicas |
| Retiro de un activo del catálogo y migración de sus consumidores | Declarado trabajo futuro en la Fase 1. Retirar un **módulo incorporado de un producto** es otra cosa, y sí está construido |
| Resolución automática de un conflicto sobre cableado modificado | La herramienta detecta e informa; decidir qué prevalece es del equipo dueño del producto (RNF-02) |
| Más de un adaptador por puerto en un producto | El marco lo restringe explícitamente y declara que la restricción puede levantarse después sin invalidar nada |
| Completar el espacio de selección con el resto del subconjunto de Service Domains | Es transcripción del documento oficial de cada capacidad, no trabajo del mecanismo |
| Documento propio de instalación y uso | Lo resuelven el README de `@bsl/cli` y su tutorial, según el reparto decidido |

---

## Qué narra el capítulo de la tesis

| Sección de `src/5-gestor-modulos.tex` | De dónde se destila |
| :-- | :-- |
| Alcance de la fase y frontera con la evaluación | este índice |
| Qué capacidades transversales existen y cuál se construyó | Doc 1, con el criterio de elección y lo descartado |
| Qué es un módulo: contrato, manifiesto y frontera entre lo empaquetado y lo generado | Doc 2 §1 a §8, con la figura del paquete al producto |
| El módulo de persistencia como caso de referencia del marco | Doc 2 §9 a §13, con la figura de las dos clases de puerto |
| A qué forma de producto sirve un módulo | Doc 2 §6, con la regla que rechaza antes de tocar nada |
| El gestor: composición, consulta, actualización y remoción | Doc 3, con la figura del camino de la composición |
| El segundo módulo del catálogo, y lo que prueba del mecanismo | Doc 2 §14 |
| Verificación y conformidad | Doc 4, citando la evidencia sin reproducirla |
| Cobertura de requerimientos y decisiones | El documento de trazabilidad del cierre |

**Qué de las rondas posteriores no entra al capítulo 5.** El almacén de plantillas, el manifiesto de una
plantilla, el motor y el intérprete se narran en el capítulo 4, y lo dice el índice de la Fase 2.

**Por qué queda anotado y no escrito.** La tesis se escribe al cerrar una fase (`GUIA-DE-TRABAJO.md`
Parte VI). La deuda vive en `PENDIENTES.md`.
