# Estudio comparativo de soluciones existentes

Evalúa ocho soluciones existentes contra las once necesidades que el análisis cualitativo dejó enunciadas, y extrae las tres brechas (`B-xx`) que ninguna de ellas cierra. Esas brechas son lo que justifica construir en lugar de adoptar.

## 1. Soluciones analizadas

| Solución | Categoría | Estado |
| :---- | :---- | :---- |
| Yeoman | Generador de scaffolding agnóstico | Activo en modo mantenimiento |
| Cookiecutter | Generador de proyectos desde plantillas | Activo y ampliamente adoptado |
| CLI de NestJS | Generador integrado a un framework |  Activo, herramienta actual del equipo |
| Copier | Generador con actualización de proyectos | Activo y en desarrollo |
| Cruft | Complemento de actualización sobre Cookiecutter | Activo y mantenido |
| Nx | Plataforma de monorepo con generadores | Activo y en desarrollo |
| Backstage | Plataforma de desarrollo interno | Activo, proyecto de la CNCF |
| Port | Portal de desarrollo interno gestionado | Activo, producto comercial |

## 2. Marco de evaluación

Cada eje responde a un tema documentado con evidencia de entrevistas, de modo que la comparación mide qué tan cerca está cada solución de resolver el problema real del contexto.

Se excluye T-03 por tratarse de un efecto organizacional y no de una capacidad evaluable en una herramienta.

**Bloque de generación**

| Eje, y los temas que lo originan | Qué significa cumplirlo |
| :---- | :---- |
| T-01, T-02 Generación desde plantilla | Producir un proyecto ejecutable a partir de una plantilla parametrizable, sin intervención manual |
| T-07, T-08 Contenido resuelto de origen | Que el proyecto generado traiga ya resueltas las capacidades transversales y las restricciones que hoy se descubren tarde |
| T-11 Externalización de la configuración | Que lo susceptible de cambiar quede fuera del código y lo estable no |

**Bloque de ciclo de vida**

| Eje, y los temas que lo originan | Qué significa cumplirlo |
| :---- | :---- |
| T-04, T-09 Composición de módulos en proyectos existentes | Incorporar una capacidad transversal a un proyecto ya en curso, de forma desacoplada |
| T-05 Propagación de cambios de una capacidad compartida | Que un cambio en una capacidad alcance a los proyectos que la usan sin intervenirlos uno por uno |
| T-06 Consistencia entre proyectos en el tiempo | Detectar y corregir la desviación entre proyectos generados con versiones distintas |
| T-12 Versionado y distribución | Que las capacidades y la propia herramienta evolucionen por versiones con adopción gradual |

**Bloque de adopción y gobernanza**

| Eje, y los temas que lo originan | Qué significa cumplirlo |
| :---- | :---- |
| T-10 Adaptabilidad de lo generado | Que el resultado se pueda modificar sin romper la relación con la herramienta |
| T-13 Verificabilidad | Que lo generado y la herramienta misma puedan someterse a verificación automática |
| T-14 Costo de uso | Que generar un proyecto cueste un comando o pocos comandos, sin configuración previa extensa |
| T-15 Gobernanza del catálogo | Que exista un catálogo con propiedad, control de acceso y reglas de incorporación |

## 3. Evaluación comparativa

**Escala de valoración**

| Símbolo | Significado |
| :---- | :---- |
| ● | Cubre el eje |
| ◐ | Cubre parcialmente, con limitaciones que impiden resolver la necesidad completa |
| ○ | No cubre el eje |

**Bloque de generación**

| Necesidad | Yeoman | Cookiecutter | CLI NestJS | Copier | Cruft | Nx | Backstage | Port |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| T-01, T-02 Generación desde plantilla | ● | ● | ◐ | ● | ● | ● | ● | ◐ |
| T-07, T-08 Contenido resuelto de origen | ○ | ◐ | ○ | ◐ | ◐ | ◐ | ● | ○ |
| T-11 Externalización de la configuración | ○ | ● | ○ | ● | ● | ○ | ● | ◐ |

**Bloque de ciclo de vida**

| Necesidad | Yeoman | Cookiecutter | CLI NestJS | Copier | Cruft | Nx | Backstage | Port |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| T-04, T-09 Composición de módulos en proyectos existentes | ◐ | ○ | ◐ | ○ | ○ | ● | ◐ | ○ |
| T-05 Propagación de cambios de una capacidad compartida | ○ | ○ | ○ | ◐ | ◐ | ◐ | ○ | ○ |
| T-06 Consistencia entre proyectos en el tiempo | ○ | ○ | ○ | ● | ● | ◐ | ◐ | ◐ |
| T-12 Versionado y distribución | ◐ | ◐ | ○ | ● | ● | ● | ● | ○ |

**Bloque de adopción y gobernanza**

| Necesidad | Yeoman | Cookiecutter | CLI NestJS | Copier | Cruft | Nx | Backstage | Port |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| T-10 Adaptabilidad de lo generado | ● | ● | ● | ● | ● | ● | ● | - |
| T-13 Verificabilidad | ○ | ○ | ○ | ◐ | ◐ | ◐ | ◐ | ◐ |
| T-14 Costo de uso | ● | ● | ● | ● | ● | ◐ | ○ | ◐ |
| T-15 Gobernanza del catálogo | ○ | ○ | - | ○ | ○ | ◐ | ● | ● |

## 4. Patrones de referencia

Aunque ninguna solución sirva como respuesta directa, varias aportan mecanismos concretos que constituyen insumo de diseño para el marco de referencia técnico.

| Solución | Patrón aportado | Aplicación al proyecto |
| :---- | :---- | :---- |
| Copier | Archivo de respuestas versionado en el proyecto, que registra la versión de plantilla usada | Permite saber qué versión de un módulo tiene incorporada cada proyecto |
| Copier | Actualización por reconstrucción, que reaplica los cambios del usuario sobre la versión nueva | Resuelve la tensión entre adaptar lo generado y seguir recibiendo mejoras |
| Cruft | Comprobación de desviación automatizable en integración continua | Detecta sin intervención humana qué proyectos quedan desalineados |
| Nx | Generadores que operan sobre un árbol virtual y modifican código existente | Es el mecanismo técnico que permite incorporar un módulo a un proyecto en curso |
| Nx | Migraciones asociadas a versiones de plugin | Modelo para que la actualización de un módulo aplique cambios automáticos |
| Backstage | Golden paths y catálogo con modelo de propiedad | Referencia para el catálogo de plantillas y módulos y su gobernanza |
| Port | Control de acceso, aprobaciones y evaluaciones de cumplimiento | Referencia para las reglas de incorporación al catálogo |
| Cookiecutter | Plantilla parametrizada con lógica condicional | Mecanismo de externalización de lo variable en la generación |
| CLI de NestJS | Generación que modifica el código que referencia lo generado | Precedente de integración automática dentro del framework de destino |

## 5. Brechas identificadas

Del cruce entre las ocho soluciones y los once ejes surgen tres capacidades que el contexto necesita y que ninguna herramienta del mercado resuelve.

**B-01 Incorporar un módulo a un proyecto en curso**

**Intervención:** Cuando meses después ese proyecto necesita autenticación, observabilidad o el consumo de un servicio compartido, no hay forma de incorporarlo salvo a mano.

**Solución más cercana:** Nx. Sus generadores operan sobre un árbol virtual del sistema de archivos y modifican código existente, no solo crean archivos nuevos, lo que permite añadir capacidades a un proyecto ya creado.

**Por qué no alcanza.** Su modelo exige que todos los proyectos convivan en un mismo repositorio, y el contexto estudiado trabaja con repositorios independientes por proyecto.

**B-02 Propagar el cambio de un módulo**

**En qué consiste:** Cuando una capacidad compartida cambia, el cambio debe llegar a los proyectos que la usan sin intervenir cada uno. Es el costo que la caracterización documenta en la migración del servicio de identidad.

**Solución más cercana:** Copier y Cruft. Registran en el proyecto la versión de plantilla que usó, detectan cuáles quedaron desactualizados y aplican los cambios preservando las modificaciones locales.

**Por qué no alcanza:** Su unidad es la plantilla completa del proyecto. Lo que cambió en el caso documentado fue una capacidad puntual, no la estructura, y actualizar la plantilla entera no propaga el cambio de un módulo.

**B-03 Catálogo con reglas y bajo costo de uso**

**En qué consiste:** Sostener un catálogo de plantillas y módulos exige propiedad definida, control de acceso y reglas de incorporación, sin que eso encarezca el uso diario de la herramienta.

**Solución más cercana:** Backstage y Port. Ofrecen catálogo con metadatos, modelo de propiedad, control de acceso por roles, aprobaciones y evaluaciones de cumplimiento.

**Por qué no alcanza:** Exigen desplegar, configurar y operar una aplicación propia antes de generar el primer proyecto, costo desproporcionado para un equipo de cuatro desarrolladores. En el extremo opuesto, las herramientas de un comando no tienen catálogo alguno.

