# Evaluación de usuario y diagnóstico técnico

  

## Resumen ejecutivo

  

La solución tiene una base técnica valiosa: permite derivar backends NestJS con una estructura consistente, contratos compartidos, separación de capas, reglas arquitectónicas, tests iniciales y trazabilidad de los assets utilizados.

  

El problema principal no es que el CLI no implemente automáticamente un producto de negocio completo. Para un bootstrap eso sería una expectativa incorrecta. El problema es que la experiencia actual puede hacer creer que seleccionar una capability equivale a obtener un producto funcional, cuando en realidad se obtiene un habilitador técnico que todavía requiere diseño de dominio, persistencia, observabilidad, documentación y evolución.

  

### Fortalezas observadas

  

- La generación produce una base ordenada y coherente.

- Los puertos y adapters aíslan decisiones técnicas.

- El producto generado conserva provenance en `project.json`.

- La arquitectura impone límites entre dominio, aplicación e infraestructura.

- El modelo declarativo evita algunas combinaciones inválidas.

- El template incluye configuración, tests, lint y build desde el inicio.

  

### Cinco riesgos principales

  

1. Confundir capability de referencia con producto de negocio terminado.

2. No distinguir placeholders de capacidades implementadas.

3. Crear productos derivados sin una estrategia clara de evolución.

4. Tener poca visibilidad operativa al arrancar y consumir el servicio.

5. Dejar ambiguo el papel de los eventos, la persistencia y la documentación.

  

### Nivel de madurez observado

  

La solución se encuentra en un nivel de **bootstrap técnico avanzado / plataforma interna temprana**. Está más madura que un template simple, pero todavía no es una plataforma productiva completa: faltan capacidades operativas, evolución de productos derivados, módulos reales de persistencia/mensajería y una experiencia más clara para usuarios no técnicos.

  

## Alcance

  

Evaluación para dos perfiles: desarrollador backend y líder estratégico/de negocio. Se basa en el CLI, el template y los proyectos generados en `poc/`, especialmente `bolsillos-w` y `user-update-flow`.

  

## Método y evidencia

  

La evaluación combina observación de uso y lectura técnica:

  

- Se inspeccionó el flujo de `bsl new`, incluyendo selección de capability, aggregate, operaciones, eventos y tests.

- Se revisaron los productos generados en `poc/`.

- Se revisaron `README.md`, `package.json`, `project.json`, controllers, casos de uso, adapters, eventos, repositorios y tests.

- Se verificó que `bolsillos-w` conserva metadata `Term Deposit`, pero usa `Bolsillo` como aggregate local.

- Se observó `InMemoryBolsilloRepository`, `InProcessEventPublisherAdapter` y el logger JSON.

- Se observó que el CLI y el landscape de capabilities son artefactos distintos del catálogo de assets.

  

### Evidencia directa versus interpretación

  

- **Evidencia directa:** el código contiene un repositorio en memoria, eventos in-process, placeholders en operaciones de control/liquidación y logger estructurado.

- **Riesgo interpretado:** un usuario podría asumir que el producto tiene persistencia, consumidores de eventos o lógica de negocio completa.

- **Recomendación:** cambiar la experiencia y documentación para que esa interpretación incorrecta sea difícil.

  

## Responsables sugeridos


| Tipo de decisión | Responsable principal |
|---|---|
| Mensajes, prompts y flujo de `bsl new` | Equipo CLI |
| Estructura, logging, health, persistencia base y tests | Equipo template |
| Nombres de capabilities y relación con estándares | Owner del landscape/catalogo |
| Contratos técnicos y compatibilidad | Equipo de plataforma |
| README, OpenAPI y documentación por audiencia | Equipo CLI + template |
| Evolución de productos ya generados | Gobernanza de la línea + equipos consumidores |

  

## 1. Estructura inicial demasiado plana

  

### Análisis

  

**Feedback:** `application/` y los eventos pueden saturarse cuando el proyecto crezca.

  

**Diagnóstico e impacto:** el generador coloca directamente casos de uso y eventos en carpetas planas. Funciona al inicio, pero no define cómo agrupar handlers, mappers, políticas, integraciones o tests de una operación compleja. Puede forzar refactors posteriores.

  

**Propuestas:**

  

1. Mantener capas y documentar un umbral de transición.

2. Agrupar operaciones complejas en subcarpetas.

3. Evolucionar hacia una estructura por feature.

  

### Sugerencia

  

**Veredicto:** mantener capas para servicios pequeños y adoptar una transición gradual por complejidad.

  

**Evaluación adversarial:** agrupar desde el inicio escala mejor, pero añade complejidad y puede ocultar la arquitectura. Mantener todo plano es simple, pero escala peor.

  

**Experiencia futura:**

  

```text

Starting structure: simple layered template

Growth guide: when a feature grows, move to application/retrieve/

and domain/bolsillo/events/ without changing the public contracts.

```

  

## 2. Feedback insuficiente del CLI

  

### Análisis

  

**Feedback:** el usuario descubrió después del error que `aggregateName` debía comenzar en mayúscula.

  

**Diagnóstico e impacto:** el modelo valida `^[A-Z][A-Za-z0-9]*$`, pero el mensaje no ofrece ejemplo ni intención. Esto produce intentos fallidos.

  

**Propuestas:**

  

1. Mejorar mensajes con formato y ejemplo válido.

2. Mostrar restricciones contextuales en prompts y `--help`.

3. Sugerir o corregir automáticamente valores seguros.

  

### Sugerencia

  

**Veredicto:** implementar primero mensajes y ejemplos; reservar autocorrección para casos no ambiguos.

  

**Evaluación adversarial:** mensajes demasiado largos saturan la terminal y autocorregir puede ocultar decisiones. Ejemplos cortos tienen bajo coste.

  

**Experiencia futura:**

  

```text

aggregateName must use PascalCase.

Example: Bolsillo or TermDeposit.

Received: bolsillo

```

  

## 3. Catálogo ligado a productos

  

### Análisis

  

**Feedback:** las pocas opciones actuales pueden hacer sentir que el CLI solo sirve para `Term Deposit` y `Party Reference`.

  

**Diagnóstico e impacto:** `service-landscape.json` mezcla estándar, capability, control record, aggregate y operaciones. Además, debe distinguirse del catálogo de assets: el landscape de capabilities vive en los artefactos del CLI, mientras que el catálogo contiene assets como `base-template` y `contracts`. El usuario puede interpretar “seleccionar producto” en lugar de “seleccionar una capacidad para generar un habilitador”.

  

**Propuestas:**

  

1. Separar estándar, capability, producto local, aggregate y servicio.

2. Presentar capabilities en lenguaje natural.

3. Permitir una capability personalizada.

  

### Sugerencia

  

**Veredicto:** separar los conceptos y mantener BIAN como referencia avanzada, no como única entrada visible.

  

**Evaluación adversarial:** agregar muchas opciones abruma; usar solo lenguaje natural puede perder precisión; capability personalizada exige validaciones más abiertas.

  

**Experiencia futura:**

  

```text

? What do you want to create?

› A service based on a business capability

A custom capability

A technical-only service

```

  

## 4. Desalineación entre capability y negocio local

  

### Análisis

  

**Feedback:** `bolsillos-w` usa aggregate `Bolsillo`, pero metadata `Term Deposit` y `Term Deposit Arrangement`.

  

**Diagnóstico e impacto:** el CLI permite cambiar el aggregate sin explicar la relación con la capability elegida. README y `project.json` pueden parecer contradictorios.

  

**Propuestas:**

  

1. Pedir confirmación cuando el nombre local difiera.

2. Registrar por separado referencia estándar, capability local, producto y aggregate.

3. Generar una explicación del mapeo en README.

  

### Sugerencia

  

**Veredicto:** combinar confirmación y metadata separada; dejar la explicación en la documentación generada.

  

**Evaluación adversarial:** advertir protege coherencia, pero añade fricción; permitir cualquier nombre es flexible, pero puede producir metadata ambigua.

  

**Experiencia futura:**

  

```text

Reference capability: Term Deposit

Local product name: Bolsillos

The local name differs from TermDeposit. Continue? Yes

```

  

## 5. Aggregate demasiado genérico

  

### Análisis

  

**Feedback:** para depósitos, `id`, `name` e `initiatedAt` parecen insuficientes.

  

**Diagnóstico e impacto:** el aggregate es una semilla técnica sin monto, moneda, estado, propietario o condiciones. Es válido, pero puede confundirse con modelo de negocio final.

  

**Propuestas:**

  

1. Mantener una semilla mínima explícita.

2. Ofrecer perfiles de dominio enriquecidos.

3. Añadir un wizard de atributos e invariantes.

  

### Sugerencia

  

**Veredicto:** mantener la semilla como default y sumar perfiles en segunda fase, sin convertir inicialmente el CLI en una herramienta completa de modelación.

  

**Evaluación adversarial:** generar atributos puede imponer supuestos incorrectos; generar solo `id/name` aporta poco valor específico; un wizard añade complejidad.

  

**Experiencia futura:**

  

```text

This aggregate is a technical seed.

Business attributes must be defined by the product team.

```

  

## 6. Bootstrap habilitador versus producto terminado

  

### Análisis

  

**Feedback:** escoger una capability puede crear expectativa de producto funcional completo.

  

**Diagnóstico e impacto:** operaciones como liquidación de intereses y control contienen placeholders. Los eventos se publican con un emitter privado sin consumidores visibles. No es un defecto que falte lógica de negocio; sí es un problema si no se explicita.

  

**Propuestas:**

  

1. Mostrar antes de generar que el resultado es un bootstrap.

2. Registrar estado por operación y evento.

3. Documentar productor, consumidores, payload y evolución.

  

### Sugerencia

  

**Veredicto:** adoptar las tres en orden: alcance, estado y documentación de eventos.

  

**Evaluación adversarial:** advertir puede hacer que parezca menos completo, pero aumenta confianza; lógica genérica automática podría crear falsa lógica de negocio.

  

**Experiencia futura:**

  

```text

Generated technical bootstrap.

Implemented operations: 1

Placeholder operations: 4

Events: in-process; no external consumers configured

```

  

### Estado observado en `bolsillos-w`

  

| Operación | Estado observado | Interpretación |
|---|---|---|
| Initiate | Implementación funcional mínima | Crea, persiste y publica un evento |
| Retrieve | Implementación funcional mínima | Consulta el repositorio en memoria |
| Update | Implementación funcional mínima | Tiene wiring, validación y persistencia base |
| Interest settlement | Esqueleto con lógica pendiente | Publica evento, pero no calcula ni modifica intereses |
| Control | Esqueleto con lógica pendiente | No aplica todavía estados o reglas de lifecycle |

  

Esta tabla indica el comportamiento observable en el PoC; no afirma que las operaciones mínimas estén listas para producción.

  

## 7. Documentación insuficiente del producto generado

  

### Análisis

  

**Feedback:** el README explica estructura y rutas, pero no estado, límites, eventos ni valor de negocio.

  

**Diagnóstico e impacto:** el usuario debe leer código para saber qué se generó y qué falta.

  

**Propuestas:**

  

1. Enriquecer README con propósito, alcance, estado y límites.

2. Generar documentos separados para backend, consumidor y negocio.

3. Añadir guía de eventos, diagramas e índice de evolución.

  

### Sugerencia

  

**Veredicto:** combinar README breve con documentación por audiencia, evitando un único manual excesivo.

  

**Evaluación adversarial:** un README excesivo puede no leerse; separar documentos mejora navegación, pero aumenta artefactos.

  

**Experiencia futura:**

  

```text

docs/

├── business-overview.md

├── consumer-guide.md

├── backend-guide.md

├── events.md

└── openapi.yaml

```

  

## 8. Falta de Swagger y prueba inmediata

  

### Análisis

  

**Feedback:** sin Swagger y ejemplos, el usuario debe leer código para consumir la API.

  

**Diagnóstico e impacto:** se listan rutas, pero no se generan OpenAPI, payloads, errores ni colección ejecutable.

  

**Propuestas:**

  

1. Generar ejemplos `curl` por defecto.

2. Generar OpenAPI/Swagger opcional.

3. Generar colección Postman o Bruno.

  

### Sugerencia

  

**Veredicto:** ejemplos ejecutables en la primera versión y OpenAPI como capability recomendada; la colección puede ser opcional.

  

**Evaluación adversarial:** Swagger describe API, no negocio; colecciones añaden valor, pero otro formato; la documentación automática debe validarse en CI.

  

**Experiencia futura:**

  

```text

OpenAPI: http://localhost:3000/docs

Consumer guide: ./docs/consumer-guide.md

Examples: ./examples/

```

  

## 9. Observabilidad y logging insuficientes

  

### Análisis

  

**Feedback:** falta ver requests, host, puerto, duración, status, errores y eventos.

  

**Diagnóstico e impacto:** existe `LoggerPort` y logger JSON, pero no logging HTTP, correlation ID, duración, status ni startup log.

  

**Propuestas:**

  

1. Añadir logging HTTP con método, ruta, status, duración y error.

2. Añadir startup log, correlation ID y métricas mínimas.

3. Preguntar nivel de verbosidad y ofrecer integración corporativa como módulo.

  

### Sugerencia

  

**Veredicto:** adoptar logging HTTP y startup log de base; dejar métricas y observabilidad corporativa para un módulo.

  

**Evaluación adversarial:** más logs pueden generar ruido o exponer datos; correlation ID requiere propagación; el logger corporativo puede necesitar otro esquema.

  

**Experiencia futura:**

  

```json

{"level":"info","message":"HTTP request completed","requestId":"req-123","method":"POST","path":"/bolsillos","statusCode":201,"durationMs":18}

```

  

## 10. Falta de health y readiness

  

### Análisis

  

**Feedback:** no hay una forma clara de saber si el servicio está vivo y listo.

  

**Diagnóstico e impacto:** no se generan `/health` ni `/ready`, dificultando integración con plataformas.

  

**Propuestas:**

  

1. Generar `/health` siempre.

2. Generar `/ready` con checks configurables.

3. Integrarlos en un módulo operativo con métricas y diagnóstico.

  

### Sugerencia

  

**Veredicto:** generar ambos endpoints desde el template y mantener checks profundos como configuración opcional.

  

**Evaluación adversarial:** checks profundos pueden fallar por dependencias opcionales; debe distinguirse proceso vivo de servicio listo.

  

**Experiencia futura:**

  

```text

GET /health -> process is alive

GET /ready -> configuration and required dependencies are available

```

  

## 11. Persistencia en memoria poco visible

  

### Análisis

  

**Feedback:** debe aclararse y, en una evolución, permitir memoria, ORM y motor de base de datos.

  

**Diagnóstico e impacto:** `InMemoryBolsilloRepository` usa un `Map`; los datos desaparecen al reiniciar. El riesgo es que parezca persistencia real.

  

**Propuestas:**

  

1. Mostrar warning en startup y README.

2. Preguntar durante `bsl new` si se desea memoria o persistencia.

3. Ofrecer ORM con SQLite u otros motores como perfiles posteriores.

  

### Sugerencia

  

**Veredicto:** adoptar el warning inmediatamente y diseñar el selector como evolución; SQLite debe presentarse como perfil local.

  

**Evaluación adversarial:** warning es barato, SQLite mejora la demo pero no es producción y un selector de ORM aumenta superficie de soporte.

  

**Experiencia futura:**

  

```text

Persistence: in-memory

Warning: data will be lost when the process stops.

```

  

## 12. Scaffold versus funcionalidad real

  

### Análisis

  

**Feedback:** debe ser evidente qué endpoint es ejemplo y cuál tiene comportamiento de negocio real.

  

**Diagnóstico e impacto:** una operación placeholder puede devolver una entidad sin modificar saldo, tasa, fecha o estado. Esto puede engañar y dificulta priorizar.

  

**Propuestas:**

  

1. Marcar operaciones como `scaffold`, `sample` o `implemented`.

2. Usar `501 Not Implemented` cuando no exista comportamiento de negocio.

3. Generar TODOs estructurados y lista de pendientes por operación.

  

### Sugerencia

  

**Veredicto:** usar metadata y documentación desde el inicio; reservar `501` para contratos que no deban simular una respuesta funcional.

  

**Evaluación adversarial:** `501` es honesto, pero reduce sensación de demo; devolver entidad es cómodo, pero engañoso.

  

**Experiencia futura:**

  

```text

POST /bolsillos/:id/interest-settlements

Status: scaffold

Business effect: not implemented

```

  

## 13. Tests planos y poca correspondencia con src

  

### Análisis

  

**Feedback:** `test/` no refleja claramente la estructura de `src/`.

  

**Diagnóstico e impacto:** tests como `test/bolsillo.entity.spec.ts` funcionan al inicio, pero pierden descubribilidad al crecer.

  

**Propuestas:**

  

1. Mantener `test/` separado y documentar una convención.

2. Reflejar `domain`, `application` e `infrastructure` dentro de `test/`.

3. Organizar por feature e incluir cobertura por capability.

  

### Sugerencia

  

**Veredicto:** mantener estructura simple en el bootstrap y evolucionar a feature al superar un umbral.

  

**Evaluación adversarial:** espejar todo puede duplicar estructura; organizar por feature requiere convenciones; reportes por capability exigen configuración.

  

**Experiencia futura:**

  

```text

test/

└── bolsillo/

├── domain/

├── application/

├── infrastructure/

└── e2e/

```

  

## 14. Falta de pruebas de integración HTTP

  

### Análisis

  

**Feedback:** aunque los endpoints sean placeholders, deben validarse para garantizar el bootstrap.

  

**Diagnóstico e impacto:** se cubren entidad y casos de uso, pero no el flujo request, validación, controller, use case, repository y response.

  

**Propuestas:**

  

1. Generar un smoke test por endpoint.

2. Añadir tests e2e completos como opción.

3. Generar colecciones o scripts de verificación local.

  

### Sugerencia

  

**Veredicto:** generar smoke tests en todos los productos; dejar e2e y colecciones como opciones.

  

**Evaluación adversarial:** smoke tests dan confianza con poco coste; e2e puede ser lento; probar placeholders valida wiring, no negocio.

  

**Experiencia futura:**

  

```text

HTTP smoke verification

✓ POST /bolsillos returns 201

✓ GET /bolsillos/:id returns 200

✓ invalid request returns 400

Note: placeholder business effects are not verified.

```

  

## Veredicto global

  

Para el desarrollador, la solución es un buen punto de partida arquitectónico, pero necesita una estrategia clara de crecimiento, persistencia, testing y observabilidad.

  

Para el líder estratégico o de negocio, el valor potencial es alto, pero la experiencia puede sobreprometer si catálogo, README y endpoints parecen representar productos completos cuando representan capacidades técnicas iniciales.

  

La mejora central es hacer visible el contrato de la generación: qué se obtiene, qué no, qué funciona, qué queda pendiente y cómo continuar.

  

## Priorización

  

| Prioridad | Problema | Impacto | Esfuerzo | Responsable sugerido |
|---|---|---:|---:|---|
| P0 | Aclarar que el resultado es bootstrap | Alto | Bajo | CLI + template |
| P0 | Mejorar feedback de validación | Medio | Bajo | CLI |
| P1 | Documentar estado de operaciones y eventos | Alto | Medio | CLI + template |
| P1 | Logging HTTP, health y readiness | Alto | Medio | Template |
| P1 | Definir evolución de productos derivados | Muy alto | Alto | Gobernanza |
| P2 | OpenAPI, colecciones y perfiles de persistencia | Medio | Medio | CLI + template |
| P2 | Rediseñar catálogo de capabilities | Alto | Alto | Owner del landscape |
  

### Alta — claridad y confianza

  

- Declarar que el resultado es bootstrap habilitador.

- Documentar placeholders, eventos y consumidores.

- Mejorar mensajes y ejemplos del CLI.

- Incorporar logging HTTP y startup log.

- Generar health/readiness.

- Hacer explícita la persistencia en memoria.

- Añadir smoke tests HTTP.

  

### Media — experiencia de plataforma

  

- Separar capability, estándar y producto.

- Enriquecer README con vistas para backend, consumidor y negocio.

- Incorporar OpenAPI/Swagger y ejemplos.

- Mejorar coherencia entre capability y aggregate.

- Definir perfiles de aggregate.

- Organizar tests por feature o espejo de `src`.

  

### Evolutiva — plataforma productiva

  

- Soportar ORM y motores de base de datos.

- Incorporar módulos de observabilidad, persistencia y mensajería.

- Definir actualización y migración de productos generados.

- Evolucionar eventos in-process hacia mensajería real.

- Administrar catálogo de capabilities y medir adopción.

  

## Roadmap

  

### Fase 1 — Claridad y confianza

  

Bootstrap explícito, mensajes guiados, README por audiencias, estado de operaciones, warning de persistencia, logging HTTP, startup log, health/readiness, ejemplos y smoke tests.

  

### Fase 2 — Experiencia de plataforma

  

OpenAPI/Swagger, documentación de eventos, capability personalizada, separación estándar/capability/producto, selector de persistencia, perfiles de aggregate y tests por feature.

  

### Fase 3 — Plataforma productiva

  

ORM y mensajería como módulos, persistencia local, observabilidad avanzada, migración de productos, catálogo administrado por capabilities y métricas de plataforma.

  

## Criterios de aceptación

  

| Área | Criterio verificable |
|---|---|
| CLI | Dado `aggregateName=bolsillo`, el error indica PascalCase, muestra un ejemplo válido y muestra el valor recibido |
| Bootstrap | El resultado informa que es técnico y lista operaciones implementadas y placeholder |
| Eventos | Cada evento documenta productor, payload, consumidores y si la publicación es solo in-process |
| Persistencia | El README y el startup log indican el adapter y si los datos sobreviven al reinicio |
| API | Se puede iniciar el servicio, entender una ruta, enviar un request válido y observar una respuesta |
| Observabilidad | Cada request registra método, ruta, status, duración y request ID |
| Health | `/health` y `/ready` distinguen proceso vivo de dependencias disponibles |
| Testing | Cada endpoint generado tiene al menos un smoke test HTTP |
| Negocio | Un líder no técnico puede explicar propósito, alcance y pendientes sin leer el código |

  

- El usuario entiende en menos de cinco minutos qué generó el CLI.

- El CLI explica restricciones antes del fallo.

- Se puede probar un endpoint sin leer el código.

- El README diferencia implementado y placeholder.

- El runtime informa host, puerto, requests y errores.

- La persistencia elegida queda visible.

- Un líder no técnico puede explicar propósito y límites.

- Un desarrollador localiza rápidamente código y tests.

- Cada evento indica si tiene consumidores reales o solo publicación local.