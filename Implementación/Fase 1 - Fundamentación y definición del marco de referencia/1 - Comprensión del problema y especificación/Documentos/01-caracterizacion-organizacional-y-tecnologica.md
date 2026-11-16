# Caracterización organizacional y tecnológica

En una entidad financiera regulada, el equipo que construye software consume un core que no controla y opera dentro de un marco institucional que no define, pero conserva autonomía plena sobre la construcción interna de sus soluciones. Esa asimetría es la que hay que tener presente para leer los hallazgos de la fase: una necesidad expresada en una entrevista significa algo distinto según lo que el equipo puede decidir por sí mismo y lo que debe acatar.

El contexto queda descrito por **propiedades comunes a cualquier equipo en una organización de ese tipo**, no por datos particulares de ésta: sin estructura interna nominal, sin composición exacta, sin stack con proveedor concreto. Son dos razones y cada una alcanza sola: la confidencialidad, y que el análisis solo es trasladable si el contexto está en propiedades y no en detalles irrepetibles. Las entrevistas se hicieron sobre el equipo que construye; a las áreas institucionales no se las entrevistó, así que lo relativo a ellas se enuncia como el marco bajo el cual el equipo opera y no como caracterización propia.

## 1. Cómo opera el entorno

El contexto es el de una entidad financiera regulada. En este tipo de organización el desarrollo de software se rige por una separación característica entre dos planos:

- **Una autoridad institucional de tecnología** que define las reglas bajo las cuales se construye y se despliega: las definiciones arquitectónicas, las políticas de seguridad y manejo de información, la forma de consumir los servicios centrales (el *core* bancario) y la autorización para desplegar en los entornos productivos. Estas reglas vienen impuestas y no son negociables desde el equipo de desarrollo.

- **Una unidad de innovación o laboratorio** que construye soluciones propias consumiendo los servicios ya existentes del *core*, con foco en agilidad y velocidad de salida al mercado. Es el equipo que desarrolla las soluciones sobre las que actúa la herramienta de este trabajo.

La propiedad relevante para el proyecto es que el equipo que construye **consume un core que no controla** y **opera dentro de un marco institucional que no define**, pero **conserva autonomía plena sobre la construcción interna de sus soluciones**.

## 2. Marco impuesto y dominio de control

La distinción entre lo que el equipo decide y lo que acata es lo que da sentido a cada hallazgo posterior. La herramienta solo puede intervenir legítimamente sobre el dominio de control del equipo.

| Definido por la autoridad institucional (impuesto) | Definido por el equipo de desarrollo (dominio de control) |
| :---- | :---- |
| Forma de consumir el core: reglas, protocolos y seguridad | Estructura interna de sus proyectos |
| Servicios del core disponibles y su comportamiento | Convenciones de código, nomenclatura y organización modular |
| Políticas de seguridad y manejo de información | Patrones y principios arquitectónicos aplicados |
| Definiciones arquitectónicas institucionales | Organización de repositorios y ciclo de trabajo |
| Autorización y ejecución de despliegues | Forma de consumir el core a nivel de código, dentro de las reglas de seguridad impuestas |

La herramienta actúa enteramente sobre la columna derecha. Nada de lo que produce puede alterar lo que la organización impone.

## 3. Propiedades del equipo de desarrollo

Las propiedades que condicionan la solución, con independencia de cifras concretas:

- **Equipo reducido y estable.** Cada desarrollador sostiene más de un producto de forma simultánea, lo que hace costoso cualquier esfuerzo repetitivo de configuración o mantenimiento manual.
- **Trabajo ágil con doble vía.** El descubrimiento (experiencia de usuario) y la entrega (desarrollo) avanzan alineados; un proyecto nuevo llega al equipo técnico a través de los roles de producto y técnico.
- **Roles presentes**, como arquetipos transferibles a cualquier equipo de estas características: dirección del laboratorio, un rol técnico transversal, roles de producto por línea, desarrolladores, pruebas (transversal) y experiencia de usuario. Estos arquetipos son la base sobre la que se seleccionan los stakeholders a entrevistar.

## 4. Entorno tecnológico

Descrito por propiedades, sin proveedor concreto:

- **Plataforma cloud corporativa** como entorno de despliegue.
- **Entorno de desarrollo Node.js con TypeScript**, con un **framework backend de referencia** (NestJS) para los servicios con servidor propio.
- **Persistencia relacional**, **análisis estático de código**, **ejecución de pruebas** y **documentación de API**, todo con herramientas estándar del ecosistema.
- **Configuración externalizada** mediante variables de entorno.
- **Repositorios corporativos** y un **registro de paquetes privado de la organización** como canal de distribución de librerías.

El registro de paquetes privado es una propiedad relevante: ya existe un canal de distribución gobernado, lo que permite que la solución se apoye en él sin desplegar infraestructura propia.

## 5. Reutilización actual y su costo

Las funcionalidades que se repiten entre soluciones incluyen: consumo del core bancario, manejo de errores, *logging*, eventos, autenticación y validación de identidad, manejo de tokens y cifrado, integración con almacenamiento, integración con proveedor de identidad, notificaciones y conexión a la base de datos del proyecto.

De todas, la única con incidencia universal conocida es el **consumo del core**, presente en el 100 % de las soluciones, porque toda solución del equipo consume el core por definición.

**Mecanismo actual de reutilización.** Para el consumo del core existe una librería propia que agiliza la conexión. Para el resto de funcionalidades, el mecanismo es **copiar y pegar**: cuando una funcionalidad es nueva se desarrolla para ese proyecto, y si otro la necesita se copia desde el primero. No existe ninguna librería interna de backend publicada.

**Evidencia del costo de propagación.** El patrón que cuantifica el problema: cuando el core publica un servicio equivalente a uno que el equipo había construido por su cuenta, migrar hacia el servicio central obliga a modificar manualmente todos los proyectos afectados —código, bases de datos y permisos—. Al no existir un mecanismo de propagación, cualquier cambio transversal se paga tantas veces como proyectos lo incorporen.
