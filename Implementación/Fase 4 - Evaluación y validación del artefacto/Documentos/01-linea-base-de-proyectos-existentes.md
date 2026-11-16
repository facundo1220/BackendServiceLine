# Línea base de proyectos existentes

Cuánto cuesta hoy, sin la herramienta, llevar un proyecto backend nuevo desde la decisión de construirlo
hasta que corre en local y queda desplegable en la rama principal; y con qué definición exacta se mide, para
que la medición de esta fase mida el otro lado y la comparación signifique algo. No hay decisiones nuevas acá: se
aplica la que la fase ya tomó sobre cómo constituirla.

---

## 1. Por qué hace falta una referencia

El objetivo específico 4 del anteproyecto compromete tres mediciones: el tiempo de configuración inicial
**frente a la línea base de proyectos existentes**, la correcta incorporación de un módulo reutilizable y el
inicio de implementación de lógica de negocio en el proyecto generado. La primera es comparativa, y una
comparación sin referencia no se puede hacer.

Lo que queda fijado, en concreto: la definición operacional de qué se mide y entre qué dos puntos, seis métricas con la
fuente de cada una, el inventario de las tareas del arranque con la parte que la herramienta cubre y la que no,
la banda de tiempo del contexto estudiado, el costo actual de reutilizar y propagar una capacidad compartida, y
los límites de todo lo anterior.

## 2. Por qué es una línea base reconstruida

El índice de esta fase declaró el documento 7 con una condición sobre su oportunidad: convenía tomarlo
**antes** de que la herramienta produjera proyectos, porque el dato es más creíble recogido antes de que exista
el artefacto. No se tomó, y la condición se venció: la herramienta deriva productos verificables desde octubre
de 2026. Por eso figuró como riesgo declarado al cerrar las fases 2 y 3, y no como tarea
olvidada.

Qué hacer con la ventana cerrada se resolvió en dos partes. La primera es que **la
ventana no se cerró para todo**: el autoreporte del costo del arranque ya estaba recogido, en las preguntas
cerradas de las entrevistas del 5 y 6 de agosto de 2026, anteriores a la primera línea de la herramienta.
Ninguna de esas respuestas pudo estar influida por el artefacto, porque el artefacto no existía. La segunda es
que lo que **sí** se perdió —una medición instrumentada del proceso en vivo— no se reemplaza con un sustituto
que parezca equivalente:

- No se levanta autoreporte nuevo. El equipo ya conoce la herramienta, y una respuesta de hoy sobre el proceso
  anterior mediría el recuerdo, no el proceso.
- No se reconstruye la línea base del historial de los repositorios de proyectos anteriores. No hay acceso
  institucional a ellos, y su historial es material privado de la organización que este expediente no publica,
  ni completo ni anonimizado. Ninguna afirmación de este documento se apoya en ese material.
- No se ejecuta un arranque manual cronometrado hoy. Quien lo hiciera ya conoce la estructura que la línea
  produce, de modo que mediría un arranque informado y no el arranque real.

Queda entonces una línea base **reconstruida y no prospectiva**, sostenida en dos fuentes: el autoreporte ya
recogido y un inventario de las tareas del arranque. La §9 declara qué no puede decir. Esa declaración es parte
del resultado: una banda presentada como si fuera una medición instrumentada sería un dato peor que un dato con
su límite escrito.

## 3. Definición operacional

Es la parte vinculante del documento. La medición de esta fase usa esta misma definición, o la comparación
no es válida.

| Elemento | Definición |
| :---- | :---- |
| **Inicio** | La decisión de construir el proyecto. No el primer commit, que ya es trabajo hecho |
| **Fin** | El proyecto corre correctamente en local **y** queda desplegable en la rama principal, de modo que el resto del equipo pueda aportar cambios reales |
| **Sujeto** | Un servicio backend nuevo del tipo que la línea produce |
| **Unidad primaria** | Días, reportados como banda. Con dos puntos de dato no se reporta promedio ni dispersión |
| **Unidad derivada** | Horas-persona, por conversión declarada con los supuestos S-1 a S-3 |

**Qué incluye.** Todo el trabajo técnico del arranque: entorno y herramientas, arquitectura del servicio,
capacidades transversales, pruebas, y el tramo de repositorio, integración continua y despliegue que el fin
declarado exige.

**Qué excluye, y por qué.**

- **El análisis previo.** El líder técnico lo señaló como el paso donde más reprocesos y cambios de fecha
  ocurren, y es anterior al inicio definido. Excluirlo es lo que mantiene la medición sobre el arranque técnico.
- **El tiempo muerto del resto del equipo.** El desarrollador interno describe al menos una semana en la que el
  equipo está a la espera y asigna su tiempo a otras iniciativas. Es un costo de oportunidad real, distinto del
  esfuerzo del arranque, y la línea base lo declara sin cuantificarlo.
- **La implementación de la lógica de negocio del producto.** Es el tercer criterio del objetivo 4 y se mide en
  los documentos de medición, no acá.

**Los tres supuestos de la conversión.** Derivados en el insumo 02 y resumidos acá:

| | Supuesto | Valor | En qué se apoya |
| :-- | :---- | :---- | :---- |
| S-1 | Jornada efectiva | **6.5 h/día** | Jornada nominal de 8 h menos 7.5 h semanales de ceremonias, el 19 % |
| S-2 | Dedicación | Una persona, completa | T-01, y la prosa «si uno se enfoca en esa tarea» |
| S-3 | Lectura de «días» | **Hábiles**, con días calendario como piso | Lectura literal de una estimación de trabajo, reportada con sensibilidad |

## 4. Las seis métricas y su fuente

| Métrica | Qué mide | Fuente | Naturaleza |
| :---- | :---- | :---- | :---- |
| **M1** | Días desde el inicio hasta el fin | Preguntas cerradas de las entrevistas | Autoreporte, anterior al artefacto |
| **M2** | Horas-persona equivalentes | M1 convertido con S-1 a S-3 | Derivada, con supuestos declarados |
| **M3** | Pasos manuales que el arranque exige | Inventario de tareas (insumo 01) | Reconstruida de T-01 y del activo base |
| **M4** | Superficie que hoy no hay que escribir | Activo base contado el 2026-11-06 | Objetiva, sobre artefacto propio |
| **M5** | Divergencia entre proyectos | Percepción declarada y T-04 | Cualitativa |
| **M6** | Costo de propagar un cambio de una capacidad compartida | Percepción declarada, T-04 y T-05 | Cualitativa, con escala |

M4 es la única métrica enteramente objetiva de este documento, y lo es porque mide un artefacto del proyecto y
no uno de la organización: los **62 archivos** que hoy entrega el activo base sin contar la salida de
compilación —31 en `src`, 18 en `test` y 13 de configuración en la raíz—. Lo que M4 dice es qué superficie deja
de escribirse a mano, no cuánto tiempo ahorra: el tiempo lo aportan M1 y M2.

## 5. El inventario, y la regla que vuelve honesta la comparación

El fin declarado en §3 es **más ancho que el alcance de la herramienta**. La derivación deja un proyecto que
corre y pasa su propia verificación, pero no crea el repositorio en el servidor corporativo, no define la
integración continua, no configura el despliegue y no crea la base de datos. Comparar el tiempo de una
derivación contra el proceso completo sobreestimaría la ganancia, y por eso rige la regla de las tres
cubetas: cada tarea se clasifica en **cubierta**, **parcialmente cubierta** o **fuera del alcance**, y la
comparación principal se reporta sobre la primera cubeta, con el total al lado como contexto.

El inventario completo, con el archivo que resuelve cada fila, está en el insumo 01. Su recuento:

| Cubeta | Tareas | Qué agrupa |
| :---- | :--: | :---- |
| Cubierta | **23** | Entorno y herramientas, arquitectura del servicio, cuatro transversales y la verificación local |
| Parcialmente cubierta | **2** | Exportar las señales a un colector y persistir el agregado: exigen incorporar un módulo del catálogo |
| Fuera del alcance | **6** | Autenticación, y el tramo de repositorio, integración continua, despliegue y base de datos |
| **Total** | **31** | |

El recuento no es el beneficio. Una tarea cubierta no pesa lo mismo que una fuera del alcance, y crear el
repositorio, el pipeline y la base de datos puede costar más que varias de las cubiertas juntas. Lo que el
recuento fija es sobre qué subconjunto se puede comparar sin inflar el resultado.

## 6. La línea base del arranque

**Criterio 1 del objetivo 4.**

| | Contexto estudiado | Contraste externo |
| :---- | :---- | :---- |
| M1, días | **8 a 15** (dos puntos: 15 del líder técnico, 8 del desarrollador interno) | 2 semanas |
| M2, horas-persona, lectura principal | **52 a 98** | — |
| M2, horas-persona, piso | 37 a 70 | — |
| Dificultad percibida del arranque (1 a 5) | 3 y 5 | 4 |
| Quién lo ejecuta | Un solo desarrollador; el resto del equipo espera (T-01) | — |

**Cómo se lee.** El arranque de un proyecto backend en el contexto estudiado cuesta, declarado por quienes lo
hacen, entre **una y dos semanas y media de trabajo efectivo de una sola persona**. La conclusión no depende de
la lectura de S-3: en la lectura de días calendario la banda baja a 37-70 horas y sigue estando en ese orden. El
dato del contexto externo coincide en magnitud y se reporta aparte, nunca sumado.

**Una corroboración que no se publica.** El
autor conoce el contexto y contrastó esta banda contra los registros de tiempo con que ese contexto mide su
propio trabajo —el historial de sus proyectos y sus métricas—, y es consistente con lo que las entrevistas
declararon. Ese material es privado: no se transcribe, no se cita, no se identifica ningún proyecto y no se
reporta ninguna de sus cifras. Por eso la corroboración **no cuenta como evidencia de este documento**: la
banda se sostiene en el autoreporte, y esta nota solo deja constancia de que quien escribe no la toma como un
dato aislado.

Dos matices que la banda sola no transmite, los dos del expediente:

- El desarrollador interno fija la expectativa contra la cual se leerá el resultado de la medición: que ese
  proceso se reduzca «a solo algunos minutos».
- El desarrollador externo aporta el matiz que sostiene el problema: **incluso con librerías y módulos
  compartidos disponibles**, persiste un espacio de configuración desde cero, porque hay que comprobar que lo
  que viene hecho funcione. La línea base no es, entonces, el costo de escribir código desde una hoja en blanco:
  es el costo de dejar un servicio funcionando y desplegable, que persiste aunque haya piezas reutilizables a
  mano.

## 7. La línea base de la reutilización y la propagación

**Criterio 2 del objetivo 4.** La medición de esta fase cubre la incorporación de un módulo reutilizable, y también
necesita contra qué.

| Qué | Estado actual |
| :---- | :---- |
| Mecanismo de reutilización | **Copia de carpetas entre proyectos**, con ajuste de variables de entorno, o reconstrucción de la estructura tomando otro proyecto como referencia visual (T-04) |
| Alcance del mecanismo | Solo código de aplicación |
| Organización de repositorios | Repositorios independientes por proyecto |
| Estándar arquitectónico | No documentado y de aplicación parcial |
| Frecuencia de reutilización por copia (1 a 5) | 3 y 4 |
| Costo percibido de propagar un cambio (1 a 5) | **4 y 5** |
| Divergencia percibida entre proyectos (1 a 5) | 2 y 3 |
| Punto más frágil | El contrato del servicio consumido: cuando cambia la estructura de la respuesta, se desencadenan ajustes en cascada en cada proyecto afectado (T-05) |
| Cuántos repositorios hay que tocar | **No disponible.** Las entrevistas dan el costo percibido, no el conteo |

Desde el rol de producto, el efecto de todo esto sobre el producto: la frecuencia con que un producto requiere
integrar funcionalidades ya existentes en otros se califica 4; el impacto de esa integración sobre el cronograma
cuando aparece a mitad de camino, 4; y la frecuencia con que **se sacrifican funcionalidades de negocio** por
estos impactos, 5. Eso es T-03 medido en percepción: el costo técnico se paga en alcance.

**Qué se compara.** Contra esta fila, no contra un tiempo: hoy incorporar una capacidad ya resuelta
es copiar y ajustar a mano, sin vínculo con el origen y sin propagación; la herramienta ofrece una operación de
un comando que la incorpora y otra que la actualiza preservando lo que el equipo cambió. La comparación es de
mecanismo y de costo de propagación, y es exactamente lo que B-01 y B-02 enuncian como brechas.

## 8. Cómo se mide el otro lado

Para que la comparación sea válida, la medición tiene que usar la definición de §3 y reportar con la regla de
§5. En concreto:

1. **Mismo inicio y mismo fin.** Desde la decisión de construir hasta un servicio que corre y queda desplegable
   en la rama principal. Si el laboratorio no despliega el producto generado, el fin se declara alcanzado
   parcialmente y se dice cuál tramo faltó.
2. **Dos tiempos, no uno.** El tiempo de la derivación y el tiempo de las tareas que quedan a cargo del equipo,
   que son las seis fuera del alcance y la parte no cubierta de las dos parciales. La suma de los dos es lo
   comparable contra M1 y M2; el primero solo, contra la cubeta cubierta.
3. **La misma unidad.** Horas-persona con los supuestos S-1 y S-2, para no comparar minutos contra días.
4. **El inventario como checklist.** Cada una de las 31 tareas se marca como resuelta por la herramienta, hecha
   por el equipo o no aplicable, y esa marca es la evidencia.

El tiempo de la herramienta **no se estima acá**: no está medido, y una estimación en este punto contaminaría
la medición de esta fase. El dato de la derivación lo produce ella, con su propio registro.

## 9. Lo que esta línea base no puede decir

- **No es una medición instrumentada.** M1 y M2 son autoreporte, y M2 además es derivada. El documento no afirma
  haber cronometrado ningún arranque.
- **n = 2** para el contexto estudiado. No hay promedio, no hay dispersión y no hay intervalo. La banda es el
  resultado, y es lo máximo que estos datos sostienen.
- **Sin corroboración publicable.** La que existe es conocimiento del autor sobre su contexto, declarada en §6
  y sin valor probatorio: no se puede verificar leyendo este expediente, y por eso no sostiene ninguna
  conclusión. No se publica por confidencialidad del material.
- **Sin conteo de propagación.** Cuántos repositorios toca un cambio de capacidad compartida no se sabe.
- **El fin es más ancho que el alcance de la herramienta**, y seis de las treinta y una tareas seguirán siendo
  trabajo del equipo después de la derivación. Cualquier lectura que atribuya la banda completa al ahorro de la
  herramienta es incorrecta, y la regla de las tres cubetas existe para impedirla.
- **El tiempo muerto del equipo y el análisis previo quedan fuera**, declarados en §3.

Ninguno de estos límites se descubre al final: todos salen de la decisión de medir con la ventana cerrada, y es
la razón por la que el índice de la fase pedía tomar este dato antes. Esa lección va al capítulo de lecciones
aprendidas de la tesis.

## 10. Trazabilidad

| Elemento | Hacia dónde traza |
| :---- | :---- |
| El problema que la línea base cuantifica | T-01, T-02, T-03 (arranque manual, concentrado y pagado en alcance) |
| El mecanismo que la §7 describe | T-04, T-05 |
| Las necesidades | T-01, T-02, T-03, T-14 |
| Las brechas | B-01 (incorporar a un proyecto en curso), B-02 (propagar el cambio de un módulo) |
| Los requerimientos que se evalúan contra esta referencia | RF-01, RF-06, RNF-01 |
| El compromiso del anteproyecto | Objetivo específico 4, criterios 1 y 2 |

**Condición de llegada de este documento**, comprobable: existe una definición operacional única que las dos
mediciones comparten; existe una banda del contexto estudiado con su origen citado; existe un inventario con
cada tarea clasificada y su archivo de respaldo; y existe una declaración de límites que dice qué no puede
concluirse. Las cuatro están en este documento y en sus dos insumos.
