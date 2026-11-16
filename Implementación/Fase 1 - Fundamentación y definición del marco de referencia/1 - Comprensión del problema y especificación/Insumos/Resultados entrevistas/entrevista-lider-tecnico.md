# Entrevista: Asesoría Líder Técnico

**Entrevistador:** Jorge Andrés Facundo Solarte
**Entrevistado:** el líder técnico
**Fecha:** 5 de agosto de 2026
**Duración:** 20 min 52 s

---

## Comentario del entrevistado sobre una herramienta propia similar (con IA)

Al ver la explicación inicial de la herramienta, el líder técnico comenta que hace un tiempo diseñó algo similar para uso personal en Python, con un cliente muy parecido. Detalles que agrega:

- Actualmente le está agregando el **tema de IA** dentro de la estructura.
- La idea: se tiene una plantilla que se activa (por CLI) y despliega todo un entorno de desarrollo con características base.
- **Qué debería ir dentro de ese entorno de desarrollo (con IA):**
  - Un área o archivo tipo `.md` con el **tema de estándares**: una carpeta con todos los estándares deseados — reglas de integración, reglas de seguridad, reglas de testeo.
  - Un módulo de **"estándares IA" o "guía IA"**, como lo básico de IA dentro del entorno.

**Respuesta del entrevistador:** el plan es que toda esta guía haga parte principalmente del **motor**, que se alimente de inteligencia artificial y de los componentes del repositorio, los estándares y la gestión de módulos; que el motor sea capaz de generar buscando equilibrio entre la **rigidez de un sistema tradicional** y la **personalización que da un sistema con inteligencia artificial**.

---

## Parte A – Preguntas abiertas

### Como rol con visión sobre todos los productos, ¿cómo describirías las diferencias estructurales entre ellos?

- Depende de las necesidades de cada proyecto.
- Depende del **tipo de usuario final**: si es un usuario de aplicaciones móviles o un usuario de oficina — el entorno en el que se mueva ese usuario final genera un cambio en la estructura.
- Depende del **tipo de integración** que vaya a tener la solución:
  - Si requiere integraciones con banco / módulos de banco.
  - Si requiere integraciones solo con terceros.
  - Si esas integraciones con el banco serán soluciones **on-premise o en nube del banco**.
- Todo esto define cómo debería ser la arquitectura.

### ¿Qué se configura manualmente cada vez que se arranca un proyecto?

- Actualmente se hace **todo el levantamiento de entornos manualmente**, desde cero.
- La **configuración de la arquitectura** o los componentes se hace normalmente de forma manual.
- Los **componentes de infraestructura** que se requieran también se hacen de forma manual.
- En resumen: en este momento, todo lo que se requiere se está realizando de forma manual.

### ¿Qué suele descubrirse tarde, ya avanzado el proyecto, que hubiera convenido resolver al inicio?

- Lo que más genera **reproceso** al momento de desplegar tiene que ver con **políticas del banco en integraciones**.
- Ejemplo: no se puede hacer una integración directa entre 2 aplicaciones en la nube si están en distintos *tenants* del banco (uno en un tenant, otro en otra plataforma de nube del mismo banco); esa comunicación debe hacerse por medio de un dispositivo **on-premise**.
- Son reglas propias del banco que solo conoce el equipo de TI del banco.
- No hay una alerta temprana de parte de ellos; el problema se detecta solo cuando se va a hacer el despliegue: en productivo no se puede ver cierto servicio, o cierto tipo de integración aún no está permitido.
- Considera que un **acompañamiento desde el inicio** del equipo de TI que conoce esas reglas y estándares del banco sería muy útil.

### ¿Cuántas personas intervienen en el arranque y qué pasa con el resto del equipo mientras tanto?

*(Aclaración: el líder técnico pregunta si se refiere al arranque completo del proyecto —que normalmente parte desde análisis— o al arranque del desarrollo; el entrevistador confirma que se refiere específicamente al arranque del desarrollo.)*

- Normalmente hay **un técnico encargado de liderar el desarrollo inicial**.
- El resto del equipo, mientras tanto, se encarga de otros proyectos.
- Casi nunca el arranque de un proyecto está dirigido por 2 o 3 desarrolladores; siempre es **uno solo**, que va integrando al resto del equipo a medida que lo requiere.
- Cuando el proyecto es robusto/grande (por ejemplo, un backend robusto que no puede soportar una sola persona), sí se integran dos personas.
- El resto del equipo se va sumando al proyecto en pasos posteriores: apoyo en análisis, apoyo en integraciones, apoyo en pruebas/QA (mencionado en la grabación como "apoyo de sonocho", posible imprecisión de la transcripción automática).

### Pregunta adicional del entrevistador: ¿el arranque técnico ha afectado la planeación o las fechas del proyecto?

*(Pregunta no incluida en el guion original, formulada por el entrevistador sobre si el arranque técnico ha afectado el modo de iniciar el proyecto o el cumplimiento de fechas prometidas.)*

- el líder técnico se remonta a un paso anterior: lo que más ha generado reprocesos y cambios de fechas ocurre en el paso previo al arranque del desarrollo, en el **análisis**.
- Considera que a veces el análisis no es lo suficientemente profundo, lo que lleva a pensar soluciones a un nivel poco estándar o poco alto nivel.
- Esto luego se ve afectado por temas de **permisos y autorizaciones** una vez se sale a productivo.
- Empiezan inconvenientes porque la solución planteada no era la adecuada.
- Concluye que el problema está más en el **previo (el análisis)** que en el inicio del desarrollo como tal.

---

## Criterio de estandarización

### ¿Qué del arranque de proyectos y de la reutilización de funcionalidades consideras que debería estandarizarse?

1. **Herramientas de desarrollo** y sus diferentes componentes y extensiones: todo el equipo debería moverse dentro del mismo framework y las mismas herramientas (en la grabación se menciona algo transcrito como "Blue Jean", posible imprecisión de la transcripción automática sobre el nombre de una herramienta o IDE).
   - No debería pasar que cada desarrollador use, por gusto, un formateador distinto.
   - Con el tema de IA, todo el equipo debería usar los mismos "harnets" (agentes/herramientas de IA) que se armen en equipo, y los mismos *skills*.
   - El objetivo: que el código generado por un desarrollador sea igual al de otro, lo que permite que las validaciones cruzadas sean más efectivas.
2. **Infraestructura:** debería existir una infraestructura base con configuraciones base.
   - Ejemplo: cada desarrollador debería poder crear un servidor de base de datos con las configuraciones de red, permisos y estándares que cualquier otro desarrollador también use — no que cada uno lo cree como mejor le parezca, sino con un estándar.
3. **Documentación:** la forma en que se documenta también debería estar estandarizada.

### ¿Qué riesgos ves en estandarizar?

- El mayor riesgo es perder ese "toque de inquietud" o de "cacharreo": la apertura de pensar cómo se pueden hacer las cosas diferente, o qué hay de nuevo en el mercado para hacerlo mejor.
- Una vez existe un estándar, el desarrollador simplemente se acoge a él.
- Se pierde un poco la visión a futuro de las cosas nuevas que van llegando.

### ¿Qué haría que un esfuerzo de estandarización perdurara en lugar de quedar desactualizado?

- Propone destinar un **espacio de 2 horas cada mes** para que el equipo revise el estándar y evalúe cómo las nuevas tecnologías pueden ayudar a que ese estándar evolucione.
- El estándar debería ser un **"estándar vivo"**: algo que se analice y actualice periódicamente.

### Si existiera un catálogo compartido de plantillas y módulos, ¿quién debería mantenerlo y bajo qué reglas debería incorporarse o cambiarse algo?

- El encargado del estándar debería ser el **líder técnico**, pero no en el sentido de que él sea quien lo arme y dicte las directrices unilateralmente.
- El líder técnico debería ser el encargado de **reunir al equipo** para que, entre todos, se hagan las modificaciones correspondientes — es un tema colaborativo.
- Sin embargo, señala que cuando una tarea queda en manos de más de una persona, casi nunca se termina haciendo; por eso siempre debe haber **un responsable** definido.
- Esto no significa que la responsabilidad de mantenerlo actualizado sea únicamente de esa persona, sino que su función es **convocar al equipo** para analizar qué se modifica y cuál es el nuevo estándar.

### Desde tu rol, ¿qué esperarías de una herramienta que apoye estos dos flujos?

- Lo primero que debe ofrecer la herramienta es una **ganancia real en tiempo**: debería permitir un despliegue más efectivo que si no se usara.
- Menciona que ha habido experiencias previas donde se intentó implementar una herramienta o metodología que terminó empeorando o entorpeciendo la funcionalidad en lugar de ayudar.
- La herramienta debe dar valor agregado en **agilidad**, específicamente agilidad en el despliegue.
- Debería llegar a ser tan **parametrizable** (entendiendo que esto sería en evolutivos posteriores) que pueda abarcar la mayoría de escenarios posibles: aplicación móvil, aplicación corporativa, aplicación con restricciones específicas, etc.
- Debe tener **flexibilidad**, sin ser tan rígida: es una herramienta para estandarizar, pero no debería limitarse a imponer un único estándar cerrado.
- Su uso e implementación deben ser **sencillos e intuitivos**, de forma que la llegada de nuevos desarrolladores o personal nuevo sea fácil, sin una curva de aprendizaje elevada.

---

## Respuestas preguntas cerradas

- Dificultad percibida del arranque de un proyecto hoy. 3
- Tiempo aproximado de un arranque hasta que el proyecto corre. 15 días
- Frecuencia con que se reutiliza código por copia entre proyectos. 3
- Costo percibido de propagar un cambio de una funcionalidad compartida. 4
- Grado de divergencia que percibes entre los proyectos del equipo. 2
- Utilidad esperada de una herramienta que automatice arranque e integración. 5
- Importancia de un rol que mantenga el catálogo para que perdure. 5