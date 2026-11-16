# Variabilidad y forma del producto generado

Fija dónde vive cada elemento de un producto de la familia, qué dependencias admite y cómo se nombra cada cosa, y declara qué difiere entre un producto y otro con la precisión suficiente para que el mecanismo de derivación lo consuma sin interpretar nada. Entrega tres archivos declarativos que la herramienta lee en ejecución: el modelo de variabilidad, el espacio de selección de dominio y los grupos de negocio.

---

## 1. Estructura canónica

El proyecto se organiza primero por capa y, dentro de la capa de dominio, por agregado. Dentro de la capa, el rol que se repite tiene carpeta propia; el que no, queda a la vista en la raíz de su carpeta.

```
src/
  config/
  domain/
    shared/
    <agregado>/
      <agregado>.entity.ts
      <agregado>.repository.ts
      events/
  application/
    <operación>/
  infrastructure/
    <adaptadores agrupados por capacidad técnica>/
```

| Ubicación | Contiene |
| :---- | :---- |
| `domain/<agregado>/` | La raíz de agregado, sus entidades, sus objetos de valor y el contrato de su repositorio |
| `domain/<agregado>/events/` | Los eventos de dominio del agregado, uno por hecho de negocio |
| `domain/shared/` | Objetos de valor comunes a más de un agregado |
| `application/<operación>/` | El caso de uso de esa operación y lo que solo a ella pertenece. No contiene reglas de negocio |
| `infrastructure/` | Los adaptadores, agrupados por la capacidad técnica que realizan |
| `config/` | La lectura y validación de la configuración externalizada |

**Por qué un nivel más.** La agrupación por agregado resuelve dónde vive una capacidad; no resuelve qué pasa cuando un rol se repite. Un producto con cinco operaciones acumula cinco casos de uso hermanos, tres eventos junto a la entidad y un tipo expuesto de entrada por operación, y la forma se aplana justo donde más crece. La carpeta propia se le da al rol que multiplica, no a todos: la entidad y el repositorio del agregado siguen siendo lo primero que se ve al abrir su carpeta.

**Límite de la regla.** Fuera del dominio no hay nivel de agregado. Un producto aloja un solo bounded context, de modo que esa carpeta sería siempre una sola y no agruparía nada.

![][image1]

## 2. Reglas de dependencia

| Origen | Destino permitido |
| :---- | :---- |
| `domain` | Únicamente `domain` |
| `application` | `domain` y contratos de puerto |
| `infrastructure` | `application`, `domain`, `config` y contratos de puerto |
| `config` | Únicamente `config` |

De esas direcciones se deriva el criterio verificable: ningún elemento de `domain` importa un elemento de `application` o de `infrastructure`. El dominio no conoce el framework de aplicación, el motor de persistencia ni el protocolo de transporte.

El punto de composición queda fuera de la restricción, porque su función es unir las capas y es el único lugar que las conoce todas a la vez.

**Verificación.** La regla se comprueba por análisis estático sobre las rutas de importación, no por revisión manual. La herramienta concreta y su configuración son del doc 2 §4.

**Severidad.** La violación se reporta como error, no como advertencia. Un proyecto que la incumpla no supera su verificación. Esa severidad es la que da contenido a RNF-03: una regla que solo advierte no restringe.

## 3. Convenciones de nomenclatura

| Aspecto | Regla |
| :---- | :---- |
| Idioma | Todo el código se escribe en inglés, incluidos los nombres del dominio, que provienen del vocabulario del Service Domain |
| Identificadores | El nombre incorpora el rol del elemento como sufijo, de modo que el rol sea evidente sin conocer la ubicación del archivo |
| Archivos | Nombre en minúsculas con guiones, seguido del sufijo de rol y la extensión |

| Elemento | Archivo |
| :---- | :---- |
| Entidad | `consumer-loan.entity.ts` |
| Objeto de valor | `money.value-object.ts` |
| Contrato de repositorio | `consumer-loan.repository.ts` |
| Evento de dominio | `consumer-loan-initiated.event.ts` |
| Caso de uso | `initiate-consumer-loan.use-case.ts` |

## 4. Frontera del contrato externo

Los tipos que un adaptador de entrada expone al exterior son distintos de los objetos de dominio, y el adaptador traduce explícitamente entre unos y otros.

Son dos contratos con ciclos de vida independientes. El objeto de dominio responde a las reglas del negocio y cambia cuando esas reglas cambian; el tipo expuesto responde al acuerdo con quienes consumen el servicio y solo debe cambiar cuando ese acuerdo cambia. Si el adaptador expone el objeto de dominio, cualquier reorganización interna se convierte en un cambio incompatible para los consumidores.

La separación tiene una consecuencia que RF-04 aprovecha: los tipos expuestos, al ser explícitos, son la fuente desde la cual se deriva la documentación del contrato.

## 5. Invariantes de la familia

Un invariante no es una decisión de este punto: es una regla ya establecida que el modelo de variabilidad no puede contradecir.

| Invariante | Origen |
| :---- | :---- |
| Estructura canónica de capas y agregado | §1 |
| Reglas de dependencia y su severidad de error | §2 |
| Convenciones de nomenclatura e idioma | §3 |
| Separación entre tipos expuestos y objetos de dominio | §4 |
| Un bounded context por producto | MR-02 §3 |
| Metadato de dominio obligatorio | MR-02 §3 |
| Configuración externalizada sin valores fijos | RNF-05 |

A ellos se suman tres valores que la fase declara fijos, y que por eso no son puntos de variación.

**Lenguaje y gestor de paquetes: TypeScript y npm.** Hacer variable el gestor obligaría a ramificar la plantilla en el archivo de bloqueo, en la configuración del registro privado y en la documentación, multiplicando los caminos a verificar. La homogeneidad es, además, el objeto de la línea.

**Protocolo del adaptador de entrada: REST.** La regla de dependencia garantiza que el núcleo no conoce el protocolo, de modo que incorporar otros es agregar adaptadores sin tocar el dominio. Queda como punto de extensión.

**Procedencia de los adaptadores iniciales: la plantilla.** La regla que impide puertos sin adaptador haría inejecutable un producto que dependiera de un módulo no instalado, y la condición de llegada de la fase exige que el producto arranque sin edición previa.

## 6. Clases de variabilidad

| Clase | Qué resuelve | Forma de la decisión |
| :---- | :---- | :---- |
| Identidad | Qué representa el producto y cómo se nombra | Un valor escrito o elegido |
| Selección | Qué capacidades del dominio incorpora | Un subconjunto de un conjunto declarado, o de los términos del estándar cuando la capacidad se declara |
| Presencia | Qué piezas opcionales se incluyen | Inclusión u omisión |

La clase de selección sitúa este modelo en el cuadrante de análisis de requerimientos de la aplicación: es el punto donde quien deriva elige características y no solo nombra lo que se genera.

## 7. Espacio de selección de dominio

El Service Domain no se escribe libremente: se elige de un conjunto declarado en `service-landscape.json`. La escritura libre dejaría el metadato de dominio sin validación posible y convertiría la alineación con el estándar en una afirmación no verificable.

Cada entrada describe una capacidad de negocio del estándar. Los campos son el contrato del archivo, y es lo que el esquema hace exigible.

| Campo | Qué aporta |
| :---- | :---- |
| `businessArea`, `businessDomain` | Clasificación superior y agrupación; se registran como metadato del producto |
| `serviceDomain` | Identidad del bounded context |
| `plainName`, `plainDescription` | La capacidad en lenguaje de negocio, que es lo primero que se lee al elegir. Redacción propia de la línea |
| `description` | Qué modela la capacidad, transcrito de su documento publicado |
| `controlRecord` | Entidad de información que el Service Domain gobierna |
| `suggestedAggregate` | Valor por defecto del nombre del agregado, en PascalCase |
| `operations[]` | Las operaciones de nivel control record, cada una con `id`, `actionTerm`, `name`, `plainDescription` y `mutates` |
| `behaviorQualifiers[]` | Las subdivisiones del control record sobre las que el estándar publica operaciones propias, con la misma forma |

*Archivo: `src/domain-space/service-landscape.json` — la entrada de `Party Reference Data Directory`, la más corta y la única sin behavior qualifiers*

```json
{
  "businessArea": "Sales and Service",
  "businessDomain": "Customer Management",
  "serviceDomain": "Party Reference Data Directory",
  "plainName": "Customer directory",
  "description": "Handles the reference data of a party: its identification and the basic information that describes it to the institution.",
  "plainDescription": "The record of who a customer is: how they are identified and the basic data that describes them.",
  "controlRecord": "Party Reference Data Directory Entry",
  "suggestedAggregate": "PartyReference",
  "operations": [
    {
      "id": "initiate",
      "actionTerm": "Initiate",
      "name": "Initiate Party Reference Data Directory Entry",
      "plainDescription": "Open one",
      "mutates": true
    },
    {
      "id": "retrieve",
      "actionTerm": "Retrieve",
      "name": "Retrieve Party Reference Data Directory Entry",
      "plainDescription": "Look one up",
      "mutates": false
    }
  ]
}
```

La descripción en lenguaje llano no es ornamental: el análisis cualitativo registró que el estándar no está en uso en el contexto, de modo que un identificador sin explicación no permitiría elegir con criterio.

**Los nueve grupos que una capacidad declarada puede elegir**, en `business-domains.json`, con su área derivada.

| Business domain | Business area |
| :-- | :-- |
| Customer Management · Sales · Servicing · Cross Channel | Sales and Service |
| Loans and Deposits · Payments · Account Management · Operational Services · Collateral Administration | Operations and Execution |

El Business Area **no se pregunta**: se lee del grupo. Eso es lo que impide que un producto responda las dos cosas por separado y se contradiga con el estándar. Los nueve llevan además una glosa en lenguaje de negocio en el archivo, para que el grupo se elija sin leer el estándar.

**La excepción que el marco admite.** MR-02 §3 permite declarar un Service Domain fuera del espacio por defecto registrando el Business Domain que lo contiene, y prohíbe solo omitir el metadato. Está implementado: una capacidad declarada elige su grupo entre los nueve, escribe su nombre y el de la entidad que gobierna, y el registro del producto la marca con `declaredOutsideCatalog`.

**Alcance y límite del dato.** El archivo contiene cinco entradas, y de ellas solo `Term Deposit` está transcrita de su documento oficial publicado. Las otras cuatro conservan la descripción parafraseada con la que entraron, sus operaciones sin verificar contra el documento y ningún behavior qualifier, porque la extracción se hizo de las vistas del landscape, que no los dan. Inventarlas está prohibido, así que el hueco queda declarado en lugar de rellenado. El resto del subconjunto se incorpora sin cambio en el formato ni en la herramienta.

## 8. Puntos de variación

Trece puntos en cuatro etapas. El archivo es `variability-model.json`, y su esquema declara qué campos admite cada uno.

| Identificador | Etapa | Clase | Obligatorio | Valores | Por defecto |
| :---- | :---- | :---- | :---- | :---- | :---- |
| `serviceDomain` | Capability | Identidad | Sí | Entrada del espacio de selección, o una capacidad declarada | — |
| `businessDomain` | Capability | Identidad | Sí | Uno de los nueve Business Domains | — |
| `capabilityName` | Capability | Identidad | Sí | Nombre, cada palabra capitalizada | — |
| `controlRecordName` | Capability | Identidad | Sí | Nombre, cada palabra capitalizada | — |
| `aggregateName` | Capability | Identidad | Sí | Identificador en PascalCase | `suggestedAggregate` de la entrada |
| `operations` | Surface | Selección | Sí, al menos una | Subconjunto de `operations` de la entrada | Todas |
| `qualifierOperations` | Surface | Selección | No | Subconjunto de las operaciones de sus behavior qualifiers | Ninguna |
| `projectName` | Project | Identidad | Sí | Cadena en kebab-case | — |
| `description` | Project | Identidad | Sí | Texto breve | — |
| `owner` | Project | Identidad | Sí | Equipo responsable | — |
| `authorEmail` | Project | Identidad | Sí | Dirección de correo | — |
| `domainEvents` | Options | Presencia | No | Booleano | `true` |
| `sampleTests` | Options | Presencia | No | Booleano | `true` |

**Cinco de los trece no siempre se ofrecen**, y la condición vive en el modelo y no en el código.

| Punto | Se ofrece |
| :---- | :---- |
| `businessDomain`, `capabilityName`, `controlRecordName` | Solo si la capacidad se declara fuera del catálogo |
| `qualifierOperations` | Solo si la capacidad declara behavior qualifiers |
| `domainEvents` | Solo si alguna operación seleccionada modifica estado |

El nombre del proyecto es también el nombre de su paquete. El producto derivado no se publica en ningún registro, por lo que no lleva espacio de nombres.

**La forma de un punto de variación es la decisión de este documento.** Lo que un punto declara es lo que la herramienta puede hacer con él sin conocerlo: de dónde salen sus opciones, qué condición debe cumplir su valor, qué produce y bajo qué regla se ofrece.

*Archivo: `src/model/variability-model.json`, un punto de cada clase*

```json
{
  "id": "aggregateName",
  "class": "identity",
  "type": "string",
  "required": true,
  "stage": "Capability",
  "prompt": "Name of the root aggregate",
  "defaultFrom": "serviceDomain.suggestedAggregate",
  "validation": {
    "pattern": "^[A-Z][A-Za-z0-9]*$",
    "maxLength": 40,
    "format": "PascalCase",
    "example": "TermDeposit"
  },
  "affects": ["src/domain/<aggregate>/", "<aggregate>.entity.ts", "<aggregate>.repository.ts"]
}
```

El campo `affects` es lo que convierte el modelo en evidencia: enumera qué produce cada punto, y es contra eso que se verifica el criterio de aceptación de RF-02 sin inspeccionar el código del generador.

**Papel de los esquemas.** Un esquema no lo lee quien deriva ni interviene en la derivación: declara qué campos son obligatorios, de qué tipo es cada uno y qué valores admite. Su función es que un error de transcripción se detecte al construir la herramienta, señalando la entrada y el campo, y no al derivar un producto, cuando el efecto es un proyecto mal generado. Hace cumplir además dos reglas condicionales: un punto de tipo `selection` o `multi-select` exige `source`, y un punto de clase `presence` debe ser booleano y traer `default`. La condición `additionalProperties: false` es deliberada: un campo escrito con un nombre equivocado se detecta como error en lugar de ignorarse en silencio.

**Formato.** Los tres artefactos se declaran en JSON, el mismo formato del manifiesto del catálogo. La uniformidad evita que la herramienta interprete dos lenguajes declarativos, permite validar todo con el mismo mecanismo y no agrega dependencias de análisis. Sus textos están en inglés, como todo el contenido de los repositorios de código.

**Consecuencia asumida.** Ampliar el espacio de selección exige publicar una versión nueva de la herramienta. A cambio, la derivación no depende de ningún servicio externo ni de conectividad.

**Qué queda por mover, declarado como punto de extensión.** El modelo de variabilidad es de la herramienta, y con más de una familia de plantillas tendría que ser de cada plantilla: hoy una plantilla puede referirse a él pero no reemplazarlo. Lo mismo vale para los nombres que el estándar impone sobre una operación, que son el último trozo de lógica del estándar dentro de la herramienta. Moverlos exige transforms encadenados en el motor, que el de hoy no tiene.

![][image2]

## 9. Validación y normalización

Cada valor se valida contra su patrón y se normaliza a las formas que las convenciones de §3 exigen. La normalización ocurre una sola vez, antes de ensamblar, de modo que las plantillas no transformen cadenas.

**La condición se declara, el mensaje se explica.** Un punto declara su condición como expresión regular, que es lo que la herramienta comprueba, y declara además dos campos para quien la lee: `format`, el nombre de la forma, y `example`, un valor que la satisface. El rechazo dice la forma, el ejemplo y lo que llegó, en lugar de imprimir la expresión; y el ejemplo viaja con la pregunta, de modo que la ayuda lo muestra antes del intento.

| Valor de entrada | Forma derivada | Dónde se usa |
| :---- | :---- | :---- |
| `aggregateName: TermDeposit` | PascalCase: `TermDeposit` | Clases, tipos, nombres de símbolo |
| | kebab-case: `term-deposit` | Directorios y nombres de archivo |
| | camelCase: `termDeposit` | Identificadores de variable y parámetro |
| | plural en kebab: `term-deposits` | Base de las rutas |
| `operations[].id: execute-interest` del qualifier `Interest` | PascalCase con el agregado intercalado: `ExecuteTermDepositInterest` | Nombre del caso de uso, y en kebab-case el de su archivo |

## 10. Qué produce cada operación seleccionada

Cada operación produce un recorrido completo desde la superficie externa hasta el contrato del repositorio.

| Elemento generado | Capa | Multiplicidad |
| :---- | :---- | :---- |
| Caso de uso | `application` | Uno por operación seleccionada |
| Tipo expuesto de entrada | `infrastructure/http` | Uno por operación que recibe datos |
| Tipo expuesto de salida | `infrastructure/http` | Uno por agregado |
| Método del controlador y su ruta | `infrastructure/http` | Uno por operación seleccionada |
| Método del contrato del repositorio | `domain` | La unión de los métodos que las operaciones seleccionadas necesitan |
| Evento de dominio | `domain` | Uno por operación con `mutates: true`, si el producto incluye eventos |

**La forma de la ruta.** La base es el agregado en plural y en kebab. El término de acción vive en el método HTTP y en el documento de la API, nunca en la ruta. Una operación de behavior qualifier anida bajo el recurso de su control record.

| Operación | Ruta |
| :---- | :---- |
| `Initiate` | `POST /term-deposits` |
| `Update` | `PATCH /term-deposits/:id` |
| `Retrieve` | `GET /term-deposits/:id` |
| `Control` | `POST /term-deposits/:id/control` |
| `Execute` con calificador | `POST /term-deposits/:id/<calificador en plural>` |
| `Interest.retrieve` | `GET /term-deposits/:id/interests/:interestId` |
| `Interest.execute` | `POST /term-deposits/:id/interests/:interestId/execute` |
| `Charge.initiate` | `POST /term-deposits/:id/charges`, sin el segundo identificador porque lo crea |

El parámetro del control record se llama `:id` y no como el estándar lo escribe: la estructura y los términos de acción son del estándar, y el nombre del parámetro es local al producto.

**Por qué una sola forma de ruta.** La forma que el estándar publica —segmentos capitalizados y el término de acción como último segmento— existió como punto de variación y se retiró. El costo de un punto de variación no es el código que lo implementa: es que cada documento gana una columna, cada tabla de rutas se escribe dos veces, el circuito deriva un producto más, y quien adopta la herramienta tiene que decidir en su primera semana algo que no sabe decidir. Y el estándar no gobierna la URL en este marco, sino el dominio: el agregado sale del control record, los casos de uso y los eventos se nombran con el término de acción, y el documento OpenAPI lleva el `operationId` del término y los tags de los dos niveles. **La trazabilidad vivía en el documento de la API, no en la URL**, y es lo que vuelve barata esa decisión. Lo que se pierde es comparar las URLs carácter a carácter con el documento publicado del Service Domain, que lo necesita quien implementa el estándar como contrato de interoperabilidad entre entidades y no quien construye un servicio interno.

**Lo que el mecanismo no genera.** El contrato del repositorio declara la unión de los métodos que las operaciones necesitan —`save` si alguna muta, `findById` si alguna consulta o muta—, no uno por operación. En `Execute` y en `Control` el efecto sobre el agregado queda marcado con un comentario y no se inventa: depende de la capacidad de negocio, que el modelo no declara.

**Recorte declarado.** Los términos de acción `Request`, `Exchange`, `Notify` y `Evaluate` no se derivan: ninguna entrada del espacio de selección los usa, y una plantilla sin un caso que la ejercite sería código no verificado. Si una entrada futura los declara, la herramienta falla al resolver la entrada nombrando el término no soportado, en lugar de generar un producto incompleto.

## 11. Eventos de dominio

La inclusión produce la clase base `DomainEvent` en `domain/shared/`, el puerto de publicación declarado en el artefacto de contratos, su adaptador en proceso en `infrastructure/events/`, y un evento por cada operación con `mutates: true`.

Se ofrece como pieza opcional porque un producto cuyas operaciones solo consultan información no tiene hechos de negocio que publicar, y generar en ese caso un puerto sin emisor dejaría en el producto una declaración sin uso. La regla `events-require-mutation` expresa esa condición.

## 12. Reglas del modelo

| Regla | Tipo | Expresión en el modelo |
| :---- | :---- | :---- |
| Al menos una operación | Obligatoriedad | `at-least-one-operation` |
| Operaciones condicionadas al Service Domain | Dependencia | `operations.source = serviceDomain.operations` |
| Operaciones de qualifier condicionadas al Service Domain | Dependencia | `qualifierOperations.source = serviceDomain.behaviorQualifiers` |
| Agregado condicionado al Service Domain | Dependencia | `aggregateName.defaultFrom` |
| Eventos condicionados a operaciones que modifican estado | Dependencia | `events-require-mutation` |
| Business Domain, nombre de capacidad y entidad gobernada, solo para una capacidad declarada | Dependencia | `declared-businessdomain`, `declared-capabilityname`, `declared-controlrecordname` |

Las reglas residen en el modelo y no en el código del generador. Esa separación es lo que permitió ampliar la variabilidad en la Fase 3 sin modificar la herramienta.

## 13. Entrada resuelta

La resolución del modelo produce un documento que el mecanismo de derivación consume, y que se admite también como entrada de la vía no interactiva, de modo que la ejecución asistida y la automatizada consuman la misma forma. Es el artefacto que hace verificable el determinismo de RF-05: dos ejecuciones con la misma entrada resuelta producen estructuras equivalentes.

*Archivo que recibe la operación de generación en su vía no interactiva*

```json
{
  "schemaVersion": "1.0",
  "projectName": "term-deposit-api",
  "description": "Servicio de apertura y gestión de depósitos a término.",
  "owner": "Laboratorio Digital",
  "authorEmail": "persona@ejemplo.co",
  "domain": {
    "businessArea": "Operations and Execution",
    "businessDomain": "Loans and Deposits",
    "serviceDomain": "Term Deposit",
    "controlRecord": "Term Deposit Facility",
    "declaredOutsideCatalog": false
  },
  "aggregateName": "TermDeposit",
  "operations": ["initiate", "update", "retrieve", "control"],
  "qualifierOperations": ["Interest.retrieve", "Interest.execute"],
  "domainEvents": true,
  "sampleTests": true
}
```

**Recorrido de una resolución.** Los puntos se resuelven en el orden declarado. `projectName` se valida contra su patrón. `serviceDomain` se resuelve contra el espacio de selección y fija la entrada de dominio; a partir de ella, `aggregateName` toma su valor por defecto de `suggestedAggregate` y `operations` ofrece únicamente las operaciones que esa entrada declara. `domainEvents` se ofrece solo si alguna operación seleccionada muta, según su `offerWhen`. El resultado no conserva opciones ni valores por defecto pendientes: cada punto aparece con un valor único y normalizado.

Tres propiedades del recorrido, que son de la resolución y no de la pantalla:

- **Lo que la pregunta no acepta se rechaza en la pregunta**, que queda abierta, con la forma, el ejemplo y lo recibido. Vale también para una selección múltiple por debajo de su mínimo. Lo obligatorio se comprueba sobre lo escrito, de modo que una respuesta vacía no pasa en un punto que no declara patrón.
- **La tecla de escape retrocede una pregunta** y, cuando no queda ninguna atrás, sale. Retroceder vuelve a la última pregunta realmente hecha —no a un punto que respondió una bandera— y olvida lo que dependía de ella. En la revisión final la tecla sale, porque es la última pantalla y la revisión ya ofrece algo mejor que un paso atrás.
- **Cancelar no es un fallo de la herramienta**: las dos salidas escriben `Cancelled. Nothing was written.` y terminan con el código que un shell usa para un comando interrumpido.

**La plantilla se decide antes de la primera pregunta del modelo**, porque lo que se deriva decide qué es el producto; con eso, un rechazo por plantilla o por catálogo ilegible llega antes de que nadie escriba nada. Si la invocación no la nombra, se pregunta, con una opción por plantilla ofrecida. Fuera de una terminal nada de esto aplica: no hay preguntas que rechazar ni teclas que leer, y el rechazo es el de siempre.

**Límite asumido.** La tecla de escape en la primera pregunta del modelo sale del comando y no vuelve a la pregunta de la plantilla, porque ésa es su propio acto antes del cuestionario y el resolvedor del núcleo conoce solo este modelo. Hacerle aceptar una pregunta que no es un punto de variación acoplaría el núcleo al catálogo por una tecla. El día que una plantilla traiga su propio modelo de variabilidad, elegirla pasa a ser la primera pregunta del cuestionario y el límite se va solo.

[image1]: <../Insumos/Diagramas/MG-01_fig1_estructura_canonica.svg>
[image2]: <../Insumos/Diagramas/MG-01_fig2_modelo_caracteristicas.svg>
