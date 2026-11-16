# Entrevista: Asesoría Rol de Arquitectura

**Entrevistador:** Jorge Andrés Facundo Solarte
**Entrevistado:** la función de arquitectura
**Fecha:** 12 de agosto de 2026
**Archivos de origen:** Grabación principal (23 min 21 s) + continuación breve de la misma sesión (42 s)

---

## Parte A – Preguntas abiertas

### Sobre iniciar proyectos

**Cuando inician nuevos proyectos en diferentes equipos, ¿qué de tu área es lo que más a menudo queda mal resuelto, mal configurado o directamente olvidado?**

- Muchas veces falla el **no tener todo el panorama completo** al hacer un diseño: los equipos se enfocan solamente en la parte específica que están viendo en el momento, sin pensar en qué se podrá reutilizar después.
- Se suele **hardcodear** y dejar cosas muy **acopladas** a algo específico, lo cual después genera problemas al querer reutilizarlo, o toca hacer ajustes forzados ("machetazos") para intentar expandir esas funcionalidades.
- Resume el problema como: al diseñar, "no se piensa en todo el bosque, sino solamente en el arbolito".
- Desde el rol de arquitectura (banco), muchas veces los buscan cuando el proyecto ya está muy adelantado, y para ese momento ya no alcanzan a dar su aporte a tiempo; cuando lo dan, la respuesta suele ser que ya están muy adelantados y que devolverse sería un retroceso.
- Otro problema visto: a veces **empiezan a desarrollar sin un diseño claro**.
- Consecuencia general: al no ver "todo el bosque", cuando luego se necesita interactuar con otras cosas o resolver otros requerimientos, se vuelve muy complicado hacer crecer esa solución o propuesta.
**Si una herramienta lo dejara bien resuelto desde el inicio, ¿qué debería garantizar exactamente?**

- Debería garantizar que la solución no solo aborde el foco puntual, sino también la visión más general: otras integraciones, escalabilidad y mejoras futuras.
- **Caso concreto — proyecto Pagaré:** cuando se inició el proyecto de pagaré, quedó pensado únicamente para los productos de microfinanzas, y era el que iba a buscar la información directamente en la fuente (WD). Al principio no era tan grande, pero cuando se necesitaron otros ajustes (por ejemplo, para tarjeta de crédito), se convirtió en un **cuello de botella**.
  - Ahí intervinieron desde arquitectura: decidieron "apificar" el proceso de pagaré para habilitar que, por ejemplo, un portal de autogestión o una app pudieran ofrecer el flujo de firma de pagaré sin depender únicamente del front-end de microfinanzas ya existente.
  - Al apificarlo, buscaron no dejarlo atado solo a microfinanzas, sino dejarlo más abierto y desacoplado, de forma que se pudiera usar vía API desde cualquier canal (no solo desde la aplicación web/oficina), mientras la plataforma de pagaré sigue administrando el proceso de fondo.
  - Antes de este cambio, si se necesitaba usar el mismo pagaré para otro producto (ej. tarjeta de crédito o cuenta de ahorros), había que desarrollar ajustes específicos y "tocaba ir por todo" para traer la información correspondiente.
  - Concluye: si esto se hubiera pensado desde el inicio, no habrían tenido que hacer todos esos ajustes posteriores para lograr reutilización de la lógica. Aun así, destaca que fue positivo que alcanzaron a intervenir a tiempo, sin dejar que el problema avanzara más.
  - Resume la lección: desde arquitectura, cuando ven que algo "podría servir para tal o cual cosa", conviene dejarlo diseñado de otra forma desde un inicio para que sea más reusable y pueda evolucionar.
---

### Sobre integrar funciones compartidas

**El punto más reutilizado entre proyectos es la integración con servicios y capacidades compartidas (por ejemplo, una pasarela de pagos o un proveedor de validación de identidad). ¿Qué debe cumplir un módulo compartido para incorporarse a muchos proyectos sin volverse un riesgo común a todos ellos?**

- Considera que **todo módulo compartido conlleva un riesgo inherente**: el simple hecho de tener un bus (para integración interna) o un API Gateway (para integración externa) como único punto de integración ya representa un riesgo — si eso falla, falla todo.
- Lo que hay que garantizar depende del tipo de componente, pero en general:
  - **Pruebas:** si es un servicio, debe tener pruebas que garanticen que no se caiga fácilmente — pruebas de carga, de estrés, entre otras.
  - **Concurrencia y escalabilidad:** validar si va a tener mucha concurrencia; si es backend, pensar en un modelo de microservicios que pueda **autoescalar horizontalmente** para garantizar disponibilidad ante mucho consumo, incluyendo balanceo de carga.
  - Componentes de uso compartido/reusado (ej. un backend al que todos apuntan) deben estar **"blindados"** para no caerse fácilmente; deben tener garantizado el crecimiento para no quedarse cortos.
  - **Seguridad:** al ser reutilizado por muchos, debe tener resueltos los temas de seguridad — tokens, certificados, buenas prácticas de desarrollo seguro (menciona OWASP). Una vulnerabilidad en un componente muy reutilizado afecta a todos, a diferencia de un servicio que solo usa una aplicación.
  - **Control de acceso:** validar temas tipo CORS, para que solo quienes realmente deban acceder puedan hacerlo (protección contra inyección de código, etc.), y así evitar que puedan "tumbar" el servicio.
  - Nota adicional: si se busca una escalabilidad prácticamente "infinita" para resistir cualquier carga, eso también implica un aumento de costos — un balance a tener en cuenta.
**Esos módulos compartidos evolucionan y cambian con el tiempo. ¿Cómo debería gestionarse ese cambio para que actualizar un módulo en muchos proyectos no se convierta en un problema de tu área?**

- Propone manejar **versionamiento**, por ejemplo en la URI del servicio (v1, v2, etc.).
- Si son ajustes pequeños que no afectan a todos los consumidores, se puede mantener la misma versión.
- Si el cambio es grande (ejemplo: agregar 10 campos obligatorios que no todos los consumidores pueden adoptar de inmediato), es mejor **versionar el servicio** (v1, v2) en lugar de forzar el cambio a todos a la vez.
- Los consumidores pueden ir migrando gradualmente a la nueva versión (los que ya estén listos o ajustados al cambio), manteniendo la versión anterior activa hasta que en algún momento se pueda dar de baja.
- Considera esto mejor que tener la misma lógica replicada en cada solución, ya que eso hace el sistema menos mantenible con el tiempo: es más fácil evolucionar y mantener un solo servicio central que mantener muchas copias replicadas.
---

### Sobre lo replicable y el riesgo

**Cuando una herramienta genera muchos proyectos desde una misma base, una buena decisión se propaga sola, pero un error también. ¿Cuál es el error más peligroso que podría quedar embebido y replicado, y por qué sería difícil de revertir una vez propagado?**

- Confirma el riesgo: si algo queda embebido (como código "hardcodeado") y se replica en varias soluciones, corregirlo después implicaría tener que **modificar solución por solución**, una por una — lo cual sería el motivo por el que sería difícil de revertir.
**¿Qué debería quedar fijo e impuesto en esa base común, y qué debería quedar configurable por cada equipo? ¿Dónde pondrías la línea?**

- Como regla general: **lo que realmente pueda variar** debería quedar por fuera del código, configurable sin tener que tocarlo.
  - Ejemplos de cosas que no deberían quemarse/hardcodearse: tipos de identificación, ciudades, barrios — este tipo de listas debería vivir en una tabla de catálogos, no en el código, para no tener que modificar código y desplegar de nuevo cada vez que se agregue un valor nuevo (ej. un barrio nuevo en Cali).
  - También menciona configuraciones propiamente dichas, como códigos de producto (ej. el código de un producto de microcrédito), que pueden llegar a cambiar en algún momento — es más impactante tener que entrar a modificar el código que simplemente cambiar un valor configurado.
  - **Endpoints:** siempre deberían ser configurables, nunca quedar pegados dentro del código, ya que una URL de servicio puede cambiar.
- Por otro lado, señala que **no todo debe externalizarse como configuración**: cosas que no son susceptibles de cambiar (ejemplo: que un código de estado HTTP 200 signifique éxito y un 400 signifique error) no necesitan estar en un archivo de configuración — de lo contrario se termina "llenando de parámetros" innecesarios.
- Conclusión: lo que es susceptible de cambiar debería estar configurado en algún lado (archivo de configuración o base de datos, dependiendo de la necesidad); lo que no cambia, no necesita externalizarse.
**¿Qué del arranque de proyectos y de la reutilización de funcionalidades consideras que debería estandarizarse?**

*(No se formuló como pregunta explícita e independiente en esta conversación; los elementos que la función de arquitectura considera que deberían estar cubiertos/estandarizados en módulos compartidos — pruebas, escalabilidad, seguridad, versionamiento, configuración externa de endpoints y catálogos — quedaron respondidos de forma dispersa a lo largo de las preguntas anteriores.)*

**¿Qué riesgos ves en estandarizar? ¿Qué debería quedar a criterio de cada equipo?**

- El principal riesgo que ve es **estandarizar algo que está mal**: si el estándar en sí mismo es incorrecto, se generan problemas para todos los que lo adoptan ("si uno estandariza algo que está mal, pues bailas" / hay problemas).
- Fuera de eso, considera que estandarizar en general es positivo.
- Sale un poco del enfoque de arquitectura para señalar que estandarizar también puede "amarrar" un poco: es bueno desde el punto de vista de control para arquitectura, pero puede generar **resistencia en otros equipos**, porque algunos preferirían hacer las cosas de otra forma.
- Otro riesgo: que el estándar quede desactualizado con el tiempo — hay que revisarlo periódicamente para confirmar si sigue aplicando o no. Ejemplo: si se establece como estándar fijo usar TLS 1.1 "para siempre", eso se volvería un problema, ya que hoy la versión vigente es TLS 1.3 y versiones anteriores se vuelven vulnerables con el tiempo. Como la tecnología cambia constantemente, hay que estar revisando que los estándares sigan vigentes.
- Conclusión: un estándar mal aplicado o desactualizado también es un riesgo ("los estándares mal aplicados, pues pailas"); el estándar es bueno, pero debe seguir evolucionando y revisándose para identificar qué hace falta ajustar y qué ya no es necesario.
---

### Sobre expectativa y confianza

**¿Qué tendría que cumplir una herramienta así para que confiaras en un proyecto generado por ella tanto o más que en uno construido a mano, desde el criterio de tu función? / Desde tu rol, ¿qué esperarías que una herramienta de este tipo hiciera bien, y qué te preocupa que hiciera mal?**

*(Estas dos preguntas del guion fueron abordadas por el entrevistador como una sola pregunta combinada, enfocada en expectativas desde un "mundo ideal".)*

- Lo primero que esperaría es que le **ayude en agilidad**: que agilice el desarrollo y que, además, lo que ofrezca tenga calidad.
- Entiende que la herramienta ayudaría a **preparar todo de antemano**: dejar definidos los módulos que se van a utilizar, dejar inicializados los llamados a librerías, imports, etc. (dependiendo del lenguaje) — básicamente dejar "el esqueleto" listo para empezar a codificar.
- Espera que, si hace esto, lo haga bien y **no genere reprocesos** — es decir, que no termine generando algo que luego él mismo tenga que revisar o corregir manualmente ("que no vaya a ser que lo tenga que voltear más").
- Riesgo/preocupación que identifica: al ser algo automático, **no se sabe exactamente qué hizo la herramienta por dentro**; si algo falla, tocaría empezar a buscar qué hizo para poder arreglarlo. Aun así, considera que si el resultado tiene calidad, el beneficio en agilidad compensa, porque evita tener que hacer todo el trabajo manualmente.
**Continuación de la conversación (grabación breve adicional de la misma sesión) — qué generaría más confianza:**

- la función de arquitectura propone que agregar **pruebas de código estático** daría más confianza: al probar el código generado, un análisis estático permitiría confirmar que las cosas se están llenando/implementando correctamente y no de forma incorrecta.
- el entrevistador menciona que esto también aplicaría al tema de seguridad: si algo rompe una práctica de seguridad de forma muy evidente, un análisis estático debería poder detectarlo y notificarlo.
- la función de arquitectura confirma que sí, que normalmente ese tipo de herramientas (de análisis estático) también evalúan temas de seguridad.
---

## Información adicional aportada por el entrevistado (fuera de las preguntas del guion)

### Comentario sobre el uso de IA en el motor de generación

*(Nota: este comentario no quedó registrado en la grabación/transcripción; fue aportado posteriormente por el entrevistador como palabras textuales del entrevistado.)*

- La IA nos podría sugerir y abordar más rápido el proceso de generación, para no tener que seleccionar.
- El motor podría ser inteligente.
### ¿Qué área o persona debería mantener/administrar esta herramienta o el estándar una vez entregada?

*(Pregunta adicional formulada por el entrevistador, no incluida en el guion original de este rol.)*

- Considera que debería estar a cargo de alguien **relativamente neutral**, aunque reconoce que su propio equipo (integraciones/arquitectura) tampoco es del todo neutral, ya que ellos son quienes actualmente dictan las reglas a las áreas técnicas (por ejemplo, mediante documentación: "me tienen que hacer esto, y punto, no puede salir de ahí").
- Propone que podría ser un **área de arquitectura** (posiblemente arquitectura de soluciones), ya que normalmente esa área es la que dicta los sistemas de estándares y cómo deben ser las cosas.
- Sugiere que no debería recaer en un equipo de desarrollo, sino en un área externa a desarrollo.
- Aclara que, en cuanto a la administración operativa (permisos, mantenimiento de módulos, etc.), eso podría repartirse entre distintas áreas según su función — por ejemplo, un área encargada de administrar permisos y otra encargada de otras cosas —, en lugar de recargar toda la responsabilidad en una sola.

---

## Respuestas preguntas cerradas

- Importancia de que una herramienta así respete los principios de tu función. 5
- Riesgo de propagar un error de tu área al embeberlo en plantillas replicables. 5
- Grado en que tu función debería condicionar el diseño de una herramienta de este tipo. 5
- Confianza que te daría un proyecto bien generado frente a uno hecho a mano. 5
