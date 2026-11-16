# Fase 2 — Diseño y construcción del mecanismo de generación

Convierte el marco en algo ejecutable. Al terminar existe una CLI instalable que, con unos parámetros,
produce un proyecto backend funcional y conforme a la estructura del marco. El orden de los documentos
sigue las dependencias reales: primero existe lo que se deriva, después el mecanismo que lo deriva.

| | |
| :-- | :-- |
| **Capítulo de tesis** | `src/4-generacion-proyectos.tex` |
| **Log de decisiones** | `01-adr-mecanismo-generacion.md` |
| **Código** | `Codigo/bsl-assets` y `Codigo/bsl-catalog` |
| **Estado** | **completa.** Los cinco documentos en `hecho`. Bloque A cerrado el 2026-10-19, B el 2026-10-22, C el 2026-10-31 |

Las versiones de los activos no se declaran acá: cambian con cada ronda y la fuente es el `package.json`
de cada paquete.

Estado posible por documento: `hecho` · `en curso` · `falta`

---

## Bloque A. La forma del producto y los activos de los que se deriva

Lo que la herramienta va a consumir, y las reglas que gobiernan lo que produce. Verificable manualmente,
sin herramienta aún: si el marco tiene un problema, se descubre aquí, barato.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 1 | Variabilidad y forma del producto generado | Dónde vive cada elemento del producto, qué dependencias admite y cómo se nombra; y qué difiere entre un producto y otro, en los tres archivos declarativos que la herramienta lee | `01-variabilidad-y-forma-del-producto.md` | hecho |
| 2 | Plantillas y contratos de la línea | Qué puede ser una plantilla —manifiesto, frontera de lo expresable como dato y contrato de forma del producto— y los dos primeros activos construidos: el artefacto de contratos con sus dos clases de puerto, y la plantilla de la que se deriva un producto | `02-plantillas-y-contratos-de-la-linea.md` | hecho |
| 3 | Catálogo y gobierno de los activos | Qué hace válido a un activo, la escala de adaptación, el versionado, el catálogo con su gobernanza y su distribución, y el procedimiento de publicación | `03-catalogo-y-gobierno-de-los-activos.md` | hecho |

## Bloque B. La herramienta de línea de comandos

Un documento: el **núcleo** común a toda operación, con su punto de extensión, y la **operación de
derivación** montada sobre él. Están juntos porque el reparto entre los dos es la decisión, y separados
en dos documentos obligaba a describir dos veces la misma frontera. La Fase 3 añade operaciones sobre
ese mismo núcleo sin modificarlo.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 4 | La herramienta: núcleo y derivación | El contrato de una operación y el punto de extensión, los seis puertos, la resolución de la entrada, el plan de cambios, los códigos de salida, la superficie de comandos, el motor de plantillas y el intérprete que deriva | `04-la-herramienta-nucleo-y-derivacion.md` | hecho |

## Bloque C. Verificación y cierre de la fase

No agrega funcionalidad: produce la evidencia de que lo construido funciona y es conforme. Las pruebas
que falten se escriben aquí. Si algo falta aquí, se corrige en un documento anterior.
Carpeta: `Documentos/`

| # | Documento | Qué resuelve | Archivo | Estado |
| :-- | :-- | :-- | :-- | :-- |
| 5 | Pruebas y conformidad del proyecto generado | Las nueve comprobaciones de conformidad del producto, el arranque y las sondas en ejecución, la prueba negativa de la regla de dependencia, el barrido de configurabilidad, las puertas del repositorio y la evidencia fechada | `05-pruebas-y-conformidad.md` | hecho |

---

## Cierre de la fase

**Condición de llegada, comprobada el 2026-10-31 por `check:push`:** un comando produce un producto que
arranca sin que nadie edite un archivo, supera su análisis estático con la regla de dependencia activa
—comprobada con una prueba negativa— y declara con qué versión del activo fue derivado. La evidencia, con
comando y fecha, está en el doc 5 §10; el estado de cada requerimiento se consolida al cerrar el
proyecto, en un documento propio.

**Requerimiento no satisfecho al cerrar:** RF-04, la documentación OpenAPI del producto, excluido por
decisión de alcance y construido después, en la ronda que lo reasignó. Su decisión y su construcción
viven hoy en el doc 2 §12, porque es una pieza de la plantilla. RNF-02 y RNF-06 quedaron satisfechos a
medias por la misma frontera: su otra mitad necesita las operaciones que la Fase 3 introduce.

---

## Fuera del alcance

| Queda fuera | Razón |
| :---- | :---- |
| Incorporación de módulos a un producto, al derivar o después | El marco trata generar y componer como operaciones distintas sobre el mismo mecanismo. Dividir la composición entre dos fases duplica el trabajo sin completar la operación |
| Construcción de módulos del catálogo | La composición se valida en la Fase 3, que es donde el módulo tiene función |
| Actualización y propagación sobre productos existentes | Requiere más de una versión publicada de un activo consumido |
| Selección entre implementaciones alternativas de una misma capacidad al derivar | El marco asignó las capacidades técnicas a los módulos, no a variantes de la plantilla |
| Despliegue, infraestructura y entrega continua | Excluidos en la especificación de requerimientos |

**Dónde cae la superficie de operación.** Que el despliegue quede fuera no deja fuera lo que el producto
expone para ser operado. Las sondas de salud son del producto: viven en su código, se versionan con él y
responden aunque nadie lo haya desplegado todavía. El orquestador que las consulta, su configuración y su
calendario de reinicios son del despliegue, y ésos sí quedan fuera.

**Una exclusión que se levantó.** La fase excluyó construir más de un activo base, con dos razones: que
un segundo activo no aporta evidencia nueva sobre el mecanismo, y que es crecimiento del catálogo. La
primera resultó falsa —con una sola plantilla, un intérprete genérico y una función escrita para ese caso
se comportan igual— y hoy la línea tiene dos plantillas publicadas más un fixture de otra familia, que
son las dos clases de evidencia del doc 2 §16. La segunda sigue en pie: cuántas plantillas tiene el
almacén es una decisión de crecimiento.

Lo diferido se registra como punto de extensión y no como limitación de la solución.

---

## Qué narra el capítulo de la tesis

La fase se destila en `src/4-generacion-proyectos.tex`. Lo fundamental, no el expediente: el capítulo
narra qué se construyó y por qué, y remite a los documentos de implementación para el paso a paso.

| Sección del capítulo | De dónde se destila |
| :-- | :-- |
| Alcance del mecanismo y frontera entre fases | este índice |
| La forma de un producto de la familia: capas, dependencias verificables y frontera del contrato externo | Doc 1 §1 a §4, con la figura de la estructura canónica |
| Variabilidad de la línea: qué difiere entre un producto y otro | Doc 1 §5 a §13, con sus dos figuras |
| Puertos y contratos de integración | Doc 2 §5, con las dos clases de puerto y el contract package como artefacto neutral |
| La plantilla como validación del marco | Doc 2 §6 a §11, con el argumento de que un activo ejecutable prueba el marco antes de que exista la herramienta |
| El almacén de plantillas: manifiesto, frontera de lo expresable como dato y contrato de forma | Doc 2 §1 a §4 y §15 a §16. La evidencia de genericidad se narra por lo que demuestra, en sus dos formas |
| Gobierno de los activos, catálogo y distribución | Doc 3 |
| Arquitectura de la herramienta: núcleo, puertos y punto de extensión | Doc 4 §1 a §11, con la figura del contrato de operación |
| La operación de derivación y el motor | Doc 4 §12 a §14, con la figura de la derivación de una operación y la del activo como salida de sus plantillas |
| La documentación de API del producto | Doc 2 §12, resumido |
| Verificación y conformidad | Doc 5, citando la evidencia y no reproduciéndola |
| Instalación y uso | `packages/cli/TUTORIAL.md`, resumido: el capítulo no es un manual |
| Cobertura de requerimientos y decisiones | El documento de trazabilidad del cierre |

**Qué no narra el capítulo.** El inventario de archivos de la plantilla y el catálogo de su manifiesto,
que son especificación; las transcripciones de salida de terminal, que son evidencia fechada; las tablas
de exenciones de cobertura; y los números de decisión y de documento.

**Qué de las rondas posteriores no entra al capítulo 4.** Lo del lado de los módulos —que un módulo
declara a qué forma de producto sirve, y que quitar un módulo restaura lo que la derivación escribió— se
narra en el capítulo 5, y lo dice el índice de la Fase 3.

**Por qué queda anotado y no escrito.** La tesis se escribe al cerrar una fase, nunca en paralelo
(`GUIA-DE-TRABAJO.md` Parte VI). La deuda vive en `PENDIENTES.md`.
