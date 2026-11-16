# Las mediciones

Los tres criterios del objetivo específico 4 medidos contra su referencia —el tiempo de generación, la correcta incorporación de un módulo y el inicio de implementación de lógica de negocio— y la segunda aplicación de la rúbrica externa sobre la versión publicada.

Lo marcado *(pendiente)* se completa con el insumo de las llamadas. **Todo lo demás —la referencia, la regla de comparación, el procedimiento, qué cuenta como correcto y los límites— está decidido antes de medir y no se cambia después de ver el resultado.**

---

## 1. Criterio 1 · El arranque

### 1.1 La referencia

| Qué | Valor |
| :---- | :---- |
| Banda del contexto estudiado | **8 a 15 días** |
| Equivalente en horas-persona | **52 a 98**, con los supuestos S-1, S-2 y S-3 del doc 1 |
| Piso si «días» eran calendario | 37 a 70 horas-persona |
| Contraste externo | 2 semanas, reportado aparte y nunca sumado |
| Naturaleza | Autoreporte de dos informantes, previo al artefacto. n=2, sin corroboración publicable |
| Inicio y fin | La decisión de construir; el proyecto corre en local y queda desplegable en la rama principal |

### 1.2 Qué se ejerció, y cómo

| Qué | Valor |
| :---- | :---- |
| Versión de la herramienta que servía el feed ese día | *(pendiente)* |
| Versión de la plantilla | *(pendiente)* |
| Instalada desde | *(pendiente: feed de la organización, o ruta local)* |
| Quién ejecutó | *(pendiente)* |
| Entorno | *(pendiente: equipo del participante, dentro o fuera de la organización)* |
| Fecha de la medición | *(pendiente de la llamada 3)* |

**Cuál de las tres formas ocurrió.** El diseño admite tres y valen distinto, así que se declara acá, en la
primera línea de la medición y no al final: `PE-03` ejecuta observado en la llamada 3, que es la forma
prevista; `PE-03` ejecuta por su cuenta con la hoja de pasos, que pierde la observación de dónde se trabó; o el
autor ejecuta y `PE-03` valida y estima, que es la más débil porque mide el artefacto en manos de quien lo
construyó.

**Forma que ocurrió:** *(pendiente)*

### 1.3 El cronómetro, paso por paso

| # | Paso | Minutos | Observación |
| :-- | :---- | :--: | :---- |
| 1 | Instalar la herramienta desde el feed | *(pendiente)* | *(pendiente: si hizo falta ayuda)* |
| 2 | Derivar el proyecto respondiendo las preguntas | *(pendiente)* | *(pendiente: cuántas respuestas corrigió en la revisión)* |
| 3 | Levantar el proyecto y verlo responder: sondas, documento OpenAPI y página de documentación | *(pendiente)* | *(pendiente)* |
| 4 | Correr la verificación propia del producto | *(pendiente)* | *(pendiente)* |
| | **Total de lo cubierto por la herramienta** | *(pendiente)* | |

### 1.4 Las tres cubetas

El fin declarado es más ancho que el alcance de la herramienta, así que el total se reparte. Es lo que vuelve
honesta la comparación.

| Cubeta | Tareas | Cómo se obtiene su costo | Resultado |
| :---- | :--: | :---- | :---- |
| **Cubierta** por la herramienta | 23 | El cronómetro de la §1.3 | *(pendiente)* |
| **Parcialmente cubierta** | 2 | El cronómetro de la incorporación del módulo, en la §2, más lo que quede manual | *(pendiente)* |
| **Fuera del alcance** | 6 | Estimación de `PE-03`, que es quien las hace hoy: crear el repositorio y sus permisos, definir la integración continua, configurar el despliegue, crear la base de datos, enganchar las revisiones previas al push y resolver autenticación | *(pendiente)* |
| | **31** | | |

### 1.5 La comparación

Dos lecturas, y las dos se reportan. La primera responde al criterio del objetivo 4; la segunda evita que
alguien lea un ahorro que no existe.

**Lectura 1 — sobre lo cubierto.** Lo que la herramienta hace, contra lo que costaba hacerlo a mano: los
minutos medidos en la §1.3, contra la porción de la banda de 52-98 horas-persona que corresponde a las 23
tareas cubiertas. *(pendiente)*

**Lectura 2 — sobre el total.** El arranque completo con la herramienta, contra el arranque completo sin ella,
incluidas las seis tareas que la herramienta no toca y que siguen costando lo que costaban. *(pendiente)*

**Cómo se reporta.** En minutos lo cubierto, en horas-persona el total, y la banda de la línea base al lado.
Sin porcentajes de ahorro sobre el total: el porcentaje sugiere una precisión que un n=2 autoreportado no
tiene.

### 1.6 RNF-03, que se mide acá

Su criterio textual es *«el proyecto generado se analiza con las herramientas de la organización sin adaptación
previa»*. Dos de los participantes tienen acceso a esas herramientas, y por eso el requerimiento dejó de ser
inverificable.

| Qué | Resultado |
| :---- | :---- |
| Herramienta de análisis que se usó | *(pendiente: se nombra por su función, no por su proveedor)* |
| Corrió sin adaptación previa | *(pendiente: sí o no)* |
| Si hubo que adaptar, qué | *(pendiente)* |
| Hallazgos que reportó | *(pendiente)* |
| **Veredicto de RNF-03** | *(pendiente)* |

Si hubo que adaptar el proyecto para que el analizador lo aceptara, el criterio **no se cumple**, aunque el
análisis después pase: el criterio es sobre la adaptación, no sobre el resultado.

### 1.7 Lo que esta medición no dice

- **No dice que un proyecto real se arranque en ese tiempo.** Mide las 23 tareas cubiertas en condiciones de
  sesión, sin las interrupciones, las esperas ni las decisiones de negocio de un arranque real.
- **No dice nada sobre la curva de aprendizaje.** Es la primera vez que el participante la usa, y lo hace con
  el autor disponible.
- **No corrige el n=2 de la referencia.** La comparación hereda la debilidad de la línea base, declarada en el
  doc 1 §9.
- **No mide adopción.** Que alguien pueda arrancar rápido una vez no dice que el equipo lo use.

## 2. Criterio 2 · La incorporación y la actualización de un módulo

El criterio nombra la correcta incorporación. Se mide además la **actualización**, que el criterio no nombra
pero las brechas sí: que actualizar no destruya lo que el equipo cambió es B-02 y la razón de ser del gestor.

### 2.1 La referencia: cómo se reutiliza hoy

| Qué | Estado actual, según la Fase 1 |
| :---- | :---- |
| Mecanismo | **Copia de carpetas entre proyectos**, con ajuste de variables de entorno, o reconstrucción tomando otro proyecto como referencia visual (T-04) |
| Alcance | Solo código de aplicación |
| Vínculo con el origen | Ninguno. Nada ata la copia a su fuente |
| Propagación de un cambio | Manual, proyecto por proyecto (T-05) |
| Punto más frágil | El contrato del servicio consumido: cuando cambia la estructura de la respuesta, se desencadenan ajustes en cascada |
| Costo percibido de propagar, 1 a 5 | **4** (`PE-02`) y **5** (`PE-03`) |
| Frecuencia de reutilizar por copia, 1 a 5 | **3** (`PE-02`) y **4** (`PE-03`) |
| Cuántos repositorios toca una propagación | No disponible. Las entrevistas dan el costo percibido, no el conteo |

La comparación es **de mecanismo**, no de minutos: hoy se copia sin vínculo, y la pregunta es si incorporar un
módulo del catálogo resuelve lo mismo de otra manera.

### 2.2 Qué significa «correcta»

Se fija antes de medir, para que no se declare correcta por una impresión favorable. Tres comprobaciones en
ejecución, más una declaración del participante.

| # | Comprobación | Cómo se verifica |
| :-- | :---- | :---- |
| 1 | El producto sigue arrancando después de incorporar el módulo | Se levanta y responde |
| 2 | El producto declara qué módulo tiene y en qué versión | Su registro lo dice, que es el criterio de **RF-10** |
| 3 | La capacidad del módulo funciona de verdad | El dato persiste y **sobrevive al reinicio** |
| 4 | El resultado es el que el participante esperaba | Su declaración, en sus palabras |

### 2.3 La incorporación

| Qué | Resultado |
| :---- | :---- |
| Módulo incorporado | *(pendiente: persistencia u observabilidad)* |
| Versión | *(pendiente)* |
| Quién ejecutó | *(pendiente)* |
| Minutos | *(pendiente)* |
| ¿Editó algún archivo del proyecto a mano? | *(pendiente: el criterio de **RF-06** es que no haga falta)* |
| Comprobación 1, arranca | *(pendiente)* |
| Comprobación 2, el registro lo declara | *(pendiente)* |
| Comprobación 3, el dato sobrevive al reinicio | *(pendiente)* |
| Comprobación 4, era lo que esperaba | *(pendiente)* |
| Fecha de la medición | *(pendiente de la llamada 3)* |

### 2.4 La actualización

Es lo que distingue al gestor de una copia. El mecanismo compara una huella para saber qué tocó el equipo y qué
no.

| Qué | Resultado |
| :---- | :---- |
| Se modificó a mano un archivo que el módulo había generado | *(pendiente: qué archivo)* |
| Se actualizó el módulo a una versión posterior | *(pendiente)* |
| ¿Se preservó lo que el equipo había cambiado? | *(pendiente)* |
| ¿Lo informó, en lugar de sobrescribir en silencio? | *(pendiente)* |
| Declaración del participante sobre ese comportamiento | *(pendiente)* |

Si la actualización hubiera sobrescrito el cambio del equipo, el hallazgo sería grave y **se reporta como
tal**, no se corrige antes de reportarlo: es la diferencia entre evaluar y demostrar.

### 2.5 RF-16, que se evalúa acá

El requerimiento pide que *«cada entrada del catálogo declare su responsable, y exista un procedimiento
documentado de incorporación»*. La primera mitad está comprobada por inspección. La segunda quedó abierta desde
la Fase 3, porque nadie había decidido qué cuenta como evidencia de que un procedimiento en prosa es
suficiente.

Se cierra con el juicio del custodio natural. `PE-02` es el rol que la Fase 1 identificó como candidato a
mantener el catálogo, y la pregunta es directa:

> Leído el procedimiento de incorporación al catálogo, ¿te alcanza para ejercer ese gobierno? ¿Qué le falta?

| Qué | Resultado |
| :---- | :---- |
| Juicio de `PE-02` | *(pendiente)* |
| Qué le faltaría | *(pendiente)* |
| **Veredicto de RF-16** | *(pendiente)* |

Es mejor evidencia que cualquier comprobación automática: un procedimiento de gobierno se valida por si quien
debe aplicarlo puede aplicarlo.

### 2.6 La comparación con el mecanismo actual

| Dimensión | Hoy | Con el gestor | Resultado |
| :---- | :---- | :---- | :---- |
| Cómo llega la capacidad al proyecto | Copia de carpeta y ajuste manual | Un comando | *(pendiente)* |
| Vínculo con el origen | Ninguno | El registro del producto declara módulo y versión | *(pendiente)* |
| Propagar un cambio | Manual, proyecto por proyecto | Un comando de actualización que preserva lo propio | *(pendiente)* |
| Costo percibido de propagar, 1 a 5 | 4 y 5 | *(pendiente: ítem C4 del instrumento)* | *(pendiente)* |
| Frecuencia de copiar, 1 a 5 | 3 y 4 | *(pendiente: ítem C3)* | *(pendiente)* |

### 2.7 Lo que esta medición no dice

- **No mide la propagación real.** Se actualiza un producto, no los varios que un cambio tocaría hoy. Cuántos
  repositorios toca una propagación sigue siendo dato no disponible, acá y en la línea base.
- **No mide el catálogo poblado.** La línea tiene dos módulos; el orden de crecimiento del doc 1 de la Fase 3
  declara el resto como trabajo posterior.
- **No dice nada sobre un módulo de otro equipo.** Los dos del catálogo los construyó la línea; que un equipo
  ajeno publique uno es parte del gobierno, no de esta medición.

## 3. Criterio 3 · El inicio de implementación de lógica de negocio

Es el criterio más difícil de los tres, porque no se mide con un cronómetro ni con una comprobación binaria: lo
que se mide es **si el andamio alcanza para empezar**, y qué le faltó a quien empezó.

### 3.1 Qué cuenta como «inicio de implementación»

Se fija antes, porque es el criterio más fácil de declarar cumplido con poca evidencia. No basta con que el
proyecto compile ni con que alguien escriba una función: cuenta cuando **una operación de negocio nueva queda
funcionando de punta a punta sobre lo derivado**.

| # | Condición | Por qué |
| :-- | :---- | :---- |
| 1 | La operación es de negocio, no técnica | Agregar un logger no es lógica de negocio |
| 2 | Atraviesa las capas: entra por su adaptador, pasa por su caso de uso y toca el dominio | Es lo que el marco declara como estructura, y lo que prueba que el andamio sirve para lo que dice servir |
| 3 | Responde por HTTP a una petición real | Lo mismo que el quinto criterio de la rúbrica externa exige del producto |
| 4 | Tiene al menos una prueba que la ejerce | Es la regla de la plantilla, y el octavo criterio de la rúbrica |
| 5 | La escribe el participante, no el autor | Si la escribe el autor, mide otra cosa |

**El límite declarado.** Esto mide el *inicio*, no la implementación de un producto. El anteproyecto pide el
inicio, y el propio artefacto se declara un habilitador técnico: la línea produce estructura, no negocio.

### 3.2 Qué se implementó

| Qué | Valor |
| :---- | :---- |
| Operación elegida | *(pendiente)* |
| Por qué esa | *(pendiente: conviene que la elija el participante, no el autor)* |
| Capacidad del producto sobre el que se escribió | *(pendiente)* |
| Quién la escribió | *(pendiente)* |
| Minutos hasta verla responder | *(pendiente)* |
| Las cinco condiciones de la §3.1 | *(pendiente, una por una)* |
| Fecha de la medición | *(pendiente de la llamada 3)* |

### 3.3 Qué entregó el andamio y qué hubo que escribir

Es el corazón del criterio: la plantilla deja un proyecto completo escrito, y la pregunta es cuáles de sus
archivos sirvieron de punto de partida y cuáles hubo que crear.

| Qué | Lo entregó el andamio | Lo escribió el participante |
| :---- | :---- | :---- |
| Estructura de carpetas por capas | Sí | — |
| Entidad y repositorio del agregado | Sí, para la capacidad derivada | *(pendiente)* |
| Caso de uso de la operación nueva | *(pendiente: si existía como andamio o hubo que crearlo)* | *(pendiente)* |
| Adaptador de entrada y validación de la petición | *(pendiente)* | *(pendiente)* |
| Evento de dominio | *(pendiente)* | *(pendiente)* |
| Prueba de la operación | *(pendiente)* | *(pendiente)* |
| Cableado en el punto de composición | *(pendiente)* | *(pendiente)* |

### 3.4 Qué esperaba encontrar y no estaba

El dato más valioso, y el que el resultado esperado 4 del anteproyecto pide con el nombre de «hallazgos sobre
su aplicación práctica». Se recoge con una pregunta abierta y se transcribe sin reinterpretar.

*(pendiente: lo que el participante dio por supuesto que estaría hecho, lo que tuvo que buscar en la
documentación, lo que resolvió copiando de otra parte del proyecto y lo que no supo cómo resolver)*

### 3.5 Lo que esta medición no dice

- **No dice que el producto sirva para producción.** Mide el inicio, con una operación y en una sesión.
- **No dice cuánto cuesta un producto completo.** Eso exigiría el caso de estudio que el anteproyecto
  comprometía y que quedó declarado no ejecutable.
- **No mide la calidad de lo escrito.** Que la operación responda y tenga prueba no dice que esté bien
  modelada; eso es juicio de diseño y no de esta fase.
- **No es generalizable a otra capacidad.** Se escribió una operación sobre un dominio; otra capacidad del
  estándar podría exigir más.

## 4. La segunda aplicación de la rúbrica externa

Los nueve criterios de aceptación del informe externo del 2026-10-28, respondidos de nuevo sobre la versión
publicada **por quien los escribió**. `PE-04` los redactó antes de que la Fase 3 construyera, así que su
primera aplicación es un «antes» comparable y no la opinión de otro momento.

### 4.1 Las dos aplicaciones no se hicieron sobre lo mismo

Declararlo es lo que hace legítima la comparación. El evaluador de octubre no vio lo que se evalúa ahora.

| Qué | Primera aplicación | Segunda aplicación |
| :---- | :---- | :---- |
| Fecha | 2026-10-28 | *(pendiente de la llamada 2)* |
| Versión de la herramienta en el feed | `0.2.1`, publicada el 2026-10-21 | *(pendiente)* |
| Versión de la plantilla | `0.1.0` | *(pendiente)* |
| Plantillas en el catálogo | Una | **Dos**: la hexagonal —que es la de la primera aplicación, renombrada— y la de Azure Functions |
| Módulos en el catálogo | Ninguno | Dos: persistencia y observabilidad |
| Sobre qué se ejerció | Una prueba de concepto propia del evaluador, dos productos | *(pendiente)* |
| Qué había entre medio | — | Ocho rondas de mejoras, diecisiete grupos, y las fases 3 y 4 |

**Y hay una plantilla más, que él no vio.** La de Azure Functions no existía en octubre y deriva un producto
sobre otro modelo de ejecución. Para la rúbrica es superficie nueva: tres de sus nueve criterios —la
documentación, la claridad de la estructura y el arranque— podrían aplicarse sobre un producto de ella además
del de la hexagonal. La decisión está tomada en el doc 2 §8: **se mide la hexagonal y la otra se muestra**.

**Tres hallazgos de octubre ya estaban resueltos y el evaluador no pudo verlos**: las sondas de salud, la
carpeta propia por rol que multiplica y el paso a la mayor siguiente del framework entraron al repositorio el
mismo 2026-10-28, después de la versión que él tenía instalada. Es la lección que condiciona esta segunda
aplicación: **se hace sobre una versión publicada**, no sobre el repositorio de trabajo.

### 4.2 Los nueve criterios

La columna «el autor declara» es el estado que el seguimiento de mejoras registra, hecho por inspección propia.
La columna de `PE-04` es la medición de esta fase. **Si las dos discrepan, vale la del evaluador.**

| # | Área | Criterio, como él lo escribió | Antes, en `0.2.1` | El autor declara | `PE-04` responde |
| :-- | :---- | :---- | :---- | :---- | :---- |
| 1 | CLI | El error indica PascalCase, muestra un ejemplo válido y el valor recibido | Falla | Cumple | *(pendiente)* |
| 2 | Bootstrap | El resultado informa que es técnico y lista operaciones implementadas y placeholder | Falla | Cumple | *(pendiente)* |
| 3 | Eventos | Cada evento documenta productor, payload, consumidores y si la publicación es solo in-process | Falla | Cumple | *(pendiente)* |
| 4 | Persistencia | El README y el log de arranque indican el adapter y si los datos sobreviven al reinicio | Falla | Cumple | *(pendiente)* |
| 5 | API | Se puede iniciar el servicio, entender una ruta, enviar un request válido y observar una respuesta | Falla | Cumple | *(pendiente)* |
| 6 | Observabilidad | Cada request registra método, ruta, status, duración y request ID | Falla | Cumple | *(pendiente)* |
| 7 | Health | Las dos sondas distinguen proceso vivo de dependencias disponibles | Falla | Cumple | *(pendiente)* |
| 8 | Testing | Cada endpoint generado tiene al menos un smoke test HTTP | Falla | Cumple | *(pendiente)* |
| 9 | Negocio | Un líder no técnico puede explicar propósito, alcance y pendientes sin leer el código | Falla | Medible, no verificado | *(pendiente: lo responde `PE-02`, §4.4)* |

**Antes: nueve de nueve fallando. Lo que el autor declara hoy: ocho cumplen y el noveno no se declara.** Lo que
esta fase establece es la última columna.

### 4.3 Discrepancias

Si `PE-04` marca como falla un criterio que el autor declara cumplido, es el hallazgo más importante: significa
que la evidencia de inspección propia no coincide con la experiencia de uso.

| Criterio | El autor declara | `PE-04` responde | Qué lo explica |
| :---- | :---- | :---- | :---- |
| *(pendiente)* | | | |

Cada discrepancia se analiza por su causa, que puede ser de tres tipos: la mejora existe pero no se encuentra
—problema de descubribilidad, no de construcción—; la mejora existe y no alcanza; o la mejora se declaró
cumplida sin evidencia suficiente. Las tres son resultados útiles, y la tercera obliga a corregir el
seguimiento de mejoras.

### 4.4 El noveno criterio, respondido por `PE-02`

Lo responde quien tiene la mirada de negocio, porque es lo que el criterio pide. Se evalúa contra las tres
cosas que el criterio nombra, y se declara cuáles aparecen en la respuesta.

| Qué pide el criterio | Apareció en la respuesta | Cómo lo dijo |
| :---- | :---- | :---- |
| **Propósito**: para qué sirve | *(pendiente)* | *(pendiente, textual)* |
| **Alcance**: hasta dónde llega, y que no es un producto de negocio terminado | *(pendiente)* | *(pendiente, textual)* |
| **Pendientes**: qué le falta | *(pendiente)* | *(pendiente, textual)* |
| **Veredicto del criterio 9** | *(pendiente)* | |

La respuesta se transcribe textual y no se parafrasea. Si dice que es «un generador de proyectos» y no
distingue el habilitador técnico del producto de negocio, el criterio **no se cumple**, por más que el resto de
la respuesta sea favorable: esa distinción es justamente lo que el informe de octubre señaló como el problema
principal del artefacto.

### 4.5 Resultado, y lo que esta medición no dice

| Qué | Resultado |
| :---- | :---- |
| Criterios que cumplen, de nueve | *(pendiente)* |
| Criterios que fallan | *(pendiente)* |
| Discrepancias con lo declarado por el autor | *(pendiente)* |
| Hallazgos nuevos, que no estaban en la rúbrica de octubre | *(pendiente)* |

Lo que `PE-04` encuentre ahora y no esté en los nueve criterios es material nuevo, y entra al informe como
hallazgo, no como falla de un criterio que nadie había escrito.

- **No es una evaluación independiente completa.** `PE-04` evalúa mejoras que su propio informe pidió, así que
  puede leer como resuelto lo que recuerda haber solicitado. Lo compensa que sus criterios estaban escritos y
  son verificables: se responden contra el artefacto, no contra el recuerdo.
- **No cubre el contexto estudiado.** `PE-04` es externo; su juicio es de transferibilidad, no de encaje con el
  proceso del laboratorio.
- **No sustituye las mediciones del objetivo 4.** La rúbrica evalúa el producto generado; los tres criterios
  evalúan el uso de la herramienta.

## 5. Dónde se trabó

De la bitácora de cada llamada. Es el material de las recomendaciones del informe, y vale tanto como los
tiempos: qué no entendió, qué tuvo que explicarse, qué resolvió por un camino distinto del previsto y qué
abandonó.

*(pendiente)*

## 6. Los veredictos

| Qué | Veredicto |
| :---- | :---- |
| Criterio 1, tiempo de generación | *(pendiente)* |
| Criterio 2, correcta incorporación de un módulo | *(pendiente)* |
| Criterio 3, inicio de implementación de lógica de negocio | *(pendiente)* |
| RNF-03, análisis con las herramientas de la organización | *(pendiente)* |
| RF-16, procedimiento de incorporación al catálogo | *(pendiente)* |
| La rúbrica externa, nueve criterios | *(pendiente)* |
