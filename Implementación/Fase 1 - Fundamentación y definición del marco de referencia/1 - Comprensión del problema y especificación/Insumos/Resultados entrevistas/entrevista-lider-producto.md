# Entrevista: Asesoría Líder de Producto

**Entrevistador:** Jorge Andrés Facundo Solarte
**Entrevistada:** la líder de producto
**Fecha:** 6 de agosto de 2026
**Archivo de origen:** Sesión Asesoría con Líder de Producto-20260806_093424-Meeting Recording

---

## Parte A – Preguntas abiertas

### ¿Cuál es el proceso regular de cómo nace un nuevo proyecto y en qué punto se empieza a incluir al equipo técnico?

- Todo parte de identificar **dos tipos de necesidades**:
  1. **La voz del mercado y la competencia:** lo que requieren los usuarios y cómo está la competencia.
  2. **Las necesidades internas:** qué metas tiene el banco, cuál es la visión estratégica y la postura que va a tener en el mercado.
- Con esas dos, se identifica la necesidad (ej. digitalizar la experiencia de un proceso/producto).
- Luego se empiezan a **definir las reglas de negocio**: reglas, variables, atributos y políticas del producto.
- Con base en eso se define qué necesita el producto, y ahí se involucra al **equipo de UX** para definir la experiencia de contratar ese producto con el banco.
- Después se empieza a incluir al **equipo técnico**: se les explica, por ejemplo, que si el cliente elige cierta opción se despliega determinada tabla, o determinadas opciones; ahí empieza la configuración y el desarrollo de las pantallas.
- Resumen del orden: primero necesidad de mercado, luego necesidades internas de la empresa, luego revisión con UX, y solo después se define lo que se requiere del equipo técnico.

### Cuando defines un producto nuevo con el equipo técnico, ¿cómo se traduce el arranque en tu planeación? ¿Es tiempo que ya das por perdido antes de ver la funcionalidad?

- En la etapa inicial, **fechas todavía no se comprometen formalmente**; hay más bien una visión amplia (ej. "de aquí a este semestre lo tengo que hacer"), es decir, hay **holgura de tiempo**.
- Reconoce que en las empresas "todo va a ser urgente" y hay que priorizar, pero en esa etapa aún no se compromete con fechas porque todavía está viendo la experiencia y activando al equipo técnico para acotar un **producto mínimo viable (MVP)** y salir más rápido.
- No se busca hacer todo perfecto (eso tomaría un año); se prefiere ir entregando en **entregas tempranas**.
- Junto con el equipo técnico se hace una alineación para definir fechas, o más que la fecha, lo que se requiere.
- Una vez se tiene el **backlog**, se baja más el detalle con los técnicos para estimar en términos de **sprint** cuánto se van a demorar.

### En tu experiencia, ¿cuánto pasa entre que un proyecto empieza y entrega su primer valor de negocio visible? ¿Qué se lleva ese tiempo?

- Le parece que es un tiempo **demorado**, pero principalmente porque muchas veces "no se tiene el terreno abonado" — es decir, el terreno todavía está lleno de maleza y hay que empezar a limpiarlo.
- Esto ocurre porque a veces la tecnología en la empresa no está acorde a las necesidades o a la visión que ella tiene como líder de producto; al equipo técnico le toca "abonar el terreno" y dejar todo listo primero.
- Una vez se construye esa base, hay una **atracción mucho más rápida**, porque ya existen plantillas de proyectos y algo modular.
- Pero al principio a veces se cae en el error de hacer las cosas rápido, no de forma modular, "a la ligera" — y luego se entrega algo no modular que después no se puede reutilizar para otro producto.
- Es una apuesta consciente del equipo, en términos de tiempo, para salir más rápido — lo cual implica dejar de hacer cosas importantes; según ella, "eso no está mal", depende de la necesidad.
- En su experiencia, a veces se sale rápido con algo así, y luego, cuando el producto ya se prueba y trae resultados (ventas/clientes), se decide ajustar al "deber ser" — lo cual toma un poco más de tiempo.

### Durante la vida de un producto, ¿con qué frecuencia el equipo tiene que incorporar algo que otro producto ya resolvió? ¿Cómo te enteras y cómo lo planeas?

- Se entera de las **capacidades que tienen los aliados** (ej. firma electrónica, validación de identidad).
- Cuando salen productos nuevos, o más bien cuando se busca digitalizar la experiencia de productos existentes que hoy se ofrecen de forma manual (100% manual, sin canal digital), ella como líder **sugiere** basándose en productos de referencia que le han llegado antes.
- Menciona que también entra en juego la visión de vicepresidentes y gerentes que ven esas necesidades en el mercado, y que **marketing** también se entera de tendencias del mercado.
- Considera que así es como "se empieza a atar todo": se identifica que un producto ya tiene resuelta cierta capacidad y se empieza a construir a partir de ahí.

### Cuando esa reincorporación aparece a mitad de camino, ¿qué le hace a tu cronograma?

*(Esta pregunta fue retomada más adelante, dentro del bloque de preguntas cerradas, con un ejemplo concreto.)*

- Responde que el impacto es **"sí, bastante"**.
- Ejemplo concreto: en un producto de captación asistida necesitaban conectarse a la API de un proveedor externo de validación de identidad; hubo que ir a ver cómo funciona esa API y ahí "uno encuentra ciertos *stoppers*" (bloqueadores).
- Menciona otro caso similar con un gestor documental de un tercero y su API, que también generó demoras.
- Conclusión: el impacto de una integración no prevista que aparece a mitad de camino sí suele ser alto.

### Si sumas el tiempo que el equipo dedicó a montar bases y reintegrar cosas comunes, ¿qué funcionalidad de negocio se queda sin hacer por eso?

*(Retomada también en el bloque de preguntas cerradas.)*

- Indica que **siempre se sacrifica algo**: el equipo "juega con eso" — deciden no ofrecer cierta regla, característica o *feature*, y la quitan. Ahí es cuando se empieza a "peluquear" (recortar) hasta llegar al MVP.
- Ejemplo concreto: en el tema de pagos, solo se dejó **PSE y cuenta**, porque era lo más fácil; se sacrificaron opciones como **efectivo, cheque y titularidad individual**, porque no había servicios disponibles para eso por el canal digital ("es que ahí no hay servicios para eso, entonces quítelo por el canal digital").
- Conclusión: por esto el canal digital se termina acotando bastante frente a lo que originalmente se quería ofrecer.

### ¿Has tenido que ajustar un compromiso o una fecha por costos de arranque o de integración que no eran de negocio? Cuéntame.

Al cierre de las preguntas abiertas, cuando el entrevistador le pregunta si hay algo más que quiera agregar como insumo (fuera de las preguntas), la líder de producto comparte un caso concreto relacionado con este tema:

- **Caso del proyecto de "actualización de datos":** es un proyecto aparte que le pide al usuario actualizar ciertos datos, pero fue desarrollado de forma **muy rígida y muy separada** de los demás productos.
- Ese proyecto no se fue actualizando a la línea visual de los demás productos (por ejemplo, de la API del producto de captación).
- Terminó siendo un producto **"como una isla aparte"**, que quedó en el olvido: era usable puntualmente para el producto de captación, pero cuando otro canal (**el móvil**) quiso usarlo, "era una galleta" porque no se le podía meter tanta robustez.
- En el producto de captación funcionaba bien porque ese era el pedido original, pero en el canal móvil no — esto generó que la experiencia de actualización de datos en ese canal "patinara", cuando necesitaba ser mucho más simple.
- Reconoce que parte de esto pudo deberse a temas técnicos (consumo de servicios del banco, etc.), pero considera que es algo que la tecnología del banco tendrá que resolver: que el proyecto sea **fácilmente parametrizable por producto** y se actualice al estándar visual general (manual de marca) de los demás productos.
- **Ejemplo concreto de desactualización:** actualizaron ciertas pantallas en el producto de captación (por ejemplo, la pantalla de datos básicos, que pasó de 11 pasos a solo 3, y se agregó una barra de progreso), pero esos mismos cambios **no se replicaron** en el proyecto de actualización de datos, que quedó igual.
- Concluye que esto ha sido un dolor que ha observado, sin ser ella la líder directa de ese proyecto de actualización de datos — lo ve como un **reto para el equipo técnico**.
- **Otro ejemplo relacionado (parametrización):** menciona que si hoy tiene una lista desplegable, por ejemplo de plazos que van de 30 días a un año, y mañana se necesita que vaya de 90 a 720 días, debería poder **parametrizar eso fácilmente** — algo que ha visto mucho en el producto de captación en términos de plazos, tasas y reglas del producto en general.

### Desde tu rol, ¿qué esperarías de una herramienta que quitara ese costo, y qué te haría desconfiar de que funcione?

- Esperaría algo **estándar**, que aplique para todo, y que no le toque estar pensando "esto lo modifiqué aquí, pero acá no se modificó".
- Ejemplo: que una funcionalidad como validación de identidad se pueda usar igual en distintos canales (aplicación, portal, producto de captación, etc.).
- Quiere algo que permita **estandarizar pero también modificar**: que sea estándar, de forma que si se modifica algo se modifique en todos los canales, salvo que el pedido sea distinto — es decir, que tenga capacidad de ser **customizable**.
- Al preguntarle si hay algo más, menciona también el tema de **escalabilidad**: a veces se construye algo pequeño que luego no es escalable y no se puede estandarizar. Considera que la escalabilidad y la estandarización en los proyectos, procesos o productos son algo importante.

---

## Información adicional aportada por la entrevistada (fuera de las preguntas del guion)

### ¿Qué funcionalidades suelen repetirse a lo largo de los proyectos del laboratorio?

*(Pregunta adicional formulada por el entrevistador, no incluida en el guion original.)*

Identifica dos temas principales que se repiten:

1. **Vinculación del usuario:** la razón de ser del banco es tener clientes, por lo que la capacidad de vincular a un usuario de forma digital es algo que se va a replicar en todos los productos. Da el ejemplo del producto de captación, que consume servicios para esto, pero indica que ningún otro producto lo tiene todavía porque no existe aún un flujo digital que lo permita — aunque reconoce que hacia allá se dirige el laboratorio, buscando reemplazar la vinculación manual.
2. **Validación de identidad:** necesita validar la identidad del cliente sin importar el producto.
3. Menciona también, de forma más general, que **todas las capacidades relacionadas con cómo "traer la plata"** (efectivo, cheque, PSE) — es decir, el módulo de cómo se recibe el dinero, sea para invertir o para otro fin — son cosas que se replican y que constituyen la base del negocio.

### ¿Qué riesgos ves en estandarizar o hacer un proceso más rígido?

*(Pregunta adicional formulada por el entrevistador, no incluida en el guion original.)*

- Considera que depende del producto: no todos necesitarán las mismas pantallas o procesos.
- Cree que debería haber **flexibilidad**, y que lo modular permite lograr esa flexibilidad — se pueden incluir ciertas pantallas o pop-ups que apliquen a un producto y quitarlos en otro.
- Ejemplo: usar una parte de validación, pero en un caso pedir solo un dato y en otro pedir tres.
- Conclusión: al final debe existir un grado de flexibilidad dentro de la estandarización.

---

## Respuestas preguntas cerradas

- Impacto del tiempo de arranque sobre tu planeación. 55
- Frecuencia con que un producto requiere integrar funcionalidades ya existentes en otros. 4
- Impacto de esa integración sobre el cronograma cuando aparece a mitad de camino. 4
- Frecuencia de funcionalidades de negocio que se sacrifican por estos impactos. 5
- Valor esperado de reducir los tiempos de arranque e integración. 5