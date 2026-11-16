# Entrevista: Asesoría Desarrollador Externo

**Entrevistador:** Jorge Andrés Facundo Solarte
**Entrevistado:** el desarrollador externo
**Fecha:** 16 de agosto de 2026
**Duración:** 50 min 15 s

**Enfoque planteado al inicio por el entrevistador:** una serie de preguntas abiertas sobre tres frentes — el arranque, la reutilización de funcionalidades, y el criterio/experiencia desde su punto de vista.

---

## Parte A – Preguntas abiertas

### Arranque

#### En tu experiencia, ¿cómo suele iniciarse un proyecto backend nuevo en los equipos donde has trabajado?

**Origen del proyecto:**
- Antes del desarrollo, lo primero que llega es **la idea de negocio**, proveniente del *owner*, del *product manager* o del *project manager*.
- A partir de esa idea vienen las etapas siguientes. Aclara que existen dos escenarios posibles, y se enfoca en el de algo **completamente nuevo** (que entiende es la intención de la pregunta).

**Etapa de diseño:**
- En ese escenario se busca entender o proponer la mejor manera de hacerlo, sin caer en el error de **subvalorar el tiempo de implementación**.
- Explica la tensión propia del rol: siempre toca buscar **cómo implementar rápido, pero también cómo hacerlo escalable y robusto**.
- En ese proceso inicial de plantear un diseño, es muy común tratar de **identificar si algo que ya se tiene existente o "a la mano"** puede dar valor. Esto se entiende como: si en algún proyecto del pasado ya se usó algún tipo de enfoque, metodología o incluso tecnología que pudiera dar un valor agregado o simplemente **acelerar la implementación**, para no tener que volver a hacer algo que ya se experimentó antes.
- **Ejemplo concreto:** si anteriormente ya se montaron conexiones HTTP con **Axios**, no tener que en la siguiente ocasión querer usar una librería nueva — a menos que se vuelva necesario evaluar las diferentes opciones.
- Considera que en esas etapas de diseño es bien importante revisar **cómo lo ha hecho la empresa antes**, o revisar incluso cómo uno mismo lo ha hecho en otros proyectos, para usarlo como **guía base**.

**El costo que persiste:**
- Aun así, suele **tomar tiempo configurar toda la estructura desde cero**.
- A pesar de haberlo hecho antes, **rara vez** queda algo listo "*out of the box*" (usa la expresión en inglés), es decir, que la herramienta venga lista para usarse de una — porque **todos los proyectos tienen algo diferente**. Entonces casi siempre toca volver a configurar desde cero.
- **Antecedente de solución en empresa anterior:** recuerda que en la empresa donde estuvo antes, en algún momento estuvieron tratando de abordar el tema. Como era muy común el conectarse a un grupo de servicios internos de la compañía, para abordar ese tema **crearon una librería**. Al ser una librería, el manejo se vuelve un poco más fácil.
- Sin embargo, señala que **muchas veces en los proyectos uno no tiene librerías ni módulos comunes**; o si los tiene, **no tiene algo que cubra todo el proceso**.
- **Conclusión general:** normalmente, cuando en las empresas donde ha estado se trata de iniciar algo nuevo, siempre se trata de **basarse en cosas que ya existen** — cosas que ya usaban otros proyectos o que ya se han usado antes en la empresa. Esto ayuda sobre todo porque **la gente ya tiene experiencia**, entonces la curva de aprendizaje de utilizar la herramienta es un poquito menor. Pero aún así, **siempre hay un espacio de tener que configurar las cosas "desde a pie"**.

---

#### ¿Ese proceso de configuración suele hacerse copiando y pegando la estructura base de proyectos similares?

*(Pregunta de seguimiento del entrevistador.)*

El desarrollador externo responde con **dos ejemplos concretos** de sus dos últimas empresas:

**Ejemplo 1 — Empresa anterior (NestJS y su CLI):**
- Usaban **NestJS** para backend (aclara explícitamente: no confundirlo con Next.js, que es de frontend).
- Lo que tenía "chévere" esta herramienta era que **reducía un poquito el tiempo**. Aclara que no era lo más significativo del mundo, pero puntualiza que **en ese punto en el que uno está tratando de avanzar, cualquier tiempo que se logre reducir es relevante**.
- Lo que tenía la herramienta era un **CLI**: uno podía indicarle "quiero agregar al proyecto un módulo X", por ejemplo un módulo de usuarios.
- Como NestJS funciona reforzando lo que es prácticamente una **estructura de inyección de dependencias** (como también lo hace Angular en el frontend), lo que eso permitía era que el CLI **creaba la estructura base**: al agregar el módulo de usuarios, creaba la carpeta `usuarios`, el archivo `usuarios.controller` y el archivo `usuarios.service`.
- Además, **conectaba de una ese módulo de usuarios**, aunque obviamente lo hacía con **funciones dummy o funciones base**, simplemente para empezar, en pro de adelantar el trabajo de crear la estructura de directorios.
- Luego, ya con la estructura de directorios creada, sí tocaba entrar a **meter la lógica de negocio** en el servicio o el controlador.
- Destaca un beneficio adicional: como ya lo hacía una herramienta por uno, **esto refuerza también la estandarización de las cosas** — al tener la herramienta configurada para que siempre cree la misma estructura de directorios, se reduce ese esfuerzo de tener que copiar y pegar la carpeta uno mismo.
- Balance: reduce el tiempo, pero **queda pendiente darle forma al módulo manualmente**, es decir, ponerle la lógica real.

**Ejemplo 2 — Empresa actual (monorepo):**
- En la empresa donde está ahora también hay otras maneras que reducen algo el tiempo, pero **sigue quedando "un asterisco pendiente"**.
- Lo que sucede ahora es que trabajan con un **monorepo**: todo el código backend de la empresa está ahí.
- El hecho de que todo el código backend esté ahí hace que, cuando se implementan **helpers, módulos comunes o módulos compartidos**, estos **en verdad sirvan para cualquier proyecto nuevo de la compañía**.
- En esta estructura de monorepo se facilita un poco más iniciar algo porque **no hay tanta duplicación de código** como habría si tocara crear las mismas funciones para diferentes repos o diferentes proyectos. Las cosas que se sabe que son reutilizables están en el módulo o carpeta **"compartido" (commons)**.
- Con eso, al iniciar un nuevo proyecto, puede **importar ciertas funciones, dependencias o funcionalidades** que pueden ser valiosas.
- **Diferencia clave frente al primer ejemplo:** en la empresa actual **no se tiene un CLI** que permita configurar algo base. Entonces aquí lo que toca no es tanto copiar y pegar el folder, sino:
  - Si uno es muy experto, va creando las carpetas y los archivos manualmente ("a pata").
  - Si no —que es su caso, ya que no lleva tanto tiempo en la empresa— normalmente le toca **abrir la vista dividida**: en una mitad de la pantalla tener como ejemplo la estructura de otro proyecto, y en el otro lado ir creando su estructura nueva siguiendo ese ejemplo.
- **Algo que sí ayuda mucho:** en la empresa actual usan **DDD**. A pesar de que no exista la herramienta CLI que ayude a crearlo y a reducir ese tiempo (como en la empresa anterior), **como sí se sigue un estándar y hay una estructura definida**, es relativamente sencillo identificar cómo hay que plantear el proyecto.
- Aun así, insiste: **si tuvieran una herramienta como la de la empresa anterior**, de simplemente decirle "venga, créeme este módulo", sería mejor, porque "cualquier minuto cuenta".

**Reflexión adicional sobre la invisibilidad del trabajo de configuración en backend:**
- Señala que uno en el rol de desarrollador, **en especial en backend, no es tan visible ni tan tangible como en el frontend**.
- A veces es **difícil justificar el tiempo** que se toma uno en hacer algo, porque no es tan fácil de entender desde un rol de negocio por qué te estás demorando. Tampoco es fácil mostrarlo, como sí sería en un front, donde uno va creando la pantalla y va dando tranquilidad.
- Cree que **especialmente en roles de backend cada minuto cuenta, sobre todo cuando son minutos de configuración**.
- Explica por qué: **la configuración es invisible** — y le pasó en un proyecto este año. A los roles de negocio no les importa lo que uno tenga que configurar para que la aplicación corra, sino que **les importa que la aplicación corra**.
- Conclusión: si se logra reducir la mayor cantidad de minutos de configuración, cuando ya se empieza con la aplicación real (desarrollo real, no configuraciones), **va a ser mejor para todos** — no solo para uno como desarrollador, sino también para los líderes de proyecto y de producto.

---

#### ¿Cuánto tiempo suele tomar dejar un proyecto listo para escribir lógica de negocio, y qué lo consume?

- Aclara que obviamente **depende de la complejidad** de lo que se tenga que hacer, "porque hay de cosas a cosas".
- Aun así, ha visto que cuando son cosas nuevas —**incluso en la empresa actual**, que ya tiene módulos compartidos en el **kernel**— el tiempo es considerable.
- Explica qué es el kernel en su contexto: es también una estructuración para poder **tener centralizados los tipos de datos y las dependencias clave del proyecto**.
- A pesar de que esos módulos ya se tienen en la compañía donde está ahora, **como es algo nuevo**, no solo se trata de configurarlo, sino que **uno tiene que probar y ver que de verdad la configuración que viene hecha funcione y que todo fluya**.
- Añade que **hay veces que, como algo es nuevo, no se tiene tan claro cómo ir organizándolo**.
- **Estimación:** esa configuración inicial puede tardarle a uno **incluso 15 días**.

---

#### ¿Has visto formas de reducir ese costo de arranque? ¿Cuáles funcionaron y cuáles no?

**Estrategia 1 — Librerías (empresa anterior):**
- El hecho de que hubiese una librería ya implicaba que para él **solo es importar el módulo y utilizarlo**, pasándole las configuraciones.
- Siente que una de las estrategias que ayuda a reducir el tiempo es **tener librerías**, en el caso de que uno tenga varios repositorios.

**Estrategia 2 — Módulo commons en monorepo (empresa actual):**
- En el caso de la empresa actual, como es un monorepo, **tener ese módulo de commons haría las veces de la librería**.

**Estrategia transversal — tener una manera de compartir código:**
- Una estrategia que usan las diferentes empresas es **tener la manera de compartir código**.
- Aclara la distinción importante: **compartir código no es copiar y pegar, sino utilizar algo ya hecho** — eso es lo que realmente ayuda.

**Extensión a infraestructura (empresa actual):**
- Si bien en la empresa anterior había una librería, la empresa actual **lo lleva a un siguiente nivel**, no solo por lo del monorepo y lo de commons, sino porque **eso mismo se logra también en la infraestructura**.
- En la empresa actual tienen **infraestructura como código**, y allá también se maneja el monorepo.
- Entonces hay muchas cosas que diferentes equipos van mejorando o construyendo, que al final pueden quedar como **especificaciones comunes** que después uno puede utilizar para crear su propia infraestructura.
- **Diferencia clave:** con la librería, al final solo se lograba avanzar el **tiempo de desarrollo**, pero quedaba todavía el **tiempo de construir la infraestructura**. En la empresa actual **se atacan ambos**: tiempo de desarrollo y tiempo de construir infra.

**Estrategia 3 — CLI que levanta estructura base (empresa anterior):**
- Otra estrategia que ayudaba era que **el CLI levantara una estructura base**.
- A pesar de que esa estructura no tuviera nada funcional, **ya le organizaba a uno las ideas**, y al final uno simplemente tiene que llegar a agregar lo que requiere.

**Reflexión propia: combinar estrategias (idea no implementada todavía):**
- Aclara que está reflexionando en el momento sobre sus anteriores experiencias, y menciona que no sabe si es algo que le vaya a preguntar más adelante.
- Si tuviera que pensar en una manera de **reducir aún mucho más el tiempo**, sería **combinar estas cosas**:
  - Que hubiera un **CLI que estructure el proyecto**.
  - Y que hubiera **módulos comunes o librerías** que permitan compartir o usar funcionalidades que ya existían desde antes.
- **Ventaja clave de esa combinación:** poder usar esas funcionalidades **sin tener que preocuparse por saber si están buenas o no**, porque ya se sabe que están configuradas, que se han usado en otro lado y que están funcionando.
- **Contraste con copiar y pegar:** cuando uno copia y pega, puede que copie algo que está funcionando en otro lado, pero **uno no sabe si en el lugar donde lo pegó le vaya a funcionar**. En cambio, cuando ya está garantizado, es mejor.

**El rol de los estándares:**
- Cree que algo que ayudaría mucho —y lo ha notado en la empresa actual— es **tener estándares**.
- En la empresa actual usan DDD, tienen **módulos comunes** e **implementación de kernel**. Tienen varias cosas que permiten que **cuando uno tenga que iniciar, no inicie de cero, sino que inicie ya con algo adelantado**.

**Propuesta concreta de herramienta:**
- Si uno pudiera tener una herramienta que **le creara la estructura al proyecto, pero además le dejara ya configurados algunos módulos** que uno sabe que siempre van a estar o que pueden ser útiles — menciona como ejemplos la **observabilidad** y la **autenticación y autorización**.
- De modo que al final uno solo tenga que **"tunearlo"**, hacerle un *fine tuning*, más que necesariamente construirlo o validarlo desde cero.

**Qué se necesita para lograr esa herramienta:**
- Cree que lo que más ayudaría es **definir estándares o definir estructuras que se tengan que cumplir**.
- Así es como lo hace la herramienta que mencionó de la empresa anterior: como ellos usan una estructura basada en **controladores y servicios**, siempre que crean un nuevo módulo lo crean en la estructura definida. Y como manejan inyección de dependencias, tienen construido su CLI para crear esa estructura y que funcione.

**Sobre el vendor locking:**
- Señala que a veces uno sí tiene que aceptar, cuando usa estas herramientas, **un poquito de "vendor locking"**, porque le toca ajustarse a la estructura que ellos dicen.
- Pero matiza: **en la medida en que esa estructura siga buenas prácticas, no debería ser un problema**. Y segundo, si sigue buenas prácticas y además te ahorra tiempo, entonces está bien.

**Comparación: herramienta vs. hacerlo manualmente (propensión a errores):**
- En la empresa actual usan DDD, pero el hecho de **no tener una herramienta con cositas automáticas** hace que sea **más propenso a errores** que incluso cuando en la empresa anterior usaban NestJS, porque NestJS ya creaba la estructura y permitía agregar el módulo o los n módulos que uno quisiera.
- En la empresa actual, a él le toca **basarse en lo que ya ha hecho otra gente** y empezar a crear la estructura.
- **Si tuviera un CLI** al que pudiera decirle "estoy usando DDD, agrégueme este módulo en esta ruta" o "agrégueme este módulo en este subproyecto del monorepo", con que se lo cree ya es mejor y **es menos propenso a errores que un humano**.
- **Beneficio adicional para onboarding:** en el caso de una persona nueva que no haya trabajado con DDD, **se ahorra el tiempo o la curva de aprendizaje** de tener que entender cómo se estructura el proyecto y cómo agregar un módulo.

---

### Reutilización de funcionalidades

#### ¿Has trabajado con librerías internas, plantillas o generadores para esto? ¿Qué tal resultó? ¿Has visto otros tipos de herramientas o generadores que se estén utilizando hoy en día?

**Uso de IA:**
- Menciona que últimamente en su empresa ha estado usando IA (referida en la transcripción como "cloud", presumiblemente **Claude**) para ayudarle a que le rinda la creación de la estructura base.
- Yendo por ese lado de la IA, cree que **sería bueno que a nivel de empresa uno tuviera un *skill* compartido de crear proyectos**, que sería **el equivalente a tener el CLI**.

**Experiencia concreta con IA (no del todo satisfactoria):**
- Cuenta una experiencia reciente en la que justo tuvo que **crear un proyecto desde cero**.
- Como tenía que crearlo desde cero y **todavía no tenía tan claro cuál era la estructura que tenía que seguir**, necesitaba que le rindiera el tiempo — reforzando lo conversado de que **al final configurar no aporta nada al negocio; lo que aporta es desarrollar las funcionalidades**.
- Como no tenía tanta experiencia en ese momento en cómo estructurar el proyecto en DDD, aprovechó la IA (Claude) y le pidió que **analizara la estructura del proyecto y le ayudara a agregar un nuevo módulo / una nueva funcionalidad**.
- **Resultado:** la experiencia **no fue tan satisfactoria**. Lo que sucedió fue que la IA sí creó algo que **aparentemente seguía la estructura**.
- Pero cuando **pasó el pull request a revisión** con sus pares y su jefe, ellos **dieron bastantes oportunidades de mejora** justamente de cara a esa estructuración: dónde debería ir este nombre de archivo, dónde debería ir esta clase, es decir, **esa organización**.
- A pesar de que la IA trató de hacerlo, **también cometió errores**.

**Propuesta de skills a nivel empresa:**
- Considera que la IA puede ser **un facilitador** en esos procesos, pero cree que **a nivel de empresa sería bueno tener un *skill* o un grupo de *skills***.
- Además, menciona el archivo que define las cosas básicas del repositorio — el **archivo `CLAUDE.md`**.
- Propone que uno debería tener ese archivo `CLAUDE.md` y, ojalá, unos *skills* de cómo crear módulos nuevos — **por equipo, por proyecto, o idealmente para toda la empresa**.
- **Razón:** porque igual **la IA está sujeta a cometer errores o problemas de interpretación**.
- Aclara que dice esto **incluso sabiendo que él trató de utilizar SDD**, pero aun así **sigue habiendo un pequeño gap de implementación** cuando se usa IA.

**Comparación IA vs. NestJS (determinismo):**
- En ese sentido, siente que incluso **le funcionó un poquito mejor NestJS**.
- **Razón: porque es más determinístico** — siempre le va a crear una estructura fija.
- En cambio, **la IA, como trata de interpretar cosas, puede hacerlo de una manera hoy, y si mañana le vuelve a pedir otro módulo, lo hace de otra manera**.

**Propuesta de combinar ambos enfoques:**
- Él combinaría los dos: **algo que le cree la estructura base**, y que esa estructura **sí o sí siempre siga lo mismo, no importa si corre el comando 20 veces**.
- Y que **sobre esa estructura base**, para terminar de acelerar el proceso de configuración, **la IA sea capaz de empezar a crear la lógica de negocio** — que es justamente lo que **no hace NestJS**: NestJS crea la estructura base, pero en cuanto a lógica de negocio **le toca 100% a uno**.
- Como hoy la IA, con *skills* o dedicándole suficiente tiempo, permite implementar algo decente, uno podría pensar en **combinar ambas cosas: que el CLI cree la estructura del proyecto y que la IA sea la que la llene**.

**Balance final sobre la IA:**
- La única otra estrategia diferente a las ya mencionadas que recuerda en ese momento es **la IA**.
- Pero su experiencia es que, **a menos que uno tenga un *skill* bien refinado o bien fuerte —o un grupo de *skills* bien refinados y bien fuertes— la IA todavía puede cometer muchos errores**.
- **Incluso con los *skills***, le ha pasado que ha creado *skills* para acelerar su proyecto en otras cosas, y **hay veces que le funcionan perfecto y otras veces que no tanto**.
- Lo resume como "el problema de la vida": **no siempre uno logra resultados iguales todo el tiempo**.

*(Comentario del entrevistador tras esta respuesta: valdría la pena tener ese estándar que guíe las decisiones, como lo hace la herramienta CLI, que al ser más rígida da la tranquilidad de que las cosas van a salir como se esperan.)*

---

### Criterio

#### ¿Qué de un proyecto backend crees que vale la pena estandarizar y qué no?

**Lo que sí vale la pena estandarizar — la arquitectura detallada:**
- Cree que es importante estandarizar **la arquitectura detallada**, es decir, **cómo uno construye la aplicación**.
- Por ejemplo, que todos usen DDD, o que todos usen **modelo-vista-controlador**, u otro patrón.
- **Alcance clave:** cuando dice "todos", se refiere **no solo a su proyecto o al nuevo proyecto que esté levantando, sino ojalá lograr un estándar a nivel de toda la empresa**.

**Por qué es importante:**
- Si toda la empresa **habla el mismo idioma de desarrollo**, es más fácil que, si en algún momento un equipo de la empresa está requiriendo **manos extras** y otra persona de otro equipo tiene que ir a ayudarlo, **esto reduzca la curva de aprendizaje**.
- En teoría, lo que se hace en una línea de producto y lo que se hace en otra estarían **estructurados relativamente parecidos o iguales**, solo que cada uno con su negocio diferente.
- Entonces, si a uno lo cambian de equipo, o si por algún motivo necesitan manos extras de otro equipo, **van a poder aprovecharlas más rápido** porque la estructuración del proyecto es común o sigue las mismas reglas.
- Concluye que vale la pena lograrlo **a nivel empresa, ni siquiera a nivel proyecto**: utilizar la misma arquitectura.

**Problema concreto que ve hoy: DDD es abstracto y no se refuerza:**
- En la empresa actual, al ser un monorepo, él está en una línea de producto y puede ver, por ejemplo, el código de las otras dos.
- Pero a pesar de que todos están utilizando **DDD**, pasa que **DDD es medio abstracto**: habla de muchos conceptos, pero **más allá de los conceptos, no habla de cómo implementarlos realmente**.
- ¿Qué pasa entonces en la empresa? Que **todos están usando DDD y todos están usando arquitectura basada en eventos**, pero puede pasar que **en una línea lo estén utilizando de forma diferente a como lo usan en las otras**.
- A pesar del esfuerzo de que todos utilicen la misma arquitectura, **no hay algo que lo estandarice o que lo refuerce** de modo tal que en serio todos lo implementen de la misma manera.
- **Consecuencia:** volviendo a su ejemplo, si él tuviera que ir a meter la mano en otra de esas líneas, **igual no le sería tan fácil**, a pesar de que supuestamente están hablando el mismo idioma.
- **Analogía que usa:** porque ellos usan sus propias palabras — "es como ir a hablar español de Argentina": uno los entiende porque al final es el mismo idioma, **pero ellos tienen sus propias expresiones y su propia forma de hablarlo**.
- Si uno pudiera estandarizarlo, **se ahorraría bastante tiempo**.

**Beneficio adicional en espacios colectivos:**
- Sería útil sobre todo en **comités técnicos o sesiones de arquitectura**: uno trae la propuesta y está mostrando incluso código.
- Como todo el código estaría bajo el mismo estándar, **eso permitiría a todos entender mejor las propuestas y usarlas**.

**Aclaración de alcance:**
- Precisa que cuando habla de arquitectura se refiere a la **arquitectura de aplicación**, no necesariamente a infraestructura (aclara: no a cosas como Lambdas).

**Lo que ve con menos valor — estandarizar el testing:**
- En la empresa actual también estandarizan **a nivel de código de testing**: que los tests tengan que estar escritos en un formato determinado (mencionado en la transcripción como "el King", posiblemente **Gherkin**).
- **Esa parte es algo a lo que le ve un poco menos de valor.**
- Aunque matiza: si uno pudiera hacerlo, y siempre siguiera una misma estructura, **también sería fácil de leer** para cuando tuviera que revisar un test o agregar uno nuevo. Aclara que se refiere a **tests unitarios**. Pero insiste: **esa parte sí es como menos valiosa**.

**Otro punto a reforzar — programación orientada a objetos:**
- Por lo que ha visto, cree que **es un poquito más fácil tener código limpio, o tratar de buscar hacer código limpio, cuando uno usa programación orientada a objetos que cuando usa programación funcional**.
- **Razón:** porque **todos los ejemplos de cómo hacer código bien hecho están usando programación orientada a objetos** — los patrones de diseño, los principios.
- Por eso, eso sería otra cosa a reforzar: **ojalá que el proyecto refuerce que uno tenga que utilizar programación orientada a objetos**.
- Aclara que esto lo dice **desde su punto de vista como programador**.

**Desde un rol de DevOps — herramientas de análisis:**
- Menciona que, desde un rol quizá de **DevOps** o similar, algo que también ayuda en la empresa es la **configuración de Sonar**.
- El valor está en **poder tener una herramienta que también le diga a uno si lo que está implementando está bien o no**.

---

#### Desde tu experiencia, ¿qué debería tener una herramienta que genere proyectos e integre módulos reutilizables para que realmente se use y no se abandone?

**Contexto del mundo bancario:**
- Como él trabaja en el mundo de las **finanzas**, y ha trabajado en bancos, señala que **hay muchas herramientas que uno no puede usar** — funcionan, pero no se pueden usar.
- Cree que **en el mundo bancario es especialmente importante que esas herramientas sean confiables**.

**Lo ya mencionado (recapitulación que él mismo hace):**
- Que permitan **estandarizar cierta estructura**.
- Que, así como cuando uno usa librerías, **tenga módulos ya configurados que funcionen** — todo funcionando.
- Que **reduzca el trabajo**, de modo que después uno simplemente tenga que hacerle *fine tuning*.

**Lo específico del mundo bancario — poder auditar la herramienta "por debajo":**
- Lo que ha visto que es especialmente importante en el mundo bancario es **poder ver esa librería o ese CLI "por debajo"**.
- **Aclaración importante:** no se refiere necesariamente a tener que ir a explorar el repositorio y ver cómo hace cada cosa — **no necesariamente tener que entender cómo lo hace**.
- Sino que es **en pro de darle tranquilidad a los *stakeholders* de tecnología**, a la gente del mundo bancario.
- Se trata de **poder consultar esa herramienta** y ver, por ejemplo, si está **libre de vulnerabilidades**.

**Mecanismos concretos que propone:**
- No necesariamente ver el código de la herramienta, sino **poder correr un pipeline** y que el pipeline diga: "sí, el CLI está libre de vulnerabilidades", o que **el CLI dé alertas** si no lo está.
- Poder revisarlo y que le diga cosas como **si el CLI está construido bien o mal**.
- Reitera: **al final el código de cómo lo hace la herramienta es indiferente**, pero para esos *stakeholders* de tecnología, "a quienes les gusta tanto ver si las cosas en verdad son seguras", esto es clave — sobre todo **porque el mundo bancario está vigilado**.
- Que ellos pudieran **correrle auditorías**: por ejemplo, correrle al CLI una **auditoría de dependencias** y que diga si no tiene ninguna dependencia vulnerable; o correrle **SonarQube** y ver que no salga ningún hallazgo.

**Observabilidad y reportabilidad hacia stakeholders:**
- Que la herramienta le permita a uno **hacerle observabilidad de algún modo**, de cara al equipo de negocio, a los *stakeholders* de tecnología, **o a los de riesgo**.
- Menciona explícitamente a los **stakeholders de riesgo**: por ejemplo, los que se encargan de construir el **plan de DRP / plan de continuidad**.
- Poder decirles: "les entrego este dashboard o esta pantalla" y mostrar, por ejemplo:
  - Que **en los últimos días nunca se ha caído el CLI**.
  - Que **el CLI con el que estamos construyendo los proyectos no inyecta vulnerabilidades**, porque no tiene vulnerabilidades.
  - Que si le corre **un chequeo de seguridad de OWASP**, no sale nada malo.

**Por qué esto importa para la adopción organizacional:**
- Señala que esto sería deseable **sobre todo si uno va a vender la idea por primera vez**, al traerla por primera vez sobre la mesa.
- Poder **vender la idea mostrando toda esta información**: que el CLI no tiene vulnerabilidades, que es *OWASP compliant*, que no tiene ese tipo de problemas.
- **Objetivo: que la gente le dé el visto bueno y se sienta tranquila de usarlo.**
- Aclara la distinción de audiencias: esto es **más allá de los desarrolladores**, porque **los desarrolladores simplemente le pueden ver el valor a algo que les brinde más tiempo y ya está**.
- Pero **si uno quiere que la iniciativa la adopte una organización**, sí toca hacer estos esfuerzos adicionales de decirles "mire que la librería que estoy proponiendo sí va a ser segura".

---

#### ¿Qué podría implementar o tener en cuenta la herramienta para que su curva de aprendizaje y su adopción sean permanentes, y no una herramienta que solo se use un tiempo y luego se deje de lado?

**Sobre la adopción — dos factores:**

1. **Generar confianza sobre la herramienta, no solo en los equipos sino en los líderes:**
   - Retoma lo que respondió antes: en la medida en que se logre generar confianza sobre la herramienta **no solo en los equipos, sino en los líderes**, se va a lograr que **la adopción sea mucho más duradera**.
   - Es decir, si la adopción surge como **una decisión de negocio o una decisión de arquitectura bien documentada**, se logrará que sea mucho más duradera.

2. **Que la herramienta sea fácil de utilizar para el desarrollador:**
   - Que en verdad sea **un comando, o pocos comandos, y ya está**.
   - **Contraejemplo:** si uno tiene que entender 10 o 12 comandos —y no solo entenderlos, sino también tener que ejecutar demasiados comandos para poder configurar un proyecto— **va a ser difícil la adopción del desarrollador**.
   - Porque el desarrollador va a decir: "tengo que hacer estos 10 pasos y ni siquiera me los he aprendido de memoria; más bien lo hago a pata, o miro qué otra opción hay".
   - Por eso **tiene que ser sencillo de usar para que pueda ser adoptable**.
   - Resume las dos condiciones para la adopción: **que los jefes lo vieran bien y que para el desarrollador fuera fácil de usar**.

**Sobre la permanencia — capacidad de evolución:**
- Aclara que **la adopción no es lo único que importa; importa la permanencia de la herramienta**, que se sostenga en el tiempo.
- Para eso es importante **permitirle evolución a la herramienta**.
- **Razón:** las arquitecturas de una empresa **evolucionan, no siempre se quedan igual**.
- **Ejemplo personal:** en la empresa donde estuvo anteriormente, cuando recién ingresó **todo era on-premise**; cuando abandonó la empresa, ya muchas cosas se estaban montando en **Lambdas, en AWS, en Azure**. Las arquitecturas y las soluciones van evolucionando.
- Si uno quiere que la herramienta no solo tenga adopción, sino que **permanezca en el tiempo, hay que darle la capacidad de evolucionar también**.
- Esto implica poder **incluir nuevos módulos o incluir nuevas arquitecturas** conforme se vaya viendo necesario — por ejemplo, si ya no se quiere utilizar arquitectura basada en **modelo-vista-controlador**, sino en **puertos y adaptadores**.
- Poder permitirse **hacer una nueva versión (versión dos)** de la herramienta, o dentro de la misma herramienta **incluir nuevas funcionalidades**, de forma que **así como vaya evolucionando la arquitectura y los equipos, el CLI lo vaya haciendo también**.
- **Riesgo si no se hace:** puede pasar que **evolucione la arquitectura pero no evolucione el CLI**, con lo cual **queda deprecado y ya no lo pueden volver a usar**.

---

## Parte B – Preguntas cerradas

1. **Dificultad típica del arranque de un proyecto backend:** 4
2. **Tiempo típico de arranque hasta escribir lógica de negocio:** 2 semanas
3. **Frecuencia de reutilización:** 4
4. **Costo típico de propagar cambios de funcionalidades compartidas:** 3
