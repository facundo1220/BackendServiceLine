# Informe de análisis cualitativo

Convierte las nueve entrevistas, consolidadas en un registro por rol, en quince temas (`T-xx`) agrupados en cinco grupos temáticos, cada uno respaldado en lo que dijo un rol concreto. Es el nodo de origen de toda la trazabilidad del proyecto: ninguna brecha ni requerimiento posterior se sostiene si no llega hasta acá.

## 1. Temas identificados

**T-01 El arranque es manual y recae en una sola persona**

El levantamiento de entornos, la configuración de la arquitectura, los componentes de infraestructura, el despliegue del repositorio, el despliegue del servicio en la nube y la creación de bases de datos se realizan a mano, en cada proyecto nuevo. El trabajo lo ejecuta un solo desarrollador y solo se incorpora una segunda persona cuando el proyecto es especialmente robusto. Mientras tanto, el resto del equipo asigna su tiempo a otras iniciativas en curso.

**Ámbito**: Arranque.
**Roles que lo evidencian:** Desarrollador interno, Líder Técnico, Desarrollador externo.

**T-02 Un proyecto en blanco genera una incertidumbre inicial costosa**

Al iniciar desde cero el desarrollador sabe qué quiere lograr pero no por dónde empezar, porque no hay archivo inicial ni estructura de referencia. Se resuelve recurriendo a asistentes de inteligencia artificial para obtener las primeras líneas, o trabajando con la estructura de otro proyecto a la vista mientras se construye la propia. El costo es cognitivo, no de configuración, y se agrava cuando el desarrollador aún no domina el patrón arquitectónico de la organización.

**Ámbito**: Arranque.
**Roles que lo evidencian:** Desarrollador interno, Desarrollador externo.

**T-03 El costo del arranque afecta el alcance del negocio y suele ser imperceptible**

El tiempo que consume montar bases técnicas e integrar capacidades no previstas se compensa recortando funcionalidades del producto hasta llegar a un mínimo viable. Ese trabajo tampoco es perceptible desde los roles de negocio, que valoran que la aplicación corra y no lo que hubo que configurar para lograrlo. Por eso resulta difícil justificar el tiempo invertido.

**Ámbito**: Transversal.
**Roles que lo evidencian:** Líder de Producto, Desarrollador externo.

**T-04 Copiar código es el mecanismo de reutilización cuando no existe uno formal**

Cuando un proyecto necesita una capacidad que otro ya resolvió y no hay librería ni módulo compartido disponible, se replica el código copiando la carpeta correspondiente y se ajustan sus variables de entorno, o se reconstruye la estructura tomando otro proyecto como referencia visual.

**Ámbito**: Integración de módulos.
**Roles que lo evidencian:** Desarrollador interno, Desarrollador externo.

**T-05 Propagar un cambio es manual, y el contrato del servicio es su punto más frágil**

Cuando una funcionalidad compartida cambia, el cambio debe replicarse manualmente en cada proyecto donde fue copiada. Lo más costoso no es copiar el código sino cambiar la estructura de la respuesta del servicio consumido. Cuando el contrato del servicio consumido cambia, se desencadena una cadena de ajustes en cascada en la lógica de cada proyecto afectado.

**Ámbito**: Integración de módulos.
**Roles que lo evidencian:** Desarrollador interno, Arquitectura.

**T-06 Los proyectos divergen porque nada propaga las mejoras ni refuerza el estándar**

Las mejoras que un producto incorpora no llegan a los que ya existen. Además, la divergencia aparece incluso donde hay un estándar declarado, porque un patrón arquitectónico define conceptos pero no cómo materializarlos y cada equipo termina interpretándose a su manera. El resultado es que trabajar en el código de otro equipo sigue siendo costoso pese a compartir el mismo estándar.

**Ámbito**: Causa estructural.
**Roles que lo evidencian:** Líder de Producto, Desarrollador externo.

**T-07 Lo que queda fijo en el código impide utilizarlo después**

Los equipos atienden el alcance inmediato sin considerar qué de lo construido podrá reutilizarse o necesitará crecer. El mecanismo por el que se pierde esa reutilización es dejar valores y referencias fijos en el código y atar la solución a un contexto específico, lo que obliga después a intervenciones forzadas para expandir.

**Ámbito**: Transversal.
**Roles que lo evidencian:** Líder de Producto.

**T-08 Lo transversal y lo institucional se descubre tarde**

La ausencia de observabilidad se detecta cuando ya hay errores en producción sin visibilidad, y obliga a construir después un registro de trazas que genera retrabajo. Las reglas institucionales de integración y permisos no tienen alerta temprana y se manifiestan al momento de desplegar.

**Ámbito**: Arranque y causa estructural.
**Roles que lo evidencian:** Desarrollador interno, Líder Técnico, Arquitectura.

**T-09 Existe un núcleo reconocido de funcionalidades transversales**

Un conjunto acotado de capacidades se repite en la mayoría de los productos y hoy se rehace o se copia en cada uno. La más recurrente es la autenticación y autorización, le siguen la observabilidad, la trazabilidad de procesos, las notificaciones al usuario, la validación de identidad y las capacidades de recaudo.

**Ámbito**: Integración de módulos.
**Roles que lo evidencian:** Desarrollador interno, Líder de Producto, Líder Técnico, Desarrollador externo.

**T-10 La estandarización se acepta si su rigidez está justificada**

Todos los roles apoyan estandarizar y todos condicionan ese apoyo a poder adaptar el resultado. La rigidez no se rechaza cuando está justificada, y resulta aceptable ajustarse a la estructura que la herramienta imponga siempre que siga buenas prácticas y ahorre tiempo. El riesgo mayor es estandarizar algo mal concebido, porque el error se propaga a todos sus adoptantes.

**Ámbito**: Condición de diseño y gobernanza.
**Roles que lo evidencian:** Desarrollador interno, Líder Técnico, Desarrollador externo, Arquitectura, Lider de Producto.

**T-11 La configuración externa separa lo fijo de lo variable**

Lo que puede variar debe configurarse fuera del código, y lo estable no necesita externalizar, porque hacerlo con todo llena la solución de parámetros innecesarios. Desde el negocio se pide poder ajustar rangos, plazos y reglas de producto sin desarrollo.

**Ámbito**: Condición de diseño.
**Roles que lo evidencian:** Arquitectura, Líder de Producto.

**T-12 La evolución por versiones permite cambiar sin romper**

Versionar las capacidades compartidas y la propia herramienta permitirá que la adopción sea gradual. Los cambios deben versionarse manteniendo activa la versión anterior hasta que todos migren. Mantener una capacidad central versionada resulta más sostenible que replicar la misma lógica en cada solución.

**Ámbito**: Condición de diseño.
**Roles que lo evidencian:** Arquitectura, Desarrollador externo.

**T-13 La confianza depende de poder verificar la herramienta y lo que produce**

Automatizar genera la preocupación de no saber qué hizo la herramienta por dentro, y esa confianza se recupera pudiendo someter lo generado a análisis estático y pudiendo modificarlo en lugar de aceptar una caja cerrada. En sectores vigilados la exigencia alcanza a la herramienta misma, que debe poder auditarse en dependencias y vulnerabilidades y presentar esos resultados a las áreas técnicas y de riesgo.

**Ámbito**: Condición de diseño y de adopción.
**Roles que lo evidencian:** Arquitectura, Desarrollador interno, Desarrollador externo.

**T-14 La adopción depende de agilidad real y facilidad de uso**

El valor de la herramienta se juzga por la ganancia efectiva de tiempo y por lo sencillo que resulte usarla, con un umbral esperado de un comando o pocos comandos. Si exige aprender y ejecutar diez o doce, el desarrollador optará por hacerlo manualmente o buscar otra alternativa.

**Ámbito**: Condición de adopción.
**Roles que lo evidencian:** Desarrollador interno, Líder Técnico, Arquitectura, Desarrollador externo.

**T-15 La permanencia exige capacidad de evolución y un responsable definido**

Un estándar requiere un espacio periódico de revisión y un responsable que convoque al equipo, porque cuando la tarea queda en manos de varios casi nunca se hace. La adopción y la permanencia son problemas distintos. La primera se resuelve con facilidad de uso y respaldo de quienes deciden, y la segunda con la capacidad de evolucionar al ritmo de la arquitectura de la organización.

**Ámbito**: Gobernanza y permanencia.
**Roles que lo evidencian:** Líder Técnico, Arquitectura, Desarrollador externo.

## 2. Agrupación de temas

Los quince temas se agrupan en cinco grupos. Cada grupo enuncia qué tiene que resolverse, y de ahí
salen los requerimientos del doc 6: un requerimiento cita el tema o los temas que lo originan, sin
una capa intermedia que los reformule.

| Grupo temático | Temas | Idea que sintetiza el grupo |
| :---- | :---- | :---- |
| G1- El costo del arranque | T-01, T-02, T-03 | Arrancar un proyecto es un proceso manual, concentrado en una persona, que impone un costo cognitivo inicial, se paga en alcance de negocio y resulta invisible para el negocio |
| G2 - La reutilización y su propagación | T-04, T-05, T-09 | Existe un núcleo reconocido de funcionalidades que se repite entre productos, pero sin un mecanismo formal para utilizarlo se recurre a copiarlo, y con el contrato del servicio como punto más frágil |
| G3 - Causas estructurales de la divergencia | T-06, T-07, T-08 | Los proyectos divergen porque nada propaga las mejoras ni refuerza el estándar, porque se diseña para el alcance inmediato acoplando lo que debería ser configurable, y porque el conocimiento transversal e institucional llega tarde |
| G4 - Condiciones de diseño | T-10, T-11, T-12, T-13 | La solución debe estandarizar con rigidez justificada, separar lo fijo de lo variable por susceptibilidad al cambio, evolucionar por versiones y ser verificable |
| G5 - Condiciones de adopción y permanencia | T-14, T-15 | Adoptar requiere agilidad real y uso sencillo; permanecer requiere capacidad de evolución y un responsable definido |

## 3. Análisis de roles de tecnologia

**Arquitectura**

**Principios y condiciones señalados.**

- Se debe considerar el uso futuro y no solo el alcance inmediato, porque la capacidad que hoy sirve a un producto será demandada por otros.
- Todo componente compartido es un riesgo inherente, por ser punto único de integración. En consecuencia, debe estar respaldado por:
  - Pruebas de carga y de estrés.
  - Diseño para escalar horizontalmente ante concurrencia.
  - Seguridad resuelta en el manejo de tokens y certificados, en las prácticas de desarrollo seguro reconocidas y en el control de acceso.
- Evolución por versionamiento, con convivencia de versiones y migración gradual de los consumidores.
- Configuración externa como criterio de diseño. Lo susceptible de cambiar debe vivir fuera del código, con los endpoints como caso explícito. Lo estable no requiere externalizar.
- Un estándar equivocado propaga el error a todos sus adoptantes, y un estándar no revisado envejece hasta volverse vulnerable.

**Qué debe respetar la solución**

- Generar estructuras que no aten la lógica a un contexto específico ni fijen en el código lo que puede variar.
- Tratar los componentes compartidos como piezas con garantías de disponibilidad, escalabilidad y seguridad, no como código copiado.
- Incorporar versionamiento como mecanismo de evolución.
- Permitir verificación de lo generado mediante análisis estático de código, que aporte confianza sobre la corrección y sobre el cumplimiento de prácticas de seguridad.
- Prever que el propio estándar que la herramienta materialice deberá revisarse periódicamente.

## 4. Contraste entre Desarrolladores internos vs Desarrolladores Externos

**Temas compartidos**

| Tema | Evidencia externa |
| :---- | :---- |
| T-01 Arranque manual y costoso | Incluso con librerías y módulos comunes disponibles, persiste un espacio de configuración desde cero. |
| T-02 Incertidumbre del proyecto en blanco | Resuelta con la estructura de otro proyecto a la vista mientras se construye la propia |
| T-03 Costo que afecta el alcance y es imperceptible | El trabajo de configuración en backend no es perceptible ni fácil de justificar ante roles de negocio |
| T-09 Núcleo de funcionalidades transversales | Nombra observabilidad y autenticación |
| T-10 Estandarización con rigidez justificada | Acepta rigidez si está justificada por buenas prácticas y ahorro de tiempo |
| T-14 Agilidad y facilidad de uso | Fija el umbral en pocos comandos |
| T-15 Permanencia por evolución | Si la arquitectura evoluciona y la herramienta no, queda obsoleta y deja de usarse |

**Contraste entre interno y externo**

La ausencia de un mecanismo formal de reutilización. Es la diferencia estructural entre ambos entornos.

|  | Contexto estudiado | Organizaciones externas |
| :---- | :---- | :---- |
| Mecanismo de reutilización | Copia de carpetas entre proyectos | Librería compartida o módulo común en monorepo |
| Alcance del mecanismo | Solo código de aplicación | Código de aplicación e infraestructura como código |
| Organización de repositorios | Repositorios independientes por proyecto | Monorepo |
| Estándar arquitectónico | No documentado y de aplicación parcial | Adoptado formalmente en toda la organización (DDD) |
| Costo de propagación reportado | 4 | 3 |

## 5. Temas emergentes

**El papel de la inteligencia artificial en la generación**

Durante el levantamiento la inteligencia artificial apareció de forma espontánea en la mayoría de las entrevistas, no como una pregunta del guión sino como una posibilidad que los propios roles plantearon para el motor de generación. El tema no es si la herramienta puede incorporar inteligencia artificial, sino en qué parte del proceso conviene hacerlo.

**Comentarios**

- Que podría acelerar el arranque evitando que el proceso inicial consista en escoger entre opciones, de modo que el motor sea inteligente y acompañe al desarrollador durante todo el proceso.
- Que el entorno generado incluya un módulo con los estándares de la organización en formato legible, junto con una guía para el uso de asistentes, de manera que la generación asistida opere sobre reglas definidas y no sobre interpretación libre.
- Que ya se usa en la práctica diaria para superar la incertidumbre del proyecto en blanco y obtener las primeras líneas de código.

- La generación de estructura requiere determinismo y la inteligencia artificial es no determinista por naturaleza, de modo que la misma petición puede resolverse de forma distinta en momentos distintos. Esto delimita el alcance del motor de generación: determinismo para la estructura y asistencia para el contenido. La estructura debe producirse siempre igual, y la asistencia puede aportar sobre esa base ya construida, guiada por los estándares que la herramienta materialice.
