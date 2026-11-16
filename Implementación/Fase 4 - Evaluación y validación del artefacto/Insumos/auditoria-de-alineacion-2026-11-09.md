# Auditoría de alineación de punta a punta

> **Instantánea del 2026-11-09.** Todas las cifras son las de ese día. **Las supera el pase de reescritura del expediente del 2026-11-10**, que cambió el conteo de archivos, el de bloques transcritos y el de notas fechadas.
> Lo que vale de forma permanente son los hallazgos y su veredicto; los conteos se vuelven a medir
> corriendo las herramientas de `Estandares/herramientas/`.

El barrido completo del proyecto —las cuatro fases del expediente y los dos
repositorios de código— hecho el 2026-11-09, después de las ocho rondas de mejoras del día y antes de
ejecutar la evaluación. No repite la auditoría de cierre del 2026-11-07: aquélla comprobó que la cadena
de trazabilidad y el encuadre se sostenían; ésta comprueba que **lo construido ese día no dejó
contradicciones**, que es el riesgo que ocho rondas en una jornada crean.

**Método.** Comprobación mecánica donde se puede comprobar —scripts sobre los archivos, y ejecución de
los dos circuitos y de cada suite— y lectura cruzada donde hay que juzgar. La regla de juicio es la que
el proyecto ya usaba: **una nota fechada que registra lo que fue cierto en su fecha no es una
contradicción; una afirmación en presente que ya no se cumple, sí.** Separar las dos es la mitad del
trabajo de este barrido, porque el expediente conserva su texto de cierre a propósito.

**Qué se buscaba.** Que el marco, el mecanismo de generación, el gestor de módulos y el diseño de la
evaluación digan lo mismo sobre las mismas cosas: cuántas plantillas hay y qué es una, cuántos módulos y
a qué sirven, qué versiones existen y cuáles están publicadas, y cuántos requerimientos están cumplidos.

---

## 1. Integridad del sistema de decisiones

| Comprobación | Resultado |
| :---- | :---- |
| Numeración global continua, sin huecos ni duplicados | **198 decisiones**, numeradas de 1 a 198. Ninguna falta, ninguna se repite |
| Los cuatro índices coinciden con las entradas de su log | **Coinciden exactamente.** Fase 1 con 43, Fase 2 con 100, Fase 3 con 47, Fase 4 con 8 |
| Ningún ADR citado en el expediente que no exista | **Ninguno.** Las citas de las cuatro fases, de `CLAUDE.md` y de `PENDIENTES.md` resuelven todas |
| El reparto por fase sigue la regla —cada decisión al log de la fase cuyo artefacto toca— | **Se sostiene.** Las dos últimas fueron a la Fase 2 porque tocan el recorrido y el reporte de la herramienta; la de la familia quedó en la Fase 1 porque el artefacto que decide es MR-01 |

## 2. Integridad del expediente

| Comprobación | Resultado |
| :---- | :---- |
| Las citas de documento por nombre de archivo resuelven | **51 citas, las 51 resuelven** |
| Los enlaces a archivos —diagramas, documentos, código— resuelven | **32 enlaces, ninguno roto.** Esto importaba esta vez: la plantilla se movió a `packages/templates/` y el renombre pudo dejar enlaces colgando |
| Los identificadores tienen consumidor | **Completo.** 15 `T-xx`, 12 `N-xx`, 3 `B-xx`, 16 `RF-xx`, 6 `RNF-xx`, 4 `PE-xx` y 8 `MR-xx`, todos citados en dos o más documentos |
| `MR-07`, que aparece en un solo documento | **No es huérfano.** Es el registro del remapeo del 2026-09-14, cuando el marco pasó de siete items a seis. Los seis existían a esta fecha |

## 3. Lo que el expediente afirma del código, contra el código

Comprobado ejecutando, no leyendo.

| Afirmación | Comprobación | Resultado |
| :---- | :---- | :---- |
| Siete paquetes con sus versiones | `package.json` de cada uno | `@bsl/contracts` 0.3.0, `@bsl/cli` **0.32.0**, `@bsl/nestjs-hexagonal-api` 0.21.0, `@bsl/azure-functions-api` 0.1.0, `@bsl/persistence` 0.4.0, `@bsl/observability` 0.2.0, `@bsl/catalog` **0.6.0** |
| El total de pruebas | Ejecutadas una por una | **505**: 2 del contrato, 12 de persistencia, 36 de observabilidad, **350 de la herramienta** y 105 del producto de referencia. Más las **4** del producto que deriva la plantilla de Azure, que corren en su propia verificación |
| El producto de referencia entrega 62 archivos | Contados | **62** |
| El circuito de generación deriva tres productos de 68, 40 y 43 archivos | `verify:generation` | **Verde, y los tres conteos exactos.** Cada uno pasa su propia verificación, y los cuatro `new` del circuito **nombran la plantilla** de la que derivan |
| El circuito de composición tiene 22 pasos y 8 rechazos | `verify:composition`, y el conteo de la enumeración del doc 7 de la Fase 3 | **Verde.** **8** aserciones de rechazo en el script y **22** filas en la enumeración del documento: coinciden |
| El catálogo tiene cinco entradas, dos de ellas plantillas | `catalog.json` | **Cinco**, todas en `active`: un `contract-package`, **dos `template`** y dos `module` |
| Las dos plantillas declaran su forma | `bsl-template.json` de cada una | `nestjs-hexagonal@1` con 8 puntos de inserción, 2 puertos y 4 supuestos; `azure-functions@1` con 5, 2 y 7 |
| Los dos módulos declaran a qué forma sirven | `bsl-module.json` de cada uno | Los dos en esquema `1.1` y los dos con `serves: [nestjs-hexagonal@1]`. **Ningún módulo del catálogo sirve la forma de Azure**, que es lo que la plantilla declaró y lo que el circuito comprueba rechazando |
| `check:push` en verde | Ejecutado | **Código 0**, cero vulnerabilidades, prettier limpio |

## 4. El lado del código, revisado aparte

| Comprobación | Resultado |
| :---- | :---- |
| Ninguna afirmación de versión vencida en los markdown de `Codigo/` | **Cero discrepancias** sobre 15 archivos. Los ocho READMEs, el tutorial y los dos índices de almacén dicen la versión que el `package.json` dice |
| El índice del almacén nombra las dos plantillas | **Sí**, con su convención de nombres y el procedimiento de agregar una |
| El credencial del feed no puede commitearse | **`.npmrc` está en `.gitignore`, no rastreado y sin aparecer en ningún commit.** El `.npmrc.example` no lleva token |
| Bloques transcritos del código en el expediente | **31 divergentes y 8 sin resolver** de 89 comparados, que es exactamente lo que **P-58** registra. No creció con las rondas del día: los tres bloques que se movieron se retranscribieron en el mismo pase |

## 5. La línea lógica, de principio a fin

Lo que se leyó cruzado, porque no se comprueba con un script. La cadena que el proyecto declara es
`T/N` → `B` → `RF/RNF` → `ADR` → `MR/MG/GM` → código → tesis, y lo que se verificó es que los cuatro
conceptos que las rondas del día movieron dicen lo mismo en todos los eslabones.

| Concepto | Dónde se define | Dónde se usa | Coherente |
| :---- | :---- | :---- | :---- |
| **Qué es una plantilla** | MR-05 §1, que ya trae la fila `Plantilla` y la condición de declarar la forma del producto | Fase 2 doc 7 (anatomía), `bsl-template.json`, `bsl templates list` | **Sí.** El marco describe por tipo y sin cardinalidad, que es lo que permitió la segunda plantilla sin tocarlo |
| **La forma del producto como contrato** | Fase 2 doc 7 | Fase 3 doc 2 (lo que un módulo compara), `product-shape.ts`, la regla 0 de `compose` | **Sí**, y es ejecutable: la composición rechaza por forma antes de resolver un punto |
| **Que la familia admite más de un modelo de ejecución** | La revisión de la exclusión, que refina MR-01 §5 | Fase 1 doc 06, el índice de la Fase 2, la plantilla de Azure | **Sí.** La exclusión quedó reescrita como «aplicaciones sin API HTTP expuesta», y la declaración de la familia no cambió una palabra |
| **Que un módulo no sirve a toda la línea** | La segunda plantilla y la nota del 2026-11-09 en Fase 3 doc 2 | El `serves` de los dos módulos, el rechazo del circuito, el tutorial | **Sí.** Ningún documento afirma que un módulo entre en cualquier producto |

## 6. Hallazgos

Cinco, **todos de estado y ninguno de fondo**: nada de lo construido contradice al marco ni a los
requerimientos; lo que había eran afirmaciones de estado que las rondas del día dejaron atrás. **Los
cinco quedaron corregidos en este mismo pase.**

| # | Hallazgo | Dónde | Corregido |
| :-- | :---- | :---- | :---- |
| **A-01** | El índice de la Fase 2 afirmaba «**ninguna publicada todavía**» cuando los seis activos están en el feed desde esa mañana, y además daba la herramienta en `0.30.0` y el catálogo en `0.5.0`. Es el peor de los cinco porque invierte el hecho que condiciona la evaluación | Fase 2, `00-indice-de-fase.md` | **Sí**, con las versiones vigentes, P-C48 y lo que queda en P-63 |
| **A-02** | La condición de llegada de la Fase 4 pedía «los **cinco** activos publicados» y apuntaba a P-C40 y P-C43. Son **seis** desde la segunda plantilla, y el pendiente que lo cerró es **P-C48** | Fase 4, `00-indice-de-fase.md` | **Sí**, nombrando los seis y lo que falta publicar |
| **A-03** | La tabla «El conteo» de la medición decía 19 cumplidos y 2 a medias, y **la nota inmediatamente debajo decía 20 y 1**. La tabla no estaba fechada, así que se leía como vigente y se contradecía con su propia página | el seguimiento de mejoras | **Sí.** El conteo vigente queda arriba y el del 2026-11-03 se conserva fechado debajo |
| **A-04** | La celda de **RNF-06** terminaba afirmando «vuelve a *a medias*» y «el feed sirve las anteriores (P-50)», mientras su propio veredicto decía `cumplido` y dos notas posteriores lo daban por comprobado por ejecución | el seguimiento de mejoras | **Sí.** La celda cierra con la evidencia por ejecución y con P-C48 |
| **A-05** | El encabezado de `PENDIENTES.md` describía lo publicado con la herramienta en `0.30.0` y no mencionaba `0.32.0` ni este barrido | `PENDIENTES.md` | **Sí** |

**Lo que une a los cinco.** Ninguno es un error de razonamiento: los cinco son el mismo tipo de dato
—qué versión, cuántos activos, cuántos requerimientos— escrito en un lugar que no se volvió a mirar al
moverlo en otro. Es el costo de ocho rondas en un día, y es barato de pagar mientras el proyecto siga
teniendo un lugar donde cada cosa es la fuente de verdad.

## 7. Lo que la auditoría no encontró

Vale escribirlo, porque la ausencia de hallazgos en estos frentes es un resultado y no un vacío.

- **Ninguna contradicción entre el marco y lo construido.** MR-01 a MR-05 describen la línea que el
  código es, incluidas las dos cosas que el día movió: que una plantilla es un activo del catálogo con
  su propio manifiesto, y que la forma del producto es un contrato.
- **Ningún requerimiento con dos veredictos distintos** en dos documentos, una vez corregido A-03.
- **Ningún enlace ni cita roto** por el renombre de `@bsl/base-template`, que era el riesgo mecánico más
  probable del día.
- **Ningún identificador huérfano** en la cadena completa.
- **Ninguna afirmación de versión vencida dentro de `Codigo/`**, que es lo que un desarrollador lee.
- **Ningún credencial en riesgo de commit.**

## 8. Lo que queda, y no lo arregla un barrido

| Qué | Dónde vive |
| :---- | :---- |
| Publicar `@bsl/catalog` `0.6.0` y `@bsl/cli` `0.32.0`. Hasta entonces el feed sirve una herramienta que **rechaza** en vez de preguntar por la plantilla, y ofrece una sola | **P-63** |
| Los 31 bloques transcritos divergentes y los 8 sin resolver, de los que 8 piden reescribir el doc 5 §8 de la Fase 2 y no retranscribirlo | **P-58** |
| Siete diagramas que ahora **contradicen** a su documento, porque dicen `@bsl/base-template` | **P-11**, que creció por contenido y no por forma |
| Lo diferido de la sexta ronda, seis puntos | **P-60**, reducido en su parte dañina |
| La deuda de narración de la tesis, capítulos 1, 3, 4, 5 y 6 | **P-42**, **P-53**, **P-61** |
| Comparar lo construido contra el compromiso del anteproyecto como paso de cierre de cada fase | **P-62**, que es el hueco de método que la auditoría del 2026-11-09 encontró |

## 9. Conclusión

El proyecto está alineado de punta a punta. Las ocho rondas del día **no rompieron la línea lógica**:
el marco sigue describiendo lo construido, la cadena de trazabilidad no tiene eslabones sueltos, los
requerimientos tienen un solo veredicto cada uno, y las siete afirmaciones del expediente sobre el
código coincidieron al ejecutarlas, conteos incluidos. Lo que se encontró —cinco afirmaciones de estado
vencidas— quedó corregido en el mismo pase.

**Lo único que bloquea por orden de ejecución es P-63**, y no por ventana de tiempo: la plantilla
hexagonal, que es la que la sesión de evaluación usa, está activa y publicada. Lo que la publicación
pendiente cambia es que el evaluador vería la herramienta **con** la pregunta de la plantilla y **con**
los pasos leídos del producto, que son las dos correcciones que los reportes de uso del autor
produjeron hoy.
