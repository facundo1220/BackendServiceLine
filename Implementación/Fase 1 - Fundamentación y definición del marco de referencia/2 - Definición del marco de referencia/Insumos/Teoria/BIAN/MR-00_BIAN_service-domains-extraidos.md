# Service Domains de BIAN v14.0 extraídos del portal

Las capacidades de negocio del Service Landscape de BIAN extraídas de su fuente oficial, con el método de extracción escrito para poder repetirlo. Existe porque el insumo de teoría solo trae los nombres y la jerarquía, y el espacio de selección de la herramienta necesita la descripción, el control record y las operaciones de cada capacidad.

## 1. De dónde sale este dato

La extracción, hecha el **2026-11-02**, de los datos que el portal público de BIAN publica para los
Service Domains del subconjunto candidato de `MR-00_Teoria_BIAN.md` §8: su descripción, su control
record y sus operaciones con el action term de cada una.

Existe porque §8 solo tiene los nombres, y esos tres campos eran el pendiente que el log de ADR de
esta fase registraba como «falta extraer los Service Domains del portal». Queda acá para que la
extracción no se repita: completar una entrada del espacio de selección es copiar de estas tablas.

**Qué no es.** No es el espacio de selección. Al cierre de esta extracción el espacio tiene cinco
entradas, y las demás están acá porque están extraídas, no porque vayan a entrar. §8 lo dice: el
subconjunto es orientativo y se amplía conforme el laboratorio construya productos.

## Cómo se obtuvo, para poder repetirlo

Las vistas del Service Landscape —`view_54081`, `view_54486`, `view_54054`— dan solo nombres y
jerarquía. Las páginas por Service Domain (`object_NN.html?object=<id>`) se arman con JavaScript, así
que no se pueden leer con una herramienta que baje la página. El dato está en los archivos que esa
página carga:

```
https://bian.org/servicelandscape-14-0-0/data/all_objects_data_<1..47>.js   128.270 objetos
https://bian.org/servicelandscape-14-0-0/data/all_objects_relations.js      relaciones
```

Son JavaScript con un único objeto literal asignado a una variable; se parsean recortando desde la
primera llave. La cadena del modelo es:

```
Capability (Service Domain) --realized by--> Business service  (operación)
                           --realized by--> Business object   (entidades que gobierna)
Business service           --accesses-----> Business object
Capability                 --is part of---> Capability        (Business Domain)
```

**El action term va en un prefijo de dos letras** del nombre de la operación, seguido del nivel al
que opera: `CR` para el control record, `BQ` para un behavior qualifier. Los prefijos, verificados
contra nombres reales del portal:

| Prefijo | Action term | Prefijo | Action term |
| :-- | :-- | :-- | :-- |
| `In` | Initiate | `Rq` | Request |
| `Up` | Update | `Ex` | Exchange |
| `Re` | Retrieve | `No` | Notify |
| `Ec` | Execute | `Ev` | Evaluate |
| `Co` | Control | `Cr` | Create |
| `Gr` | Grant | `Ca` | Capture |
| `Pr` | Provide | | |

**La regla del control record.** Es el Business object que acceden las operaciones marcadas `CR`. Esa
es la definición del estándar y es la única que no falla. Una regla aparentemente equivalente —tomar
el objeto que nombra los servicios `_Invocation` o `_Instantiation`— da un valor equivocado en varios
casos: para `Consumer Loan` devuelve `Consumer Loan` en lugar de `Consumer Loan Facility`.

**Lo que la extracción corrigió.** Tres datos del proyecto que contradecían al estándar:

| Dónde | Decía | Dice v14.0 |
| :-- | :-- | :-- |
| `service-landscape.json`, Term Deposit | control record `Term Deposit Arrangement` | **`Term Deposit Facility`** |
| `service-landscape.json`, Party Reference Data Directory | `Reference Data / Party` | **`Sales and Service / Customer Management`** |
| MR-02 y la tesis | diez Business Domains, con `Party` entre ellos | **nueve**: `Party` solo contiene `Party Routing Profile` y `Legal Entity Directory`, que el laboratorio no modela |

## El alcance de la derivación, que acota qué operaciones sirven

El estándar define nueve action terms y **esta release de la herramienta deriva cinco**: `Initiate`,
`Update`, `Retrieve`, `Execute` y `Control`. Las tablas de abajo listan las cinco en la columna de
operaciones, y las demás aparte, para que ampliar la derivación sea un trabajo con su lista hecha.

Solo se listan operaciones de nivel `CR`. Las de nivel `BQ` son de los behavior qualifiers del
Service Domain, un nivel por debajo del agregado raíz que el mecanismo genera.

## Las 46 capacidades del subconjunto

**41 completas** y 5 sin operaciones de nivel `CR` en v14.0.
Las que están hoy en el espacio de selección van marcadas.

### Sales and Service

**Cross Channel**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Contact Handler** | Customer Contact Operating Session | `ContactHandler` | initiate, update, retrieve, execute, control | Exchange, Request |
| **Party Authentication** | Party Authentication Assessment | `PartyAuthentication` | update, retrieve, execute | Evaluate, Exchange, Grant, Request |
| **Service Directory** | Service Directory Entry | `ServiceDirectory` | initiate, update, retrieve, execute, control | — |
| **Session Dialogue** | Customer Contact Session Procedure | `SessionDialogue` | initiate, update, retrieve, execute, control | — |
| **Transaction Authorization** | Interactive Transaction Assessment | `TransactionAuthorization` | update, retrieve, execute | Evaluate, Exchange, Grant, Request |

**Customer Management**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Customer Access Entitlement** | Customer Access Profile Agreement | `CustomerAccessEntitlement` | update, retrieve, execute, control | Evaluate, Grant, Request |
| **Customer Agreement** | Customer Agreement | `CustomerAgreement` | update, retrieve, control | Evaluate, Request |
| **Customer Consent** | Customer Mandate Agreement | `CustomerConsent` | — | — |
| **Customer Credit Rating** | Customer Credit Rating State | `CustomerCreditRating` | initiate, retrieve, execute, control | Exchange, Request |
| **Customer Event History** | Customer Event Log | `CustomerEventHistory` | initiate, update, retrieve, control | — |
| **Customer Financial Insights** | Customer Financial Position Analysis | `CustomerFinancialInsights` | retrieve | — |
| **Customer Product And Service Eligibility** | Customer Eligibility Assessment | `CustomerProductAndServiceEligibility` | update, retrieve, execute | Evaluate, Exchange, Grant, Request |
| **Customer Relationship Management** | Customer Relationship Management Plan | `CustomerRelationshipManagement` | update, retrieve, execute, control | Create, Grant, Request |
| **Party Reference Data Directory** · en el espacio | Party Reference Data Directory Entry | `PartyReferenceDataDirectory` | initiate, update, retrieve, execute, control | Exchange, Request |

**Sales**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Customer Offer** | Customer Offer Procedure | `CustomerOffer` | initiate, update, retrieve, execute, control | Exchange, Request |
| **Lead and Opportunity Management** | Leadand Opportunity Procedure | `LeadAndOpportunityManagement` | initiate, update, retrieve, execute, control | — |
| **Party Lifecycle Management** | Party Relationship Administrative Plan | `PartyLifecycleManagement` | initiate, update, retrieve, execute, control | Exchange, Request |
| **Product Matching** | Product to Customer Combination Assessment | `ProductMatching` | update, retrieve, execute | Evaluate, Exchange, Grant, Request |
| **Underwriting** | Underwriting Assessment | `Underwriting` | update, retrieve, execute | Evaluate, Exchange, Grant, Request |

**Servicing**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Customer Case** | Customer Case Procedure | `CustomerCase` | initiate, update, retrieve, execute, control | Exchange, Request |
| **Customer Case Management** | Customer Case Management Plan | `CustomerCaseManagement` | update, retrieve, execute | Create, Request |
| **Payment Order Initiation** | Payment Order Initiation Transaction | `PaymentOrderInitiation` | initiate, update, retrieve | — |
| **Servicing Issue** | Servicing Issue Procedure | `ServicingIssue` | initiate, update, retrieve, execute, control | — |
| **Servicing Order** | Servicing Order Procedure | `ServicingOrder` | initiate, update, retrieve, execute, control | Exchange, Request |

### Operations and Execution

**Account Management**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Account Reconciliation** | Account Reconciliation Procedure | `AccountReconciliation` | initiate, update, retrieve, execute, control | — |
| **Customer Position** | Customer Position State | `CustomerPosition` | initiate, update, retrieve, control | Exchange, Request |
| **Fraud Evaluation** | Fraud Evaluation Assessment | `FraudEvaluation` | execute | Evaluate, Exchange, Grant, Request |
| **Transaction Engine** | Transaction Schedule Facility | `TransactionEngine` | initiate, update, retrieve, execute, control | Exchange |

**Collateral Administration**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Collateral Asset Administration** | Collateral Asset Administrative Plan | `CollateralAssetAdministration` | update, retrieve | Create |
| **Collections** | Collateral Asset Liquidation Procedure | `Collections` | initiate, update, retrieve, execute, control | Exchange, Request |
| **Party Asset Directory** | Party Asset Directory Entry | `PartyAssetDirectory` | — | — |

**Loans and Deposits**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Consumer Loan** · en el espacio | Consumer Loan Facility | `ConsumerLoan` | initiate, update, retrieve, control | — |
| **Current Account** · en el espacio | Current Account Facility | `CurrentAccount` | initiate, update, retrieve, control | — |
| **Loan** | Loan Facility | `Loan` | initiate, update, retrieve, control | — |
| **Savings Account** · en el espacio | Savings Account Facility | `SavingsAccount` | initiate, update, retrieve, control | — |
| **Standing Order** | Standing Order Facility | `StandingOrder` | initiate, update, retrieve, execute, control | — |
| **Term Deposit** · en el espacio | Term Deposit Facility | `TermDeposit` | initiate, update, retrieve, control | — |

**Operational Services**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Channel Activity History** | Channel Activity Log | `ChannelActivityHistory` | initiate, update, retrieve, control | — |
| **Customer Billing** | Customer Billing Procedure | `CustomerBilling` | initiate, update, retrieve, control | Exchange, Request |
| **Delinquent Account Handling** | Delinquent Account Procedure | `DelinquentAccountHandling` | initiate, update, retrieve, control | Exchange |
| **Disbursement** | Disbursement Transaction | `Disbursement` | initiate, update, retrieve, execute, control | Exchange, Request |

**Payments**

| Service Domain | Control record | Agregado sugerido | Operaciones derivables | Fuera del alcance |
| :-- | :-- | :-- | :-- | :-- |
| **Financial Gateway** | Financial Gateway Operating Session | `FinancialGateway` | initiate, update, retrieve, control | Request |
| **Payment Confirmation** | Payment Confirmation Procedure | `PaymentConfirmation` | — | — |
| **Payment Orchestration** | Payment Orchestration Procedure | `PaymentOrchestration` | — | — |
| **Payment Rail** | Payment Rail Operating Session | `PaymentRail` | initiate, update, retrieve, execute, control | — |
| **Payment Settlement** | Payment Settlement Procedure | `PaymentSettlement` | — | — |

## Las cinco sin operaciones de nivel CR

No es que falte extraerlas: v14.0 les define control record pero no les modela operaciones sobre él.
Para entrar al espacio de selección necesitarían una decisión sobre qué operaciones publicar.

| Service Domain | Business Domain | Control record |
| :-- | :-- | :-- |
| Customer Consent | Customer Management | Customer Mandate Agreement |
| Payment Orchestration | Payments | Payment Orchestration Procedure |
| Payment Settlement | Payments | Payment Settlement Procedure |
| Payment Confirmation | Payments | Payment Confirmation Procedure |
| Party Asset Directory | Collateral Administration | Party Asset Directory Entry |

## Descripciones

Tomadas de la categoría «1. Role Definition» de cada capacidad, recortadas a una o dos oraciones.
Son el texto del estándar, no una redacción propia.

**Customer Relationship Management.** This function handles managed customer relationships. There will typically be a customer development plan and budget/targets for higher value customers.

**Customer Agreement.** The Customer Agreement service domain captures and maintains the master legal terms of conditions in force for a customer (which as noted can be a complex multinational with many underlying product and service specific agreements).

**Customer Credit Rating.** This service domain handles the derivation and maintenance of each customer's credit rating for both consumer and corporate customers.

**Customer Consent.** This service domain administers customer consents for their preferences and constraints on accepting direct debit collection requests, request to pay against their accounts held at the bank, or preferences for credit transfer (e.g.

**Customer Product And Service Eligibility.** This Service Domain maintains a list of products and services for which a customer is eligible. This could include products and services that the customer has had in the past.

**Customer Access Entitlement.** This profile is used for servicing and fulfillment controls covering products, services and channel/device usage entitlements.

**Party Reference Data Directory.** The party reference data directory service domain maintains a potentially wide range of party reference data that might be used in any interaction between the bank and the party including relationship development, sales/marketing, servicing and product delivery.

**Customer Event History.** The service domain captures a wide range of customer events to build a comprehensive history of customer activity that can support subsequent behavioral analysis.

**Customer Financial Insights.** This service domain references the historical record of the customer's financial profile covering their account cash flows, lending and deposit position (credit) and their collateral/wealth holdings as maintained in the Customer Position service domain in order to develop financial insights.

**Customer Offer.** The Offer Management Service Domain can process offers for all types of customers and any allowed combination of product or service.

**Lead and Opportunity Management.** This service domain captures, evaluates and progresses identified lead/opportunities that may arise during customer relationship development, sales, servicing and fulfillment interactions.

**Party Lifecycle Management.** This service domain tracks the state of a party relationship with the bank from the initial checks made when establishing a new business relationship with a customer or partner and then that are performed as necessary over the duration of the relationship.

**Underwriting.** The underwriting decision considers the ability of the borrower to finance the loan based on their known cash flows and credit worthiness.

**Product Matching.** The service domain implements a decision service (that might be interactive) to isolate the preferred product(s) for which a customer is eligible in a specific servicing situation.

**Servicing Issue.** Capture, track, resolve and report on the more general customer servicing issues that may arise in the servicing center.

**Customer Case.** Case resolution tasks follow specific procedures for the type of case involved.

**Customer Case Management.** Manage customer case handling, track the effectiveness and impact of case resolution.

**Servicing Order.** The Servicing Order service domain handles the processing of a request that may impact multiple products and services and may involve processing cycles/steps and possibly have associated fees/charges.

**Payment Order Initiation.** This service domain supports payment services for consumer and business customers by capturing the payment instruction and forwarding it to Payment Orchestration to handle different types of payment transactions, both within the bank as well as with other banks through different payment schemes.

**Party Authentication.** Customer/party authentication is a cross-channel/device capability that provides identity confirmation for customers accessing the bank through any interactive channel.

**Transaction Authorization.** This service domain is used to mitigate transaction risk for interactive product and service access fulfillment and works in collaboration with customer identity authentication services.

**Session Dialogue.** The customer contact dialogue handling capability can provide highly structured orchestration to streamline a customer interaction by consolidating and presenting customer related data in context.

**Contact Handler.** BIAN defines a customer contact as the overarching structure handling a customer interaction from start to end.

**Service Directory.** This Service Domain handles the context sensitive presentation and selection of services that a customer may choose from to access the bank.

**Consumer Loan.** The consumer loan product may include different properties/features depending on a bank's preferences and policies.

**Loan.** The loan product represents a generic loan capability that may include different properties/features depending on a bank's preferences and policies.

**Current Account.** The Current Account or Demand Deposit Account as it can be called is a financial facility that represents the general checking account facility at the core of the consumer and small business banking activity.

**Savings Account.** The savings account product may share many features with a standard bank current account (e.g. standing orders, direct debits, payments and deposit services) with some constraints/limitations.

**Term Deposit.** A Term Deposit is an interest bearing account into which a customer can place a fixed amount of funds for a fixed amount of time.

**Standing Order.** Customers can issue standing orders to the bank. In most cases this is for the execution of a periodical payment, but there are other standing instructions like, sweeping balances at end of month, topping off excess funds for a current account, etc.

**Payment Orchestration.** This service domain orchestrates the execution of the payment instruction, which may involve the coordination of multiple steps depending on the type of payment instruction (e.g., credit transfer, direct debit, request to pay, etc.) and on whether it is an intrabank or inter-bank/overseas payment request.

**Payment Rail.** This Service Domain handles the operational interface with one or more external payment services or 'payment rails'.

**Payment Settlement.** This service domain performs the funds movements between the customer account and an internal bank account or holding account to ensure funds are available for interbank settlement by the Payment Rail.

**Payment Confirmation.** This service domain performs the required checks that include internal bank policies and account eligibility checks, ensuring funds availability, verifying any customer, payment rail or counterparty preferences, performing limits checks both for bank/customer/product limits as well as any counterpary specific limits, earmarking of funds in both customer's funding account and the counterparty related holding account.

**Financial Gateway.** This service domain supports the operational connections with the range of financial networks that support interbank and financial institution connectivity.

**Customer Position.** Individual products will maintain different financial views for the customer.

**Transaction Engine.** The Service Domain provides a utility/background operational support service to orchestrate a schedule of payment transaction and reporting activities for the fulfillment of certain long term instruments or structured facilities.

**Account Reconciliation.** Match, reconcile and resolve identified discrepancies between selected financial accounts in collaboration with the account 'owner' as necessary

**Fraud Evaluation.** This service domain handles the structured execution of fraud detection tests/routines that are used to identify possible fraud by detecting out of pattern behaviors.

**Disbursement.** This service domain handles the disbursement of funds typically for different loan facilities. Though typically a rather simple service it is modeled as a discrete service center as many banks handle disbursements from a specialist unit

**Delinquent Account Handling.** This service domain determines and executes strategies for eliciting payment from high risk accounts.

**Customer Billing.** This service domain provides a general customer billing service. The service domain is provided with the applicable fees and charges that are authorized for invoicing typically by a product or service fulfillment service domain.

**Channel Activity History.** This service domain captures transaction activity across multiple channels/devices to provide recent activity details (such as an attempt at a self-service product application) to influence/inform service routing.

**Collections.** Administer the recovery and/or liquidation of collateral against problem accounts

**Collateral Asset Administration.** This service domain handles the oversight, administration and confirmation of maintenance tasks associated with different types of collateral items.

**Party Asset Directory.** The Party Asset Directory maintains reference details of non-bank owned assets with which the bank may have some interest.

## Qué entra al espacio de selección, y con qué criterio

Una entrada existe cuando sirve a un propósito escrito del proyecto, no para poblar un catálogo. Al
2026-11-02 son cinco:

| Service Domain | Propósito, y dónde está escrito |
| :-- | :-- |
| Consumer Loan | El ejemplo de derivación del marco: MR-02 §6 y su figura 4 |
| Term Deposit | El caso de selección con cinco operaciones: Fase 2, doc 1 §5 |
| Party Reference Data Directory | El agregado de referencia del activo base: Fase 2, docs 2 y 3 |
| Savings Account | Una capacidad que ningún producto derivó todavía, para que el caso de estudio de la Fase 4 parta de cero |
| Current Account | Completa `Loans and Deposits` con las capacidades que el contexto construye, de modo que la línea cubra un Business Domain coherente |

**`suggestedAggregate` no es dato del estándar.** Es el valor por defecto que la herramienta ofrece, y
el PascalCase del nombre del Service Domain da nombres impracticables para los nombres largos
—`CustomerProductAndServiceEligibility`—. En el espacio de selección, `Party Reference Data Directory`
lleva `PartyReference`, elegido a mano. Las tablas de arriba traen el valor mecánico, que es un punto
de partida y no una recomendación.

## Una forma de capacidad que el espacio todavía no ejercita

Las cinco entradas actuales crean su propio control record: todas tienen `initiate`. En el subconjunto
hay capacidades que **no lo tienen** —`Customer Agreement`, `Underwriting`, `Product Matching`,
`Customer Case Management`, `Collateral Asset Administration`, `Customer Financial Insights`—, porque
el control record lo crea otra capacidad. Incorporar una de ellas ejercitaría una variabilidad que
ninguna entrada cubre hoy, y puede destapar un supuesto del activo base, que genera la fábrica
`initiate` del agregado en todos los casos. Queda anotado, no decidido.

