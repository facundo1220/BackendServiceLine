# Fundamentos teóricos de BIAN

**Documento previo a MR-02. Explica el modelo de referencia sobre el que se apoyan las decisiones de delimitación del dominio, con las fuentes que lo sustentan.**

## 1. Qué es BIAN

BIAN (Banking Industry Architecture Network) es una asociación de bancos, proveedores de tecnología y académicos que publica un modelo de referencia de la arquitectura de tecnología de información bancaria. No es software, ni una especificación ejecutable, ni un estándar de mensajería: es un vocabulario y una descomposición de capacidades acordada por la industria.

Su artefacto principal es el Service Landscape, un marco de referencia que define áreas de negocio amplias y dominios de negocio de grano más fino, dentro de los cuales se organiza la colección completa de service domains identificados.

La propia documentación de BIAN subraya una limitación que conviene tener presente desde el inicio: el Service Landscape es un marco para organizar los service domains, y no pretende representar el plano de diseño de ningún tipo de banco en particular. BIAN no describe cómo debe ser una entidad concreta; ofrece un mapa de todas las capacidades que un banco puede tener, para que cada organización ubique las suyas en él.

## 2. El Service Landscape: jerarquía de tres niveles

| Nivel | Qué representa | Cantidad en v14.0 |
| :---- | :---- | :---- |
| Business Area | Conjunto amplio de capacidades y responsabilidades. Nivel más alto de la jerarquía | 5 |
| Business Domain | Capacidad funcional de grano grueso, útil para la arquitectura bancaria estratégica | 38 |
| Service Domain | Capacidad de negocio discreta. Unidad atómica del modelo | Más de 300 |

La relación entre los tres niveles es de contención: cada nivel agrupa al siguiente hasta llegar al Service Domain, que es donde se detiene la descomposición.

![][image1]

*Figura 1. Jerarquía del Service Landscape.*

La estructura cambia entre versiones. La versión 9.1 organizaba el modelo en nueve áreas de negocio con nombres distintos, y la versión 14.0 introdujo renombramientos, eliminaciones e incorporaciones, particularmente en el área de pagos. Por esa razón toda referencia a BIAN en este trabajo debe declarar la versión empleada.

## 3. Las cinco Business Areas y sus Business Domains

| Business Area | Business Domains que contiene |
| :---- | :---- |
| Sales and Service | Channel Specific, Cross Channel, Marketing, Sales, Customer Management, Servicing |
| Reference Data | Party, External Agency, Market Data, Product Management |
| Operations and Execution | Product Specific Fulfillment, Loans and Deposits, Investment Management, Trade Banking, Wholesale Trading, Cards, Market Operations, Corporate Financing and Advisory Services, Consumer Services, Cross Product Operations, Payments, Account Management, Operational Services, Collateral Administration |
| Risk and Compliance | Bank Portfolio and Treasury, Business Analysis, Regulations and Compliance, Models |
| Business Support | IT Management, Non-IT and Non-HR Enterprise Services, Buildings Equipment and Facilities, Business Command and Control, Finance, Human Resource Management, Knowledge and Intellectual Property Management, Corporate Relations, Business Direction, Document Management and Archive |

De los 38 Business Domains, **nueve** corresponden al tipo de productos que construye el contexto de aplicación. (Corregido el 2026-11-02: decía diez. El de más era `Party`, que se creía contenedor de `Party Reference Data Directory`; el portal lo sitúa en `Customer Management` y deja a `Party` con `Party Routing Profile` y `Legal Entity Directory`, que el laboratorio no modela.) El resto cubre capacidades que la organización tiene, pero que no son objeto de los productos digitales del laboratorio.

![][image2]

*Figura 2. Mapa del Service Landscape v14.0.*

## 4. Qué es un Service Domain

Un Service Domain es el diseño conceptual de una capacidad de negocio discreta. Su alcance se define como elemental, lo que significa que si se descompone más, las partes resultantes pierden su contexto de negocio propio y pasan a ser de naturaleza utilitaria. Ejecuta su función de negocio para el ciclo de vida completo de todas sus ocurrencias.

De esa definición se derivan dos propiedades que son las que este trabajo aprovecha.

**Elementalidad.** El Service Domain marca el piso de la descomposición funcional. Descomponer por debajo de ese nivel produce piezas sin significado de negocio propio.

**No solapamiento.** Los Service Domains definen capacidades de negocio discretas y no solapadas, de lo que se sigue que la información de negocio que gobiernan es igualmente discreta y no solapada. Dos Service Domains pueden gobernar información representable con estructuras de datos similares, pero el dato en sí no es el mismo ni es compartido.

## 5. Anatomía de un Service Domain

| Elemento | Qué es |
| :---- | :---- |
| Control record | El objeto de negocio que el Service Domain gobierna y cuyo ciclo de vida administra de principio a fin |
| Behavior qualifiers | Descomposición del control record en partes y subpartes |
| Functional pattern | Patrón que determina el comportamiento del dominio. La lista es cerrada: Fulfill, Manage, Direct, Administer, Catalog, Design, Develop, Track, Analyse, Monitor, Operate, Transact, Agree Terms, Enroll, Allocate, Process, Advise, Assess, Maintain. Cada patrón trae asociado un artefacto genérico: Fulfill produce un Arrangement, Transact una Transaction, Catalog un Directory Entry, Track un Log |
| Service operations | Operaciones expresadas con verbos normalizados: Initiate, Create, Register, Activate, Update, Retrieve, Evaluate, Execute, Notify, Request, Control, Exchange, Configure, Capture, Provide, Grant, Feedback |
| Semantic API | Interfaz que expone las service operations del dominio |
| Business Object Model | Vocabulario común de objetos de negocio (Party, Product, Payment, Facility, Collateral) que garantiza que dos dominios signifiquen lo mismo al nombrar la misma entidad |

![][image3]

*Figura 3. Anatomía de un Service Domain.*

## 6. Correspondencia conceptual con Domain-Driven Design

La cercanía entre el modelo de BIAN y el vocabulario de Domain-Driven Design es la razón por la que ambos pueden convivir en un mismo marco sin competir. La correspondencia no es uniforme: opera en tres niveles de intensidad distintos, y distinguirlos evita atribuirle a BIAN un alcance que no tiene.

| Concepto BIAN | Concepto DDD equivalente | Nivel de correspondencia |
| :---- | :---- | :---- |
| Service Domain | Bounded context | Directa |
| Elementalidad del Service Domain | Criterio de granularidad del bounded context | Directa |
| No solapamiento entre Service Domains | Frontera de responsabilidad entre contextos | Directa |
| Control record | Agregado raíz | Analógica |
| Behavior qualifiers | Entidades y objetos de valor internos del agregado | Analógica |
| Service operations | Casos de uso y operaciones expuestas | Orientativa |

Las correspondencias directas fundamentan decisiones del marco. Las analógicas se emplean como guía de nomenclatura. La orientativa aporta un conjunto de verbos, no una especificación.

![][image4]

*Figura 4. Correspondencia entre BIAN y Domain-Driven Design.*

## 7. Alcance de aplicabilidad al artefacto

BIAN modela capacidades de negocio bancario. No modela infraestructura técnica de aplicaciones. Esta delimitación determina qué puede y qué no puede fundamentar en este trabajo.

| Elemento | Aplicabilidad | Razón |
| :---- | :---- | :---- |
| Service Landscape como taxonomía | Aplica | Aporta el vocabulario para identificar y nombrar el dominio del proyecto generado |
| Elementalidad y no solapamiento | Aplica | Fundamentan la regla de un bounded context por proyecto |
| Control record como referencia de nomenclatura | Aplica | Orienta el nombre del agregado raíz del esqueleto de dominio |
| Service operations | Aplica parcialmente | Puede informar la convención de nombres de casos de uso y endpoints |
| Functional patterns | No aplica | Describen comportamiento de negocio que el artefacto no implementa |
| Semantic APIs | No aplica | Son especificaciones de negocio concretas, fuera del alcance |
| Business Object Model | No aplica | Modelo de datos de negocio, fuera del alcance |

**El área Business Support no habilita el catálogo de módulos.** La Business Area de Business Support incluye un Business Domain llamado IT Management, con Service Domains como Systems Operations, System Development, Development Environment o Platform Operations. Su presencia podría sugerir que BIAN cubre las capacidades técnicas del catálogo de módulos, pero no es así: esos Service Domains modelan la gestión de tecnología del banco como capacidad de negocio, es decir, la función organizacional de operar sistemas o administrar entornos. No modelan componentes técnicos reutilizables como registro de eventos, cifrado o persistencia. El catálogo de módulos de este trabajo queda por tanto fuera del alcance de BIAN, y su gobierno corresponde al marco de referencia propio.

## 8. Service Domains candidatos para el contexto de aplicación

El contexto de aplicación atiende principalmente a microempresarios y construye productos digitales que consumen servicios del core bancario. Sobre esa base, los Service Domains de la versión 14.0 con mayor probabilidad de corresponder a productos del laboratorio son los siguientes.

| Business Domain | Service Domains candidatos |
| :---- | :---- |
| Customer Management | Customer Relationship Management, Customer Agreement, Customer Credit Rating, Customer Consent, Customer Product And Service Eligibility, Customer Access Entitlement, Party Reference Data Directory, Customer Event History, Customer Financial Insights |
| Sales | Customer Offer, Lead and Opportunity Management, Party Lifecycle Management, Underwriting, Product Matching |
| Servicing | Servicing Issue, Customer Case, Customer Case Management, Servicing Order, Payment Order Initiation |
| Cross Channel | Party Authentication, Transaction Authorization, Session Dialogue, Contact Handler, Service Directory |
| Loans and Deposits | Consumer Loan, Loan, Current Account, Savings Account, Term Deposit, Standing Order |
| Payments | Payment Orchestration, Payment Rail, Payment Settlement, Payment Confirmation, Financial Gateway |
| Account Management | Customer Position, Transaction Engine, Account Reconciliation, Fraud Evaluation |
| Operational Services | Disbursement, Delinquent Account Handling, Customer Billing, Channel Activity History |
| Collateral Administration | Collections, Collateral Asset Administration, Party Asset Directory |

Este listado es un subconjunto orientativo del Service Landscape, no una asignación definitiva. Su función es acotar el espacio de selección del metadato de dominio que el mecanismo de derivación solicita, y puede ampliarse conforme el laboratorio construya productos en áreas no contempladas aquí.

## 9. Relación con ISO 20022

BIAN e ISO 20022 operan en capas distintas y complementarias. BIAN describe capacidades de negocio y su descomposición; ISO 20022 describe los mensajes con que las instituciones financieras intercambian información. La documentación de BIAN referencia de forma creciente correspondencias hacia ISO 20022, y la versión 14.0 incorporó vínculos adicionales hacia ese estándar.

Esa relación delimita con precisión el punto de contacto: BIAN toca ISO 20022 en la capa de especificación de mensajes, que es exactamente la capa que el artefacto de este trabajo no produce. El artefacto genera estructura de proyecto y componentes técnicos transversales, no mensajería financiera.

## 10. Versión adoptada

Este trabajo adopta la versión 14.0 del Service Landscape de BIAN, consultada en el portal público de arquitectura. Toda referencia a Business Areas, Business Domains o Service Domains en los documentos del marco corresponde a esa versión.

**Fuentes**

BIAN. *BIAN Service Landscape V14.0, Matrix View.* Portal de arquitectura, versión 14.0. Disponible en `bian.org/servicelandscape-14-0-0`.

BIAN. *Architecture Overview Portal v.14.0.* Incluye BIAN Information Architecture, Control Record Model Overview, Business Object Model Overview y BIAN Metamodel Overview.

BIAN. *Practitioner's Guide* y *How To Guide — Design Concepts & Techniques.* Definiciones canónicas de Service Domain, control record y service operations.

The Open Group. *BIAN Service Landscape, Version 7.0*, en *Portfolio of Digital Open Standards.* Descripción del marco de referencia y de la jerarquía de niveles.

[image1]: <MR-00_BIAN_fig1_jerarquia.svg>
[image2]: <MR-00_BIAN_fig2_mapa_landscape.svg>
[image3]: <MR-00_BIAN_fig3_anatomia_service_domain.svg>
[image4]: <MR-00_BIAN_fig4_correspondencia_ddd.svg>
