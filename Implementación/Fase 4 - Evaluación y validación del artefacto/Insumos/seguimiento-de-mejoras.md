# Seguimiento de las mejoras de la revisión externa

El registro antes/después de la revisión externa del 2026-10-28: para cada hallazgo de ese informe,
en qué estado estaba el artefacto cuando el revisor lo usó, en qué estado está hoy, qué grupo de
mejora lo cierra y con qué evidencia se puede afirmar.

**No es un backlog.** Un grupo de mejora entra porque el artefacto dice de sí mismo algo falso o
incompleto, porque un criterio verificable del informe falla por poco, o porque una propuesta del
informe tiene mérito y nadie la había juzgado por mérito. Lo que no entra queda con su argumento
escrito en la última sección.

**Dónde van los ADR de estas mejoras.** Al log de la fase cuyo artefacto toca cada uno, con
numeración global continua. Lo que toca el activo base o la herramienta va al log de la Fase 2; lo que
toca el manifiesto de un módulo o la composición, al de la Fase 3.

**Las fuentes son dos:** el informe original, en esta misma carpeta, y este documento. El triage que
la Fase 3 usó para decidir qué entraba se retiró el 2026-11-02, porque era una compuerta de alcance
que se leía como veredicto de mérito; lo que decía quedó absorbido en el tablero maestro.

## Cómo se lee

| Estado | Qué significa |
| :-- | :-- |
| `resuelto antes` | Ya estaba resuelto en el repositorio el día de la revisión, pero no en la versión que el revisor tenía instalada |
| `resuelto` | Construido después de la revisión, con su ADR y su comprobación |
| `parcial` | Una parte construida y la otra declarada fuera con argumento, o pendiente de un grupo |
| `abierto` | Ni construido ni descartado. Tiene grupo asignado o razón de por qué no lo tiene |
| `en curso` | Grupo en construcción |
| `excluido` | Descartado con argumento escrito |

**Qué cuenta como evidencia.** Un comando con su salida, o un archivo con su línea, o un ADR. Una
afirmación no cuenta. Ningún hallazgo pasa a `resuelto` sin una fila en la bitácora de §7.

## El antes, fijado

El triage de la Fase 3 dice que la revisión se hizo sobre "una versión anterior a las decisiones de
078". Eso no sirve como línea de partida, así que se fijó contra el historial del repositorio.

| Qué | Valor |
| :-- | :-- |
| Fecha de la revisión | 2026-10-28 |
| Versiones publicadas en el feed ese día | `@bsl/cli` **0.2.1**, `@bsl/base-template` **0.1.0**, `@bsl/contracts` 0.1.0, `@bsl/catalog` 0.1.0, publicadas el 2026-10-21 |
| Productos sobre los que se ejerció | PoC propio del revisor: `bolsillos-w` y `user-update-flow` |
| Perfiles de la evaluación | Desarrollador backend y líder de producto |
| Versiones hoy | `@bsl/cli` **0.8.0**, `@bsl/base-template` **0.7.0**, `@bsl/contracts` 0.2.0, `@bsl/persistence` 0.1.0 |

El antes/después de este seguimiento es, entonces, **0.2.1 a 0.8.0**.

**Tres hallazgos ya estaban resueltos, y el revisor no pudo verlos.** Las sondas de salud, la carpeta
propia por rol que multiplica y el paso a NestJS 12 entraron al repositorio el mismo 2026-10-28,
después de la versión instalada, y se publicaron el 2026-10-29 en `@bsl/base-template` 0.5.0 y
`@bsl/cli` 0.6.0. Eso no invalida los hallazgos: confirma desde fuera que eran huecos
reales. Y deja una lección que condiciona la segunda revisión: **se hace sobre una versión
publicada**, o mide un artefacto que nadie podría instalar.

## Tablero maestro

Los catorce hallazgos del informe, más los cinco huecos que la verificación del 2026-11-02 encontró
al volver a pasar la revisión por el artefacto terminado. El estado de la columna «Hoy» se verificó
leyendo el código, no los documentos.

| ID | Hallazgo | Antes (0.2.1) | Hoy (verificado el 2026-11-02) | Estado | Grupo | Evidencia |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 1 | Estructura inicial demasiado plana | Casos de uso y eventos en carpetas planas | Carpeta propia por rol que multiplica | `resuelto antes` | — | `template/src/domain/party-reference/events/`, `application/initiate-party-reference/`, `infrastructure/http/requests/` |
| 2 | Feedback insuficiente del CLI | El rechazo mostraba el patrón, sin formato ni ejemplo | Formato, ejemplo y valor recibido en el rechazo, y el ejemplo en la ayuda | `resuelto` | — | `cli/src/core/input/input-resolver.ts:166` |
| 3 | Catálogo ligado a productos | Dos Service Domains; la selección parecía elegir producto | Siguen dos, y la transcripción de las otras cuarenta y cuatro necesita el portal del estándar. G4 corrigió lo que sí era del proyecto: las dos entradas declaraban una Business Area que el estándar no tiene | `en curso` | G4 | queda abierto, con su hoja de trabajo en `Fase 2 .../Insumos/transcripcion-del-service-landscape.md` |
| 4 | Desalineación entre capability y negocio local | `bolsillos-w` con agregado `Bolsillo` y metadata `Term Deposit`, sin explicación | El README explica el mapeo cuando los nombres difieren, y el registro guarda los dos | `resuelto` | — | `cli/src/operations/generate/derive.ts:485` |
| 5 | Aggregate demasiado genérico | Semilla de `id`, `name` e `initiatedAt` sin declararse como semilla | El README declara que es una semilla técnica. Perfiles de agregado y wizard, descartados | `parcial` | — | `README.md.tpl`, sección «What this product is». Perfiles: §8 |
| 6 | Bootstrap habilitador vs producto terminado | Nada fuera del código decía que el resultado era un habilitador técnico | El README abre declarándolo y lista el estado de cada operación | `resuelto` | — | `README.md.tpl` |
| 7 | Documentación insuficiente del producto | README de estructura y rutas | README con propósito, alcance, estado por operación, persistencia, eventos, ejemplos, verificación y procedencia. Documentación por audiencia, descartada | `parcial` | — | Por audiencia: §8 |
| 8 | Falta de Swagger y prueba inmediata | Ni OpenAPI ni ejemplos ejecutables | `GET /openapi.json` sin configuración, armado con los esquemas de validación del producto, y ejemplos `curl` en el README. Interfaz de exploración y colección, descartadas | `resuelto` | — | `template/src/infrastructure/http/openapi.controller.ts`. **Cerrado del todo el 2026-11-06 (G12, ):** el producto sirve `GET /docs` con el visor de OpenAPI instalado en él |
| 9 | Observabilidad y logging insuficientes | Logger JSON, sin log de arranque ni registro de requests | Log de arranque, dos formas de log, y una entrada por request con método, ruta, status, duración e identificador, que además viaja a toda entrada escrita durante esa request. ~~Correlación entre servicios y métricas siguen en el módulo~~. **Cerrado el 2026-11-05**: la correlación entre servicios entró al activo base con la traza del estándar W3C, y las métricas y la exportación con el módulo `@bsl/observability` (). Nada de este hallazgo queda del lado del catálogo | `resuelto` | G2, **G11** | `request-logging.interceptor.ts`, `request-context.ts`, `telemetry.ts` |
| 10 | Falta de health y readiness | Sin sondas | `GET /health/live` y `GET /health/ready`, con el criterio de lo que la sonda no expone | `resuelto antes` | — | `template/src/infrastructure/http/health.controller.ts` |
| 11 | Persistencia en memoria poco visible | `Map` en proceso, sin aviso | Aviso en el README y módulo `@bsl/persistence` con motor relacional real, incorporable y actualizable. Selector en `bsl new`, descartado | `resuelto` | — | — |
| 12 | Scaffold versus funcionalidad real | Una operación de andamio devolvía la entidad sin decir que no tenía efecto | El README marca `implemented` o `scaffold` por operación, el registro lo guarda y `bsl status` lo cuenta. `501`, descartado | `resuelto` | G1 | `derive.ts`, `project.json.tpl`, `status.operation.ts` |
| 13 | Tests planos y poca correspondencia con `src` | `test/` plano | Igual, por decisión: una jerarquía para tres archivos de ejemplo es ruido | `excluido` | — | — |
| 14 | Falta de pruebas de integración HTTP | Sin ninguna | Todo producto trae `test/http-smoke.spec.ts`: arranca la aplicación y pide a cada ruta una respuesta por HTTP. Corre dentro de su `npm run verify`. Las e2e siguen descartadas | `resuelto` | G3 | `http-smoke.spec.ts.tpl` y sus seis fragmentos, `verify-generation.mjs` |
| H-1 | El README del producto compuesto sigue declarando persistencia en memoria después de `bsl add persistence` | No aplicaba: no había módulos | El módulo declara su nota en una región del README, y el circuito comprueba que el aviso de pérdida de datos ya no está y que el adaptador generado queda nombrado | `resuelto` | G1 | `bsl-module.json`, `README.md.tpl`, `plan-writer.ts`, `verify-composition.mjs` |
| H-2 | El log de arranque no declara el adaptador de persistencia ni la durabilidad | Sin log de arranque | Cada adaptador de repositorio se declara al inicializarse: el de memoria avisa que el dato se pierde, el relacional dice que sobrevive. La línea cambia sola al componer | `resuelto` | G1 | `in-memory-*.repository.ts`, `sql-repository.ts.tpl`, ambos circuitos |
| H-3 | Sin identificador de request en la entrada del log | Sin registro de requests | Cada request se nombra, el nombre vuelve en la cabecera `x-request-id` y toda entrada escrita mientras se atiende lo lleva, incluidas las del caso de uso | `resuelto` | G2 | `request-context.ts`, `console-logger.adapter.ts`, `verify-generation.mjs` |
| H-4 | El registro del producto no guarda el estado de cada operación | Sin estado en ninguna parte | `derivation.operations` guarda `id` y `businessEffect`, y la lectura tolera la forma anterior | `resuelto` | G1 | `project-context.ts`, `project.json.tpl`, `status.operation.ts` |
| H-5 | El README no lista los eventos que el producto publica | Sin sección de eventos | Tabla de evento, operación que lo publica y payload, solo cuando el producto publica eventos | `resuelto` | G1 | `derive.ts`, `verify-generation.mjs` |

**Cuenta al 2026-11-02, cerrados G1, G2 y G3, y G4 a medias.** De los catorce hallazgos del informe:
**once resueltos**, dos parciales por decisión escrita, uno excluido y el 3 en curso. **Nada queda
abierto que sea trabajo del mecanismo**: lo que falta del 3 es transcribir cuarenta y cuatro Service
Domains del portal del estándar, que es trabajo del autor y no se puede inferir sin inventar
contenido del estándar. Los cinco huecos nuevos están todos resueltos.

## Los nueve criterios de aceptación del informe

El informe no solo dejó propuestas: dejó nueve criterios verificables, escritos por alguien ajeno a
la construcción y antes de que la Fase 3 construyera. Son la rúbrica de este seguimiento, y serán el
instrumento de medición de la Fase 4.

| Área | Criterio del informe | Antes (0.2.1) | Hoy | Después esperado |
| :-- | :-- | :-- | :-- | :-- |
| CLI | El error indica PascalCase, muestra un ejemplo válido y el valor recibido | Falla | **Cumple** | Cumple |
| Bootstrap | El resultado informa que es técnico y lista operaciones implementadas y placeholder | Falla | **Cumple** | Cumple |
| Eventos | Cada evento documenta productor, payload, consumidores y si la publicación es solo in-process | Falla | **Cumple** (G1) | Cumple |
| Persistencia | El README y el log de arranque indican el adapter y si los datos sobreviven al reinicio | Falla | **Cumple** (G1), y los dos siguen al cableado cuando se incorpora el módulo | Cumple |
| API | Se puede iniciar el servicio, entender una ruta, enviar un request válido y observar una respuesta | Falla | **Cumple** | Cumple |
| Observabilidad | Cada request registra método, ruta, status, duración y request ID | Falla | **Cumple** (G2) | Cumple |
| Health | `/health` y `/ready` distinguen proceso vivo de dependencias disponibles | Falla | **Cumple** | Cumple |
| Testing | Cada endpoint generado tiene al menos un smoke test HTTP | Falla | **Cumple** (G3), y el circuito comprueba que ninguna ruta declarada quede sin caso | Cumple |
| Negocio | Un líder no técnico puede explicar propósito, alcance y pendientes sin leer el código | Falla | Medible, no verificado | Se mide en la Fase 4, no se declara acá. **Nota del 2026-11-07:** ya tiene quien lo responda —la mirada de negocio del líder técnico, que observa sin usar la herramienta— y se mide en el doc 6 de esa fase |

Al 2026-11-02, cerrada la primera iteración: **ocho de los nueve cumplen**, y el noveno —«Negocio»—
no se declara sino que se mide, y es trabajo de la Fase 4. **Ninguno falla.** Antes de G1 cumplían
cinco.

## Grupos de mejora

| Grupo | Qué cierra | Condición de cierre comprobable | Estado |
| :-- | :-- | :-- | :-- |
| **G1** | Lo que el producto declara de sí mismo: H-1, H-2, H-4, H-5 y la mitad pendiente del hallazgo 12 | `verify:composition` comprueba que el README del producto compuesto no sigue declarando persistencia en memoria y que la línea de arranque cambió; `verify:generation` comprueba la línea del adaptador, la tabla de eventos y el estado por operación en el registro | **cerrado el 2026-11-02** |
| **G2** | Observabilidad mínima del request: H-3 y la mitad pendiente del hallazgo 9 | Cada entrada de request lleva un identificador, propio o tomado de la cabecera; el nombre vuelve al llamador; y toda entrada escrita durante la request lo lleva, lo que el circuito comprueba | **cerrado el 2026-11-02** |
| **G3** | Smoke tests HTTP del producto: hallazgo 14 | Cada operación derivada tiene una prueba que ejerce su ruta por HTTP, el producto la corre en su propia verificación, y el circuito comprueba que ninguna ruta del README quede sin caso | **cerrado el 2026-11-02** |
| **G4** | Datos del catálogo: hallazgo 3 por su causa real | El dato del estándar está extraído y guardado, y el espacio de selección tiene las entradas que sirven a un propósito escrito | **cerrado el 2026-11-02** |
| **G5** | Lo que la herramienta dice antes y durante: propuestas 6.1, 4.1, 2.2 y 1.1 | El alcance se declara antes de generar; una diferencia de nombre aparece en esa declaración; el prompt muestra el formato que espera; el README del producto dice cuándo mover su estructura | **cerrado el 2026-11-02** |
| **G6** | El espacio de selección: propuestas 3.1 y 3.2, más agrupar las opciones | La lista se lee primero en lenguaje de negocio y la pregunta de operaciones muestra la ruta que va a salir | **reabierto y cerrado construido el 2026-11-03**. Agrupar las opciones sigue descartado por |
| **G7** | El dato del estándar, corregido con su documento oficial | La entrada de `Term Deposit` dice lo que el documento OpenAPI v14.0 publica, y la forma de ruta es un punto de variación con las dos formas derivando | **cerrado el 2026-11-03** |
| **G8** | El segundo nivel del estándar: los behavior qualifiers | El descriptor los declara, se eligen al derivar y cada operación produce su caso de uso, su ruta anidada y su andamio | **cerrado el 2026-11-03** |
| **G9** | La capacidad que el catálogo no ofrece: propuesta 3.3 | Un producto declara su capacidad con la forma cerrada, el registro lo marca y el producto arranca | **cerrado el 2026-11-03** |
| **G10** | El flujo de creación: propuestas 3.1, 3.2 y la mitad pendiente del 6.1 | Las preguntas se leen en negocio con el nombre del estándar al lado, y la derivación cierra con una revisión que deja corregir una respuesta sin perder las demás | **cerrado el 2026-11-03** |

**Por qué G1 primero.** Es el diagnóstico central del informe —hacer visible el contrato de la
generación— reaparecido un nivel más arriba, después de la composición; es el único grupo donde el
artefacto hoy dice algo **falso** de sí mismo y no algo incompleto; y se comprueba extendiendo el
circuito que ya existe, sin herramienta nueva. Ninguna parte de G1 depende de publicar: la
verificación local no usa el feed.

### G1, cambio por cambio

| ID | Cambio | Decisión que exige | Dónde se comprueba |
| :-- | :-- | :-- | :-- |
| G1-a | El módulo declara su nota en el README del producto, en una región delimitada | Si un módulo puede escribir en la documentación del producto y no solo en su código. Se resolvió que sí, declarado por el módulo, por coherencia con | `verify:composition` |
| G1-b | El adaptador del repositorio declara al inicializarse su naturaleza y la durabilidad del dato | Quién escribe la línea. La escribe el adaptador y no `main.ts`, para que quede correcta por construcción al componer | `verify:generation` y `verify:composition` |
| G1-c | El registro del producto guarda el estado de negocio de cada operación, y `bsl status` lo informa | Cambia el formato que fijó, y tres operaciones lo leen. Hay que elegir entre tolerancia de lectura y subir `schemaVersion` | `verify:generation` y prueba unitaria |
| G1-d | El README lista cada evento con la operación que lo publica y su payload | Ninguna: es contenido, y cae bajo | `verify:generation` |

## Auditoría a nivel de propuesta

**Por qué existe esta sección.** El informe trae catorce hallazgos y **cada uno tres propuestas
numeradas**: cuarenta y dos en total. Durante la Fase 3 hubo un documento de triage que decidía, por
hallazgo, qué entraba a esa fase. Era una compuerta de alcance, no un análisis de mérito, y arrastró
dos efectos: marcó hallazgos enteros como adoptados cuando solo una de sus tres propuestas lo
estaba, y descartó propuestas por no caber en la fase y no por no servir. **Ese documento se retiró
el 2026-11-02.** Este tablero es desde entonces la única fuente de seguimiento, y lo que sigue es el
análisis rehecho propuesta por propuesta, juzgando mérito y no alcance de fase.

**Qué cuenta como descarte.** Solo un ADR o un documento de fase con argumento propio. Una propuesta
que quedó fuera porque no entraba en la Fase 3 **no está descartada**: vuelve a estar sobre la mesa.

| Estado | Cuántas |
| :-- | --: |
| Hecho | 17 |
| Descartado con ADR o documento de fase propio | 8 |
| Diferido al módulo de observabilidad | 3 |
| **Entra: G5** | **4** |
| **Entra: G6**, construido en la segunda ronda | **2** |
| **Entra: G9**, construido en la segunda ronda | **1** |
| Se decide con lo que muestre la medición | 1 |
| No entra, con argumento nuevo escrito acá | 7 |

Suman cuarenta y tres porque la propuesta **9.3** pide dos cosas con destinos distintos: la
integración con el logger corporativo va al módulo, y preguntar la verbosidad al derivar no entra.
G6 lleva además un punto que **no sale del informe**: agrupar las capacidades al elegir.

**Movimientos de la segunda ronda (2026-11-03).** Tres propuestas que la primera ronda había cerrado
sin construir quedaron construidas: **3.1** y **3.2** salen de «se decide midiendo» a G6, y **3.3**
sale de «excluido con argumento» a G9. Las tres están revisadas más abajo, con la fecha y el motivo
por el que el argumento anterior no se sostiene. Lo único que queda en «se decide midiendo» es
**5.2**, los perfiles de agregado enriquecidos.

### Lo hecho

| # | Propuesta |
| :-- | :-- |
| 1.2 | Agrupar operaciones complejas en subcarpetas |
| 2.1 | Mensajes con formato y ejemplo válido |
| 4.2 | Registrar por separado referencia, capability, producto y aggregate |
| 4.3 | Explicación del mapeo en el README |
| 5.1 | Semilla mínima explícita |
| 6.2 | Estado por operación y por evento |
| 7.1 | README con propósito, alcance, estado y límites |
| 8.1 | Ejemplos `curl` por defecto |
| 8.2 | OpenAPI |
| 9.1 | Logging HTTP con método, ruta, status, duración y error |
| 10.1 | `/health` siempre |
| 11.1 | Aviso de persistencia en arranque y README |
| 11.3 | ORM y motor real como perfil |
| 12.1 | Marcar operaciones como scaffold o implemented |
| 12.3 | Lista de pendientes por operación |
| 13.1 | `test/` separado con su convención documentada |
| 14.1 | Smoke test por endpoint |

### Descartado con argumento propio

| # | Propuesta |
| :-- | :-- |
| 1.3 | Estructura por feature |
| 2.3 | Autocorregir un valor rechazado |
| 5.3 | Wizard de atributos e invariantes |
| 11.2 | Preguntar memoria o persistencia en `bsl new` |
| 12.2 | `501 Not Implemented` |
| 13.2 | Espejar las capas dentro de `test/` |
| 13.3 | Tests por feature y cobertura por capability |
| 14.2 | Tests e2e completos |

### Diferido al módulo de observabilidad

| # | Propuesta | Por qué el módulo y no el activo |
| :-- | :-- | :-- |
| 9.2 (métricas) | Métricas mínimas | Amplían el puerto y dependen de la plataforma de la organización ( fijó el corte) |
| 9.3 (integración) | Integración con el logger corporativo | Mismo corte |
| 10.3 | Módulo operativo con métricas y diagnóstico | Mismo corte. `/ready` deja el punto de extensión donde registrarse |

**Resuelto el 2026-11-05.** Las tres entran con el módulo, que es G11. Con dos precisiones sobre lo que decía el corte: las métricas **no** amplían el puerto del logger, porque un asiento y una medición no son la misma señal, y de la plataforma de la organización depende una dirección en la configuración y nada más, porque lo que se habla es un protocolo publicado. La integración con el logger corporativo es exactamente eso: el producto entrega al módulo **la misma entrada que escribió**, y el módulo la exporta.

### G5 — Lo que la herramienta dice antes y durante · **cerrado el 2026-11-02**

Cuatro propuestas baratas que compartían una causa: **todo lo que el artefacto explicaba de sí mismo
se leía después de generar.** El hallazgo central del informe es ese, y se había cerrado con
artefactos posteriores al hecho. Las cuatro están construidas y verificadas; el umbral de
estructura (1.1) quedó en el README del producto y en el del activo.

| # | Qué entra | Por qué ahora |
| :-- | :-- | :-- |
| 6.1 | Declarar que el resultado es un bootstrap **antes** de generar, en el resumen que precede a la confirmación | Es el hallazgo central. Hoy el README y el resumen lo dicen, y los dos se leen cuando el producto ya existe |
| 4.1 | Confirmar cuando el agregado local difiere del que sugiere la capability | Es la mitad preventiva del hallazgo 4. Lo que hay explica la diferencia después de escribirla en el registro |
| 2.2 | Mostrar el formato esperado en el prompt, no solo en el rechazo y en la ayuda | El punto de variación ya declara su `format`; el prompt no lo usa. Evita el intento fallido en lugar de explicarlo |
| 1.1 | Documentar el umbral de transición de estructura en el README del producto | Las capas están y el umbral nunca se escribió, que era la otra mitad de la propuesta |

### G6 — El espacio de selección · **cerrado por decisión el 2026-11-02**

Tres propuestas que se volvían una sola cosa porque **G4 las hacía urgentes**: si el espacio pasaba a
cuarenta y seis entradas, elegir en una lista plana dejaba de ser practicable. **La ronda disolvió esa
causa**: el espacio tiene cinco entradas, una por propósito escrito. Agrupar o filtrar deja de ser
necesario, y las dos propuestas de presentación pasan a decidirse midiendo.

| # | Qué entra | Por qué ahora |
| :-- | :-- | :-- |
| 3.1 | Separar en la presentación estándar, capability, producto y agregado | El registro ya los separa; lo que no los separa es lo que se ve al elegir |
| 3.2 | Lenguaje natural en la pregunta de operaciones | La pregunta de capacidad ya trae su descripción de negocio. La de operaciones muestra `Execute Term Deposit Interest Settlement` con `Execute` de pista, que no dice qué endpoint sale. Se resuelve con la ruta y una glosa derivada del action term: cinco frases, sin dato nuevo por Service Domain |
| — | Agrupar o filtrar las capacidades al elegir | **No está en el informe**: el revisor vio dos opciones. Era consecuencia de tener cuarenta y seis, y con cinco no hay problema que resolver. **Descartado por , y vuelve si el espacio crece |

**Lo que queda de 3.1 y 3.2.** No es navegación, es claridad: la pregunta de operaciones sigue
mostrando `Execute Term Deposit Interest Settlement` con `Execute` de pista, que no dice qué endpoint
sale. Se arregla con la ruta y una glosa derivada del action term, sin dato nuevo. Entra si la
segunda revisión vuelve a tropezar con ello.

### Se decide con lo que muestre la medición

| # | Propuesta | Qué la decide |
| :-- | :-- | :-- |
| 5.2 | Perfiles de dominio enriquecidos | Que la evaluación muestre que la semilla no alcanza. Decidirlo antes es inventar el requisito |
| 3.3 | Capability personalizada | **Resuelta el 2026-11-03, construida en G9 con .** No hacía falta esperar la evaluación: el marco ya traía la válvula escrita y sin implementar (MR-02 §3), y la tensión con el objetivo general se resuelve manteniendo la forma cerrada en lugar de admitir escritura libre |

### No entra, con argumento escrito acá

| # | Propuesta | Por qué no |
| :-- | :-- | :-- |
| 6.3 | Documentar la **evolución** de un evento | Un producto recién derivado no tiene historia de evento que contar. Lo que sí hacía falta —productor, payload, consumidores— está en la tabla de eventos |
| 7.2 | Documentos separados por audiencia | El README cubre hoy las tres vistas en un archivo que se lee de arriba abajo. Partirlo multiplica artefactos que el equipo tiene que mantener desde el primer día, y el informe mismo advertía que un manual excesivo no se lee |
| 7.3 | Diagramas e índice de evolución en el producto | Un diagrama generado queda desactualizado en el primer cambio del equipo y nadie lo regenera. El documento OpenAPI cumple ese papel y se arma de los esquemas reales |
| 8.3 / 14.3 | Colección Postman o Bruno, o script de verificación local | `GET /openapi.json` permite generarla en el momento con la herramienta que cada quien use, y los ejemplos `curl` cubren la prueba a mano. Mantener otro formato en la línea cuesta más de lo que ahorra |
| 9.3 (verbosidad) | Preguntar el nivel de verbosidad al derivar | Es `LOG_LEVEL`, una variable de entorno: se cambia por entorno y no por producto. Preguntarlo al derivar fija en el código una decisión que pertenece al despliegue |
| 10.2 | Checks configurables en `/ready` | La ruta distingue proceso vivo de servicio listo, y deja el punto donde un módulo registra su check. Hacerlos configurables sin un módulo que los aporte es diseñar contra un consumidor que no existe |

### G7 a G10, cambio por cambio

La segunda ronda la abren dos cosas: el autor decide construir las tres propuestas que la primera
ronda había cerrado sin construir, y aparece un dato que no se tenía. El **documento OpenAPI oficial
de `Term Deposit` v14.0** es la publicación del Service Domain, no una vista del landscape, y es
justo lo que la hoja de trabajo de la transcripción declaraba inalcanzable. Contra ese documento, la entrada del espacio
de selección tenía tres errores.

| ID | Cambio | Decisión que exige | Dónde se comprueba |
| :-- | :-- | :-- | :-- |
| G7-a | `Term Deposit` dice lo que su documento oficial publica: la definición literal, cuatro operaciones de nivel control record y `control` mutando | De dónde sale el dato de una capacidad. Del documento oficial del Service Domain, no de una vista ni de una paráfrasis | `verify:artifacts` y los conteos del circuito |
| G7-b | El verbo y la última porción de la ruta salen del action term, y la forma de ruta es punto de variación con `bian` por defecto | Si se adopta la forma del estándar, que sube la curva de adopción, o se conserva la de recurso. Las dos, desde un solo descriptor | `verify:generation` deriva en las dos formas |
| G7-c | El script de artefactos cruza el action term declarado contra los que la release deriva, y la fuente de opciones contra las que la herramienta sirve | Ninguna: eran dos huecos. Un `Notify` pasaba la validación y explotaba al elegirlo | Las dos reglas, rotas a propósito |
| G8-a | El descriptor gana `behaviorQualifiers`, con los diez de `Term Deposit` y sus treinta operaciones transcritas | Cómo se ofrecen dos niveles en un modelo que resuelve una lista. Aplanados en una sola pregunta | `verify:artifacts` y tres reglas nuevas |
| G8-b | Una operación de qualifier produce caso de uso, ruta anidada, evento y caso de humo, y ninguna entidad nueva | Si se genera una sub-entidad por qualifier. No: el agregado es inmutable y los atributos de un qualifier son tan desconocidos como los del agregado | `verify:generation` con cuatro operaciones de qualifier |
| G8-c | Una pregunta sin opciones no se hace | Ninguna: una capacidad sin qualifiers mostraba una lista vacía. Vale para cualquier punto cuyas opciones vengan de una respuesta anterior | Los tres productos sin qualifiers derivan sin esa pregunta |
| G9-a | Se admite declarar una capacidad fuera del catálogo, con Business Domain entre los nueve y action terms entre los cinco | Si la familia admite un producto cuya capacidad el estándar no publica. Sí, y estaba ya declarado en MR-02 §3 sin implementar | `verify:generation` deriva `pocket-api` y comprueba su metadato |
| G9-b | El registro del producto escribe `declaredOutsideCatalog` | Ninguna: es la condición que MR-02 §3 pone para admitir el caso | El circuito comprueba los cuatro campos y el área derivada |
| G10-a | El espacio de selección se presenta en lenguaje de negocio, con el nombre del estándar al lado, y la pregunta de operaciones muestra la ruta que va a salir | Si la glosa es dato o código. Dato del artefacto, y declarada como redacción propia y no como transcripción | `verify:artifacts`, con los campos obligatorios |
| G10-b | La derivación cierra con una revisión que deja corregir una respuesta sin perder las demás | Qué se vuelve a preguntar al corregir. Solo lo que depende de la respuesta corregida, con las dependencias declaradas y no inferidas | Dos pruebas: corregir el agregado, y corregir la capacidad |
| G10-c | Las catorce preguntas se agrupan en cuatro etapas, anunciadas solo cuando una pregunta se hace | Ninguna: el modelo declara la etapa y la resolución avisa por un callback, porque el núcleo no escribe en la terminal | `verify:artifacts`, con `stage` obligatorio |
| G10-d | El README del producto trae la definición oficial de su capacidad | Ninguna: hasta ahora esa definición moría en la pista de la pregunta y lo que viajaba era el texto libre del proyecto | `derive.spec.ts` |

## Sigue siendo una línea de producto

La pregunta no es retórica: G9 admite un producto cuya capacidad el estándar no publica, y el
objetivo general del proyecto es generar proyectos **alineados con BIAN**. Tres hechos del propio
proyecto sostienen que la línea no se rompe.

**Uno. El «conjunto cerrado» está acotado, y su justificación se cumple.** La frase aparece una sola
vez en todo el proyecto, en la tabla de clases de variabilidad del **doc 1 §3** de la Fase 2, donde
describe cómo se responde una clase de variabilidad y no la línea entera. Su justificación está en
**§5** del mismo documento, y es estrecha y verificable: «la escritura libre dejaría el metadato de
dominio sin validación posible y convertiría la alineación con el estándar en una afirmación no
verificable». Una capacidad declarada **exige** su Business Domain y su control record, y deriva el
Business Area del grupo en lugar de preguntarlo. El metadato sigue validado, así que la justificación
se cumple: lo que cae es la forma, no la razón.

**Dos. El marco ya traía esta válvula.** MR-02 §3 la escribe y la tesis la repite: se permite
declarar un Service Domain fuera del subconjunto por defecto, y lo único que no se admite es omitir
el metadato. G9 implementa lo que estaba declarado; no inventa una excepción.

**Tres. La derivación sigue siendo sistemática.** Lo abierto son los valores hoja y nunca la forma:
el Business Domain se elige entre nueve, el action term entre cinco, la estructura y las plantillas
son las mismas, y no hay un camino de código que solo la capacidad declarada recorra. Los cuatro
productos del circuito —dos capacidades del catálogo en las dos formas de ruta, y una declarada—
pasan la misma verificación.

Queda como **desviación declarada**, en el estilo de MR-01 §6: la familia admite un producto cuya
capacidad no está en el espacio por defecto, y el registro lo marca para que la evaluación pueda
contarlo.

**Y agrega un flujo que el modelo pedía y no tenía.** MR-01 §4 declara entre sus cinco flujos «el
retorno de nuevos requerimientos hacia el dominio», que hasta ahora no tenía por dónde ocurrir:
nada en un producto derivado decía que su capacidad no estuviera en el catálogo. Con
`declaredOutsideCatalog` en el registro se puede preguntar al conjunto de productos del laboratorio
qué capacidades propias se repiten, y tres productos declarando la misma es la evidencia que
justifica una entrada nueva. El atajo es lo menos valioso de G9.

## Cierre de la primera iteración

La primera iteración tuvo **dos rondas**. La primera cerró el 2026-11-02 con seis grupos; la segunda
la abrió el autor el 2026-11-03, para construir las tres propuestas que la primera había cerrado sin
construir, y con un dato nuevo: el documento OpenAPI oficial de `Term Deposit` v14.0.

**Primera ronda, 2026-11-02.** De las cuarenta y dos propuestas del informe: diecisiete ya estaban
hechas, **once se construyeron** (G1 a G5), ocho estaban descartadas con ADR propio, siete quedaron
fuera con argumento escrito acá, tres diferidas al módulo de observabilidad y dos se decidían
midiendo. De los cinco huecos que la verificación del artefacto encontró por su cuenta, los cinco
cerrados, con nueve decisiones.

**Segunda ronda, 2026-11-03.** Cuatro grupos nuevos y **G6 reabierto y cerrado construido**. Las tres
propuestas que habían quedado sin construir —3.1, 3.2 y 3.3— están hechas, así que de «se decide
midiendo» queda solo **5.2**, los perfiles de agregado. Ocho decisiones. Y tres cosas
que nadie había pedido salieron a la luz al construir:

| Hallazgo propio | Qué era |
| :-- | :-- |
| La regla que exige un caso de humo por ruta **no tenía dientes** | Se satisfacía con que la ruta apareciera en el **título** de la prueba, y los títulos la nombran desde G3. Una prueba que pidiera otra ruta pasaba. Ahora compara contra las peticiones que la prueba hace de verdad, y rota a propósito falla |
| Un `Execute` sin calificador enrutaba a `:id/s` en forma de recurso | Pluralizar una cadena vacía da `s`. Ninguna entrada del catálogo lo alcanzaba porque todas califican sus ejecuciones; una capacidad declarada sí. Corregido a `:id/execute` |
| `control` tenía `mutates` distinto según la capacidad | `true` en cuatro entradas y `false` en `Term Deposit`, de modo que la misma operación del estándar producía dos formas y eso no estaba escrito. El documento oficial lo zanja: `control` muta |

**La rúbrica del revisor: ocho de nueve criterios cumplidos, ninguno falla.** El noveno —que un líder
no técnico pueda explicar propósito, alcance y pendientes sin leer código— no se declara: se mide, y
es trabajo de la Fase 4. La segunda ronda trabaja a favor de ese noveno sin declararlo: las preguntas
y el README del producto se leen ahora en lenguaje de negocio.

**Diecisiete decisiones en total**, cada una en el log de la fase cuyo artefacto toca.

**Verificado el 2026-11-03.** `check:push` en verde, código de salida 0: **253 pruebas** (2
contracts, 12 persistence, 193 herramienta, 46 activo base), cero vulnerabilidades. El circuito de
generación deriva **cuatro** productos y cada uno pasa su propia verificación: `term-deposit-api` 57
archivos en forma del estándar con cuatro operaciones de qualifier y diez rutas en su documento
OpenAPI, `party-directory-api` 34, `deposit-rest-api` 38 en forma de recurso y sin eventos, y
`pocket-api` 37 para una capacidad declarada. El circuito de composición incorpora el módulo a un
producto que persiste y sobrevive al reinicio.

### Qué queda para el segundo ciclo

| Qué | Por qué todavía no | Quién lo mueve |
| :-- | :-- | :-- |
| **La segunda revisión externa** sobre la versión publicada, con el mismo revisor | Es lo que cierra el ciclo: convierte la revisión del 2026-10-28 en el «antes» medido. **Desbloqueada el 2026-11-04**, cuando se publicó lo que hay que revisar. **Asignada el 2026-11-06**: es el documento 6 de la Fase 4, y el evaluador es uno de sus cuatro participantes caracterizados, así que la segunda aplicación de la rúbrica la hace la misma persona que escribió sus nueve criterios. **Corregido el 2026-11-07: los nueve entran.** El evaluador es el **desarrollador externo**, de modo que la segunda aplicación la hace quien escribió los criterios; y el noveno —un líder no técnico explicando propósito, alcance y pendientes— lo sostiene la **mirada de negocio del líder técnico**, que participa sin usar la herramienta: observa y reacciona | El autor y el evaluador |
| ~~**Publicar** el activo base `0.14.0` y la herramienta `0.18.0`~~ | **Hecho el 2026-11-04.** El feed sirve las cinco versiones vigentes, comprobado con `npm view`. Con eso la segunda revisión externa ya puede instalar del feed y no de tarballs, que era la condición para que midiera el artefacto real. Cerró además **RF-15** y **RNF-06** en la medición de requerimientos | El autor, hecho |
| ~~**La línea base medida**~~ | **Hecho el 2026-11-06.** El primer criterio del objetivo 4 ya tiene contra qué medir: constituyó la línea base como reconstruida —autoreporte anterior al artefacto más inventario de tareas— y el documento 7 de la Fase 1 fija la banda de **8 a 15 días** (52-98 horas-persona), las **31 tareas** del arranque con 23 cubiertas, 2 parciales y 6 fuera del alcance, y la **regla de las tres cubetas** con la que esta fase tiene que reportar su comparación | El autor, hecho |
| **Una** propuesta que se decide midiendo: perfiles de agregado enriquecidos (5.2) | Depende de que la evaluación muestre que la semilla no alcanza. Decidirlo antes es inventar el requisito. Las otras tres de esta fila se construyeron el 2026-11-03 | La evaluación |
| Tres propuestas **diferidas al módulo de observabilidad**: métricas (9.2), integración corporativa (9.3) y el módulo operativo con los checks de `/ready` (10.3) | Amplían el puerto y dependen de la plataforma de la organización | Una fase posterior |
| **Los ajustes a documentos de fase** que declararon | Es deuda documental. La auditoría del 2026-11-03 encontró que **los ADR la declaraban incompleta**: no son tres documentos sino **ocho, más un insumo y dos diagramas**. El inventario verificado está en. Conviene aplicarla antes de narrar los capítulos 4 y 5 | El autor |
| **Una capacidad sin `initiate`** en el espacio de selección | Ejercitaría una variabilidad que ninguna entrada cubre, y puede destapar un supuesto del activo base | Decisión abierta, anotada en el insumo de la Fase 1 |
| **Las cinco capacidades sin operaciones de nivel CR** en v14.0 | Entrar al espacio les exigiría decidir qué operaciones publicar, que es diseño y no transcripción | Solo si alguna encuentra un propósito |
| **Transcribir las otras cuatro entradas** de su documento oficial, con sus behavior qualifiers | fija la fuente y solo `Term Deposit` tiene su documento a la vista. Queda abierto, junto con la extracción de las cuarenta y una capacidades restantes | El autor, con el documento de cada Service Domain |
| **La medición de los 22 requerimientos** sobre las fases 1, 2 y 3 completas | Levantada el 2026-11-03, y es el punto de partida de la evaluación y no su resultado. Se rehace una vez al cierre del proyecto, en el documento de trazabilidad | La Fase 4 |

**Nada de lo que queda es trabajo del mecanismo**, con una excepción de datos y no de diseño:
transcribir las otras cuatro entradas de su documento oficial. Lo demás es publicar, medir, y
aplicar la deuda documental.

## Bitácora

Una fila por cambio aplicado. Sin fila, el tablero no mueve un estado.

| Fecha | Grupo | Qué cambió | Versión | Comando que lo prueba |
| :-- | :-- | :-- | :-- | :-- |
| 2026-11-02 | G1-d | El README del producto lista cada evento con la operación que lo publica y su payload, y solo cuando el producto publica eventos | `@bsl/cli` 0.9.0 | `npm test -w @bsl/cli` (dos pruebas nuevas en `derive.spec.ts`) · `npm run verify:generation -w @bsl/cli` |
| 2026-11-02 | G1-b | Cada adaptador de repositorio declara al inicializarse qué es y si el dato sobrevive al reinicio. Lo escribe el adaptador y no `main.ts`, así que incorporar el módulo cambia la línea sin que nadie la actualice | `@bsl/base-template` 0.8.0, `@bsl/persistence` 0.2.0 | `npm --prefix packages/base-template/template test` (tres pruebas nuevas) · ambos circuitos |
| 2026-11-02 | G1-c | `derivation.operations` guarda `id` y `businessEffect`; la lectura tolera la forma anterior con `derivedOperations`; `bsl status` cuenta las implementadas y nombra los andamios | `@bsl/cli` 0.9.0 | `npm test -w @bsl/cli` (tres pruebas nuevas en `status.operation.spec.ts`, una de ellas sobre un registro de la forma anterior) |
| 2026-11-02 | G1-a | El módulo declara su nota en la región `bsl:persistence` del README. El marcador admite la forma de comentario de Markdown, y el circuito comprueba que el aviso de pérdida de datos desaparece | `@bsl/persistence` 0.2.0, `@bsl/cli` 0.9.0 | `npm run verify:composition -w @bsl/cli`: «deposit-api rewrote what its readme says it stores» |
| 2026-11-02 | G1 | Cierre del grupo | — | `npm run check:push` en verde, código de salida 0: 205 pruebas (2 contracts, 12 persistence, 158 herramienta, 33 activo base), cero vulnerabilidades, conteos del producto de referencia intactos en 48 y 31 archivos |
| 2026-11-02 | G2 | Cada request se nombra: el interceptor toma `x-request-id` o acuña un UUID, lo devuelve en la respuesta y corre el manejo dentro de un `AsyncLocalStorage`. El adaptador de registro adjunta `requestId` a toda entrada escrita durante la request, incluidas las del caso de uso, que no saben que existe. La forma legible le da una columna propia, con elipsis cuando tuvo que cortar | `@bsl/base-template` 0.9.0, `@bsl/cli` 0.10.0 | `npm --prefix packages/base-template/template test` (siete pruebas nuevas) · `npm run verify:generation -w @bsl/cli`: «Its log names every request, keeps the name a caller gives and ties 2 entries to it» |
| 2026-11-02 | G2 | Cierre del grupo | — | `check:push` en verde, código de salida 0: **214 pruebas** (2 contracts, 12 persistence, 158 herramienta, 42 activo base), cero vulnerabilidades. Conteos del producto de referencia: **49 y 32**, porque `request-context.ts` viaja copiado |
| 2026-11-02 | G3 | Todo producto trae `test/http-smoke.spec.ts`: arranca la aplicación real y pide a cada ruta una respuesta por HTTP. Un caso por operación, sin que ninguno dependa de otro, más uno que almacena y lee de vuelta cuando el producto inicia y consulta. Siete plantillas nuevas y `test/setup.ts`, que fija el entorno antes de cualquier import | `@bsl/base-template` 0.10.0, `@bsl/cli` 0.11.0 | `npm run verify:generation -w @bsl/cli`: los dos productos pasan su propia verificación, `term-deposit-api` con ocho casos de humo y `party-directory-api` con uno |
| 2026-11-02 | G3 | Cierre del grupo | — | `check:push` en verde, código de salida 0: **220 pruebas** (2 contracts, 12 persistence, 160 herramienta, 46 activo base), **cero vulnerabilidades con las tres dependencias de desarrollo nuevas**. Conteos del producto de referencia: **51 y 34** |
| 2026-11-02 | G4 | Las dos entradas del espacio de selección pasan a declarar una Business Area del estándar: `Operations and Execution / Loans and Deposits` y `Reference Data / Party`. Corregido también el ejemplo del esquema y el `project.json` del activo base, que declaraba `Party` como área | sin cambio de versión | `npm run verify:artifacts -w @bsl/cli` · `check:commit` en verde |
| 2026-11-02 | G5 | La derivación declara su alcance **antes** de escribir —bootstrap, operaciones con y sin efecto, persistencia, eventos— y en un terminal pide confirmación; la diferencia entre el agregado local y el que sugiere la capability va en esa misma declaración, como una fila y no como una pregunta aparte; el prompt del agregado dice `(PascalCase, e.g. TermDeposit)`; y el README del producto gana la sección de estructura con el umbral para moverla | `@bsl/base-template` 0.11.0, `@bsl/cli` 0.12.0 | `npm test -w @bsl/cli`: cuatro pruebas nuevas, entre ellas que responder `no` no escribe nada · `check:push` en verde con **224 pruebas** |
| 2026-11-02 | G4 | **Corrección de la corrección.** Consultada la vista matriz del Service Landscape v14.0 en el portal, `Party Reference Data Directory` está en `Sales and Service / Customer Management` y no en `Reference Data / Party`, que es donde lo había puesto razonando desde el documento del marco. corrige el dato y fija la regla: ante una discrepancia sobre la jerarquía manda el portal | `@bsl/base-template` 0.12.0, `@bsl/cli` 0.13.0 | `npm run verify:artifacts -w @bsl/cli` · `check:push` en verde |
| 2026-11-02 | G4 | Hoja de trabajo verificada contra el portal: los cuarenta y seis nombres existen en v14.0 y están donde MR-00 §8 los pone, en **dos** Business Areas y **nueve** Business Domains. Anotado qué da el portal —nombres y jerarquía— y qué no: la descripción, el control record y las operaciones están en la página de cada Service Domain, que se arma con JavaScript | — | Las tres vistas del landscape se leyeron; ninguna trae el detalle por capacidad |
| 2026-11-02 | G4 | Hoja de trabajo de la transcripción: `Fase 2 .../Insumos/transcripcion-del-service-landscape.md`, con las diez agrupaciones, los campos que faltan por entrada, el límite de los cinco action terms derivables y cómo se comprueba | — | No es código: deja la transcripción mecánica para cuando se haga con el portal |
| 2026-11-03 | G7 | `Term Deposit` dice lo que publica su documento oficial: la definición literal, cuatro operaciones de nivel control record en lugar de cinco, y `control` mutando. `execute-interest-settlement` sale de ese nivel | sin cambio de versión | `npm run verify:artifacts -w @bsl/cli` · el producto de referencia pasa de 51 a 50 archivos |
| 2026-11-03 | G7 | El verbo y la última porción de la ruta salen del action term, y la forma de ruta es punto de variación: `bian` por defecto sirve `POST /TermDeposit/Initiate` y `PUT /TermDeposit/{id}/Update`; `rest` conserva la forma de recurso con `201` en la iniciación | `@bsl/base-template` 0.13.0, `@bsl/cli` 0.15.0 | `npm run verify:generation -w @bsl/cli`: `term-deposit-api` en forma del estándar y `current-account-api` en forma de recurso, los dos pasando su propia verificación |
| 2026-11-03 | G7 | Dos huecos del script de artefactos: un action term que la release no deriva pasaba la validación y explotaba al elegirlo, y una fuente de opciones que la herramienta no sirve dejaba la pregunta vacía | — | Las dos reglas rotas a propósito: `declares the action term 'Notify', which this release does not derive` y `reads its options from 'model/shapes.json', which the tool does not serve` |
| 2026-11-03 | G7 | Cierre del grupo | — | `check:push` en verde, código 0: **234 pruebas** (2 contracts, 12 persistence, 174 herramienta, 46 activo base), cero vulnerabilidades. Conteos: 50, 34 y 45 |
| 2026-11-03 | G8 | El descriptor gana `behaviorQualifiers`: los diez de `Term Deposit` con treinta operaciones, transcritas del documento oficial sin su código de nivel. Se ofrecen aplanados en una sola pregunta, y una capacidad sin qualifiers no la recibe | `@bsl/cli` 0.16.0 | `npm run verify:artifacts -w @bsl/cli` · tres reglas nuevas rotas a propósito |
| 2026-11-03 | G8 | Una operación de qualifier produce su caso de uso, su ruta anidada bajo la instancia, su evento y su caso de humo, en el mismo controlador y con el mismo repositorio. Ninguna recibe cuerpo y todas son andamio | `@bsl/cli` 0.16.0 | `verify:generation`: `term-deposit-api` con 57 archivos y diez rutas, `PUT /TermDeposit/{id}/Interest/{interestId}/Execute` entre ellas |
| 2026-11-03 | G8 | **La regla que exige un caso de humo por ruta no tenía dientes**: la satisfacía el título de la prueba, que nombra la ruta desde G3. Ahora compara contra las peticiones que la prueba hace | — | Rota a propósito: `/TermDeposit/:id/Interest/:interestId/Retrieve is a route of term-deposit-api and its smoke test does not ask for it` |
| 2026-11-03 | G8 | Cierre del grupo | — | `check:push` en verde, código 0: **244 pruebas** (184 herramienta), cero vulnerabilidades. Conteos: 57, 34 y 38 |
| 2026-11-03 | G9 | Se admite declarar una capacidad fuera del catálogo: Business Domain entre los nueve del marco, nombre y control record escritos, operaciones entre los cinco action terms, y el Business Area derivado del grupo sin preguntarse. El registro escribe `declaredOutsideCatalog` | `@bsl/base-template` 0.14.0, `@bsl/cli` 0.17.0 | `verify:generation` deriva `pocket-api` para `Savings Pocket` y comprueba su metadato: «The declared capability carries its metadata, with the area read from its group» |
| 2026-11-03 | G9 | Un `Execute` sin calificador enrutaba a `:id/s` en forma de recurso, porque pluralizar una cadena vacía da `s`. Ninguna entrada del catálogo lo alcanzaba; una capacidad declarada sí | — | `pocket-api` sirve `POST /savings-pockets/:id/execute` |
| 2026-11-03 | G9 | Cierre del grupo | — | `check:push` en verde, código 0: **250 pruebas** (190 herramienta), cero vulnerabilidades. Cuatro productos derivados y cada uno pasando su propia verificación |
| 2026-11-03 | G6, G10 | El espacio de selección se presenta en lenguaje de negocio con el nombre del estándar alineado al lado, y la pregunta de operaciones muestra **la ruta que va a salir**, que es la real porque el estilo y el agregado ya están contestados. Las catorce preguntas se agrupan en cuatro etapas | `@bsl/cli` 0.18.0 | `npm run verify:artifacts -w @bsl/cli` con los campos de glosa y `stage` obligatorios · tres roturas a propósito |
| 2026-11-03 | G10 | La derivación cierra con una revisión que muestra cada respuesta y deja corregir una sin perder las demás. Corregir la capacidad vuelve a preguntar solo lo que depende de ella. El README del producto gana la definición oficial de su capacidad | `@bsl/cli` 0.18.0 | `npm test -w @bsl/cli`: corregir el agregado conserva el resto, y corregir la capacidad no vuelve a preguntar la descripción ni el responsable |
| 2026-11-03 | G6, G10 | Cierre de los grupos y de la segunda ronda | — | `check:push` en verde, código 0: **253 pruebas** (2 contracts, 12 persistence, 193 herramienta, 46 activo base), cero vulnerabilidades. Conteos: 57, 34, 38 y 37 |
| 2026-11-05 | G11-b | `TelemetryPort` entra al contrato con `record`, `span` y `measure`, y ningún adaptador del activo base lo satisface. El producto reporta a un puerto que puede no tener implementación y lo inyecta opcional, así que incorporar el módulo no cambia una línea del producto | `@bsl/contracts` 0.3.0 | `npm run verify -w @bsl/contracts` · `npm --prefix packages/base-template/template test` |
| 2026-11-05 | G11-c | El producto reporta en los tres lugares donde produce telemetría: cada entrada que el logger escribió, y el span y la duración de la request desde el interceptor y desde el filtro de errores, que son los dos lugares donde una request termina | `@bsl/base-template` 0.19.0, `@bsl/cli` 0.23.0 | `npm --prefix packages/base-template/template test`: **98 pruebas**, con la entrada reportada, la descartada por nivel y el span de un `4xx` que no dice que el servicio falló |
| 2026-11-05 | G11-a | `@bsl/observability` 0.1.0: exportador del protocolo OpenTelemetry en JSON sobre HTTP, sin dependencias de ejecución; muestreo del estándar —una traza que llegó conserva la decisión del llamador—, cola de 2048 señales y series acumulativas. Seis variables, todas con el nombre que el estándar les da | `@bsl/observability` 0.1.0, `@bsl/catalog` con cuatro entradas | `npm run verify -w @bsl/observability`: **36 pruebas** · `npm pack` revisado: dieciséis archivos, solo `dist/`, manifiesto, esquema y README |
| 2026-11-05 | G11-a | **Hallazgo al ejecutar.** El adaptador del módulo pedía `LOGGER_PORT` y cerraba un ciclo con el logger del producto, que reporta al puerto de telemetría. El producto arrancó, atendió y **no exportó nada, sin un solo aviso**. El adaptador pasa a pedir el logger al contenedor cuando tiene algo que informar | `@bsl/observability` 0.1.0 | `npm --prefix packages/base-template/template test`: la prueba de cableado compone un módulo con la forma correcta, y la variante que toma el logger por constructor **tiene que fallar** |
| 2026-11-05 | G11-d | El módulo declara la región `bsl:telemetry` del README del producto, octavo punto de inserción, con el mecanismo de y **sin tocar la herramienta**: `scaffolds` y `bindings` ya eran opcionales | `@bsl/cli` 0.23.0 | `npm run verify:composition -w @bsl/cli`: el README del producto deja de decir que nada sale del proceso |
| 2026-11-05 | G11-e | El circuito gana cinco pasos y un rechazo: incorpora el segundo módulo al producto que ya tiene el primero, levanta un colector del protocolo en el propio script y comprueba que las señales salen | `@bsl/cli` 0.23.0 | `npm run verify:composition -w @bsl/cli`: «deposit-api exported 3 spans, its entries and the duration of its requests, continuing the trace of its caller» |
| 2026-11-05 | G11 | Cierre del grupo y de la tercera ronda | — | `check:push` en verde, código 0: **342 pruebas** (2 contracts, 12 persistence, 36 observability, 98 activo base, 194 herramienta), cero vulnerabilidades. Tres productos derivados en 67, 39 y 42 archivos, y un producto con **dos módulos** del catálogo |
| 2026-11-07 | G13-a, G13-b, G13-e | La condición que el punto de variación declara viaja con la pregunta, así que lo que no se acepta se rechaza en la pregunta, que queda abierta; una selección por debajo de su mínimo también; y lo obligatorio se comprueba sobre lo escrito. `validate` se partió en `reasonToReject`, que devuelve el motivo, y el que lo lanza: la condición queda declarada una vez y leída una vez | `@bsl/cli` 0.28.0 | `npm test -w @bsl/cli` (tres pruebas nuevas en `input-resolver.spec.ts`) · `bsl new --description "" --non-interactive` responde `description is required, so it cannot be left empty.` |
| 2026-11-07 | G13-c, G13-d | La tecla de escape retrocede una pregunta y sale cuando no queda ninguna atrás; la interrupción sale directamente. Las dos por `CancelledError`, línea informativa y código 130, nunca «defecto de la herramienta». El recorrido pasó de un `for` a un índice que retrocede, con la pila de los puntos realmente preguntados | — | `npm test -w @bsl/cli` (cuatro pruebas del paso atrás en `input-resolver.spec.ts`, cuatro en `escape-key.spec.ts`, tres en `exit-codes.spec.ts`, dos en `generate.operation.spec.ts`) |
| 2026-11-07 | G13-f, G13-g, G13-h | Se separan `required` y `asked`; la ayuda marca los once obligatorios, abre con su línea de invocación, agrupa los diecisiete parámetros de `new` en cinco bloques y cierra con ejemplos. Los booleanos que vienen en sí nombran su forma negada | `@bsl/cli` 0.28.0 | `npm test -w @bsl/cli` (ocho pruebas en `help.spec.ts`, la primera suite propia de la ayuda) · `bsl new --help` |
| 2026-11-07 | G13 | Cierre del grupo y de la quinta ronda | `@bsl/cli` 0.28.0 | `check:push` en verde, código 0: **378 pruebas** (2 contracts, 12 persistence, 36 observability, 223 herramienta, 105 activo base), cero vulnerabilidades. Tres productos derivados en 68, 40 y 43 archivos y los seis rechazos del circuito de composición, los dos intactos. Seis commits en `main`, sin publicar |
| 2026-11-09 | G14-a, G14-b, G14-c, G14-d, G14-e | El almacén: una plantilla se describe a sí misma en `bsl-template.json`, sus archivos salen de la herramienta, el motor gana condición y repetición con gramática cerrada, se escribe la frontera de lo expresable como dato, y `derive.ts` pasa a ser un intérprete. 51 archivos `.tpl` a **29**; `derive.ts` de 919 a 586 líneas más 203 de intérprete | `@bsl/cli` 0.29.0 | `npx jest reference-aggregate` en verde **sin tocar el activo**, que es el oráculo de la migración · `npm run verify:generation -w @bsl/cli` con los tres productos en 68, 40 y 43 archivos · `bsl templates list` y `bsl templates show base-template` en una terminal real |
| 2026-11-09 | G14-f, G14-g | La forma del producto es un contrato: la plantilla la declara en `productShape`, el producto la lleva en `shape` y el esquema del registro se compara por versión mayor. Ocho puntos de inserción con su clase y su comentario, dos puertos y cuatro supuestos | `@bsl/cli` 0.30.0 | `npm test -w @bsl/cli` (doce pruebas en `product-shape.spec.ts`, una de ellas comparando la forma implícita contra el manifiesto real, más dos en `project-context.spec.ts`) |
| 2026-11-09 | G14-j, G14-k, G14-l | El módulo declara `serves` y la composición lo comprueba antes de las ocho reglas; `nest` pasa a `composition`; la actualización comprueba lo que comprueba la incorporación | `@bsl/persistence` 0.4.0, `@bsl/observability` 0.2.0 | `npm run verify:composition -w @bsl/cli`: «refused: a module that does not serve the shape of the product», con el producto idéntico después · tres pruebas nuevas en `compose.spec.ts` y tres en `upgrade.spec.ts` |
| 2026-11-09 | G14-m, G14-h | `bsl modules remove` quita un módulo restaurando lo que la derivación escribió, y la superficie se agrupa en `templates` y `modules`, con los tres nombres publicados como alias vivos | `@bsl/cli` 0.30.0 | `npm run verify:composition -w @bsl/cli`: «deposit-api is back to what the derivation wrote, with both modules taken out» y «passed its own verification again with no module incorporated» · ocho pruebas en `remove.spec.ts` |
| 2026-11-09 | G14-i | Una plantilla de otra familia entra como fixture: Python, trabajo por lotes, comentarios `#`, forma `python-batch@3` y un contrato que no es el de esta línea | — | `npm test -w @bsl/cli` (once pruebas en `foreign-template.spec.ts`) |
| 2026-11-09 | G15-f | El circuito incorpora el mismo módulo a un **segundo producto**, derivado de otra capacidad, y comprueba que el adaptador se llama por el agregado de ese producto, que **no** contiene el del primero y que la ligadura nombra su propio token. De paso los dos quedan con versiones distintas del mismo módulo a la vez, que es el criterio literal de RNF-06 | — | `npm run verify:composition -w @bsl/cli`: «@bsl/persistence is incorporated in deposit-api (0.5.0) and in party-directory-api (0.4.0, declared ^0.4.0), each wired to its own aggregate: two products, two versions of one module, at the same time» |
| 2026-11-09 | G16-a, G16-b, G16-c | La familia admite un producto sin servidor propio; toda plantilla vive bajo `packages/templates/` con convención escrita, validador compartido y procedimiento para agregar una; `@bsl/base-template` pasa a `@bsl/nestjs-hexagonal-api`; y el producto registra la plantilla que lo derivó en vez de un literal | `@bsl/nestjs-hexagonal-api` 0.21.0, `@bsl/cli` 0.30.0 | `npm run check:push` en verde · `bsl templates list` muestra las dos entradas · una prueba nueva en `derive.spec.ts` comprueba que el README del producto dice `Derived from @bsl/nestjs-hexagonal-api@…` desde el manifiesto |
| 2026-11-09 | G16-d | Entra `@bsl/azure-functions-api`: 24 archivos derivados, forma `azure-functions@1`, cinco puntos de inserción, sin contenedor de inyección y sin producto de referencia | `@bsl/azure-functions-api` 0.1.0, `@bsl/catalog` 0.5.0 | `npm run verify -w @bsl/azure-functions-api`: «@bsl/azure-functions-api derived a product of shape azure-functions@1 that passed its own verification» — deriva, comprueba que el producto registre ese paquete y esa forma, lo instala y corre su lint, sus 4 pruebas y su build |
| 2026-11-09 | G16-e | **Publicados los seis activos**, y usar la herramienta del feed destapó tres cosas: la entrada de `azure-functions-api` quedó en `proposed` con el paquete ya servido, el rechazo por un nombre inexistente nombraba solo las plantillas **ofrecidas** —así que una propuesta quedaba invisible y un typo se leía como «nunca se agregó»—, y `bsl templates show` **se negaba a leer** una plantilla propuesta, que es la que alguien necesita mirar para decidir si la adopta | `@bsl/catalog` 0.6.0 | `npm view` de los seis paquetes · `bsl templates show azure-function-api` nombra ahora `The catalog holds: nestjs-hexagonal-api, azure-functions-api (proposed)` · tres pruebas nuevas en `template-reference.spec.ts` |
| 2026-11-09 | G16-f | **Y un cuarto hallazgo, que lo produjo activar la entrada:** `verify:generation` derivaba **sin `--template`**, admisible mientras una sola plantilla estuviera ofrecida, y con dos la herramienta se niega a adivinar. Los dos circuitos nombran ahora la plantilla, que es además lo honesto: lo que verifican es **esa** | — | `npm run verify:generation -w @bsl/cli` en verde con los tres productos (68, 40 y 43 archivos). Lo encontró `check:push`: el estado del catálogo no es insumo de ninguna prueba unitaria, y activar una entrada es un cambio de **un** campo en otro repositorio que cambió el comportamiento de un comando |
| 2026-11-09 | G16-g | **Un quinto hallazgo, de la misma clase que el cuarto:** los tres archivos de identidad del producto de referencia —`package.json`, `README.md` y `project.json`— seguían nombrando la plantilla **`@bsl/base-template`**, que es justo la mentira que corrigió en todos los demás lados. **Nada lo vio porque son los tres archivos que `reference-aggregate.spec.ts` excluye a propósito** de la comparación byte a byte, por ser la identidad privada del activo y no la de un producto. Más la tabla de scopes de `ESTANDAR-DE-COMMITS.md`, que declaraba un `scope-enum` de tres entradas cuando el real tiene seis, y dos `examples` del esquema del catálogo | — | `npx jest reference-aggregate` en verde con el nombre nuevo, que es lo que prueba que el renombre no mueve un byte de lo comparado. Lo encontró un `grep` de `base-template` sobre `Codigo/`, no una prueba |
| 2026-11-09 | G16 | Cierre del grupo y de la octava ronda, **después de publicar los seis activos** | — | `check:push` en verde, código 0: **494 pruebas** (2 contracts, 12 persistence, 36 observability, **339 herramienta**, 105 plantilla hexagonal), más las **4** del producto que deriva la plantilla de Azure, que corren en su propia verificación. Cero vulnerabilidades, los **22 pasos y 8 rechazos** del circuito de composición, los tres productos de la generación —68, 40 y 43 archivos—, y **las dos plantillas pasando su propia verificación**, las dos nombrando ahora de qué plantilla derivan. Cuarenta y siete commits en `main` de `bsl-assets` en el día y siete en `bsl-catalog`. **Los seis activos publicados**; queda el catálogo `0.6.0` sin publicar, con lo que la segunda plantilla **se lista y todavía no se puede usar** desde el feed () |
| 2026-11-09 | G15 | Cierre del grupo y de la séptima ronda. Nueve de las diez divergencias se cerraron **escribiendo**; una pidió el paso de circuito de arriba | — | El expediente: el log de la Fase 4 corre a , el índice de la fase corregido a los objetivos textuales con §4.b y §5.b nuevas, el índice de la fase en plural, el informe de evaluación con las divergencias, y los docs 8 y 9 de la Fase 3 con el paso nuevo |
| 2026-11-09 | G14 | Cierre del grupo y de la sexta ronda | `@bsl/cli` 0.30.0, `@bsl/persistence` 0.4.0, `@bsl/observability` 0.2.0 | `check:push` en verde, código 0: **490 pruebas** (2 contracts, 12 persistence, 36 observability, 335 herramienta, 105 activo base), cero vulnerabilidades. Tres productos derivados en 68, 40 y 43 archivos; el circuito de composición con **21 pasos y 8 rechazos**. Veinticuatro commits en `main`, **sin publicar** |

**Hueco de esta bitácora.** La cuarta ronda (G12, 2026-11-06) **no dejó filas acá**, aunque el encabezado
diga que sin fila el tablero no mueve un estado. Lo que esa ronda hizo está en su propia sección y en
La decisión de la página, con su verificación; lo que falta es el asiento. No se reconstruye acá porque una fila declara el
comando que lo probó, y ese comando no lo corrió esta ronda.

**Cada regla nueva se comprobó rompiéndola**, que es la regla del circuito.

| Regla | Cómo se rompió | Qué dijo, y quién lo dijo |
| :-- | :-- | :-- |
| El README del producto compuesto deja de declarar memoria | Se quitó el binding sobre `README.md` del manifiesto del módulo | `The readme still claims the product stores nothing after the module went in.` — el circuito de composición |
| El producto declara su adaptador al arrancar | Se cambió `scope: 'persistence'` por `scope: 'store'` en la plantilla del adaptador de memoria | `The product did not declare which persistence adapter is bound.` — el circuito de generación |
| El manejo de la request corre dentro de su contexto | Se quitó el envoltorio `withRequestId` en el interceptor | `Received: undefined` en la prueba `makes the identifier readable from inside the handling of the request` — **la propia suite del producto** |
| Toda entrada de la request lleva su identificador | Se cambió la clave que adjunta el adaptador por `traceId`, lo que pasa el lint y el typecheck del activo | `No entry of the domain carried the request that caused it, so the log cannot be read per request.` — el circuito de generación |
| Ninguna ruta declarada queda sin caso de humo | Se apuntó la plantilla del caso de consulta a otra ruta | `/party-references/:id is a route of party-directory-api and its smoke test does not name it.` — el circuito de generación |

Todas se restauraron y los circuitos volvieron a verde. Las dos últimas muestran que la correlación
queda con **dos redes**: una viaja dentro del producto y otra vive en la línea.

Dos cosas se descubrieron sin provocarlas, y las dos cambiaron una decisión:

- La comprobación de la tabla de eventos falló contra `party-directory-api`, que se deriva sin
  eventos. La regla quedó condicionada a lo que el registro declara en `domainEvents`, y comprueba
  también el caso inverso: que un producto sin eventos no liste ninguno.
- La columna del identificador en la forma legible cortaba a ocho caracteres, y contra un producto
  real `edge-7781` salió como `edge-778`: un identificador corto mostrado como si estuviera completo
  y fuera otro. La columna pasó a nueve, muestra entero lo que entra y marca con elipsis lo que
  cortó.

### Las roturas de la segunda ronda

| Regla | Cómo se rompió | Qué dijo, y quién lo dijo |
| :-- | :-- | :-- |
| El espacio de selección solo declara action terms que la release deriva | Se puso `actionTerm: "Notify"` en una operación de `Term Deposit` | `Term Deposit/initiate declares the action term 'Notify', which this release does not derive.` — `verify:artifacts`, que antes lo dejaba pasar |
| Un punto de selección lee de una fuente que la herramienta sirve | Se apuntó `routeStyle` a `model/shapes.json` | `routeStyle reads its options from 'model/shapes.json', which the tool does not serve.` — `verify:artifacts` |
| Dos behavior qualifiers de una capacidad no comparten nombre | Se renombró `Charge` como `Interest` | `Duplicated behavior qualifiers in Term Deposit.` — `verify:artifacts` |
| Una operación de qualifier no deriva el nombre de una del control record | Se agregó `execute-interest` al nivel control record | `Term Deposit/Interest/execute derives the same name as the control-record operation 'execute-interest'.` — `verify:artifacts` |
| Un qualifier solo declara action terms derivables | Se puso `Exchange` en una operación de `Interest` | `Term Deposit/Interest/retrieve declares the action term 'Exchange', which this release does not derive.` — `verify:artifacts` |
| Ninguna ruta declarada queda sin un caso de humo **que la pida** | Se apuntó la plantilla del caso de qualifier a otra ruta | `/TermDeposit/:id/Interest/:interestId/Retrieve is a route of term-deposit-api and its smoke test does not ask for it.` — el circuito de generación, **después** de darle dientes a la regla |
| El documento OpenAPI agrupa cada operación bajo su nivel | Se quitó el prefijo `BQ - ` del tag | `The api document of term-deposit-api does not group retrieve-interest under 'BQ - Interest'.` — el circuito de generación |
| Una capacidad declarada registra el Business Domain que la contiene | Se derivó sin `--business-domain` | `No value given for: businessDomain.` — la resolución de la entrada |
| El Business Domain de una capacidad declarada es uno de los nueve | Se pasó `Treasury` | `businessDomain: 'Treasury' is not one of Customer Management, Sales, Servicing, Cross Channel, Loans and Deposits, Payments, Account Management, Operational Services, Collateral Administration.` |
| El nombre de una capacidad declarada es un nombre | Se pasó `savings pocket` | `capabilityName must use the name of a capability, each word capitalised. Example: Savings Pocket. Received: 'savings pocket'.` |
| Un Business Domain no se declara para una capacidad del catálogo | Se pasó `--business-domain` con `Term Deposit` elegido | `A business domain is declared only for a capability that is not in the catalog.` — la regla del modelo |
| Toda capacidad y toda operación traen su glosa, y toda pregunta su etapa | Se quitó un `plainName`, un `plainDescription` de qualifier y un `stage` | `must have required property 'plainName'`, `'plainDescription'` y `'stage'` — `verify:artifacts` |

Todas se restauraron y los circuitos volvieron a verde. **La séptima es la que más enseña**: la regla
existía desde G3, se leía correcta y no lo era. Una prueba que pidiera otra ruta pasaba, porque el
título de la prueba nombra la ruta. Romper una regla no sirve si la rotura no la toca.

## Tercera ronda — el segundo módulo del catálogo (G11), 2026-11-05

El segundo módulo del catálogo, `@bsl/observability`, que construye la primera capacidad del orden de crecimiento. Prueba que un módulo de otra naturaleza entra sin cambiar el núcleo, el esquema del manifiesto ni la operación.
### G11, cambio por cambio

| # | Qué cambió | Versión |
| :-- | :-- | :-- |
| G11-a | `@bsl/observability` `0.1.0`: exporta las entradas del log, el span de cada request y las mediciones a un colector del protocolo OpenTelemetry, en su codificación JSON sobre HTTP y **sin dependencias de ejecución**. Muestreo del estándar, cola de 2048 señales, series acumulativas | `@bsl/observability` 0.1.0, `@bsl/catalog` con cuatro entradas |
| G11-b | `TelemetryPort` entra al contrato con tres operaciones, y **ningún adaptador del activo base lo satisface**. El producto reporta a un puerto que puede no tener implementación, y lo inyecta opcional | `@bsl/contracts` 0.3.0 |
| G11-c | El producto reporta en los tres lugares donde produce telemetría: el adaptador del logger entrega cada entrada que escribió, el interceptor y el filtro el span y la duración de la request que respondió y de la que falló | `@bsl/base-template` 0.19.0, `@bsl/cli` 0.23.0 |
| G11-d | El módulo declara la región `bsl:telemetry` del README del producto, que es el octavo punto de inserción, con el mecanismo que abrió y **sin tocar la herramienta** | — |
| G11-e | El circuito gana cinco pasos y un rechazo: incorpora el segundo módulo al producto que ya tiene el primero y comprueba, contra un colector de verdad, que las señales salen y que la traza del llamador se continúa | `@bsl/cli` 0.23.0 |

## Cuarta ronda — la API documentada como página (G12), 2026-11-06

La API documentada como página: el producto sirve `GET /docs` con el visor de OpenAPI cargado de la copia instalada y nunca de internet.
### G12, cambio por cambio

| # | Qué cambió | Versión |
| :-- | :-- | :-- |
| G12-a | El producto sirve `GET /docs`: una página que renderiza el documento que `/openapi.json` ya sirve, con el visor de OpenAPI cargado **de la copia instalada con el producto** y nunca de internet. Dos archivos del visor, cada uno en su ruta explícita: no hay ruta que componer ni directorio que exponer | `@bsl/base-template` 0.20.0, `@bsl/cli` 0.26.0 |
| G12-b | `API_DOCS` decide si la ruta existe, con `auto` por default: prendida en todo ambiente salvo producción. Apagada, `/docs` responde `404` y el servicio tiene la superficie que tenía antes | — |
| G12-c | El asiento de arranque nombra la dirección de la página al lado de la de las sondas, y solo cuando la página responde | — |
| G12-d | El circuito de generación comprueba sobre un producto derivado que la página responde como HTML, que el visor responde desde el producto, que renderiza `/openapi.json` y que **no carga nada de internet** | `@bsl/cli` 0.26.0 |

## Quinta ronda — el recorrido de creación (G13), 2026-11-07

El recorrido de creación de `bsl new`, abierto por dos reportes de uso del autor: «si se me daña algo se me sale todo», y que no se ve qué campo es obligatorio.
### G13, cambio por cambio

| # | Qué cambió | Versión |
| :-- | :-- | :-- |
| G13-a | Una respuesta que la pregunta no acepta se rechaza **en la pregunta**, que queda abierta. Antes se validaba después de cerrarla: un valor que rompía el patrón de su punto terminaba el comando y tiraba todo lo contestado. La condición sigue declarada una vez en el modelo y leída una vez en el núcleo | `@bsl/cli` 0.28.0 |
| G13-b | Una selección múltiple por debajo de su mínimo se rechaza ahí mismo. Desmarcar las cuatro operaciones terminaba el comando al final de la resolución, con el `minItems: 1` del modelo sin llegar nunca a la pregunta | — |
| G13-c | La tecla de escape **retrocede una pregunta**; cuando no queda ninguna atrás, sale. Vuelve a la última pregunta realmente hecha, no a un punto que respondió una bandera, y olvida lo que dependía de ella | — |
| G13-d | Cancelar deja de reportarse como defecto de la herramienta. La interrupción de la terminal llegaba a la raíz de composición como fallo no previsto y respondía `This is a defect of the tool. Report it with the command that produced it.` Ahora es `CancelledError`, línea informativa y código 130 | — |
| G13-e | Lo obligatorio se comprueba de verdad sobre lo escrito: `description` y `owner` son obligatorios y sin patrón, así que una respuesta vacía pasaba y el producto quedaba con descripción vacía | — |
| G13-f | La ayuda marca los once parámetros obligatorios de `bsl new`, que no marcaba ninguno: la operación los declaraba desde el modelo sin copiar el campo que lo dice. Se distinguen `required` y `asked`, porque exigirlos como bandera habría pedido trece banderas antes de preguntar nada | `@bsl/cli` 0.28.0 |
| G13-g | Los argumentos sin bandera se declaran como dato, y con eso cada ayuda abre con su línea de invocación. `bsl add persistence` estaba documentado solo en el texto del error que se queja de su ausencia | — |
| G13-h | Los diecisiete parámetros de `bsl new` se agrupan por la etapa que el modelo declara, más un bloque de los propios del comando, y las dos ayudas cierran con invocaciones de ejemplo | — |

## Sexta ronda — el almacén de plantillas (G14), 2026-11-09

El almacén de plantillas. No la abrió el informe externo ni un reporte de uso, sino una auditoría del anteproyecto: su alcance compromete un sistema de almacenamiento de plantillas, el objetivo específico 2 habla de plantillas en plural, y la línea tenía una y no tenía dónde poner una segunda.
### G14, cambio por cambio

| # | Qué cambió | Versión |
| :-- | :-- | :-- |
| G14-a | Una plantilla es un activo del catálogo del mismo rango que un módulo, y **se describe a sí misma** en un `bsl-template.json` dentro de su paquete, con su esquema al lado. El catálogo gana el tipo `template` y `bsl templates list` muestra el almacén | `@bsl/cli` 0.29.0 |
| G14-b | Las plantillas salen de la herramienta y pasan al paquete de la plantilla. El `files` de `@bsl/cli` queda en `bin` y `dist` | — |
| G14-c | El motor gana condición y repetición con una gramática cerrada, sin `eval`: la condición la lee **el mismo evaluador** que lee una restricción del modelo, con cuatro formas nuevas. **51 archivos `.tpl` bajan a 29** | — |
| G14-d | Se escribe la frontera: qué es expresable como dato y qué no, con su lista cerrada. Dos cosas se **eliminan** en vez de expresarse —el formato por ancho de línea y el impresor de literales del documento OpenAPI | — |
| G14-e | `derive.ts` pasa de 919 a 586 líneas y entra `interpret.ts`, de 203, con una firma que **no nombra framework, estándar ni carpeta de un producto** | — |
| G14-f | La forma del producto es un contrato declarado: la plantilla la declara, el producto la lleva en su `project.json` y el módulo dice a qué formas sirve. Ocho puntos de inserción con su clase y su comentario, dos puertos y cuatro supuestos | `@bsl/cli` 0.30.0 |
| G14-g | El esquema del registro de un producto se compara **por versión mayor**. Era por igualdad exacta, contra lo que su propia prosa decía | — |
| G14-h | La superficie se agrupa: `new · templates list\|show · modules list\|add\|update\|remove · status`. `bsl add`, `bsl update` y `bsl assets` quedan como alias vivos en todo `0.x`, listados aparte | — |
| G14-i | Una plantilla de otra familia entra **como fixture de prueba**: Python, trabajo por lotes, comentarios `#`, forma propia y un contrato que no es el de esta línea. Once pruebas | — |
| G14-j | El módulo declara `serves`, y la composición lo rechaza antes de las ocho reglas si no coincide | `@bsl/persistence` 0.4.0, `@bsl/observability` 0.2.0 |
| G14-k | `nest` pasa a `composition`: el framework es propiedad de la forma y no del módulo. `nest` se sigue leyendo como alias | — |
| G14-l | La actualización comprueba lo que comprueba la incorporación. No repetía ninguna de las ocho reglas, y eso era un hueco: un `update` podía meter un módulo de otro mayor del contrato, o de otra forma, sin que nadie lo mirara | — |
| G14-m | **`bsl modules remove`**: quitar un módulo restaura lo que la derivación escribió. Es la tercera queja del autor y la única del grupo que **ningún requerimiento pide**, así que ampliar el alcance de la línea fue decisión suya, declarada como tal | — |

## Séptima ronda — las divergencias del anteproyecto (G15), 2026-11-09

Las divergencias respecto del anteproyecto. El expediente declaraba una y había diez; ninguna era un descuido, y en todas faltaba el acto de decir que lo prometido no se cumple así y por qué.
### G15, divergencia por divergencia

| # | Qué promete el anteproyecto | Qué pasó, y qué se hizo |
| :-- | :-- | :-- |
| G15-a | El rango de Node del objetivo general y del alcance: «(v22–v24)» | El piso real es **24** y el punto de entrada rechaza v22 y v23 con código 2. lo subió con tres razones correctas y sin ver que revisaba el objetivo general. Se declara: se eligió entregar un producto verificable en una versión antes que uno no verificable en tres |
| G15-b | «alineados con … BIAN e **ISO 20022**» | ISO 20022 **no se cumple**. lo excluyó bien y cerró diciendo que mantenía «sin cambios la redacción de los objetivos», que es correcto pero no dice **qué cláusula** queda sin cumplir. Se nombra. Y se declara la cobertura de BIAN: **5 de las 46** capacidades extraídas, con solo `Term Deposit` transcrita de su documento oficial |
| G15-c | «documentación openAPI **basada en los módulos y funcionalidades integradas**» | **El anteproyecto se contradice**: su metodología dice «basada en la **estructura** del proyecto generado», y eso sí se cumple. La cláusula del alcance es **incumplible por diseño**, porque fija que un módulo no aporta adaptadores de entrada. Se declara citando las dos frases |
| G15-d | Los cuatro riesgos éticos y sus mitigaciones | **No se mencionaban en ningún documento del expediente**, comprobado por búsqueda sobre todo `Implementación/`. Se declaran uno por uno: el 1 cumplido y verificado por ejecución, el 2 no materializado con su condición de reactivación escrita, el 3 **cumplido a medias** —la documentación por niveles de experiencia se rechazó en la Fase 3 por oportunidad, sin ver que era un compromiso ético—, y el 4 con el mecanismo probado y el ejercicio ausente |
| G15-e | «**Desarrollo** de un sistema de almacenamiento de plantillas» | Cumplido **por adopción y no por desarrollo**: el almacén existe desde G14 y el servicio que guarda los bytes es el registro de la organización. Y tenía que ser así, porque **RF-15** pide explícitamente que no haya canal propio de distribución |
| G15-f | «contratos … **compartidos entre proyectos**» y «compartidas **entre múltiples proyectos**» | **Lo único que pidió código.** El circuito trabajaba sobre **un** producto. Se agrega un paso que incorpora el mismo módulo a un segundo producto y comprueba que el cableado se nombra por **el agregado de cada uno**, con la comprobación negativa incluida. El circuito pasa a **22 pasos** |
| G15-g | El plural de «plantillas **configurables**» del objetivo 2 | Cerrado construyendo, en G14 |
| G15-h | «en el contexto del **Laboratorio Digital del Banco W**» | Ya estaba declarada |
| G15-i | La lista de objetivos del índice de la fase | Corregida a los cuatro objetivos **textuales**, citados y no parafraseados, más dos secciones nuevas: el objetivo general cláusula por cláusula y el alcance capacidad por capacidad |

## Octava ronda — la segunda plantilla del almacén (G16), 2026-11-09

La segunda plantilla del almacén, sobre Azure Functions. Lo primero fue verificar si se podía: el proyecto excluía serverless dos veces, y el anteproyecto no lo excluye.
### G16, cambio por cambio

| # | Qué cambió | Versión |
| :-- | :-- | :-- |
| G16-a | La familia admite un producto **sin servidor propio**. La exclusión pasa de «aplicaciones serverless» a **«aplicaciones sin API HTTP expuesta»**, porque la condición mínima de pertenencia —exponer una API HTTP documentada bajo OpenAPI— la cumple una función con trigger HTTP. **Revisión**, no Ruptura | — |
| G16-b | Toda plantilla vive bajo `packages/templates/`, con convención de nombres escrita, el validador de manifiesto **compartido** en `scripts/` y el procedimiento de agregar una en `packages/templates/README.md`. `@bsl/base-template` pasa a **`@bsl/nestjs-hexagonal-api`** | `@bsl/nestjs-hexagonal-api` 0.21.0 |
| G16-c | El producto **registra la plantilla que lo derivó** y no un literal. El scope gana `templatePackage` y `templateVersion`, y el `role` pasa de `base` a `template` | `@bsl/cli` 0.30.0 |
| G16-d | Entra **`@bsl/azure-functions-api`**, que deriva un API HTTP de un Service Domain sobre Azure Functions, forma `azure-functions@1`, con sus tres límites declarados | `@bsl/azure-functions-api` 0.1.0, `@bsl/catalog` 0.5.0 |

## Novena ronda (G17) — El recorrido abre eligiendo la plantilla

El recorrido abre eligiendo la plantilla. Lo abrió un reporte de uso, y lo que apareció es más grande que la pregunta que falta: el cuestionario corría antes de leer el catálogo.
| Fecha | Grupo | Qué cambió | Versión | Comando que lo prueba |
| :-- | :-- | :-- | :-- | :-- |
| 2026-11-09 | G17-a | **La plantilla se decide antes de la primera pregunta del modelo.** La lectura del catálogo y la resolución de la plantilla se mueven delante del cuestionario, así que un rechazo por plantilla —o un catálogo ilegible— llega **antes de que nadie escriba nada** | `@bsl/cli` 0.32.0 | Prueba de orden en `generate.operation.spec.ts`, **comprobada rompiéndola** como pide : con el orden anterior el error que sale es `No value given for: projectName` y no el de la plantilla, así que la prueba falla. Y con la herramienta real, sin terminal: el rechazo es la primera línea después de leer el catálogo |
| 2026-11-09 | G17-b | **Si la invocación no nombra la plantilla, se pregunta**: una opción por plantilla ofrecida, el id como etiqueta y lo que deriva como pista. Con una sola ofrecida no se pregunta, que es lo de antes. Una `proposed` no se ofrece, porque la derivación la rechazaría | `@bsl/cli` 0.32.0 | Siete pruebas en `template-reference.spec.ts` y dos en `generate.operation.spec.ts`. **El render lo confirma el autor**, que exige terminal real |
| 2026-11-09 | G17-c | **Un hueco de documentación, no de código:** la tabla de parámetros del comando de derivación —hoy el doc 4 §11 de la Fase 2— **nunca nombró `--template`**, siendo el parámetro que decide qué deriva el comando. Existía desde | — | Encontrado al alinear el doc 5; queda como fila con su forma `id` o `id@version` |

| 2026-11-09 | G17-d | **Un hallazgo propio, y es de la puerta:** `check:push` **no hacía typecheck**. Corre `lint`, el `verify` de cada activo, los dos circuitos y la auditoría, y ninguno pasa `tsc --noEmit` sobre el monorepo: el `build` del `verify` usa `tsconfig.build.json`, que **no incluye `test/`**. Así que un error de tipos en una prueba **pasaba la puerta lenta** y lo atrapaba solo el `pre-commit`. Es la segunda vez en el día que la puerta lenta comprueba **menos** que la rápida —la primera fue que no linteaba los `scripts/`, en G14— | — | Lo encontró el `pre-commit` rechazando un commit que `check:push` había dado por bueno minutos antes, con el mismo archivo en disco. `npm run typecheck` entra a `check:push` después del `lint` |

| 2026-11-09 | G17-e | **Segundo reporte de uso, y éste no es una molestia: son instrucciones que fallan al ejecutarlas.** Los pasos que `bsl new` imprime al terminar estaban **escritos en el código de la herramienta** —`cp .env.example .env` y `npm run start:dev`—, y con una sola forma de producto eran verdad **por casualidad**. El producto de Azure Functions no tiene ninguno de los dos: su archivo de configuración es `local.settings.json.example` y se arranca con `npm start`, que envuelve `func start`. Es el mismo patrón del literal que encontró en `project.json.tpl` | `@bsl/cli` 0.32.0 | Derivando los dos productos con la herramienta construida: el hexagonal imprime **exactamente** los pasos de antes, el de Azure imprime los suyos, y el `cp` que reporta se ejecutó sin error. Dos pruebas nuevas, la segunda derivando con la plantilla real de Azure, **comprobada rompiéndola** como pide |
| 2026-11-09 | G17-f | **Y el dato que vuelve el episodio claro: la instrucción correcta ya existía.** El `README.md` que la plantilla de Azure escribe en el producto dice textualmente `cp local.settings.json.example local.settings.json` y `npm start`. La plantilla sabía los pasos y la herramienta los afirmaba por su cuenta, y entre las dos tenía razón **la plantilla**, porque es la que escribe el producto. Ahora todo paso se lee del plan aplicado, y el reporte cierra apuntando al readme en vez de repetir lo que una forma necesita de más | — | Se descartó declarar los pasos en el manifiesto —que es lo que el plan de la sexta ronda diseñó y nunca se construyó, un punto de— por dos razones: un manifiesto puede **mentir** y el plan **es** el producto, y las dos plantillas están publicadas sin esa sección. Leer el producto funciona además para la plantilla de un tercero sin que declare nada |

| 2026-11-09 | G17-g | **Un error de método propio, y el autor lo destapó reportando el mismo fallo media hora después.** El arreglo estaba construido y commiteado; lo que corría el autor era una **instalación global de `0.31.0` anterior al arreglo**, y el arreglo había entrado **dentro de esa misma `0.31.0`** sin publicar, así que la copia y el checkout decían la misma versión y se comportaban distinto | `@bsl/cli` **0.32.0** | Leyendo las líneas de `reporter.info` del `dist` instalado contra las del `dist` del checkout. **Regla nueva:** una versión se vuelve a mover en cuanto un build de ella **salió del checkout** —publicado o instalado—, no solo al publicar. El `README` del monorepo gana *Running the tool you are changing*, con las dos formas de correr lo que se cambia y la comprobación de `which bsl` y `bsl --version` como primer paso |
| 2026-11-09 | G17-h | **Y una comprobación mal hecha, que vale anotar:** el primer `grep` del literal `cp .env.example .env` sobre el `dist` dio positivo en **las dos** copias, porque pegaba en el TSDoc de y no en código. Afirmé desde ese grep antes de distinguirlo | — | Un `grep` que no distingue comentario de código **no es evidencia**. Lo que decidió el caso fue leer las líneas de `reporter.info` del archivo construido |

| 2026-11-09 | G17-i | **`func: command not found`, y la validación dice que no es un defecto:** `npm install` y `npm run verify` —analizador, cuatro pruebas y build— pasan **sin** `func`; el readme del producto dice textualmente `npm start # needs the Azure Functions Core Tools`; y las consecuencias asumidas de ya lo declaraban. Meter las Core Tools al producto queda **descartado con un número detrás**: `azure-functions-core-tools@4.16.0` pesa 39 KB porque **baja el binario de internet en un `postinstall`**, lo que haría que `npm install` de todo producto derivado dependa de un CDN externo — exactamente lo que mantiene lejos | — | `npm install` y `npm run verify` en el producto derivado, los dos en código 0 sin `func`. `npm view azure-functions-core-tools scripts` muestra el `postinstall` |
| 2026-11-09 | G17-j | **Pero el paso impreso era cierto e incompleto**, y el autor decidió corregirlo: un paso que corre un script del producto **muestra el comando que corre**, leído de sus `scripts` como todo lo demás del reporte. `npm start  # func start`, `npm run start:dev  # nest start --watch`. Así la herramienta externa se nombra **antes** de que el paso falle, sin que la plantilla declare nada | `@bsl/cli` 0.32.0 | Derivando los dos productos. Se evaluó la primitiva `pairs` que reserva para pares alineados y se descartó acá: alinearía a una columna común y la línea larga del `cp` empujaría el comentario al margen; como solo dos pasos del bloque son scripts, no hay nada que alinear |

| 2026-11-09 | G17-k | **Validado contra el documento oficial del host, y encontró un defecto de la plantilla.** El autor pidió validar si había alguna forma de correr su función local sin los Core Tools. La guía de Microsoft dice que no la hay —*«you must run the host provided by the local Functions runtime»*— y para JavaScript en macOS lista exactamente dos entornos, los dos exigiéndolo. Pero el `local.settings.json.example` que la plantilla derivaba declaraba `AzureWebJobsStorage: UseDevelopmentStorage=true`, que la guía exige **solo para triggers que no son HTTP** y que obliga a tener **Azurite instalado y corriendo**. El producto tiene solo tres `app.http` y persiste en memoria: la línea le agregaba un emulador como requisito de arranque, o sea **una segunda pared** después de instalar `func` | — | Retirada del ejemplo; el README del producto declara por qué no está y cuándo agregarla. `npm run verify -w @bsl/azure-functions-api` en verde. Es el patrón de en otro estándar: el dato venía del scaffold genérico de `func init`, no del documento oficial de esta forma |
| 2026-11-09 | G17-l | **Y la instrucción de instalación queda escrita para un equipo mixto**, que es lo que el autor pidió: `npm install -g azure-functions-core-tools@4`, **el mismo comando en macOS, Windows y Linux**, con `brew` y la extensión de VS Code como alternativas por plataforma. De paso quedó explicado por qué el compañero del autor «solo lo corría» en Windows: la extensión de VS Code le instaló los Core Tools sola | — | La guía oficial también documenta un **Azure Functions CLI v5** en *preview*, con instalación por *workloads* y por lo tanto mucho más chica. No se adopta como requisito de la línea por estar en preview, y queda anotado como alternativa para una máquina de desarrollo |

| 2026-11-10 | G17-m | **La regla de se rompió dos veces el mismo día que se escribió**, y lo encontró comprobar el feed después de publicar. `@bsl/cli`: el commit del bump a `0.32.0` fue seguido por seis más, uno de ellos la anotación `# func start`, así que el **tarball publicado imprime `npm start` pelado**. `@bsl/azure-functions-api`: la corrección que retiró `AzureWebJobsStorage` entró **sin subir la versión**, así que la plantilla publicada sigue derivando el ajuste que exige Azurite | `@bsl/cli` **0.33.0**, `@bsl/azure-functions-api` **0.2.0** | Extrayendo el `.tgz` publicado y derivando un producto **del feed**, no desde la caché de `npx`. **Una regla sin mecanismo no se cumple:** el mecanismo candidato —que el `prepublishOnly` compare el contenido contra el último publicado de esa versión— queda escrito en y sin construir, porque construirlo sin pedido amplía el alcance |

## Excluido con argumento

No son huecos: son propuestas que no encontraron requisito que las sostenga, cada una con el
documento que la descarta.

| Propuesta del informe | Por qué no entra |
| :-- | :-- |
| `501 Not Implemented` en las operaciones de andamio (12) | La operación no está sin implementar: carga el agregado, lo persiste, publica su evento y registra el resultado. Lo que falta es el efecto de negocio, que pertenece al equipo del producto. Un `501` habría que borrarlo a mano en cada producto, contra RNF-02 |
| Autocorregir un valor rechazado (2) | El nombre del agregado nombra carpetas, clases, rutas y eventos; cambiarlo en silencio esconde una decisión del desarrollador |
| Wizard de atributos e invariantes (5) | Convierte la herramienta en una de modelado de dominio e impone supuestos de negocio a cada producto |
| Perfiles de agregado (5) | Depende de que la evaluación muestre que la semilla no alcanza. Decidirlo antes de medir es inventar el requisito (el índice de la Fase 3). Si la Fase 4 lo muestra, es recomendación del informe |
| Lenguaje natural en la pregunta de operaciones (3, propuesta 2) | Reabierto el 2026-11-02 como candidato medible. **Construido el 2026-11-03 en G6 y G10.** Medirlo primero no bajaba la curva de adopción, que es el hallazgo que lo motiva. La pregunta muestra ahora la glosa en lenguaje llano y, al lado, **la ruta que va a salir**: el estilo de ruta y el agregado ya están contestados cuando esa pregunta llega, así que la ruta mostrada es la real |
| Reorganizar `test/` por feature o espejo de `src` (13) | Una jerarquía para tres archivos de ejemplo es ruido, y las pruebas que el equipo escriba son suyas |
| Documentación por audiencia (7) | Crece con los módulos incorporados; hacerla antes documenta un producto que todavía va a cambiar de forma (el índice de la Fase 3) |
| Separar estándar, capability, producto y agregado en la presentación (3, propuesta 1) | ~~Es reestructuración del espacio de selección y no cambia qué puede incorporarse~~. **Revisada el 2026-11-03: construida en G6 y G10.** El argumento confundía reestructurar el espacio con presentarlo: la lista se lee ahora en lenguaje de negocio con el nombre del estándar alineado al lado, y eso no reestructura nada ni cambia qué puede incorporarse. Es dato del artefacto, una glosa por entrada, no código |
| Capability personalizada (3) | ~~Debilita la alineación con el estándar, que es el objetivo general del proyecto~~. **Revisada el 2026-11-03: construida en G9.** El argumento se cae contra el propio marco: MR-02 §3 y la tesis ya admiten declarar un Service Domain fuera del espacio por defecto y prohíben solo omitir el metadato. Estaba declarado y no implementado. La forma queda cerrada —Business Domain entre los nueve, action terms entre los cinco, área derivada del grupo— así que el metadato sigue validado y la alineación no se debilita: lo que cae es la forma, no la razón |
| Interfaz de exploración del tipo Swagger UI (8) | ~~Exige una dependencia en todo producto o un script externo, inadmisible en el entorno~~. **Revisada el 2026-11-06: construida en G12.** El argumento mezclaba dos razones. La del script de internet sigue en pie y se respeta: el visor se carga de la copia instalada con el producto, en rutas del propio servicio, y el circuito comprueba que la página no contiene ninguna dirección `http`. La de la dependencia protegía lo que un servicio **desplegado** carga, y eso no cambia: el visor es dependencia **de desarrollo**, ausente de una instalación de producción, y la auditoría de RNF-04 corre con `--omit=dev`. Lo que dejaba abierto —«quien quiera la interfaz la monta en su producto»— es lo que G12 resuelve una vez para la línea |
| Colección Postman o Bruno (8) | `GET /openapi.json` permite generarla fuera del producto, sin que la línea cargue con otro formato |
| Pruebas e2e del producto (14) | Un circuito e2e con datos de prueba tarda, se rompe por razones ajenas al cambio que se prueba y es trabajo del equipo. Lo que la línea entrega es el humo: barato, estable y suficiente para que un cableado roto no pase la puerta |
| Selector de persistencia en `bsl new` (11) | Primero el módulo existe y se incorpora. Ofrecerlo al derivar agrega un camino más sin resolver nada nuevo (doc 3 §13 de la Fase 3) |
| Segundo módulo, observabilidad avanzada, mensajería, catálogo administrado y métricas de plataforma | ~~Catálogo posterior ya declarado: ~~. **Revisada el 2026-11-05: el segundo módulo está construido** (G11, ), y con él la observabilidad y las métricas, que eran la primera capacidad del orden del doc 1 §10 de la Fase 3 y la que habían dejado lista para construir. La mensajería, el catálogo administrado y las demás capacidades siguen declaradas como crecimiento con el mismo argumento, y conservan su orden. El dominio BIAN, en ; el retiro y la migración de activos, en |
