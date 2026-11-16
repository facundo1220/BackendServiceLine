# Log de decisiones — Evaluación y validación del artefacto

Trabajo de grado: *Desarrollo de una herramienta CLI para la generación automatizada de proyectos backend e integración de módulos reutilizables*
Fase 4 — evaluación y validación del artefacto

Cómo se evalúa, con quién, con qué instrumentos y qué se acepta como evidencia. A diferencia de los logs
anteriores, acá casi ninguna decisión es sobre el artefacto: son decisiones de **método**, y cada una
condiciona qué puede concluir la tesis. Por eso quedan registradas antes de medir y no después, donde serían
una justificación de lo que salió. Cada una es trazable a una actividad del anteproyecto, a un requerimiento
de la Fase 1 o a una decisión previa del marco, del mecanismo o del gestor.

## Convenciones

- **Terminología**: como en los logs anteriores, los términos técnicos se mantienen en inglés dentro de prosa
  en español.
- **Estados**: Aceptada · Aceptada (provisional) · Diferida · Revisada · Sustituida.
- **Numeración**: continúa la numeración global del proyecto. Este log abre en **ADR-167**: ADR-165 quedó en el
  log de la Fase 1, con la línea base, y ADR-166 en el de la Fase 2, con la presentación de las listas de la
  herramienta. La regla es que cada decisión va al log de la fase cuyo artefacto toca, no al de la fase en
  curso.

**Significado de los estados**

| Estado | Qué indica |
| :---- | :---- |
| Aceptada | Decisión firme de método, aplicada en la evaluación |
| Aceptada (provisional) | Decisión tomada antes de tener evidencia de que el método funciona, con su condición de revisión declarada |
| Diferida | Corresponde a trabajo futuro; se conserva como insumo |
| Revisada | Modifica una decisión previa de esta fase o de una anterior |
| Sustituida | Reemplazada por otra; se conserva por trazabilidad |

## Índice de decisiones

| ID | Decisión | Documento | Estado | Revisada después por |
| :---- | :---- | :---- | :---- | :---- |
| ADR-167 | La evaluación se hace con las personas del contexto y en su entorno, no como caso de estudio del laboratorio | el índice de la fase | Aceptada, con nota de revisión del 2026-11-07 | — |
| ADR-168 | Tres llamadas de una hora, conversadas y no guionadas, que cierran con un instrumento escrito; y lo que se busca es viabilidad y adopción, no un veredicto | Doc 1 / Doc 2 | Aceptada | — |
| ADR-184 | El cumplimiento del anteproyecto se audita antes de evaluar, y cada divergencia se declara | el índice de la fase / el índice de la fase | Aceptada | — |
| ADR-185 | El piso de Node es 24, que es más estrecho que el rango que el anteproyecto promete | el índice de la fase | Aceptada | — |
| ADR-186 | Qué cláusula del objetivo general no cumple la exclusión de ISO 20022, y hasta dónde llega la alineación con BIAN | el índice de la fase | Aceptada | — |
| ADR-187 | La documentación OpenAPI se deriva de la estructura del producto y no de sus módulos | el índice de la fase | Aceptada | — |
| ADR-188 | Los cuatro riesgos éticos, uno por uno, con lo que se hizo y lo que no | el índice de la fase | Aceptada | — |
| ADR-189 | El almacén de plantillas se cumple adoptando el registro de la organización, no desarrollando uno | el índice de la fase | Aceptada | — |

---

## ADR-167 · La evaluación se hace con las personas del contexto y en su entorno, no como caso de estudio del laboratorio

**Estado:** Aceptada · 2026-11-06 · el índice de la fase

**Contexto.** El anteproyecto compromete un **caso de estudio en el laboratorio**: aplicar la solución
en un entorno de desarrollo real, dentro de una iniciativa. El autor ya no pertenece a ese
laboratorio, y eso alcanza a cuatro compromisos:

| Compromiso | Qué pedía | Estado |
| :---- | :---- | :---- |
| Actividad 2 del anteproyecto | Derivar un proyecto e incorporar un módulo en el entorno real, dentro de una iniciativa | No ejecutable como está escrito |
| **RNF-03** | Que el producto se analice con las herramientas de la organización sin adaptación previa | Recuperable: los participantes de dentro pueden instalar la herramienta del feed en su entorno |
| Noveno criterio de la rúbrica externa | Que un líder no técnico explique propósito, alcance y pendientes sin leer código | **Medible**: el líder técnico tiene mirada de negocio y no usa la herramienta |
| La medición de los requerimientos | Daba por hecho que la Fase 4 mide «en el laboratorio y con un equipo que lo usa» | Esa frase deja de ser cierta: la evaluación se hace en los entornos de los participantes |

**Decisión.** La evaluación se ejecuta con las personas del contexto estudiado y en sus propios
entornos, y no como un caso de estudio sancionado por el laboratorio.

**Qué preserva.** Los tres participantes técnicos son **los mismos informantes de la Fase 1**, y dos de
ellos son quienes declararon la banda de 15 y 8 días que hoy es la línea base. La evaluación queda como
un antes/después con los mismos informantes. Los dos pueden instalar la herramienta del feed dentro de
la organización, con lo que RNF-03 se mide con su criterio textual.

**Qué pierde.** El encuadre formal: no hay iniciativa real sobre la cual derivar, no hay un equipo
observado en el tiempo, y no hay autorización institucional. Mide **uso informado por participantes
individuales**, no adopción por un equipo.

**Qué no se hace para disimular la pérdida.** No se presenta el ejercicio como el caso de estudio del
anteproyecto, no se construye un caso ficticio que se le parezca, y no se sustituye el rol no técnico
por un técnico que responda en su nombre.

**Alternativas.** *Evaluar solo con el autor, instrumentado*: produce datos reproducibles y no dice
nada de usabilidad; queda como una de las cuatro participaciones y no como la evaluación. *Buscar otra
organización*: mediría contra una línea base que no es la del documento 7. *Reescribir el compromiso
en el anteproyecto*: es norte fijo, y la divergencia se declara en la tesis.

**Por qué.** Es la operación que **ADR-165** aplicó a la línea base, por la misma razón: cuando una
condición del diseño se pierde, el daño lo hace el sustituto que parece equivalente, no la pérdida.

**Consecuencia.** El doc 1 caracteriza cuatro participantes `PE-xx` con su distancia y su sesgo, y el
doc 2 fija un protocolo por participante. El doc 7 declara la divergencia en su apertura y el índice de la fase la
lleva al cierre. En la tesis se narra en el capítulo 6 y su límite entra en las conclusiones.

**Traza.** Anteproyecto, objetivo específico 4 y actividades 1 a 4 · resultado esperado 4 · RNF-03 ·
ADR-165, ADR-168 · P-41 · el índice de la fase, Doc 1, Doc 2, Doc 7, el índice de la fase.

---

## ADR-168 · Tres llamadas de una hora, conversadas y no guionadas, que cierran con un instrumento escrito

**Estado:** Aceptada · 2026-11-07 · Doc 1 / Doc 2

**Contexto.** ADR-167 fijó con quién se evalúa; faltaba el cómo. Lo determinan cuatro hechos: la
disponibilidad es de tres llamadas de una hora, cada participante aporta algo distinto, los tres
criterios del objetivo 4 no se miden mirando una demostración, y la Fase 1 ya resolvió este problema
con un instrumento que funcionó.

**La forma se hereda de la Fase 1, y no por comodidad.** Su protocolo fijó una entrevista
semiestructurada de diseño mixto: conversación abierta y, al cierre, ítems cerrados que producen datos
agregables. Repetir esos ítems convierte **el dato de agosto de 2026 en el «antes» y el de esta sesión
en el «después»**, con la misma escala y las mismas personas. Ya está tomada la mitad: «dificultad del
arranque hoy: 3 y 5», «tiempo hasta que el proyecto corre: 15 y 8 días», «costo de propagar un cambio:
4 y 5», «utilidad esperada: 5 y 5».

**Decisión.** Tres llamadas de una hora, conversadas y no guionadas, cada una cerrando con un
instrumento escrito que cada participante completa por separado.

| Llamada | Quién | Qué ocurre | Qué produce |
| :---- | :---- | :---- | :---- |
| 1 | `PE-03` desarrollador interno y `PE-02` líder técnico, juntos | Demostración y conversación abierta | El instrumento de cada uno, por separado, y la reacción del rol de negocio |
| 2 | `PE-04` desarrollador externo | Demostración, uso y conversación | Su instrumento, y la segunda aplicación de su propia rúbrica |
| 3 | `PE-03`, solo | **Uso con las manos**: instala del feed, deriva, incorpora el módulo y escribe la primera operación de negocio | Las tres mediciones del objetivo 4 |

| Participante | Qué hace | Qué sostiene |
| :---- | :---- | :---- |
| `PE-03` Desarrollador interno | Instala, deriva, incorpora y escribe la primera operación. Es quien la usaría a diario y el sujeto de la medición | Los tres criterios del objetivo 4 |
| `PE-04` Desarrollador externo | La usa y vuelve a aplicar la rúbrica que él mismo escribió | El juicio externo, con su propio «antes» |
| `PE-02` Líder técnico | **No la usa.** Observa, reacciona y dice si puede explicar propósito, alcance y pendientes sin leer código | El noveno criterio, y la adoptabilidad |
| `PE-01` Autor | Conduce, cronometra y registra. No responde por usabilidad ni comprensión | Ninguno: produce el registro |

**Lo que la evaluación busca, dicho antes de medir.** Viabilidad y usabilidad en el equipo,
oportunidades de mejora y recomendaciones de adopción. **No un veredicto.** Un hallazgo que muestre que
algo no sirve es un resultado de la fase, y el doc 7 lo reporta con el mismo peso que lo que funcionó.
Queda como decisión y no como intención del informe porque, escrito después de medir, sería una
coartada.

**Si la tercera llamada no ocurre**, el reemplazo está decidido de antemano y en este orden: la misma
tarea entregada para que `PE-03` la haga por su cuenta con una hoja de instrucciones y reporte sus
tiempos; y si tampoco, la ejecuta el autor y `PE-03` revisa y estima qué le habría costado. Las tres
formas valen distinto, y el documento que la use declara cuál ocurrió.

**Alternativas.** *Una llamada con los tres juntos*: el externo no comparte contexto y obligaría a
conversar en el mínimo común. *Guion cerrado*: suprime lo que el participante trae sin que se le
pregunte, y el rigor viene del instrumento del cierre, que sí es cerrado e igual para todos. *Solo
ítems cerrados*: no produciría recomendaciones, que es la mitad de lo que la fase busca.

**Riesgos declarados.** Tres horas no miden adopción en el tiempo. En la primera llamada los dos están
juntos, así que uno puede anclar al otro: por eso el instrumento se completa por separado y el uso con
las manos ocurre a solas. La presencia del autor condiciona lo observado, y la bitácora lo registra
como observación de método. Y `PE-03` conoce el proyecto: no es un sujeto ingenuo.

**Consentimiento.** Igual que en la Fase 1: a cada participante se le dice para qué es la sesión, que
se registra, qué se publica —su rol, nunca su nombre— y que puede pedir que algo no se registre.

**Consecuencia.** El doc 2 **tiene que existir antes de la primera llamada**, con el instrumento
escrito, lo que se cronometra y qué cuenta como evidencia de cada criterio: sin instrumento no hay dato
agregable y las llamadas quedan como anécdota. El acto y la evidencia de cada criterio del objetivo 4
están en los documentos 4, 5 y 6.

**Traza.** Anteproyecto, objetivo específico 4 y actividades 2 y 3 · Fase 1 doc 03 · ADR-165, ADR-167 ·
T-14, RNF-01 · RF-06, RF-10 · Doc 1, Doc 2, Doc 3, Doc 4, Doc 5, Doc 6.

---

## ADR-184 · El cumplimiento del anteproyecto se audita antes de evaluar, y cada divergencia se declara

**Estado:** Aceptada · 2026-11-09 · el índice de la fase / el índice de la fase

**Contexto.** La Fase 4 evalúa el artefacto contra el anteproyecto: sus cuatro objetivos específicos, sus cuatro resultados esperados y su alcance. Hasta esta fecha el expediente declaraba **una** divergencia respecto de la letra del anteproyecto, la de ADR-167, y el proyecto había operado durante tres fases contra los identificadores de su propio expediente —`T/N`, `B`, `RF/RNF`— que son la traducción del anteproyecto y no el anteproyecto.

Una auditoría de las promesas verificables del anteproyecto encontró **diez brechas de declaración más**. Ninguna es un fraude ni un descuido aislado: cada una tiene una decisión razonada detrás, y lo que falta en todas es el acto de decir *esto que el anteproyecto promete no se cumple así, y esta es la razón*. Esa omisión es la que esta decisión cierra, porque **una divergencia declarada es un resultado y una divergencia no declarada es un hallazgo del jurado**.

**La causa mecánica, que es el peor hallazgo de la auditoría.** El el índice de la fase de esta fase, que es el documento que cierra el proyecto contra sus objetivos, **mide contra una lista de objetivos que no es la del anteproyecto**:

| El el índice de la fase decía | El anteproyecto dice |
| :---- | :---- |
| 1 · Caracterizar el problema y especificar requerimientos | *(no existe como objetivo específico)* |
| 2 · Definir el marco de referencia técnico | 1 · Definir y documentar un marco de referencia que establezca las convenciones, patrones y criterios de organización modular, **así como los lineamientos de alineación con los estándares BIAN e ISO 20022** |
| 3 · Construir el mecanismo de generación y el gestor de módulos | 2 · Implementar un mecanismo de generación de proyectos mediante **plantillas configurables** · 3 · Construir un gestor de módulos reutilizables mediante contratos de integración definidos y **compartidos entre proyectos** |
| 4 · Evaluar el comportamiento midiendo los tres criterios | 4 · Evaluar el comportamiento de la solución **en el contexto del Laboratorio Digital del Banco W** midiendo los tres criterios |

Inventa un objetivo que no existe, colapsa dos en uno, y al colapsarlos **pierde exactamente las dos cláusulas que la auditoría encontró incumplidas**: el plural de «plantillas configurables» y el «compartidos entre proyectos». No es casualidad que nadie las viera: el documento que tenía que compararlas había reescrito la lista.

**Decisión.** Cuatro cosas.

1. **El el índice de la fase se corrige a los cuatro objetivos textuales del anteproyecto**, citados y no parafraseados, y §5 a los cuatro resultados esperados textuales. Lo mismo vale para el alcance, que pasa a tener su propia tabla: siete capacidades contempladas y tres exclusiones, cada una con su veredicto.
2. **Cada divergencia se declara en un ADR propio**, con qué cláusula no se cumple, por qué, y qué se hizo en su lugar. Son ADR-185 a 189 y ADR-190 en el log de la Fase 3.
3. **Se declaran antes de medir**, que es la regla de este log. Después de la sesión serían una justificación de lo que salió.
4. **El informe de evaluación las lleva**, porque un informe que reporta tres criterios cumplidos y calla que el piso de Node no es el prometido no es un informe honesto.

**Qué cambia de veredicto y qué no.** Ninguna de las diez brechas invalida un requerimiento de la Fase 1: los 22 se miden contra su propio criterio de aceptación y ese veredicto no se toca. Lo que cambia es el **cumplimiento del anteproyecto**, que es otra cosa y es lo que la Fase 4 reporta.

| Brecha | Dónde queda | Clase |
| :---- | :---- | :---- |
| El rango de Node del objetivo general y del alcance | **ADR-185** | Divergencia declarada |
| ISO 20022 en el objetivo general y en el objetivo específico 1 | **ADR-186** | Divergencia declarada |
| «Documentación OpenAPI basada en los módulos» | **ADR-187** | Contradicción interna del anteproyecto, resuelta |
| Los cuatro riesgos éticos y sus mitigaciones | **ADR-188** | Dos cumplidas, una no materializada, una parcial |
| «Desarrollo de un sistema de almacenamiento de plantillas» | **ADR-189** | Cumplido por adopción y no por desarrollo |
| «Compartidos entre proyectos» del objetivo 3 y del resultado 3 | **ADR-190**, Fase 3 | Cerrada con evidencia nueva |
| El plural de «plantillas configurables» del objetivo 2 | **ADR-171**, Fase 2 | Cerrada construyendo el almacén |
| El contexto del Laboratorio Digital del objetivo 4 | **ADR-167** | Ya declarada |
| La cobertura de BIAN: 5 de 46 Service Domains | ADR-186, tercera parte | Alcance declarado, no incumplimiento |
| La lista de objetivos del índice de la fase | Esta decisión | Corregida |

**Lo que esta auditoría dice del método, y conviene que quede escrito.** El proyecto tiene un mecanismo de evolución del marco (MR-01 §7), un log por fase, una tabla de pendientes y una auditoría de cierre, y **ninguno de los cuatro compara lo construido contra el compromiso original**: los cuatro comparan lo construido contra el expediente. Fue barato de arreglar y habría sido caro de descubrir en la sustentación. Queda como lo que es: un hueco del método, no del marco, y la recomendación es que una auditoría de cumplimiento del anteproyecto sea un paso de cierre de cada fase y no de la última.

**Traza.** Objetivo general, objetivos específicos 1 a 4, resultados esperados 1 a 4, alcance del anteproyecto, riesgos éticos, ADR-167, ADR-171, ADR-185 a 190, el índice de la fase, el índice de la fase.

---

## ADR-185 · El piso de Node es 24, que es más estrecho que el rango que el anteproyecto promete

**Estado:** Aceptada · 2026-11-09 · el índice de la fase · revisa el alcance declarado de ADR-080

**Contexto.** El objetivo general del anteproyecto dice «una herramienta CLI para entornos Node.js **(v22–v24)**», y su alcance repite «para su uso en un entornos de desarrollo Node.js **(v22-v24)**». Lo construido no corre en v22 ni en v23: el `engines.node` de la herramienta y de sus paquetes declara `>=24`, el del producto derivado `>=24.9.0`, y el punto de entrada **rechaza explícitamente** un runtime anterior, antes de cargar una sola línea de la herramienta, con código de salida 2 y el mensaje `This tool needs Node 24 or later. You are running v<x>.`

No es un descuido de implementación: es una decisión tomada y verificada. **ADR-080** subió el piso con tres razones concretas —`require(esm)` de NestJS 12, la bandera que Jest necesita para cargar un paquete ESM, y que por debajo de 24.9 las pruebas del producto no corren— y lo dijo así: «la herramienta sube a 24 para no entregar un producto que quien lo generó no pueda verificar». Lo que ADR-080 no vio es que al hacerlo **revisaba el objetivo general y el alcance del anteproyecto**, y no lo declaró.

**Decisión.** La divergencia se declara: **el proyecto cumple el objetivo general con un rango de runtime más estrecho que el prometido**. De los tres valores del rango, la herramienta sirve uno: v24. El `(v22–v24)` del anteproyecto queda incumplido en sus dos primeros valores, y el motivo es que un producto derivado sobre v22 no puede correr su propia verificación, que es la condición de llegada de la Fase 2.

**Por qué no se cumple el rango en vez de declararlo.** Se evaluó y se descarta: sostener v22 obliga a quedarse en NestJS 11 —que es lo que **ADR-079** y **ADR-080** decidieron abandonar por el criterio de madurez de ADR-042— o a renunciar a que el producto corra sus pruebas, que es peor que no cumplir un rango de versiones. Entre entregar un producto verificable en una versión y uno no verificable en tres, la línea elige el primero, y eso es una decisión de calidad y no una limitación técnica.

**Lo que esto no cambia.** Ningún requerimiento de la Fase 1 fija el rango: **RNF-04** habla de dependencias sin vulnerabilidades y ninguno de los 22 nombra una versión de Node. El rango vive solo en el anteproyecto, que es exactamente por lo que esta brecha no la vio nadie durante tres fases: el expediente no lo lleva.

**Consecuencia.** El informe de evaluación lo declara, y el capítulo 1 de la tesis tiene que nombrarlo donde transcribe el objetivo general y el alcance. Eso cae en **P-42** y en **P-61**, con la regla de siempre: la tesis se narra al cerrar.

**Traza.** Objetivo general, alcance del anteproyecto, ADR-042, ADR-073, ADR-079, ADR-080, ADR-184, P-22, el índice de la fase.

---

## ADR-186 · Qué cláusula del objetivo general no cumple la exclusión de ISO 20022, y hasta dónde llega la alineación con BIAN

**Estado:** Aceptada · 2026-11-09 · el índice de la fase · completa ADR-007

**Contexto.** El objetivo general dice «alineados con los estándares **BIAN e ISO 20022**», y el objetivo específico 1 pide documentar «los **lineamientos de alineación** con los estándares BIAN e ISO 20022». **ADR-007** excluyó ISO 20022 con una justificación que sigue siendo correcta —el artefacto no produce, transforma ni transporta mensajes financieros, y BIAN referencia ISO 20022 en la capa de especificación de mensajes, que es la capa que el artefacto no produce— y cerró con una frase que es el problema: «se documenta la no aplicabilidad al artefacto, **manteniendo sin cambios la redacción de los objetivos**».

Mantener la redacción sin cambios es lo correcto, porque el anteproyecto no se modifica. Lo que falta es decir **qué parte de esa redacción queda sin cumplir**, y ADR-007 no lo dice: habla de no aplicabilidad, que suena a que la promesa nunca existió. Existió, está escrita dos veces, y hay además una contradicción en el propio expediente: la trazabilidad de cierre del proyecto y `3-fundamentacion.tex` tratan la exclusión como cerrada mientras el objetivo general sigue nombrando el estándar.

**Decisión.** Tres declaraciones.

**1. La cláusula incumplida, nombrada.** Del objetivo general queda sin cumplir «**e ISO 20022**», y del objetivo específico 1 queda sin cumplir la parte de «los lineamientos de alineación con … ISO 20022». Lo que **sí** se cumple de los dos es la alineación con BIAN, que es la que el artefacto materializa: el espacio de selección, los términos de acción, los behavior qualifiers, las rutas y el `operationId` del documento OpenAPI salen del estándar, transcritos de su documento oficial (ADR-139).

**2. La razón, con su categoría.** No es una omisión de trabajo sino un **hallazgo de la Fase 1**: ISO 20022 opera en una capa que el artefacto no produce, y un marco que declarara lineamientos de alineación con un estándar de mensajería para un artefacto que no emite mensajes habría producido prosa sin referente. La alternativa honesta a excluirlo era inventarlo, y eso es peor que incumplirlo.

**3. Lo que queda como extensión legítima.** ADR-007 ya lo registró y se confirma: un módulo del catálogo que encapsule mensajería ISO 20022 es un **consumidor legítimo** del marco, no parte de él, y la línea tiene hoy el mecanismo para recibirlo —el contrato, el manifiesto de un módulo y la operación de composición— sin cambiar nada. Eso es lo más cerca que el artefacto puede estar de esa promesa, y vale decirlo así.

**Y la cobertura de BIAN, que es un alcance y no un incumplimiento.** El espacio de selección declara **cinco** Service Domains —`Consumer Loan`, `Current Account`, `Savings Account`, `Term Deposit` y `Party Reference Data Directory`— de las **46** capacidades candidatas que el insumo `MR-00_BIAN_service-domains-extraidos.md` extrajo, es decir **el 11 %**. De las cinco, solo `Term Deposit` está transcrita de su documento OpenAPI oficial, con sus diez behavior qualifiers y sus treinta operaciones; las otras cuatro conservan descripciones parafraseadas y ningún qualifier, y eso está declarado en **P-35** y **P-38** con su causa: el proyecto solo tiene el documento oficial de `Term Deposit`, y **ADR-139** prohíbe transcribir de una paráfrasis. Ningún objetivo ni resultado esperado promete una cobertura, así que esto no incumple nada; lo que no se puede es afirmar «alineado con BIAN» sin decir el número, y el informe lo dice.

**Traza.** Objetivo general, objetivo específico 1, resultado esperado 1, ADR-006, ADR-007, ADR-138, ADR-139, ADR-141, ADR-184, P-06, P-35, P-38, MR-02, la trazabilidad de cierre del proyecto, el índice de la fase.

---

## ADR-187 · La documentación OpenAPI se deriva de la estructura del producto y no de sus módulos

**Estado:** Aceptada · 2026-11-09 · el índice de la fase · resuelve una contradicción del anteproyecto

**Contexto.** El anteproyecto dice dos cosas distintas sobre lo mismo, en dos secciones:

| Dónde | Qué dice |
| :---- | :---- |
| Alcance | «Generación automática de documentación openAPI **basada en los módulos y funcionalidades integradas**» |
| Metodología, actividad de la Fase 2 | «Implementar la generación automática de documentación openAPI **basada en la estructura del proyecto generado**» |
| Resultado esperado 2 | «documentación de API generada automáticamente bajo el estándar OpenAPI», sin decir de qué se deriva |

Lo construido cumple la segunda y **no puede** cumplir la primera, y la razón es una decisión del marco y no un límite de esfuerzo: **ADR-156** fija que **un módulo no aporta adaptadores de entrada**. Un módulo de la línea provee capacidades técnicas detrás de puertos —persistencia, telemetría— y nunca una ruta HTTP, así que no hay endpoint de un módulo que pueda aparecer en el documento OpenAPI de un producto. Incorporar `@bsl/persistence` o `@bsl/observability` no agrega una sola ruta, por diseño, y el circuito de composición lo comprueba.

**Decisión.** La cláusula del alcance queda declarada como **incumplible por diseño**, y la del método como **cumplida**. El documento OpenAPI de un producto se arma de sus propios esquemas y de sus propias rutas —las que su capacidad y sus operaciones producen—, lo sirve `GET /openapi.json`, lo renderiza `GET /docs` con el visor instalado (ADR-164), y lleva el `operationId` y los tags del estándar en las dos formas de ruta (ADR-146). Eso es «basada en la estructura del proyecto generado», literalmente.

**Por qué se elige la cláusula de la metodología y no la del alcance.** Porque es la que describe lo que un documento OpenAPI puede ser: un documento OpenAPI describe la **superficie de entrada** de un servicio, y la superficie de entrada de un producto de esta línea es suya y de nadie más. Para que la cláusula del alcance fuera cumplible habría que permitir que un módulo aporte rutas, lo que **ADR-156** rechaza con el argumento del marco: un módulo que aporte una ruta se mete en el bounded context del producto, que es de su equipo (RNF-02, MR-04).

**Lo que sí es verdad de la cláusula del alcance, y conviene no exagerar la divergencia.** Lo que un módulo incorporado cambia del documento del producto es **nada**, y lo que cambia de lo que el producto **declara de sí mismo** es su README, en una región que el módulo reemplaza (ADR-130). Así que «las funcionalidades integradas» quedan documentadas —en el lugar donde un humano las lee— y no en el documento OpenAPI, donde un cliente HTTP no las encontraría porque no son rutas.

**Traza.** Alcance del anteproyecto, metodología Fase 2, resultado esperado 2, RF-04, RNF-02, ADR-072, ADR-113, ADR-130, ADR-146, ADR-156, ADR-164, ADR-184, MR-04, el índice de la fase.

---

## ADR-188 · Los cuatro riesgos éticos, uno por uno, con lo que se hizo y lo que no

**Estado:** Aceptada · 2026-11-09 · el índice de la fase

**Contexto.** El anteproyecto declara cuatro riesgos éticos, y cada uno declara su mitigación en una
frase que es un compromiso. El expediente **no los menciona en ninguno de sus documentos**, comprobado
por búsqueda sobre todo `Implementación/`. Tres fases pasaron sin volver a mirarlos, y lo que hay que
decir antes de evaluar es cuál mitigación se cumplió y cuál no.

**Decisión.** Se declaran así, y el informe de evaluación los lleva.

**1 · Exposición de información sensible en plantillas y módulos. Cumplida, y por diseño.** El
compromiso era separar estructura base de valores sensibles, con variables de entorno y gestión de
secretos desde el diseño. Es lo que **RNF-05** exige y lo que el artefacto hace: ninguna dirección ni
credencial en el código del producto, toda configuración por variable validada por esquema, el circuito
de generación **barre el producto derivado** buscando valores fijos y direcciones, y el asiento del log
**redacta por nombre de clave** (ADR-152). La `.npmrc` del producto lleva la dirección del feed y nunca
un token. Está verificada por ejecución, que es más de lo que el compromiso pedía.

**2 · Propagación de lógica financiera mal interpretada. No se materializó, así que la mitigación no se
ejerció.** El compromiso era revisión técnica especializada antes de incorporar un módulo con lógica
financiera. El catálogo tiene dos módulos y **ninguno la lleva**: uno guarda y lee registros, el otro
exporta señales de OpenTelemetry. Las dos capacidades son técnicas por decisión del marco —**MR-04**
reparte: lo técnico al módulo, el dominio al producto—, así que el riesgo no existe en lo construido.
**Condición de reactivación:** el día que entre un módulo que interprete un estándar financiero —la
mensajería ISO 20022 que ADR-186 deja como extensión es el caso obvio—, la revisión especializada es
exigible antes de su entrada, y el procedimiento del doc 3 §7 de la Fase 2 es dónde se declara.

**3 · Exclusión de equipos con menor capacidad técnica. Cumplida a medias, y la mitad que falta se
rechazó sin ver que era un compromiso ético.** La primera parte, «documentación accesible orientada a
distintos niveles de experiencia», **se rechazó**: figura en el informe externo como «documentación por
audiencia» y el índice de la Fase 3 la descartó por oportunidad —«crece con los módulos
incorporados»—. Ese argumento es razonable como decisión de alcance de fase y **no es una respuesta al
riesgo ético**, porque nadie vio que lo fuera: el rechazo compara la propuesta contra el calendario y no
contra el compromiso. No se construyó, el informe lo declara, y queda como la primera recomendación de
adopción del doc 7.

La segunda parte sí está: el producto nace con un README que explica qué es, qué operación lleva efecto
de negocio y cuál es un andamio, y cuándo mover cada capa; el recorrido se lee en lenguaje de negocio
con el nombre del estándar al lado (ADR-144); la herramienta declara su alcance antes de escribir
(ADR-136); y los errores dicen qué encontró, qué esperaba y qué comando resuelve (ADR-081). Ninguno de
los documentos que lo produjeron sabía que estaba mitigando un riesgo ético. El acompañamiento con
formación es organizacional y queda fuera de lo que un artefacto puede hacer.

**4 · Concentración de poder técnico. El mecanismo existe, el ejercicio no.** El compromiso era un
modelo de gobernanza distribuido con procesos participativos, conocimiento documentado y evolución
según necesidades colectivas:

| Parte del compromiso | Estado |
| :---- | :---- |
| Procesos participativos para incorporar cambios | **El mecanismo está, el ejercicio no.** El catálogo declara un responsable por activo, `CODEOWNERS` exige aprobación del gobierno sobre la ruta del manifiesto, y el procedimiento tiene sus pasos y sus condiciones verificables por tipo. Lo que no hay es **más de un participante**: el doc 3 §7 de la Fase 2 lo declara desde que se escribió |
| El conocimiento documentado de forma exhaustiva | **Cumplido.** 198 decisiones con su contexto, su alternativa y su traza; setenta y seis archivos de expediente; un marco con su mecanismo de evolución; y la regla de que toda decisión se funda en un documento |
| La evolución responde a necesidades colectivas | **Parcial, y con evidencia.** Los quince temas y las tres brechas salen de cinco entrevistas con las personas del contexto; la revisión externa movió el artefacto en cinco rondas; y dos rondas las abrieron reportes de uso. Lo que no existe es un proceso en operación con varios equipos |

**La condición que explica las tres** es la de ADR-167: el autor salió del laboratorio y el proyecto se
construyó con una sola persona en los tres roles. Una gobernanza distribuida instanciada con un
participante es un mecanismo probado y un ejercicio ausente. Trasladarlo a operación consiste en cambiar
quién figura como responsable, y eso es la recomendación de adopción.

**Por qué va en un ADR y no solo en el informe.** Es una decisión de método tomada **antes de medir**:
se decide qué se va a reportar de los cuatro riesgos, con qué evidencia y con qué palabra. Después de la
sesión, declarar que una mitigación no se ejerció sería una explicación de por qué no salió algo.

**Traza.** Riesgos éticos del anteproyecto, T-01, T-02 a T-15, RNF-02, RNF-05, ADR-035, ADR-081, ADR-130, ADR-136, ADR-144, ADR-152, ADR-156, ADR-167, ADR-184, ADR-186, MR-04, MR-05 §1 y §6, Fase 2 doc 3 §2
y §7, el índice de la Fase 3, Doc 7 §6, el índice de la fase.

---

## ADR-189 · El almacén de plantillas se cumple adoptando el registro de la organización, no desarrollando uno

**Estado:** Aceptada · 2026-11-09 · el índice de la fase · declara el cumplimiento de ADR-171

**Contexto.** El alcance del anteproyecto compromete el «**Desarrollo de un sistema de almacenamiento de plantillas**, asegurando su disponibilidad para los equipos». El 2026-11-09, con **ADR-171**, la línea tiene un almacén: el catálogo admite el tipo `template`, una plantilla se describe a sí misma en su propio manifiesto, `bsl templates list` lo muestra y `bsl new --template <id>` deriva de cualquiera de sus entradas. Lo que **no** se hizo es *desarrollar* un sistema de almacenamiento: las plantillas se distribuyen como paquetes versionados en el **registro privado que la organización ya tiene**, y lo que el proyecto construyó es el manifiesto que las describe y las operaciones que las leen.

**Decisión.** La cláusula se declara **cumplida por adopción y no por desarrollo**, y la razón se declara con ella, porque es una de las conclusiones del proyecto y no una economía.

**Por qué adoptar y no construir.** Está decidido desde la Fase 1 y tiene evidencia empírica detrás. **B-03** es la brecha de que ninguna herramienta existente resuelve la distribución gobernada de activos en este contexto, y **T-14** es la necesidad de que el mecanismo no agregue infraestructura que alguien tenga que operar. Un almacén propio —un servicio, su base de datos, su autenticación, su disponibilidad— habría sido un sistema más que mantener en una organización regulada, con su propio proceso de aprobación, su propio responsable y su propio riesgo de quedar sin dueño; y habría competido con un registro de paquetes que ya existe, ya está autenticado contra el directorio corporativo y ya lo usan los equipos todos los días. **RF-15** lo dice en su criterio de aceptación: la herramienta obtiene módulos y plantillas del registro «**sin canal propio de distribución**». Desarrollar un almacén habría incumplido RF-15 para cumplir la letra del alcance.

**Qué sí se desarrolló, que es lo que el compromiso persigue.** «Asegurar su disponibilidad para los equipos» es el verbo que importa, y eso es lo construido:

| Pieza | Qué aporta a la disponibilidad |
| :---- | :---- |
| `bsl-template.json` y su esquema | Una plantilla declara qué deriva, qué forma de producto produce y de qué está hecha, de modo que un equipo puede decidir si le sirve sin leer su código |
| La entrada del catálogo, tipo `template` | La plantilla tiene identificador, responsable, estado de ciclo de vida y condiciones de validez verificables |
| `bsl templates list` y `templates show` | Un equipo descubre qué hay sin preguntarle a nadie, que es la diferencia entre un almacén y una carpeta compartida |
| `bsl new --template <id>` | La plantilla se consume con un comando, resuelta del registro y cacheada por versión |
| El `prepublishOnly` de cada activo | Lo que llega al registro se puede instalar (ADR-163) |

**La frontera, declarada.** Lo que el proyecto **no** aporta es el servicio que almacena bytes ni su operación: eso es del registro de la organización, y queda fuera del alcance por la exclusión del propio anteproyecto —«integración con procesos de despliegue, infraestructura o automatización DevOps»—, que es la misma razón por la que esta decisión no es una contradicción del alcance sino su lectura coherente.

**Traza.** Alcance del anteproyecto, objetivo específico 2, resultado esperado 2, B-03, T-14, RF-14, RF-15, RF-16, ADR-050, ADR-162, ADR-163, ADR-171, ADR-184, MR-05 §1 y §5, Fase 2 doc 3, doc 10, el índice de la fase.

---

## Decisiones pendientes de esta fase

| Pendiente | Documento | Estado |
| :---- | :---- | :---- |
| Qué sostiene la medición hecha por quien construyó el artefacto, y cómo se acota su sesgo | Doc 1 | Abierta |
| Si el tiempo se mide cronometrando una ejecución o reconstruyéndolo por tareas, y con qué unidad | Doc 2 | Abierta |
| **RF-16**: qué cuenta como evidencia de que el procedimiento de incorporación al catálogo es suficiente | Doc 2, Doc 4 | Abierta. El custodio natural del catálogo participa en la evaluación |
| **RNF-03**: con qué herramientas se analiza el producto generado, y quién las corre | Doc 2, Doc 3 | Abierta |
| El hito `1.0.0` de la línea (P-52) | el índice de la fase | Abierta |
