# Fundamentos teóricos de línea de producto de software

**Documento previo a MR-01. Explica el cuerpo teórico sobre el que se apoyan las decisiones del marco de referencia, con las fuentes que lo sustentan.**

## 1. Qué problema resuelve

Toda organización que construye más de un sistema parecido enfrenta la misma decisión: construir cada producto desde cero, copiar el anterior, o compartir una base entre todos. La línea de producto de software es el cuerpo de teoría que estudia la tercera opción de forma sistemática.

Se origina en la ingeniería de software basada en componentes de las décadas de 1980 y 1990, cuando la industria identificó que las similitudes entre productos podían tratarse como una ventaja de ingeniería en lugar de una coincidencia. Se consolidó como disciplina en los años noventa, con la publicación del marco de referencia del Software Engineering Institute de Carnegie Mellon, que sigue siendo la fuente más citada del campo.

La definición de referencia:

Conjunto de sistemas intensivos en software que comparten un conjunto común y gestionado de características, que satisfacen las necesidades de un segmento determinado y que se desarrollan a partir de un conjunto común de activos siguiendo un procedimiento establecido.

**Fuente:** Clements, P. y Northrop, L. (2001). *Software Product Lines: Practices and Patterns.* Addison-Wesley. SEI Framework for Software Product Line Practice.

## 2. Enfoque frente a mecanismo

Una línea de producto de software no es una categoría de herramienta. Es un enfoque de ingeniería: declara un alcance, una arquitectura común, un conjunto de activos y un procedimiento de derivación.

Esta distinción es la que evita el error más frecuente al leer la literatura. Los generadores de plantillas, los gestores de paquetes y las plataformas internas de desarrollo son mecanismos de reutilización: cada uno atiende una preocupación concreta y la resuelve dentro de su ámbito. Ninguno declara alcance, arquitectura ni procedimiento, porque no es su propósito. Una línea de producto no los sustituye ni los supera: opera en un plano distinto, los ordena y se materializa empleándolos.

La relación es análoga a la que existe entre un proceso de desarrollo y las herramientas que lo soportan: el proceso no compite con el control de versiones, lo emplea.

## 3. Los elementos constitutivos

El marco del SEI representa la relación entre los productos de una línea, el dominio al que pertenecen, la arquitectura que comparten y los activos con que se construyen.

![][image1]

*Figura 1. Productos, dominio, arquitectura y activos. Elaboración propia a partir de Clements y Northrop (2001).*

La figura establece una cadena de tres relaciones: los productos pertenecen a un dominio de negocio, ese dominio se satisface con una arquitectura, y esa arquitectura se construye con componentes y servicios. Sumando el procedimiento establecido que la definición exige, resultan cuatro elementos constitutivos. La ausencia de cualquiera impide hablar de línea de producto.

| Elemento | Qué exige | Qué ocurre sin él |
| :---- | :---- | :---- |
| Alcance gestionado | Declaración explícita de qué productos pertenecen a la familia | Los activos se generalizan hasta volverse inservibles o se especializan hasta servir a un solo producto |
| Arquitectura común | Una estructura compartida por todos los productos de la familia | Un mismo activo no puede servir a varios productos, porque cada uno lo espera en un lugar distinto |
| Core assets | Activos reutilizables que incluyen contratos, modelos y documentación, no solo código | Existe un repositorio de piezas sueltas sin estructura que las relacione |
| Mecanismo de derivación | Procedimiento que produce un producto a partir de los activos y de una selección de características | Los activos existen pero su ensamblaje vuelve a ser manual |

La conclusión que el propio marco del SEI resalta al pie de la figura es la definición operativa de una línea de producto en la práctica: toma ventaja económica de lo común entre productos, y acota su variación.

## 4. Los dos ciclos de ingeniería

Construir los activos y construir un producto con ellos son actividades distintas, con insumos, salidas y ritmos diferentes. La literatura las separa en dos ciclos.

![][image2]

*Figura 2. Los dos ciclos de una línea de producto. Elaboración propia a partir de Pohl, Böckle y van der Linden (2005).*

La **ingeniería de dominio** toma el conocimiento del dominio como insumo y produce los activos: el modelo de variabilidad y los componentes reutilizables. La **ingeniería de aplicación** toma los requerimientos de un producto concreto, consulta esos activos y produce el producto.

La relación no es de un solo sentido. La ingeniería de aplicación consume los activos, pero también puede generar una necesidad nueva que la ingeniería de dominio debe incorporar.

## 5. El modelo de referencia de cuatro cuadrantes

Los cuatro elementos describen qué debe existir, y los dos ciclos describen quién construye qué. Falta el mecanismo que los articula. El modelo de referencia más detallado del campo cruza los dos ciclos con una segunda dimensión: el espacio del problema frente al espacio de la solución.

![][image3]

*Figura 3. Modelo de referencia de cuatro cuadrantes. Elaboración propia a partir de Apel, Batory, Kästner y Saake (2013).*

El espacio del problema representa qué características existen y cuáles requiere un producto. El espacio de la solución contiene el código o artefacto que implementa cada característica. Del cruce resultan cuatro cuadrantes.

| Cuadrante | Qué ocurre en él |
| :---- | :---- |
| Análisis del dominio | Se delimita el alcance de la familia y se modela la variabilidad en un feature model. Incluye scoping y modelado de variabilidad como una sola actividad |
| Implementación del dominio | Se construyen los activos que implementan cada característica del modelo |
| Análisis de requerimientos | Se selecciona, sobre el mismo feature model, qué características requiere un producto concreto |
| Derivación del producto | Se ensamblan los activos correspondientes a la selección y se obtiene el producto |

Cinco flujos conectan los cuadrantes y definen el procedimiento completo.

| Flujo | Origen y destino | Significado |
| :---- | :---- | :---- |
| Mapeo | Análisis del dominio → Implementación del dominio | Establece qué activo implementa cada característica. Ocurre una sola vez, no por producto |
| Características | Análisis del dominio → Análisis de requerimientos | El modelo construido en el dominio es el mismo que se usa para configurar un producto |
| Nuevos requerimientos | Análisis de requerimientos → Análisis del dominio | Una necesidad que el modelo no contempla obliga a ampliarlo, y queda disponible para todos los productos futuros |
| Activos comunes | Implementación del dominio → Derivación del producto | Los activos construidos una vez alimentan cada derivación |
| Selección de características | Análisis de requerimientos → Derivación del producto | La configuración elegida determina qué activos se ensamblan |

Este modelo es el que fundamenta la exigencia de un feature model formal: el flujo de selección de características solo puede automatizarse si existe un árbol del que seleccionar.

## 6. Las tres actividades esenciales

El marco del SEI describe el trabajo continuo de sostener una línea de producto como tres actividades que ocurren en paralelo y se retroalimentan.

![][image4]

*Figura 4. Las tres actividades esenciales. Elaboración propia a partir de Clements y Northrop (2001).*

| Actividad | En qué consiste |
| :---- | :---- |
| Core Asset Development | Construir y mantener los activos reutilizables |
| Product Development | Derivar productos concretos a partir de los activos |
| Management | Decidir el alcance, asignar responsables y sostener la línea en el tiempo |

Las tres comparten un borde en el diagrama porque ninguna se sostiene sin las otras dos: sin gestión, el desarrollo de activos pierde alcance y dirección; sin desarrollo de producto, los activos no se validan contra un caso real; sin desarrollo de activos, cada producto vuelve a construirse desde cero.

## 7. Variabilidad y feature model

La variabilidad es la propiedad de un activo de admitir más de una realización. Un punto de variación es el lugar concreto donde esa elección ocurre.

El mecanismo formal para representar qué varía entre los productos de una familia y qué permanece fijo es el modelo de características, o feature model, introducido en el método FODA.

**Fuente:** Kang, K. C., Cohen, S. G., Hess, J. A., Novak, W. E. y Peterson, A. S. (1990). *Feature-Oriented Domain Analysis (FODA) Feasibility Study* (CMU/SEI-90-TR-21). Software Engineering Institute, Carnegie Mellon University.

Un feature model organiza las características en forma de árbol y declara, para cada nodo, su tipo de relación con el padre, más las restricciones que cruzan el árbol.

![][image5]

*Figura 5. Notación de un feature model.*

| Tipo de relación | Significado |
| :---- | :---- |
| Obligatoria | Todo producto de la familia la incluye |
| Opcional | El producto puede incluirla o no |
| Alternativa | El producto elige exactamente una entre varias |
| Or | El producto elige una o más entre varias |
| Restricción cruzada | Una característica exige o excluye a otra que no es su pariente en el árbol |

Sobre ese árbol, la ingeniería de aplicación configura un producto marcando qué características incluye, respetando las restricciones declaradas. El resultado de esa configuración es lo que la Figura 3 llama selección de características.

El tratamiento moderno de estos modelos y su relación con la implementación se desarrolla en la obra de referencia del campo.

**Fuente:** Apel, S., Batory, D., Kästner, C. y Saake, G. (2013). *Feature-Oriented Software Product Lines: Concepts and Implementation.* Springer.

## 8. Binding time

Una característica no solo se selecciona: se resuelve en algún momento del ciclo de vida del producto. Ese momento se denomina binding time.

![][image6]

*Figura 6. Binding time.*

El binding time determina qué tan flexible es una característica después de derivado el producto. Una característica resuelta en generación queda escrita en el código y cambiarla exige volver a derivar. Una resuelta en tiempo de ejecución puede cambiarse por configuración externa sin regenerar nada.

El ligado temprano produce productos más simples y verificables, a costa de flexibilidad posterior. El ligado tardío conserva flexibilidad, a costa de exigir mecanismos de configuración y validación. Por esa razón cada punto de variación debe declarar su binding time de forma explícita.

## 9. Alcance de la línea

La delimitación del alcance decide qué productos pertenecen a la línea y cuáles no. La literatura le dedica atención específica porque un alcance mal definido invalida el resto del esfuerzo: si es demasiado amplio, ningún activo sirve a todos los productos; si es demasiado estrecho, el esfuerzo de construir la línea no se justifica frente al de construir un solo producto.

**Fuente:** Clements, P. (2002). *On the Importance of Product Line Scope*, en *Software Product-Family Engineering.* Springer.

En el modelo de cuatro cuadrantes, la delimitación del alcance y el modelado de la variabilidad no son actividades separadas: ambas ocurren en el cuadrante de análisis del dominio y se informan mutuamente.

## 10. Clone-and-own

Clone-and-own designa la construcción de un producto nuevo a partir de la copia de uno existente, sin que se conserve vínculo entre la copia y el origen. La literatura lo reconoce como una forma legítima de reutilización en etapas tempranas, por su bajo costo inicial y su nula fricción de adopción.

El problema que la literatura documenta de manera característica es uno solo: **los productos clonados se separan con el tiempo.** Al no existir un mecanismo que propague los cambios, cada copia evoluciona por su cuenta, lo que incrementa el esfuerzo de propagación de cambios, de análisis de dominio y de control de calidad, y genera conflictos cuando el origen y los clones evolucionan en paralelo. El costo crece con el número de copias.

**Fuente:** Dubinsky, Y. et al. (2013). *An Exploratory Study of Cloning in Industrial Software Product Lines.* European Conference on Software Maintenance and Reengineering.

Conviene precisar el alcance de esta afirmación. La divergencia progresiva está documentada en la literatura. Otras limitaciones que pueden observarse en un contexto concreto, como la imposibilidad de incorporar una capacidad a un producto ya construido, no forman parte del diagnóstico canónico del clone-and-own y, de aparecer, constituyen hallazgos propios del trabajo de campo, no consecuencias derivables de la teoría.

## 11. Límites del modelo clásico

La teoría clásica opera sobre dos asunciones implícitas que conviene hacer explícitas, porque no todo contexto las satisface.

**El producto permanece bajo el gobierno de la línea.** En el modelo de cuatro cuadrantes no existe ningún flujo de retorno desde el producto derivado: una vez producido, queda fuera del diagrama. La teoría no contempla un producto que se entregue a un equipo autónomo que lo modifique libremente después.

**La derivación ocurre en un acto único.** El flujo de selección de características precede a la derivación y sucede una sola vez. La teoría no contempla que la selección se complete en varios momentos separados en el tiempo sobre un producto ya derivado, situación que la literatura denomina configuración por etapas.

Un trabajo cuyo contexto no satisfaga alguna de estas asunciones debe declararla como desviación explícita, en lugar de forzar el caso dentro de un esquema que no lo previó.

## 12. Correspondencia con los documentos del marco

| Concepto | Fuente | Dónde se aplica |
| :---- | :---- | :---- |
| Definición y elementos constitutivos | Clements y Northrop (2001) | MR-01, punto 2 |
| Enfoque frente a mecanismo | Clements y Northrop (2001) | MR-01, punto 1 |
| Clone-and-own | Dubinsky et al. (2013) | MR-01, punto 3 |
| Modelo de cuatro cuadrantes | Apel et al. (2013) | MR-01, punto 4 |
| Alcance de la línea | Clements (2002) | MR-01, punto 5 |
| Límites del modelo clásico | Apel et al. (2013) | MR-01, punto 6 |
| Arquitectura común de la línea | Clements y Northrop (2001) | MR-02, MR-03, MR-04 |
| Core assets | Clements y Northrop (2001) | MR-04, MR-05 |
| Feature model y binding time | Kang et al. (1990); Apel et al. (2013) | MR-01 |
| Tres actividades esenciales | Clements y Northrop (2001) | MR-05 |

**Fuentes**

Clements, P. y Northrop, L. (2001). *Software Product Lines: Practices and Patterns.* Addison-Wesley.

Clements, P. (2002). *On the Importance of Product Line Scope*, en *Software Product-Family Engineering.* Springer.

Pohl, K., Böckle, G. y van der Linden, F. (2005). *Software Product Line Engineering: Foundations, Principles and Techniques.* Springer.

Apel, S., Batory, D., Kästner, C. y Saake, G. (2013). *Feature-Oriented Software Product Lines: Concepts and Implementation.* Springer.

Kang, K. C., Cohen, S. G., Hess, J. A., Novak, W. E. y Peterson, A. S. (1990). *Feature-Oriented Domain Analysis (FODA) Feasibility Study* (CMU/SEI-90-TR-21). Software Engineering Institute, Carnegie Mellon University.

Dubinsky, Y. et al. (2013). *An Exploratory Study of Cloning in Industrial Software Product Lines.* European Conference on Software Maintenance and Reengineering.

[image1]: <MR-00_LPS_fig1_productos_arquitectura_activos.svg>
[image2]: <MR-00_LPS_fig2_dos_ciclos.svg>
[image3]: <MR-00_LPS_fig3_cuatro_cuadrantes.svg>
[image4]: <MR-00_LPS_fig4_actividades_esenciales.svg>
[image5]: <MR-00_LPS_fig5_feature_model.svg>
[image6]: <MR-00_LPS_fig6_binding_time.svg>
