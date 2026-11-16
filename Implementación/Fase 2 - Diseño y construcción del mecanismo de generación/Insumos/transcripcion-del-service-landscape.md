# Transcripción del subconjunto del Service Landscape

Hoja de trabajo para completar el espacio de selección de dominio con el subconjunto de Service Domains
que el contexto de aplicación necesita: de dónde sale cada dato, con qué se verifica y qué límite tiene.

**Lo que este insumo ya no dice.** Afirmaba que el detalle de cada Service Domain no se puede traer con
una herramienta de lectura de páginas y que por eso la descripción, el control record y las operaciones
son trabajo manual. La fuente que faltaba apareció después: el **documento OpenAPI publicado de cada
Service Domain**, que trae los tres campos y además los **behavior qualifiers**, el segundo nivel del
estándar. El documento oficial es hoy la única fuente admisible, y el segundo nivel ya está modelado.
`Term Deposit` está transcrito así; las otras cuatro entradas siguen parafraseadas. La forma vigente de
una entrada está en el doc 1 §7 de esta fase, transcrita del archivo real.

**Lo que sigue vigente:** el método de extracción, la regla de que ante una discrepancia sobre la
jerarquía manda el documento oficial, y el límite de los cinco action terms derivables.

## Qué es este insumo

La hoja de trabajo para completar `service-landscape.json` con el subconjunto de Service Domains que
el contexto de aplicación necesita. Hoy el archivo trae dos entradas, y por eso una demostración de
la herramienta se lee más pobre de lo que el mecanismo es: fue el hallazgo 3 de la revisión externa
del 2026-10-28, cuya causa real es de datos y no de diseño.

**Qué no es.** No es una decisión. El subconjunto ya está declarado en el marco y el formato ya está
fijado por el esquema; esto solo ordena el trabajo para que transcribir sea mecánico.

**Quién lo llena.** El autor, leyendo el portal público de BIAN v14.0. No se completa de memoria ni
por inferencia: `controlRecord` y las operaciones de un Service Domain son contenido del estándar, y
lo que se invente rompe la alineación que es el objetivo general del proyecto.

## De dónde sale el subconjunto, y verificado contra el portal

El subconjunto de capacidades candidatas lo declara `MR-00_Teoria_BIAN.md` §8. El **2026-11-02 se
verificó contra el portal público**, en la vista matriz del Service Landscape v14.0:

```
https://bian.org/servicelandscape-14-0-0/views/view_54081.html
```

**Los cuarenta y seis nombres del subconjunto existen en v14.0 y están donde §8 los pone.** La vista
confirma además a qué Business Area pertenece cada Business Domain, que es el campo que no hace falta
buscar por capacidad.

**Qué corrigió esa verificación.** El código declaraba `Party Reference Data Directory` en
`Reference Data / Party`, y el 2026-11-02 **se movió mal**: se razonó desde §3 en lugar del
portal. La vista es inequívoca en dos cosas: el Business Domain `Party` del área `Reference Data`
contiene solo `Party Routing Profile` y `Legal Entity Directory`, y `Party Reference Data Directory`
aparece bajo `Sales and Service / Customer Management`, que es exactamente donde §8 lo ponía.
**MR-00 §8 tenía razón y el código estaba mal desde antes.** Quedó corregido.

De ahí sale una regla para esta transcripción: **cuando el documento del marco y el portal
discrepan, manda el portal**, y la discrepancia se anota. Lo contrario es lo que produjo el error.

**Qué queda sin resolver de MR-00.** §3 cierra diciendo que «diez Business Domains corresponden al
tipo de productos que construye el contexto», y el subconjunto de §8 tiene **nueve** filas, que es lo
que el portal sostiene. La frase de §3 es la que está de más, no la tabla. Se ajusta al revisar ese
insumo.

## Qué falta por entrada

El esquema exige siete campos, y de los Service Domains del subconjunto solo se conoce el nombre.

| Campo | De dónde sale | Estado |
| :-- | :-- | :-- |
| `businessArea` | MR-00 §3, por el Business Domain | Se deriva de la tabla, sin consultar el portal |
| `businessDomain` | MR-00 §8, es la columna que agrupa | Se deriva de la tabla |
| `serviceDomain` | MR-00 §8 | Se deriva de la tabla |
| `description` | Portal: el propósito del Service Domain, en lenguaje de negocio | **Falta** |
| `controlRecord` | Portal: la entidad de información que el Service Domain gobierna | **Falta** |
| `suggestedAggregate` | Se escribe del `serviceDomain` en PascalCase, sin espacios | Se deriva, pero conviene revisarlo cuando el nombre es largo |
| `operations` | Portal: las service operations del Service Domain, con su action term | **Falta** |

**Qué da el portal y qué no, comprobado el 2026-11-02.** Las vistas del Service Landscape
—`view_54081`, `view_54486` y `view_54054`— dan **solo nombres y la jerarquía**: ninguna trae
descripción, control record ni operaciones. Ese detalle vive en la página de cada Service Domain
(`servicelandscape-14-0-0/object_NN.html?object=<id>`), que se arma con JavaScript, así que no se
puede traer con una herramienta de lectura de páginas: **hay que abrirla en un navegador**. Tampoco
se encontró un export público de v14.0 con control records y operaciones. Por eso los tres campos de
arriba son trabajo manual y no se pueden inferir: inferirlos es inventar contenido del estándar.

## El límite que acota qué operaciones transcribir

El esquema admite nueve action terms —`Initiate`, `Update`, `Retrieve`, `Execute`, `Request`,
`Control`, `Exchange`, `Notify`, `Evaluate`—, y **esta release deriva cinco**: `Initiate`, `Update`,
`Retrieve`, `Execute` y `Control`. Una operación declarada con uno de los otros cuatro queda
ofrecida en el espacio de selección y la derivación la rechaza al elegirla.

**Consecuencia para la transcripción.** Por ahora se transcriben solo operaciones con los cinco
términos derivables. Las demás se dejan fuera y se anotan, de modo que ampliar la derivación sea un
trabajo con su lista ya hecha y no una búsqueda de nuevo en el portal.

## Forma de una entrada

Tomada del archivo real, que es la referencia que no se desalinea:

```json
{
  "businessArea": "Operations and Execution",
  "businessDomain": "Loans and Deposits",
  "serviceDomain": "Term Deposit",
  "description": "Handles the opening and servicing of term deposits, including the master agreements that set the standard conditions with the customer.",
  "controlRecord": "Term Deposit Arrangement",
  "suggestedAggregate": "TermDeposit",
  "operations": [
    { "id": "initiate", "actionTerm": "Initiate", "name": "Initiate Term Deposit", "mutates": true },
    { "id": "retrieve", "actionTerm": "Retrieve", "name": "Retrieve Term Deposit", "mutates": false }
  ]
}
```

Reglas de forma que el esquema o el script de validación hacen cumplir:

- Todo el contenido en inglés, con los términos del estándar tal como el estándar los publica.
- `id` en kebab-case y único dentro de su Service Domain. Cuando la operación no lleva calificador,
  el `id` es el action term en minúscula (`initiate`); cuando lo lleva, es el término más el
  calificador (`execute-interest-settlement`).
- `mutates` dice si la operación cambia el estado del control record. Decide si el producto publica
  un evento de dominio para esa operación.
- `serviceDomain` tiene que ser único en todo el archivo.

## Cómo se comprueba

```bash
cd Codigo/bsl-assets
npm run verify:artifacts -w @bsl/cli
```

Valida el archivo contra su esquema con ajv y comprueba la unicidad que el esquema no puede
expresar. Después, para ver una entrada nueva funcionando de punta a punta:

```bash
npm run verify:generation -w @bsl/cli
```

**Una entrada nueva no es visible para la herramienta instalada hasta republicarla**, porque los
artefactos declarativos viajan dentro del paquete. Es el mismo efecto que el catálogo tuvo mientras la
herramienta lo resolvía por versión fija.

## Las nueve agrupaciones por transcribir

Verificadas contra la vista matriz de v14.0. Son **dos** Business Areas y **nueve** Business
Domains. Las dos entradas que ya existen quedan marcadas.

### Sales and Service · 24 Service Domains

| Business Domain | Service Domains |
| :-- | :-- |
| Customer Management | Customer Relationship Management · Customer Agreement · Customer Credit Rating · Customer Consent · Customer Product And Service Eligibility · Customer Access Entitlement · Customer Event History · Customer Financial Insights · **Party Reference Data Directory (ya está)** |
| Sales | Customer Offer · Lead and Opportunity Management · Party Lifecycle Management · Underwriting · Product Matching |
| Servicing | Servicing Issue · Customer Case · Customer Case Management · Servicing Order · Payment Order Initiation |
| Cross Channel | Party Authentication · Transaction Authorization · Session Dialogue · Contact Handler · Service Directory |

### Operations and Execution · 22 Service Domains

| Business Domain | Service Domains |
| :-- | :-- |
| Loans and Deposits | Consumer Loan · Loan · Current Account · Savings Account · Standing Order · **Term Deposit (ya está)** |
| Payments | Payment Orchestration · Payment Rail · Payment Settlement · Payment Confirmation · Financial Gateway |
| Account Management | Customer Position · Transaction Engine · Account Reconciliation · Fraud Evaluation |
| Operational Services | Disbursement · Delinquent Account Handling · Customer Billing · Channel Activity History |
| Collateral Administration | Collections · Collateral Asset Administration · Party Asset Directory |

**Cuántas son.** Cuarenta y seis, de las cuales dos están transcritas. No hace falta hacerlas todas
de una vez: cada entrada completa es utilizable por sí sola, y el síntoma del hallazgo 3 —que la
herramienta parezca servir para dos productos— desaparece alrededor de la quinta o sexta.

**Dónde conviene empezar.** Por `Loans and Deposits`, que es donde está el producto de referencia y
donde el laboratorio construye: `Current Account` y `Savings Account` comparten estructura con
`Term Deposit`, así que son las entradas más rápidas y las que mejor muestran la variabilidad.
