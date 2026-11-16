# Participantes y diseño de la evaluación

Quién participa, qué sostiene su participación y qué la sesga; y con qué instrumento se mide, qué se cronometra, qué cuenta como evidencia de cada criterio y qué se hace si algo no ocurre. Es la actividad 1 del objetivo específico 4, y **tiene que estar escrita antes de la primera llamada**: medir sin instrumento no produce un dato agregable, y una respuesta vale según quién la da y desde dónde.

---

## 1. Criterio de identificación y marco de clasificación

Participa quien puede sostener algo que la evaluación necesita. Cuatro formas de aportar, y nadie aporta en
todas:

- **Uso:** instala, ejecuta y produce con la herramienta. Es el único aporte que mide los criterios del
  objetivo 4.
- **Juicio técnico:** valora el artefacto sin haberlo construido.
- **Observación de negocio:** entiende, o no, qué es esto y para qué sirve, sin leer código.
- **Conducción y registro:** muestra, cronometra y anota. No responde por lo que se siente al usarlo.

Se clasifica por la **distancia respecto del artefacto**, el mismo criterio de la Fase 1, porque para evaluar
esa distancia es lo que determina el valor de una respuesta: cuanto más cerca del artefacto, más confiable es
lo que la persona dice sobre su funcionamiento y menos confiable lo que dice sobre su claridad.

| Distancia | Qué puede afirmar con autoridad | Qué no |
| :---- | :---- | :---- |
| **Constructor** | Qué hace el artefacto, cuánto tarda, qué pasos exige | Si se entiende, si se adopta, si convence |
| **Usuario del contexto** | Si le sirve, si lo adoptaría, qué le costó, qué le faltó | Nada sobre otros contextos |
| **Par técnico externo** | Si el artefacto se sostiene fuera del contexto que lo originó | La comparación contra la línea base, que es de otro contexto |
| **Mirada de negocio** | Si el propósito, el alcance y los pendientes se entienden sin leer código | Nada sobre el código ni sobre el costo técnico |

## 2. Los cuatro participantes

### 2.1 PE-01 · Autor del artefacto

**Rol en el proyecto.** Construyó la línea completa: el marco, el mecanismo, el gestor y los dos módulos.
**Distancia.** Constructor. Cero.

**Qué hace en la evaluación.** Conduce las tres llamadas: introduce la herramienta, muestra cómo funciona —la
instalación, el uso y el mantenimiento—, cronometra lo que haya que cronometrar y registra todo en la bitácora.

**Qué sostiene su participación.** La medición instrumentada: tiempos, pasos, conteos, comandos y su salida.
Todo lo que un tercero podría repetir leyendo el registro.

**Qué la sesga, dicho sin rodeos.** Conoce la respuesta antes de la pregunta. Sabe dónde está cada cosa, qué
orden de preguntas conviene y qué errores evitar, de modo que **cualquier medición suya de usabilidad, de
claridad o de tiempo de aprendizaje está contaminada de origen**. Su presencia conduciendo también condiciona
lo que los demás dicen, y eso se anota como observación de método en cada entrada de la bitácora.

**Qué no puede sostener.** Ninguno de los tres criterios del objetivo 4 por sí solo, porque los tres preguntan
por el uso y él no es un usuario. Su medición es el **piso técnico** sobre el que se leen las de los demás.

### 2.2 PE-02 · Líder técnico, con mirada de negocio y producto

**Rol en el proyecto.** Informante de la Fase 1, el 2026-08-05. Es el único rol con visión horizontal sobre el
conjunto de productos, y la Fase 1 lo identificó como el **custodio natural del catálogo**, función que no
tiene titular. Conoce lo técnico, pero su lente es de producto.
**Distancia.** Mirada de negocio.

**Qué hace en la evaluación.** Participa en la primera llamada y **no usa la herramienta**: observa la
demostración, reacciona, pregunta y recomienda. Al cierre completa el instrumento escrito y responde, con sus
palabras, qué es esto, hasta dónde llega y qué le falta.

**Qué sostiene su participación.**

- **El noveno criterio de la rúbrica externa**, el único que quedaba sin medir: que alguien con mirada no
  técnica pueda explicar propósito, alcance y pendientes sin leer el código. Su respuesta textual *es* esa
  medición.
- La **adoptabilidad**: si la estandarización que la línea propone es la que el equipo necesita, y si el
  gobierno del catálogo es sostenible por alguien.
- El **antes/después de sus propios ítems cerrados** de agosto: divergencia entre proyectos, costo de propagar
  un cambio, conveniencia de estandarizar y utilidad esperada de una herramienta así.

**Qué la sesga.** Declaró la banda de 15 días que hoy forma parte de la línea base: es juez y parte de la
referencia contra la que se compara. Y conoce el proyecto desde su inicio, así que no es un observador nuevo.

**Qué no puede sostener.** El tiempo de un arranque real, porque no arranca proyectos; ni la suficiencia del
andamio, porque no escribe el código.

### 2.3 PE-03 · Desarrollador interno

**Rol en el proyecto.** Informante de la Fase 1, el 2026-08-05. **Es quien ejecuta hoy el proceso que la
solución quiere reemplazar**, y quien usaría la herramienta en el día a día.
**Distancia.** Usuario del contexto.

**Qué hace en la evaluación.** Participa en la primera llamada con `PE-02`, y en la tercera, **solo y con las
manos**: instala la herramienta desde el feed, deriva un proyecto, incorpora un módulo del catálogo y escribe
la primera operación de negocio sobre lo derivado. Al cierre completa el instrumento.

**Qué sostiene su participación.** **Los tres criterios del objetivo específico 4.** Es el único participante
cuya ejecución los mide:

| Criterio | Qué aporta `PE-03` |
| :---- | :---- |
| Tiempo de generación | Lo que tarda él, no el autor, desde instalar hasta que el proyecto corre. Y la estimación de las seis tareas que la herramienta no cubre, que son las que hace hoy |
| Incorporación de un módulo | La ejecuta, y dice si el resultado es lo que esperaba |
| Inicio de lógica de negocio | Escribe la primera operación y dice qué le faltó para empezar |

Y el antes/después más directo que tiene el proyecto: sus seis ítems de agosto, incluido **«tiempo hasta que el
proyecto corre: 8 días»** y **«dificultad del arranque hoy: 5»**, el valor más alto de la escala.

**Qué la sesga.** Conoce el proyecto y conoce al autor; no es un sujeto ingenuo. Su tiempo de agosto es parte
de la línea base, con lo que también es juez y parte. Y sabe que lo que mide es el trabajo de alguien cercano,
lo que presiona hacia la cortesía: el instrumento escrito e individual existe, entre otras cosas, para bajar
esa presión.

**Qué no puede sostener.** Nada sobre otros contextos, ni sobre el gobierno del catálogo, que no es su función.

### 2.4 PE-04 · Desarrollador externo, y autor del informe del 2026-10-28

**Rol en el proyecto.** Informante de la Fase 1 —el contraste externo— y **autor del informe de evaluación
externa del 2026-10-28**, con sus nueve criterios de aceptación, escritos antes de que la Fase 3 construyera y
sobre la versión `0.2.1` de la herramienta. Ese informe gobernó dos rondas de mejoras y diecisiete grupos de
trabajo.
**Distancia.** Par técnico externo.

**Qué hace en la evaluación.** Participa en la segunda llamada: usa la herramienta, conversa y **vuelve a
aplicar su propia rúbrica** sobre la versión publicada. Al cierre completa el instrumento y declara cómo la
percibe hoy.

**Qué sostiene su participación.**

- **La rúbrica completa, con su «antes» real.** Es la segunda aplicación por la misma persona, no por un
  tercero que la aplica prestada: eso es lo que convierte la primera en un «antes» comparable y no en una
  opinión de otro momento.
- La **transferibilidad**: si el artefacto se sostiene en otro entorno regulado, con otro stack y otras
  convenciones.
- El contraste de su propio dato de agosto —«dos semanas» de arranque—, que se reporta aparte y nunca se suma
  a la banda del contexto estudiado.

**Qué la sesga.** Su informe de octubre produjo mejoras que él mismo va a evaluar, de modo que puede leer como
resuelto lo que recuerda haber pedido. Lo compensa el hecho de que sus criterios eran verificables y están
escritos: se vuelven a responder contra el artefacto, no contra el recuerdo.

**Qué no puede sostener.** La comparación contra la línea base del contexto estudiado, porque su proceso de
arranque es otro.

## 3. Cobertura: qué sostiene cada participante

Garantiza que ninguna pregunta de la fase quede sin fuente y que ninguna participación exista sin propósito.

| Qué hay que establecer | Quién lo sostiene |
| :---- | :---- |
| Tiempo de generación frente a la línea base | `PE-03`, con el registro de `PE-01` |
| Correcta incorporación de un módulo | `PE-03`, con el registro de `PE-01` |
| Inicio de implementación de lógica de negocio | `PE-03` |
| Los nueve criterios de la rúbrica externa | `PE-04`, salvo el noveno |
| El noveno criterio: explicar el producto sin leer código | `PE-02` |
| Adoptabilidad en el equipo y gobierno del catálogo | `PE-02`, con la opinión de `PE-03` |
| Transferibilidad fuera del contexto | `PE-04` |
| Conformidad técnica y reproducibilidad | `PE-01` |
| RNF-03: análisis con las herramientas de la organización | `PE-03`, por tener acceso a ellas |
| Oportunidades de mejora y recomendaciones | Los cuatro, cada uno desde su distancia |

## 4. Lo que ningún participante cubre

Declarado para que su ausencia no se lea como olvido:

- **No hay tester.** La Fase 1 lo identificó como beneficiario funcional —todo lo generado pasa por su
  trabajo— y aportó requerimientos de consistencia externa. Nadie lo representa, así que la consistencia entre
  productos desde la perspectiva de cliente **no se mide**.
- **No hay líder de producto.** `PE-02` aporta mirada de negocio, que es lo que el noveno criterio pide, pero
  no es el rol que sufre el costo en alcance. Lo que la Fase 1 documentó como sacrificio de funcionalidades por
  costos técnicos —T-03, con un 5 de 5 en frecuencia— **no se vuelve a medir**.
- **No hay función de arquitectura.** Sus definiciones condicionaron la forma de lo generado y nadie verifica
  su cumplimiento acá, más allá de lo que RNF-03 mida por análisis estático.
- **Hay una sola persona por rol.** Ningún dato de esta fase admite promedio ni dispersión: se reporta
  individualmente, con el rol que lo produjo.

## 5. Confidencialidad y consentimiento

Igual que en la Fase 1, y es la regla 3 del proyecto:

- A cada participante se le dice al abrir la llamada para qué es la sesión, que se registra, qué se va a
  publicar —su rol, nunca su nombre— y que puede pedir que algo no quede registrado.
- La bitácora puede nombrar a la persona; **los documentos de esta fase la citan por su `PE-xx` y su rol**; la
  tesis, solo por el rol.
- No entra al expediente ningún dato privado de la organización: ni nombres de productos internos, ni rutas de
  repositorios, ni configuración con proveedor concreto. Lo que haya que nombrar se describe por su propiedad,
  como en el resto del proyecto.

## 6. Qué se mide, y con qué forma

Tres criterios del objetivo específico 4, más la rúbrica externa, más las recomendaciones.

La forma se hereda del protocolo de la Fase 1: **conversación abierta más un conjunto reducido de ítems
cerrados al final**. Esa fase lo llamó entrevista semiestructurada de diseño mixto, y acá se usa por una razón
que ninguna otra forma da: **si los ítems cerrados se repiten, el dato de agosto de 2026 es el «antes» y el de
estas llamadas es el «después»**, en la misma escala y con las mismas personas. La mitad de la medición ya está
tomada.

Lo abierto produce las recomendaciones; lo cerrado produce la comparación. Ninguno de los dos sobra.

## 7. Definición operacional, heredada sin modificar

Es la del doc 1. Si esta fase midiera con otro inicio, otro fin u otra unidad, la comparación no valdría.

| Elemento | Definición |
| :---- | :---- |
| **Inicio** | La decisión de construir el proyecto |
| **Fin** | El proyecto corre correctamente en local **y** queda desplegable en la rama principal, de modo que el resto del equipo pueda aportar cambios reales |
| **Unidad primaria** | Días. En esta fase, además, minutos para la parte que la herramienta ejecuta |
| **Unidad derivada** | Horas-persona, con los supuestos S-1 (jornada efectiva de 6.5 h), S-2 (una persona dedicada) y S-3 (días hábiles) |
| **Regla de las tres cubetas** | La comparación principal se reporta sobre las **23 tareas cubiertas** por la herramienta. Las **2 parciales** y las **6 fuera de alcance** se reportan al lado, estimadas con `PE-03`, que es quien las hace hoy |

**La línea base contra la que se compara:** 8 a 15 días, equivalentes a 52 a 98 horas-persona, con n=2 y sin
corroboración publicable. El inventario de las 31 tareas está en
`Insumos/Linea base/01-inventario-de-tareas-de-arranque.md`.

## 8. Qué superficie usa la sesión

Es una decisión que la sesión no puede improvisar: la herramienta tiene **dos plantillas** y una de ellas
cambió de nombre desde la última vez que un participante la vio.

| Qué | Lo que la sesión usa |
| :---- | :---- |
| Plantilla de la demostración y de la medición | **`nestjs-hexagonal-api`**, la hexagonal. Es la que la línea base compara, la que el evaluador externo aplicó en octubre y la única que tiene módulos que la sirvan |
| `azure-functions-api` | **Se muestra y no se mide.** Existe para que el participante vea que el almacén es plural y que agregar una plantilla no cuesta una versión de la herramienta. Medir dos plantillas duplica la sesión y ninguna quedaría medida bien |
| El nombre que el evaluador instaló en octubre | Se le dice **antes de empezar** que el paquete de la plantilla cambió de nombre y que lo que deriva no cambió. Que lo descubra a mitad de la sesión contamina la medición de usabilidad con un problema de nombre |
| Los comandos | La superficie agrupada: `bsl templates list`, `bsl new --template`, `bsl modules list\|add\|update\|remove`. Los nombres anteriores siguen vivos, y **también se dice**, porque un participante que tenga un guion escrito contra el nombre viejo necesita saber que no se le rompió |

**Por qué se decide acá y no en la llamada.** Las dos cosas que esta tabla fija —qué plantilla se mide y qué se
le cuenta al participante antes de empezar— cambian el resultado. Decidirlas después de medir sería elegir la
lectura que convenga.

**La consecuencia que hay que aceptar.** La forma `azure-functions@1` **no queda medida** por esta evaluación,
y eso incluye su propio arranque, que ninguna puerta del repositorio comprueba porque exige las Azure Functions
Core Tools. Queda declarado como límite del informe y como trabajo futuro.

## 9. Las tres llamadas

Una hora cada una. Conversadas, no guionadas: el autor introduce la herramienta, muestra la instalación, el uso
y el mantenimiento, y se habla abiertamente. El rigor no está en el guion, está en el instrumento del cierre.

### 9.1 Llamada 1 · `PE-03` desarrollador interno y `PE-02` líder técnico

| Tramo | Qué ocurre |
| :---- | :---- |
| 5 min | Para qué es la sesión, que se registra, qué se publica y qué no. Consentimiento |
| 10 min | Qué es la línea: qué produce la herramienta y qué **no** produce. Se dice explícitamente que es un habilitador técnico y no un producto de negocio terminado |
| 20 min | Demostración de punta a punta: instalación, **la lista de plantillas para que vea que el almacén es plural**, derivación de un proyecto con la plantilla hexagonal, lo que queda escrito, cómo se incorpora un módulo, cómo se actualiza y cómo se quita |
| 20 min | Conversación abierta. Se deja hablar; lo que el participante trae sin que se le pregunte es el dato más valioso |
| 5 min | Cierre y entrega del instrumento, que **cada uno completa por separado y en escrito**, no durante la llamada |

### 9.2 Llamada 2 · `PE-04` desarrollador externo

Misma estructura, con dos diferencias: usa la herramienta durante la llamada, y en el instrumento se le agrega
**la rúbrica de nueve criterios que él escribió** el 2026-10-28, para que la responda de nuevo.

### 9.3 Llamada 3 · `PE-03`, solo y con las manos

Es la llamada que mide el objetivo 4. No es una demostración: el participante teclea.

| # | Paso | Qué se cronometra |
| :-- | :---- | :---- |
| 1 | Instala la herramienta desde el feed de la organización | Minutos, y si hizo falta ayuda |
| 2 | Deriva un proyecto respondiendo las preguntas, sin que el autor dicte las respuestas | Minutos, y cuántas preguntas tuvo que volver a corregir en la revisión |
| 3 | Levanta el proyecto y comprueba que responde: sondas, documento OpenAPI y la página de documentación | Minutos hasta la primera respuesta correcta |
| 4 | Incorpora un módulo del catálogo | Minutos, y si el producto siguió arrancando |
| 5 | Reinicia y comprueba que el dato sobrevive | Sí o no |
| 6 | Pasa el producto por el analizador estático de la organización | Si pasó sin adaptación previa, que es el criterio textual de **RNF-03** |
| 7 | Escribe la primera operación de negocio sobre lo derivado | Minutos, y qué le faltó para empezar |
| 8 | Estima las seis tareas que la herramienta no cubre | Su estimación, en sus unidades |

**Si la llamada 3 no ocurre**, los reemplazos quedan decididos de antemano, en este orden, y hay que declarar
cuál se usó:

1. **La misma tarea, asincrónica.** Se le entrega a `PE-03` la hoja de pasos y reporta sus tiempos. Se pierde
   la observación de dónde se trabó, que es lo más valioso.
2. **La ejecuta el autor.** `PE-03` revisa el resultado y estima qué le habría costado a él. Es la más débil:
   mide el artefacto en manos de quien lo construyó, y la medición lo dirá en su primera línea.

## 10. El instrumento de cierre

Lo completa cada participante **por separado, en escrito y después de la llamada**. Quince ítems —doce cerrados
y tres abiertos, más los añadidos por rol— para que se complete en pocos minutos: un instrumento largo se
responde con prisa, y el dato pierde valor.

### 10.1 Los seis ítems de agosto, repetidos

Misma escala, misma redacción, ahora sobre el artefacto. La columna del «antes» ya está tomada y **no se vuelve
a preguntar**: se cita.

| # | Ítem, ahora sobre la herramienta | Escala | Antes · `PE-02` | Antes · `PE-03` | Antes · `PE-04` |
| :-- | :---- | :---- | :--: | :--: | :--: |
| C1 | Dificultad de arrancar un proyecto **con la herramienta** | 1 a 5 | 3 | 5 | 4 |
| C2 | Tiempo hasta que el proyecto corre, **con la herramienta** | horas o días | 15 días | 8 días | 2 semanas |
| C3 | Frecuencia con que habría que reutilizar por copia, **teniendo el catálogo** | 1 a 5 | 3 | 4 | 4 |
| C4 | Costo de propagar un cambio de una capacidad compartida, **con un módulo incorporado** | 1 a 5 | 4 | 5 | 3 |
| C5 | Divergencia esperable entre proyectos **generados por la herramienta** | 1 a 5 | 2 | 3 | — |
| C6 | Utilidad **comprobada** de la herramienta, después de verla funcionar | 1 a 5 | 5 | 5 | — |

En C6 el «antes» era *utilidad esperada* y el «después» es *utilidad comprobada*. Es el único ítem donde el
enunciado cambia, y cambia a propósito: una expectativa y una comprobación no son lo mismo, y el informe lo
dirá así.

### 10.2 Seis ítems nuevos, sobre el artefacto

Escala de 1 a 5. La columna de la derecha dice quién puede responder cada uno: a quien no usó la herramienta no
se le pregunta por la instalación.

| # | Ítem | Quién responde |
| :-- | :---- | :---- |
| N1 | Claridad de qué produce la herramienta y qué no: que es un habilitador técnico y no un producto de negocio | Los tres |
| N2 | Facilidad de la instalación y del primer uso | `PE-03`, `PE-04` |
| N3 | Confianza en el proyecto generado frente a uno hecho a mano | Los tres |
| N4 | Suficiencia del andamio para empezar a escribir la lógica de negocio | `PE-03`, `PE-04` |
| N5 | Claridad del mantenimiento: cómo se actualiza y quién lo sostiene | Los tres |
| N6 | Viabilidad de adoptarlo en el equipo | Los tres |

Se descartaron dos ítems que estaban propuestos —facilidad del flujo de preguntas y probabilidad de usarlo en
el próximo proyecto— porque se solapan con N2 y N6. Un instrumento con ítems redundantes mide dos veces lo
mismo y cansa a quien responde.

### 10.3 Tres preguntas abiertas, y los añadidos por rol

1. ¿Qué te sirvió y qué no?
2. ¿Qué le falta para que lo adoptes?
3. Si solo pudieras pedir un cambio, ¿cuál sería?

La tercera está así a propósito: forzar la prioridad produce mejor dato que pedir una lista.

**A `PE-02`** se le agrega una sola pregunta, de respuesta libre, y su respuesta textual **es** la medición del
noveno criterio de la rúbrica:

> Con tus palabras, y sin leer código: ¿qué es esto, hasta dónde llega y qué le falta?

El criterio dice *«un líder no técnico puede explicar propósito, alcance y pendientes sin leer el código»*, así
que se evalúa contra esas tres cosas y se declara cuáles aparecen en la respuesta.

**A `PE-04`** se le agregan sus nueve criterios, respondidos de nuevo con la misma escala con que los escribió:
cumple o falla. Ocho figuran hoy como cumplidos en el seguimiento de mejoras, y ese registro es del autor: acá
los responde el evaluador. Si alguno que el seguimiento declara cumplido él lo marca como falla, **el dato que
vale es el suyo**.

## 11. Qué cuenta como evidencia

Un criterio no se declara cumplido por una impresión favorable.

| Criterio | Evidencia suficiente |
| :---- | :---- |
| **Tiempo de generación** | El cronómetro de la llamada 3, paso por paso, más la estimación de `PE-03` para las seis tareas no cubiertas. Se reporta en minutos para lo cubierto y en horas-persona para el total, contra la banda de la línea base |
| **Correcta incorporación de un módulo** | Tres hechos comprobados en ejecución: el producto sigue arrancando, su registro declara el módulo y su versión, y el dato sobrevive al reinicio. Más la declaración de `PE-03` de si el resultado fue lo que esperaba. **RF-16** se evalúa aparte: si `PE-02` considera que el procedimiento de incorporación al catálogo le alcanza para ejercer el gobierno |
| **Inicio de lógica de negocio** | La operación escrita por `PE-03`, corriendo, con su prueba. Y la lista de lo que tuvo que resolver él y esperaba encontrar hecho |
| **RNF-03** | El producto generado pasa por el analizador de la organización **sin adaptación previa**. Si hubo que adaptarlo, se declara qué y el criterio se reporta como no cumplido |
| **Rúbrica externa** | Los nueve criterios respondidos por `PE-04`, salvo el noveno, que lo responde `PE-02` |
| **Viabilidad y adopción** | Los ítems N5, N6 y las tres abiertas, de los tres participantes, más lo que haya quedado en la bitácora |

## 12. Amenazas a la validez, y qué las contiene

| Amenaza | Qué la contiene |
| :---- | :---- |
| En la llamada 1 un participante ancla al otro | El instrumento se completa por separado, en escrito y después de la llamada |
| El autor conduce y condiciona | Se registra como observación de método en cada entrada de la bitácora. El autor no responde ningún ítem del instrumento |
| Cortesía hacia el autor | El instrumento es escrito e individual, y la tercera pregunta abierta obliga a nombrar un cambio: no admite «está todo bien» |
| Los participantes no son ingenuos | Declarado participante por participante en la §2. Es el costo de que sean los mismos informantes de la Fase 1, que es lo mismo que hace válido el antes/después |
| Una hora alcanza para ver, no para usar | Por eso existe la llamada 3, y por eso es la que carga el objetivo |
| El artefacto se evalúa en una versión y se corrige después | La medición declara qué versión servía el feed el día de cada llamada. Corregir es otra ronda, no parte de esta medición |

## 13. Qué no se mide, y por qué

- **Adopción en el tiempo.** Tres llamadas no la miden.
- **Consistencia entre productos desde la perspectiva de cliente.** No hay tester entre los participantes.
- **El costo en alcance de negocio** que T-03 enuncia. No hay líder de producto entre los participantes.
- **El cumplimiento de las definiciones de arquitectura** más allá de lo que RNF-03 cubra por análisis
  estático.
- **Nada con promedio ni dispersión.** Hay una persona por rol, y cada dato se reporta con el rol que lo
  produjo.
