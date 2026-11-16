# Entrevista: Asesoría Desarrollador Interno

**Entrevistador:** Jorge Andrés Facundo Solarte
**Entrevistado:** el desarrollador interno
**Fecha:** 5 de agosto de 2026
**Duración:** 29 min 53 s

---

## Pregunta del entrevistado sobre el alcance de la herramienta

**El desarrollador interno pregunta:** ¿Este sistema tiene como alcance también creaciones en bases de datos, es decir, crear tablas, o simplemente crear los servicios?

**Respuesta del entrevistador:** La conexión a base de datos también sería un sistema compartido, uno de los módulos que se quisiera estandarizar. Sí se adoptaría, ya que la base de datos es un contrato que se tiende a repetir en todos los procesos. Sería la configuración más la creación de la base de datos (aunque no necesariamente se tenga en cuenta todo, sí la configuración y conexión).

---

## Parte A – Preguntas abiertas

### ¿En qué proyectos trabajas actualmente y desde hace cuánto?

- Actualmente trabaja en un producto digital de captación del banco.
- También en un nuevo proyecto llamado **Perfilamiento**.
- Lleva **8 meses** en la organización.
- Ha trabajado en diferentes proyectos, pero estos dos son los que tiene activos actualmente.

### ¿Cómo describirías tu participación típica en el ciclo de vida de un producto?

- Su perfil es **full stack**.
- Ha participado tanto en proyectos ya empezados (como el producto de captación, desde el front y el backend) como en proyectos creados **totalmente desde cero** (backend completo, arquitectura y desarrollo del front).
- **Ese producto:** lleva alrededor de **tres años** en el banco; en este caso él entró a acoplarse a un desarrollo existente.
- **Perfilamiento:** el desarrollo fue **netamente desde cero**.

---

## Flujo de arranque

### Paso a paso del último arranque de proyecto (desde que se decide crear el servicio hasta que corre sin error)

1. **Fase de ideación / planeación de la lógica del proyecto:** es netamente funcional. Le gusta trabajar los flujos en papel/cuaderno.
2. **Incertidumbre inicial ("abismo"):** al iniciar un proyecto desde cero no se sabe con qué archivo empezar; se sabe qué se quiere lograr, pero no cómo iniciar.
3. **Uso de IA para las primeras líneas de código:** le ha ayudado bastante para romper esa incertidumbre y tener algo con qué empezar y adaptar.
4. **Inicialización del proyecto:** proceso demorado — toca inicializar el proyecto, desplegarlo en **Azure**, hacer todos los procesos de **CI/CD**.
5. Si uno se enfoca en esa tarea, **puede tardar alrededor de una semana o al menos algunos días**.
6. Identifica que estas son **tareas repetitivas**: se repiten en otros proyectos que también se inician desde cero (dentro y fuera de su organización/entidad), y siempre se ven los mismos pasos para iniciar un proyecto.

### ¿Qué parte de ese arranque consume más tiempo y por qué?

- El proceso de arranque en general (mencionado como respuesta breve, ligado a lo anterior: inicialización, despliegue en Azure, CI/CD).

### ¿Qué se configura manualmente cada vez que se arranca un proyecto?

- **Autenticación y autorización** (inicio de sesión): factor común en aproximadamente el **90% de los proyectos**.
  - Primero: loguearse en un servicio.
  - Segundo: todo el tema de **roles**.
  - Aunque es común a muchos proyectos, en todos es necesario volver a desarrollarlo.
  - Es una de las cosas que más ha visto a lo largo de los proyectos en los que ha trabajado, porque en la mayoría lo ha necesitado.

### ¿Qué suele descubrirse tarde, ya avanzado el proyecto, que hubiera convenido resolver al inicio?

- **Monitoreo / observabilidad del proyecto:** muchas veces, ya en producción, empiezan a presentar errores para los cuales no se tiene visibilidad. Se sabe que el usuario tuvo un error en cierto punto, pero no se sabe por qué, o es complejo encontrar la causa.
- Esto ha llevado a implementar, por ejemplo, una **tabla de logs** con creación automática: registrar en qué punto se cayó el usuario y por qué (falló un servicio, se envió mal la información, etc.), haciendo el error más granular.
- Esto **siempre ha causado retrabajo**, porque inicialmente no se contempló el monitoreo o registro de esos posibles errores.
- Siempre se piensa en el **"happy path"** y a veces el desarrollo de esas medidas preventivas se pasa por alto.

### ¿Cuántas personas intervienen en el arranque y qué pasa con el resto del equipo mientras tanto?

*(Aclaración: el desarrollador interno pregunta si se refiere a la fase de ideación o a la parte técnica; el entrevistador confirma que se refiere a la parte técnica, una vez finalizada la ideación, cuando empieza a "tirar código".)*

- El proceso de arranque queda normalmente **centralizado en DevOps**.
- Ejemplo: el compañero de **Frontend**, en la primera fase, no puede hacer mucho, ya que se depende de que el servicio/aplicación/repositorio esté disponible en Azure (en su caso), es decir, de tener algo ya en la nube que permita el trabajo en conjunto.
- Hay **cierto tiempo muerto** para una parte del equipo.
- El peso recae en la persona que está desplegando y creando el proyecto.
- Mientras tanto, los demás desarrolladores quedan **bloqueados/esperando** ("esperanzados") a que ese proceso finalice, preguntando cómo va o cuánto falta.
- En el banco, sacar un proyecto es demorado porque debe pasar por **permisos de varias áreas**.
- La **inicialización** abarca: despliegue del repositorio, despliegue del servicio en Azure, creación de bases de datos.
- Este tiempo suele tardar **al menos una semana** bien trabajada, tiempo en el cual el equipo está a la espera.
- Normalmente ese tiempo de espera se usa para **trabajar en otras iniciativas**.

### Pregunta sobre adaptación de BIAN o estándares

*(No se formuló como pregunta independiente en la conversación transcrita; el tema de estándares bancarios — BIAN, ISO 20022, Domain Driven Design, Arquitectura Hexagonal — fue mencionado por el entrevistador en la explicación inicial de la herramienta, no como pregunta al entrevistado.)*

---

## Flujo de integración de módulos

### Cuando un producto en curso necesita una funcionalidad que otro proyecto ya tiene, ¿cómo se incorpora hoy?

- Ejemplo de ese producto: hace consumos a servicios directamente del banco.
- Se planteó tener una **carpeta dentro del mismo proyecto llamada "integraciones"**, que permite hacer esos llamados a los servicios del banco.
- Cuando se necesita ese servicio en otro proyecto: se **copia la carpeta**, se **pega en el nuevo proyecto**, y se empiezan a arreglar **variables de entorno** para que el servicio funcione en el nuevo proyecto (variables de identificación, etc.).
- Se pasa la lógica de un lugar a otro y se cambian las variables de identificación.
- Esto agiliza el proceso para no hacer todo desde cero, pero es efectivamente un **"copy-paste"**.

### ¿Qué tan seguido ocurre eso durante la vida de un producto?

- Es **muy común** en el banco.
- La carpeta de integraciones es el ejemplo más presente: los productos que sacan necesitan hacer consultas a servicios del banco, y esas consultas no son solo llamar un endpoint, sino que tienen un paso a paso para obtener una respuesta.
- Esa carpeta de integraciones se suele migrar en la **mayoría de proyectos**.
- Ha trabajado en aproximadamente **4 proyectos** desde que está en la organización: en los 2 vigentes actualmente y en los otros 2 también se usó la misma carpeta.
- Copiar y pegar la carpeta de integraciones de servicios del banco es algo a lo que está acostumbrado; lo ha hecho en al menos **4 proyectos**.

### ¿Qué pasa cuando una de esas funcionalidades compartidas cambia después de haberse copiado a varios proyectos?

- Es un **dolor identificado**: si cambia en un lado, tiene que cambiar en todos los proyectos donde se implementó.
- Es una **falla identificada pero no abordada**.
- Si un servicio cambia, o una respuesta cambia, o una entrada cambia, el cambio debe hacerse manualmente en cada proyecto donde esté implementada la carpeta (si son 4 proyectos, hay que entrar a los 4 y hacer el cambio).

### Caso concreto en que un cambio obligó a tocar varios proyectos / lo más frágil o costoso de reutilizar código

- Lo más **frágil** que puede cambiar es la **respuesta del servicio**: el sistema ya está esperando una respuesta con cierta estructura; si esa respuesta cambia, se genera un **efecto "bola de nieve"**.
- Hay que ajustar la lógica: qué hacer si se recibe tal cosa, o qué mostrar en caso de que la nueva respuesta sea distinta.
- Se produce un **"efecto mariposa"**: un pequeño cambio desencadena una serie de acciones/ajustes, dependiendo de la aplicación.

---

## Criterio de estandarización

### ¿Qué del arranque y de la reutilización tendría sentido estandarizar?

Tres temas identificados como factor común en los proyectos:

1. **Login / autenticación y autorización:** para él ya es "de receta" — el *core* de esa lógica casi siempre es el mismo, aunque pueda haber variaciones agregadas.
2. **Tabla de procesos / de "request":** sirve como tabla núcleo que lleva el proceso de un determinado usuario; con un ID de identificación se puede saber todo el trazo/flujo que un usuario está siguiendo. Aplica para proyectos donde el usuario realiza un flujo para adquirir un producto (X o Y), algo común en varios proyectos del banco.
3. **Notificaciones / comunicación con el usuario:** dar retroalimentación al usuario sobre lo que ha hecho (esto salió bien, esto salió mal), incluyendo casos como "algo salió mal, puedes continuar desde acá" cuando el usuario se cae en medio de un flujo. Lo estandarizable sería al menos la **forma de comunicarse** (no necesariamente el canal — WhatsApp, SMS o correo — sino que sea estándar el mecanismo de comunicación).

### ¿Qué no debería estandarizarse, o qué se perdería si se hiciera?

*(No se obtuvo una respuesta explícita y directa a esta pregunta en la transcripción; el desarrollador interno se enfocó en responder qué sí tendría sentido estandarizar, ver punto anterior.)*

### ¿Qué esperarías de una herramienta que apoyara estos dos flujos?

- Recordando que el proceso de inicialización puede tardar alrededor de una semana, esperaría una herramienta que **simplifique ese tiempo a solo algunos minutos**.
- Algo que se pueda hacer de forma **ágil**; considera que esta solución tendría un **impacto grandísimo** en el desarrollo de los proyectos.
- Que sea **altamente escalable**: que no sea algo cerrado (ej. "me hizo un módulo de autenticación, pero tengo que someterme al funcionamiento que ellos dieron").
- Como programador, le gustaría tener **acceso y poder modificar** las cosas que quiera modificar.
- Que sea una herramienta que ayude a **romper ese abismo inicial** (cuando no se ve ningún archivo de código en un proyecto nuevo), pero que aun así permita el desarrollo normal: poder agregar o quitar líneas, que sea **totalmente configurable**.
- Que su objetivo sea **reducir en gran medida el tiempo inicial** de despliegue/creación de un proyecto.
- Que sea **fácil de usar**: no que haya que estar configurando un archivo durante 4 horas, ni tener que leer mucha documentación.
- Que sea **amigable**, similar a la idea de "hundir un botón y que eso cree todo" (aunque reconoce que en la práctica se necesita algo de contexto, no es tan simple).
- **Entre más ágil y menos cosas pida, mejor.**

---

## Respuestas preguntas cerradas

- Dificultad percibida del arranque de un proyecto hoy. 5
- Tiempo aproximado de un arranque hasta que el proyecto corre. 8 días
- Frecuencia con que se reutiliza código por copia entre proyectos. 4
- Costo percibido de propagar un cambio de una funcionalidad compartida. 5
- Grado de divergencia que percibes entre los proyectos del equipo. 3
- Utilidad esperada de una herramienta que automatice arranque e integración. 5