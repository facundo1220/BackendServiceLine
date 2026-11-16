# Inventario de tareas de arranque

La lista de lo que hay que hacer para llevar un proyecto backend nuevo desde la
decisión de construirlo hasta que corre en local y queda desplegable en la rama principal, con cada tarea
clasificada según qué hace hoy la línea de producto con ella. Es el instrumento de la línea base: el documento
13 lo usa para medir M3 y M4, y la Fase 4 lo usa para saber sobre qué subconjunto puede comparar.

---

## 1. De dónde sale cada fila

Dos fuentes, y ninguna otra:

- **T-01**, que enumera el trabajo del arranque tal como lo describieron los roles entrevistados: levantamiento
  de entornos, configuración de la arquitectura, componentes de infraestructura, despliegue del repositorio,
  despliegue del servicio en la nube y creación de bases de datos. T-01 también fija quién lo hace: un solo
  desarrollador, mientras el resto del equipo trabaja en otras iniciativas.
- **El activo base de la línea**, contado el 2026-11-06: 62 archivos sin contar la salida de compilación, de
  los cuales 31 en `src`, 18 en `test` y 13 de configuración en la raíz. Cada fila nombra qué archivo o archivos
  resuelven la tarea, para que la clasificación sea verificable y no una opinión.

No se usa ninguna otra fuente. En particular, el inventario no se apoya en el historial de proyectos anteriores
de la organización, que es material privado y queda fuera del expediente por la regla de confidencialidad.

## 2. Regla de clasificación

| Cubeta | Qué significa |
| :---- | :---- |
| **Cubierta** | La herramienta la resuelve completa al derivar el producto, sin intervención del equipo |
| **Parcialmente cubierta** | La herramienta entrega una parte y el equipo completa la otra, o la tarea exige incorporar un módulo del catálogo con una operación de la herramienta |
| **Fuera del alcance** | La herramienta no la toca, y la línea lo declara así |

La cubeta es una propiedad de la herramienta, no de la tarea: una fila fuera del alcance sigue siendo trabajo
que el arranque exige, y por eso se cuenta. Lo que la regla evita es sumar al beneficio de la herramienta un
trabajo que la herramienta no hace.

## 3. Grupo A — Entorno y herramientas del proyecto

Corresponde al *levantamiento de entornos* de T-01.

| # | Tarea | Qué la resuelve hoy en el activo base | Cubeta |
| :-- | :---- | :---- | :---- |
| A1 | Fijar la versión del runtime y el registro de paquetes | `.npmrc`, `npmrc`, `engines.node` en `package.json` (`>=24.9.0`) | Cubierta |
| A2 | Declarar dependencias y scripts del proyecto | `package.json`: 7 dependencias de ejecución, 18 de desarrollo y 9 scripts | Cubierta |
| A3 | Configurar el compilador | `tsconfig.json`, `tsconfig.build.json` | Cubierta |
| A4 | Configurar formato y análisis estático, con la regla de dependencia entre capas | `eslint.config.mjs` con `eslint-plugin-boundaries`, `.prettierrc` | Cubierta |
| A5 | Configurar el corredor de pruebas | `jest.config.ts`, `test/setup.ts` | Cubierta |
| A6 | Configurar el framework de aplicación | `nest-cli.json` | Cubierta |
| A7 | Declarar las variables de entorno y validarlas al arrancar | `env.example`, `src/config/config.schema.ts`, `src/config/config.ts` | Cubierta |
| A8 | Declarar qué no entra al control de versiones | `gitignore` | Cubierta |

## 4. Grupo B — Arquitectura del servicio

Corresponde a la *configuración de la arquitectura* de T-01.

| # | Tarea | Qué la resuelve hoy en el activo base | Cubeta |
| :-- | :---- | :---- | :---- |
| B1 | Establecer la estructura de carpetas por capas | Los 31 archivos de `src` distribuidos en dominio, aplicación, infraestructura y configuración | Cubierta |
| B2 | Montar el punto de composición y el arranque del servicio | `src/app.module.ts`, `src/platform.module.ts`, `src/main.ts` | Cubierta |
| B3 | Declarar los puertos técnicos y asociar sus adaptadores | `@bsl/contracts` y la asociación en `platform.module.ts` | Cubierta |
| B4 | Modelar la primera capacidad: entidad, repositorio y evento de dominio | `src/domain/` (4 archivos) | Cubierta |
| B5 | Escribir los casos de uso de esa capacidad | `src/application/` | Cubierta |
| B6 | Escribir el adaptador de entrada HTTP: controlador, request validado y response | `src/infrastructure/http/` | Cubierta |
| B7 | Publicar el documento OpenAPI del servicio | `openapi.ts`, `openapi.controller.ts` | Cubierta |
| B8 | Servir la documentación de la API como página | `api-docs.controller.ts` con el visor instalado con el producto | Cubierta |
| B9 | Publicar los eventos de dominio | `in-process-event-publisher.adapter.ts` | Cubierta |

## 5. Grupo C — Capacidades transversales

Corresponde a los *componentes de infraestructura* de T-01 y al núcleo transversal que T-09 reconoce.

| # | Tarea | Qué la resuelve hoy | Cubeta |
| :-- | :---- | :---- | :---- |
| C1 | Registrar los eventos de operación con formato, redacción y contexto de request | `src/infrastructure/logging/` (7 archivos) | Cubierta |
| C2 | Continuar la traza distribuida del llamador | `trace-context.ts`, según el estándar W3C Trace Context | Cubierta |
| C3 | Responder por todo fallo en un solo lugar | `error-handler.filter.ts`, `request-context.middleware.ts`, `request-logging.interceptor.ts` | Cubierta |
| C4 | Exponer las sondas de salud | `health.controller.ts` | Cubierta |
| C5 | Exportar las señales a un colector | El producto reporta por `TelemetryPort` y queda listo; exportar exige incorporar `@bsl/observability` con una operación de la herramienta | Parcialmente cubierta |
| C6 | Persistir el agregado | El activo base trae el adaptador en memoria; la persistencia real exige incorporar `@bsl/persistence`, y crear la base de datos es E4 | Parcialmente cubierta |
| C7 | Autenticar y autorizar las peticiones | Nada: es una capacidad del orden de crecimiento del catálogo y todavía no tiene módulo | Fuera del alcance |

## 6. Grupo D — Verificación local

Corresponde a la condición que T-13 enuncia.

| # | Tarea | Qué la resuelve hoy en el activo base | Cubeta |
| :-- | :---- | :---- | :---- |
| D1 | Escribir la suite de pruebas del esqueleto, con un caso de humo por ruta | Los 18 archivos de `test` | Cubierta |
| D2 | Poder verificar el proyecto antes de integrarlo | El script `verify`: análisis estático, pruebas y compilación | Cubierta |

## 7. Grupo E — Repositorio, integración continua y despliegue

Corresponde al *despliegue del repositorio*, al *despliegue del servicio en la nube* y a la *creación de bases
de datos* de T-01. Es el tramo que el fin declarado exige y que la herramienta no cubre.

| # | Tarea | Qué la resuelve hoy | Cubeta |
| :-- | :---- | :---- | :---- |
| E1 | Crear el repositorio en el servidor corporativo y definir sus permisos | Nada | Fuera del alcance |
| E2 | Definir la integración continua: compilación, pruebas, análisis y auditoría de dependencias | Nada: el activo base no incluye definición de pipeline | Fuera del alcance |
| E3 | Configurar el despliegue del servicio y sus ambientes | Nada | Fuera del alcance |
| E4 | Crear la base de datos, sus credenciales y su acceso desde el ambiente | Nada | Fuera del alcance |
| E5 | Enganchar las revisiones previas al push en el repositorio del producto | Nada: la línea las usa en su propio monorepo, no las instala en el producto | Fuera del alcance |

## 8. Recuento

| Cubeta | Tareas | Cuáles |
| :---- | :--: | :---- |
| Cubierta | **23** | A1 a A8, B1 a B9, C1 a C4, D1, D2 |
| Parcialmente cubierta | **2** | C5, C6 |
| Fuera del alcance | **6** | C7, E1 a E5 |
| **Total** | **31** | |

**Cómo se lee este recuento.** Veintitrés de las treinta y una tareas del arranque las resuelve la derivación de
un producto, dos exigen además incorporar un módulo del catálogo con una operación de la herramienta, y seis
siguen siendo trabajo manual del equipo. El recuento no es el beneficio: una tarea cubierta no equivale a una
tarea del mismo peso fuera del alcance, y E1 a E4 pueden costar más que varias de las cubiertas juntas. Lo que
el recuento fija es **sobre qué subconjunto puede comparar la Fase 4** sin sobreestimar.

## 9. Límites de este inventario

- Las tareas no están ponderadas por esfuerzo. El inventario cuenta, no estima: el tiempo lo aporta el
  autoreporte de M1 y M2, que es la otra fuente de la línea base.
- La granularidad es una decisión. Una fila como E3 agrupa trabajo que en otra organización serían varias, y por
  eso el recuento vale como estructura de la comparación y no como índice absoluto.
- El inventario describe el arranque de un servicio backend del tipo que la línea produce. No cubre frontend,
  ni trabajo de análisis previo, que el líder técnico señaló como el paso donde más reprocesos ocurren y que es
  anterior al inicio definido para la medición.
