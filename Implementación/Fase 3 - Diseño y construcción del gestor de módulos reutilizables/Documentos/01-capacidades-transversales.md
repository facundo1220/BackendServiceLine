# Capacidades transversales y la capacidad elegida

Produce el inventario categorizado de las capacidades transversales de la línea y elige, con criterio explícito, la que esta fase construye como módulo.

---

## 1. De dónde sale el inventario

Cuatro fuentes, todas anteriores a esta fase. El inventario no agrega capacidades que nadie enunció.

| Fuente | Qué aporta |
| :-- | :-- |
| Caracterización organizacional (Fase 1, doc 01 §3) | La lista de funcionalidades que se repiten entre soluciones: consumo del core bancario, manejo de errores, logging, eventos, autenticación y validación de identidad, manejo de tokens y cifrado, integración con almacenamiento, integración con proveedor de identidad, notificaciones y conexión a la base de datos del proyecto |
| T-09, del análisis cualitativo | El orden de recurrencia según los entrevistados: primero autenticación y autorización, después observabilidad, trazabilidad de procesos, notificaciones al usuario, validación de identidad y capacidades de recaudo |
| El marco | La agrupación que adoptó para el catálogo: registro de eventos, observabilidad, cifrado, identidad, persistencia y consumo de servicios corporativos |
| El artefacto construido | Qué de todo eso ya está resuelto: los puertos del contrato con sus adaptadores en la plantilla, y las sondas de estado |

**Por qué el artefacto es una fuente.** Una capacidad ya cubierta por la plantilla no necesita módulo. Confundir las dos cosas es la forma más fácil de construir un módulo que no resuelve nada: el registro estructurado de eventos de aplicación, por ejemplo, es una capacidad transversal con su puerto y su adaptador desde la Fase 2.

## 2. Con qué ejes se categoriza

| Eje | Valores | Para qué sirve |
| :-- | :-- | :-- |
| Clase de puerto | Técnico · De dominio | Un puerto técnico lo declara el contract package y lo implementa un módulo. Un puerto de dominio es del producto y ningún módulo puede apropiárselo |
| Reparto de la realización | Todo el módulo · Módulo más adaptador del producto | Define qué cantidad del trabajo queda del lado del equipo. La persistencia es el caso donde el módulo aporta la capacidad técnica y el producto escribe su adaptador de repositorio |
| Dependencia de infraestructura externa | Ninguna · Servicio institucional · Proveedor externo | Determina si la capacidad es verificable fuera del entorno corporativo. Lo que no se puede verificar por comando no puede sostener la condición de llegada de la fase |
| Estado en el artefacto | Cubierta por la plantilla · Mínimo cubierto · No cubierta | Evita construir un módulo para algo que ya funciona, y muestra dónde el artefacto tiene un hueco declarado |

## 3. Inventario categorizado

Doce capacidades. La columna de estado se refiere al artefacto tal como está hoy.

| # | Capacidad | Evidencia | Clase de puerto | Realización | Infraestructura externa | Estado |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| C-01 | Registro estructurado de eventos de aplicación | T-08 | Técnico | Todo el módulo | Ninguna | Cubierta por la plantilla: adaptador de líneas JSON y registro de cada request |
| C-02 | Observabilidad: correlación, métricas y exportación a la plataforma corporativa | T-08, T-09, revisión externa | Técnico, puerto propio que no amplía el del logger | Todo el módulo | Una dirección en la configuración | **Cubierta**: la correlación y la traza del estándar están en la plantilla, y la exportación, el muestreo y las métricas en `@bsl/observability` |
| C-03 | Publicación y consumo de eventos entre servicios | T-09 | Técnico | Todo el módulo | Servicio institucional de mensajería | Mínimo cubierto: adaptador en proceso en la plantilla. El puerto ya anticipa su reemplazo |
| C-04 | Configuración externalizada y validada | T-07, RNF-05 | Técnico | Todo el módulo | Ninguna | Cubierta por la plantilla: esquema con validación al arranque |
| C-05 | Verificación de estado del servicio | T-08, revisión externa | Adaptador de entrada, excepción declarada por el marco | Todo el módulo | Ninguna | Cubierta por la plantilla: sondas de vida y de preparación |
| C-06 | Persistencia de datos del producto | Revisión externa | Técnico, más puerto de dominio del producto | Módulo más adaptador del producto | Ninguna, con un motor en proceso | **Cubierta** por el módulo que esta fase construye |
| C-07 | Autenticación y autorización | T-09, la más recurrente | Técnico | Todo el módulo, con política por producto | Proveedor de identidad institucional | No cubierta |
| C-08 | Validación de identidad de personas | T-09 | Técnico | Todo el módulo | Proveedor externo | No cubierta |
| C-09 | Cifrado y manejo de tokens y secretos | Caracterización | Técnico | Todo el módulo | Servicio institucional para custodia de claves | No cubierta |
| C-10 | Consumo de servicios corporativos | T-05 | Técnico | Módulo más tipos del producto | Servicio institucional, con contrato propio | No cubierta |
| C-11 | Notificaciones al usuario | T-09 | Técnico | Todo el módulo | Proveedor externo | No cubierta |
| C-12 | Manejo uniforme de errores y respuestas de la API | Caracterización | No es puerto: es forma del producto | De la plantilla | Ninguna | Cubierta por la plantilla, y no corresponde al catálogo. Declarada acá para que la ausencia no se lea como olvido |

**Capacidades de negocio.** Trazabilidad de procesos y recaudo, que T-09 también nombra, no son capacidades técnicas: son dominio bancario. El marco las excluyó del catálogo de esta línea y las declaró trabajo futuro como módulos de dominio alineados a BIAN.

## 4. Relación con BIAN, y su límite

La actividad de la fase enunciada en el anteproyecto pide identificar y categorizar las funcionalidades transversales «tomando como referencia los dominios funcionales definidos por BIAN». Esta categorización no se apoya en BIAN, y la razón está decidida desde la Fase 1.

BIAN modela capacidades de negocio bancario y no modela infraestructura técnica de aplicaciones. El catálogo de esta línea agrupa capacidades técnicas —las doce de arriba—, así que queda fuera del alcance del estándar y su gobierno corresponde al marco de referencia propio. Forzar una correspondencia produciría etiquetas sin contenido: no existe un Service Domain que signifique «persistencia» o «cifrado».

**Dónde sí se cumple la referencia a BIAN.** En el eje de dominio del producto, que la Fase 2 construyó: la derivación sitúa cada producto en un Business Domain y un Service Domain del estándar, y ese metadato queda en el registro del producto. La alineación con BIAN es del producto derivado, no del catálogo técnico que lo compone.

**Consecuencia.** Un lector que compare el anteproyecto con lo construido encontrará esta diferencia. Queda registrada como decisión con su fundamento, no como omisión.

## 5. Con qué criterios se elige el módulo de la fase

La fase construye un módulo. Cinco criterios, en orden de peso.

| # | Criterio | Por qué pesa |
| :-- | :-- | :-- |
| 1 | Verificable por comando sin infraestructura corporativa | La condición de llegada de la fase exige evidencia ejecutable: incorporar, arrancar, actualizar. Una capacidad que necesita un servicio institucional no se puede comprobar fuera del entorno, y el expediente no documenta el stack con proveedor concreto |
| 2 | Ejercita el mecanismo de composición en su caso más exigente | El objeto de la fase es el mecanismo, no el catálogo. Vale más la capacidad que obliga a repartir trabajo entre el paquete y el producto que la que se resuelve enteramente dentro del paquete |
| 3 | Cierra un hueco que el artefacto exhibe hoy | Un módulo que resuelve algo que el producto derivado ya no tiene como problema no agrega evidencia para la Fase 4 |
| 4 | No fija un contrato que pertenece a la organización | Las reglas institucionales de integración y permisos son de la institución (T-08). Un trabajo de grado que fije ese contrato impone una decisión que no le corresponde |
| 5 | Admite una segunda versión publicable con un cambio real | RF-11 a RF-13 exigen actualizar un módulo incorporado. Sin un cambio con sentido entre dos versiones, la actualización se prueba contra una versión inventada |

## 6. Evaluación de los candidatos

Se evalúan las seis capacidades no cubiertas que el catálogo admite, más las dos que estaban cubiertas en su mínimo y podían crecer como módulo.

| Candidata | 1. Verificable | 2. Ejercita el mecanismo | 3. Cierra un hueco | 4. Contrato propio | 5. Segunda versión | Veredicto |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| C-06 Persistencia | Sí, con un motor en proceso | **Sí, el caso más exigente**: puerto técnico del contrato, puerto de dominio del producto y adaptador escrito por el equipo | Sí: el producto guarda en memoria y la revisión externa lo marcó | Sí | Sí: agregar transacción sobre la conexión | **Elegida** |
| C-02 Observabilidad | Solo en parte: la correlación sí, la exportación no | Parcialmente | No: el mínimo ya estaba cubierto | La plataforma de observabilidad, no | Sí | Crecimiento, y es el que se construyó primero |
| C-09 Cifrado y tokens | Sí, con las primitivas de la plataforma | No: el módulo aporta el adaptador y el producto no escribe nada. La custodia de claves, que es la parte difícil, es institucional | No: ningún producto derivado exhibe hoy el hueco | La custodia de claves, no | Sí | Crecimiento |
| C-10 Consumo de servicios corporativos | No: su valor está en los contratos reales, que son privados | Sí, en el reparto de tipos | Sí, para T-05 | No: el contrato del servicio es de la organización | Sí | Crecimiento |
| C-07 Autenticación y autorización | No: exige el proveedor de identidad institucional | Sí | Sí | **No**, y es el criterio que lo descarta | Sí | Crecimiento |
| C-03 Mensajería | No fuera del entorno: exige el bus institucional | Sí | No: el mínimo en proceso ya está cubierto | No | Sí | Crecimiento |
| C-08 Validación de identidad | No: proveedor externo | No | No | No | Sí | Crecimiento |
| C-11 Notificaciones | No: proveedor externo | No | No | No | Sí | Crecimiento |

**La capacidad más recurrente no es la elegida, y conviene decirlo.** T-09 pone a la autenticación y autorización primero. Queda como crecimiento por el criterio 4: su contrato lo fija la organización, no este trabajo, y sin el proveedor de identidad no hay forma de comprobar por comando que un producto compuesto arranca y responde. Construir una versión simulada daría un módulo que nadie incorporaría y una evidencia que no prueba nada.

## 7. La capacidad elegida: persistencia

La fase construye el módulo de persistencia de datos del producto, con un motor relacional en proceso.

| Elemento | Valor |
| :-- | :-- |
| Identificador en el catálogo | `persistence` |
| Paquete | `@bsl/persistence` |
| Tipo de activo | Módulo |
| Capacidad que aporta | Conexión al almacén relacional y ejecución de sentencias dentro de una transacción |
| Qué no aporta | El adaptador del repositorio del producto, que lo escribe el equipo |

**Por qué la persistencia y no otra.** Es el caso de referencia con que el marco explica el acople entre módulo y producto: el repositorio del agregado es un puerto de dominio del producto, la conexión y la transacción son puertos técnicos del contrato, y el adaptador lo escribe el equipo apoyándose en la capacidad que el módulo provee. Ninguna otra candidata ejercita las dos clases de puerto a la vez. Como consecuencia, el dominio del producto no conoce el motor y cambiarlo no altera ninguna declaración de la capa de dominio, que es la propiedad que el marco buscaba y que hasta esta fase ningún artefacto había comprobado.

**Qué hueco cierra.** El producto derivado persiste en memoria y los datos desaparecen al reiniciar. La Fase 2 lo hizo visible en el resumen de la derivación y en el README del producto porque no podía resolverlo: el módulo no existía.

## 8. El motor es un adaptador interno del módulo

Un producto que necesite otro motor relacional no incorpora otro módulo: recibe una versión posterior del mismo módulo que trae ese adaptador, y lo elige por configuración. El catálogo guarda una entrada por **capacidad**, no una por motor.

**Por qué.** Una entrada por motor multiplica el catálogo por el número de motores y obliga a que el producto cambie de dependencia cuando cambia de infraestructura, que es justo lo que el puerto técnico evita. La capacidad es la misma; lo que cambia es su realización.

**Consecuencia asumida.** Un producto que necesite un motor que el módulo todavía no trae tiene que esperar una versión del módulo, o escribir su propio adaptador del puerto técnico y registrarlo en lugar del que el módulo provee, que es una operación que la escala de adaptación ya admite y que no afecta al producto más allá de su punto de composición.

## 9. Qué queda como crecimiento del catálogo

RF-09 pide un módulo funcional y declara en su criterio de aceptación que las demás capacidades identificadas quedan como catálogo a construir posteriormente. Quedan seis, con su categorización ya escrita, en el orden que los criterios de §5 sugieren.

| Orden | Capacidad | Qué falta para construirla |
| :-- | :-- | :-- |
| 1 | C-10 Consumo de servicios corporativos | Los contratos reales de los servicios consumidos, que son privados. Es la capacidad que T-05 señala como la más costosa de propagar, y necesita además un cliente HTTP que la plantilla todavía no trae |
| 2 | C-07 Autenticación y autorización | Que la organización fije el contrato de integración y permisos, y acceso al proveedor de identidad para verificar |
| 3 | C-09 Cifrado y manejo de tokens | Decidir dónde viven las claves. Las primitivas son locales; la custodia es institucional |
| 4 | C-03 Mensajería entre servicios | El bus institucional. El puerto ya existe y el adaptador en proceso ya cubre el mínimo |
| 5 | C-08 Validación de identidad | El proveedor externo y su contrato |
| 6 | C-11 Notificaciones al usuario | El proveedor externo y la política de canales |

**C-02 salió de esta lista construida.** Releídos los cinco criterios contra el artefacto, los cumplía los cinco y agregaba el caso de composición que la persistencia no podía dar: un módulo que no llena un hueco del producto sino que **recibe lo que el producto ya produce**. C-12 no entra en la lista por otra razón: es crecimiento de la plantilla, no del catálogo.

## 10. Límites de alcance del módulo

| Límite | Razón |
| :-- | :-- |
| Sin mapeo objeto-relacional | El módulo aporta la capacidad técnica, no una base de adaptador que el producto extienda. La herencia entre un activo del catálogo y el código del producto crea un acoplamiento que ninguna de las dos partes controla |
| Sin framework de migraciones | El esquema de datos describe el dominio del producto, así que es del producto. El módulo ejecuta lo que el producto declara; versionar esquemas es trabajo futuro |
| Un solo motor en esta versión | El motor es un adaptador interno del módulo: §8 |
| Sin selector de persistencia en la derivación | La revisión externa lo dejó como candidato y sigue siéndolo. Primero el módulo existe y se incorpora; ofrecerlo al derivar es otra decisión |
