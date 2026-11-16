# Fichas de las ocho soluciones analizadas

El material de campo del estudio comparativo: qué es cada solución, cómo funciona por dentro, dónde
está su límite y qué patrón aporta al proyecto. El veredicto por necesidad está en la matriz del
documento 05, que es la que se cita; acá está la lectura de la que esa matriz salió.

**Estado del arte al momento de la revisión.** Las notas de categoría y estado fechan la revisión, y
son parte del dato: una herramienta en modo mantenimiento y una en desarrollo activo no pesan igual.

| Solución | Categoría | Origen y año | Estado al revisarla | Ecosistema | Licencia |
| :-- | :-- | :-- | :-- | :-- | :-- |
| **Yeoman** | Generador de scaffolding agnóstico | Chrome DevRel, Google; 2012, estable 1.0 en 2013 | Activo **en modo mantenimiento**: relanzado en 2025 con la estabilidad como objetivo declarado, no el desarrollo de funcionalidades | Agnóstico, corre sobre Node.js | BSD-2-Clause |
| **Cookiecutter** | Generador de proyectos desde plantillas | Audrey Roy Greenfeld; ~2013 | Activo y ampliamente adoptado, con un ecosistema grande de plantillas | Construido en Python, agnóstico en lo que genera | BSD-3-Clause |
| **CLI de NestJS** | CLI de scaffolding integrada a un framework | Equipo de NestJS | Activo, parte central del framework. **Es la herramienta actual del equipo** | NestJS, sobre TypeScript y Node.js | MIT |
| **Copier** | Generador con actualización de proyectos | copier-org | Activo y en desarrollo continuo | Construido en Python, agnóstico | MIT |
| **Cruft** | Complemento de actualización sobre Cookiecutter | cruft/cruft | Activo y mantenido | Python, compatible con plantillas Cookiecutter | MIT |
| **Nx** | Plataforma de monorepo con generadores | Nrwl, hoy Nx | Activo y en desarrollo continuo, con adopción amplia | JavaScript y TypeScript, otros por plugins | MIT, con funcionalidades de pago |
| **Backstage** | Plataforma de desarrollo interno | Spotify; interno desde 2016, abierto en 2020. **Proyecto de la CNCF** | Activo, con adopción en organizaciones grandes | Node.js y React, se instala en infraestructura propia | Apache-2.0 |
| **Port** | Portal de desarrollo interno gestionado | Port, getport.io; enero de 2022 | Activo, ofrecido como servicio gestionado | Agnóstico; se conecta a lo que la organización ya tiene | **Producto comercial** con plan gratuito |

---

## Yeoman

**Cómo funciona.** Yeoman solo provee la infraestructura; el trabajo lo hacen los generadores, módulos
de Node.js publicados como `generator-<nombre>`. `yo <generador>` lanza prompts, y con las respuestas
copia archivos, crea directorios y ejecuta lógica. Hay miles de generadores de terceros.

**Dónde está su límite.** Genera una vez y olvida el proyecto: cuando el generador evoluciona no hay
forma de alcanzar lo ya creado. La calidad de cada generador depende de su autor y muchos quedan
obsoletos. Su árbol de dependencias legado produce advertencias de auditoría en proyectos recién
creados.

**Qué aporta.** Es el referente histórico del scaffolding por generadores y valida generar desde
plantillas parametrizables con prompts. Aporta el patrón de generación y no el mantenimiento del ciclo
de vida: no resuelve la actualización (T-05, T-06), no compone módulos (T-04, T-09) ni gobierna un catálogo
(T-15).

## Cookiecutter

**Cómo funciona.** Una plantilla es un directorio cuya raíz se nombra con una variable, más un
`cookiecutter.json` que declara las variables y sus valores por defecto. `cookiecutter <ruta>` pregunta
por cada una —o toma los defaults con `--no-input`— y procesa todo con **Jinja2**, sustituyendo
marcadores en el contenido y en los nombres de archivo.

**Dónde está su límite.** Genera y olvida: no hay relación entre la plantilla y el proyecto creado. No
compone módulos ni integra capacidades en proyectos existentes. Su modelo es sustitución de texto, sin
conocimiento del framework de destino: no entiende de módulos ni actualiza código existente.

**Qué aporta.** El referente maduro y agnóstico de la generación por plantillas parametrizadas, con
plantillas prescriptivas y condicionales. Aporta ese patrón; no gestiona el ciclo de vida.

## CLI de NestJS

**Cómo funciona.** Se basa en **schematics** y se invoca con `nest g <tipo> <nombre>`. Cada comando
crea los archivos del elemento y, lo destacable, **modifica el código existente para integrarlo**: al
generar un servicio actualiza el módulo correspondiente para registrarlo en sus providers. Incluye un
generador de recursos que produce un CRUD completo en un paso.

**Dónde está su límite.** Genera lo que el framework define, no lo que una organización necesita. La
estructura y las convenciones están fijadas por NestJS; no admite codificar las convenciones de un
equipo ni incorporar las capacidades transversales que se repiten entre proyectos.

**Qué aporta, y qué evidencia.** Es el punto de comparación más directo porque es la herramienta actual
del equipo. Demuestra el valor de generar componentes que además modifican el código existente para
integrarse —patrón que el proyecto retoma—, y evidencia la brecha con claridad: su plantilla es la del
framework y no la de la organización (T-07, T-08), y no compone módulos entre proyectos (T-04, T-09).

## Copier

**Cómo funciona.** Al generar guarda en el proyecto un `.copier-answers.yml` con la versión de la
plantilla —un commit de Git— y las respuestas dadas. Su capacidad distintiva es `copier update`:
reconstruye el proyecto como era con la versión anterior, calcula el diff contra el proyecto actual
para saber qué modificó el equipo, genera una versión nueva con la última plantilla y fusiona.

**Dónde está su límite.** Su unidad es la plantilla completa del proyecto, no el módulo. Resuelve
mantener N proyectos alineados con una plantilla base, y no incorporar de forma desacoplada una
capacidad transversal a un proyecto en curso. La actualización opera por diff de texto, así que un
cambio de plantilla que se solapa con una edición local produce conflicto.

**Qué aporta.** Es el precedente más directo del diferencial que el proyecto persigue: demuestra que
mantener un vínculo vivo entre plantilla y proyecto es posible y valioso. Se descarta porque su unidad
es la plantilla y no el módulo desacoplado que T-04, T-09 requiere.

## Cruft

**Cómo funciona.** Usa Cookiecutter por debajo, así que hereda su compatibilidad total con las
plantillas existentes. `cruft create` escribe un `.cruft.json` con el hash del commit de la plantilla;
`cruft check` verifica si el proyecto está al día —integrable en CI para detectar deriva— y
`cruft update` sincroniza.

**Dónde está su límite.** Comparte el modelo de Cookiecutter y sus límites: la unidad es la plantilla
completa, la actualización opera por diff y merge de texto sin comprensión semántica, y es un
complemento de un solo problema.

**Qué aporta.** Junto con Copier, es la evidencia de que el problema de propagación que la
caracterización documenta es reconocido y tiene soluciones establecidas. `cruft check` en CI y
`cruft update` son exactamente el patrón que el gestor de módulos necesita, trasladado del plano de la
plantilla al del módulo.

## Nx

**Cómo funciona.** Combina dos mecanismos. Los **executors** ejecutan build, test y lint de forma
consistente sobre cada proyecto. Los **generators**, invocados con `nx g <plugin>:<generador>`,
automatizan la creación y la modificación de código: son funciones que operan sobre un árbol virtual
del sistema de archivos, guiadas por un esquema JSON que define opciones, validaciones y prompts.

**Dónde está su límite.** Su modelo está construido alrededor del monorepo y no encaja en un esquema de
repositorios independientes por proyecto, que es el del contexto. Adoptarlo implica asumir su sistema
de construcción y su estructura de workspace completos: una decisión de plataforma, no una herramienta
acotada de arranque.

**Qué aporta.** Es la más relevante del estudio frente al problema de propagación: generadores que
modifican código existente (T-04, T-09) más migraciones que actualizan proyectos ya creados (T-05, T-06) es
el precedente más cercano a lo que el proyecto busca. Se descarta porque su valor está atado al
monorepo y a adoptar toda la plataforma.

## Backstage

**Cómo funciona.** Se instala como aplicación propia y se construye alrededor de un catálogo de
software centralizado con metadatos de servicios y componentes. Su función de generación, las
**Software Templates**, la ejecuta el **Scaffolder**: un YAML declara qué entradas pedir, qué acciones
ejecutar y qué salidas producir, y el desarrollador completa un formulario guiado.

**Dónde está su límite.** Es una plataforma, no una herramienta: hay que desplegarla, configurarla y
sostenerla como un producto interno. Su scaffolding resuelve la creación y no el ciclo de vida
posterior.

**Qué aporta.** Es el referente de estandarización del arranque a escala organizacional y de *golden
paths*: demuestra el valor de codificar plantillas curadas con gobernanza y registro central. Se
descarta por desproporción de escala frente a lo que T-14 exige.

## Port

**Cómo funciona.** Se organiza alrededor de un catálogo basado en **blueprints**, definiciones de
entidad personalizables que representan cualquier activo. Sobre el catálogo ofrece **acciones de
autoservicio**: el desarrollador ejecuta una acción y Port envía una carga con las entradas a la
infraestructura del propio equipo, donde un flujo de trabajo hace el trabajo real.

**Dónde está su límite.** No resuelve el problema técnico de generar ni de componer: es una capa de
portal, catálogo y gobernanza **sobre** una capacidad de generación que el equipo debe construir. Fuera
de la caja es un contenedor vacío.

**Qué aporta.** El modelo de gobernanza (T-15) —catálogo, control de acceso, aprobaciones y
evaluaciones de cumplimiento— como referencia para administrar un catálogo de plantillas y módulos con
reglas claras. Se descarta porque delega el núcleo del problema —generar y componer, T-01, T-02 y T-04, T-09— a
infraestructura que habría que construir de todos modos.
