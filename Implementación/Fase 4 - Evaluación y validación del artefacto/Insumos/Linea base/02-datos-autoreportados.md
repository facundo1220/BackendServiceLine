# Datos autoreportados de la línea base

Los datos que las entrevistas dejaron sobre el costo de arrancar un proyecto y
sobre el costo de reutilizar y propagar una capacidad compartida, consolidados en un solo lugar y con su origen
declarado. Es la única fuente de la línea base que es **anterior al artefacto**, y por eso la línea base
la toma como ancla.

Los datos se citan por rol y nunca por persona, según la regla de confidencialidad del proyecto. Las
entrevistas completas están en `1 - Comprensión del problema y especificación/Insumos/Resultados entrevistas/`.

---

## 1. Por qué estos datos sirven y qué los hace limpios

Las entrevistas se realizaron el **5 y el 6 de agosto de 2026**. La primera línea de la herramienta se escribió
después, y los primeros productos derivados verificables son de octubre de 2026. Ninguna respuesta pudo estar
influida por el artefacto, porque el artefacto no existía. Esa es la propiedad que la línea base aprovecha: la ventana
se venció para una medición instrumentada, no para el autoreporte, que ya estaba recogido.

El contexto estudiado aporta **dos** puntos de dato de tiempo. El tercero proviene de un desarrollador de otra
organización y se reporta como contraste, nunca sumado a la banda del contexto estudiado.

## 2. Tiempo de arranque declarado

| Rol | Fecha | Pregunta cerrada | Valor |
| :---- | :---- | :---- | :---- |
| Líder técnico | 2026-08-05 | Tiempo aproximado de un arranque hasta que el proyecto corre | **15 días** |
| Desarrollador interno | 2026-08-05 | Tiempo aproximado de un arranque hasta que el proyecto corre | **8 días** |
| Desarrollador externo *(contraste)* | — | Tiempo típico de arranque hasta escribir lógica de negocio | **2 semanas** |

**Banda del contexto estudiado: 8 a 15 días.** Con dos puntos no se reporta promedio ni dispersión.

Lo que la prosa agrega, y que la pregunta cerrada no captura:

- El desarrollador interno describe la tarea como algo que, **con foco**, toma «alrededor de una semana o al
  menos algunos días», y describe por separado un tramo de «al menos una semana bien trabajada» durante el cual
  **el resto del equipo está a la espera** y asigna su tiempo a otras iniciativas. Ese tiempo muerto del equipo
  no se cuenta en M1 ni en M2: es un costo de oportunidad distinto del esfuerzo del arranque, y la línea base
  lo declara sin cuantificarlo.
- El mismo rol fija la expectativa contra la cual se va a leer el resultado: que ese proceso se reduzca «a solo
  algunos minutos».
- El desarrollador externo estima la configuración inicial en «incluso 15 días» en prosa, y aporta el matiz que
  sostiene el problema: **incluso con librerías y módulos compartidos disponibles**, persiste un espacio de
  configuración desde cero, porque hay que probar que lo que viene hecho funcione.

## 3. Percepción del arranque y de la reutilización

Escala de 1 a 5, tal como quedó en cada entrevista.

| Pregunta cerrada | Líder técnico | Desarrollador interno | Desarrollador externo *(contraste)* |
| :---- | :--: | :--: | :--: |
| Dificultad percibida del arranque de un proyecto hoy | 3 | 5 | 4 |
| Frecuencia con que se reutiliza código por copia | 3 | 4 | 4 |
| Costo percibido de propagar un cambio de una capacidad compartida | **4** | **5** | 3 |
| Grado de divergencia percibida entre proyectos | 2 | 3 | — |
| Utilidad esperada de una herramienta que automatice arranque e integración | 5 | 5 | — |

Del rol de producto (2026-08-06), que no estima tiempo técnico pero sí su efecto: frecuencia con que un producto
requiere integrar funcionalidades ya existentes en otros, 4; impacto de esa integración sobre el cronograma
cuando aparece a mitad de camino, 4; frecuencia de funcionalidades de negocio que se sacrifican por estos
impactos, **5**; valor esperado de reducir los tiempos de arranque e integración, 5.

**Anomalía de transcripción declarada.** En la entrevista del rol de producto, la respuesta a «impacto del
tiempo de arranque sobre tu planeación» figura como `55` en una escala de 1 a 5. Se transcribe tal cual y no se
corrige: lo más probable es un doble golpe de tecla sobre el valor 5, pero el dato no se usa en ninguna métrica
y no se repara por inferencia.

## 4. Mecanismo actual, en las palabras del análisis

Estos tres hallazgos del análisis cualitativo son lo que la línea base mide del lado de la reutilización:

- **T-01.** El levantamiento de entornos, la configuración de la arquitectura, los componentes de
  infraestructura, el despliegue del repositorio, el despliegue del servicio en la nube y la creación de bases
  de datos se hacen a mano en cada proyecto nuevo. **Lo ejecuta un solo desarrollador**, y se suma una segunda
  persona solo si el proyecto es especialmente robusto.
- **T-04.** Cuando un proyecto necesita una capacidad que otro ya resolvió y no hay librería ni módulo
  compartido disponible, se replica copiando la carpeta y ajustando sus variables de entorno, o se reconstruye
  la estructura tomando otro proyecto como referencia visual.
- **T-05.** Propagar un cambio es manual y hay que repetirlo en cada proyecto donde se copió. Lo más costoso no
  es copiar el código, sino el cambio en la estructura de la respuesta del servicio consumido, que desencadena
  ajustes en cascada.

La tabla de contraste del análisis agrega el dato estructural: en el contexto estudiado el mecanismo de
reutilización es la **copia de carpetas entre proyectos**, frente a librería compartida o módulo en monorepo en
las organizaciones externas, y el estándar arquitectónico **no está documentado y se aplica parcialmente**.

## 5. Los tres supuestos de la conversión a horas-persona

M1 está en días y la herramienta se mide en minutos. La conversión exige supuestos, y se declaran como
supuestos y no como medición.

**S-1 · Jornada efectiva: 6.5 horas por día.** Se deriva del calendario real de trabajo del equipo, no de una
convención:

| Concepto | Cálculo |
| :---- | :---- |
| Jornada nominal | 7:00 a 17:00 menos 2 horas de almuerzo = 8 h/día, de lunes a viernes = 40 h/semana |
| Reunión diaria de seguimiento | 30 min × 5 = 2.5 h/semana |
| Planificación | 1 h cada dos semanas = 0.5 h/semana |
| Retrospectiva | 1 h cada dos semanas = 0.5 h/semana |
| Revisión | 2 h cada dos semanas = 1 h/semana |
| Refinamiento | 1 h cada dos semanas = 0.5 h/semana |
| Reuniones varias | 2 a 3 h/semana, se toma 2.5 |
| **Total de ceremonias** | **7.5 h/semana, el 19 % de la jornada nominal** |
| **Jornada efectiva** | 32.5 h/semana = **6.5 h/día** (6.4 a 6.6 según la semana) |

**S-2 · Dedicación: una persona, completa.** Lo respalda T-01, que declara que el trabajo lo ejecuta un solo
desarrollador, y la prosa del desarrollador interno, que estima el tiempo «si uno se enfoca en esa tarea».

**S-3 · Qué significan «8» y «15 días».** La pregunta cerrada no distinguió días hábiles de días calendario. Se
adopta la lectura de **días hábiles**, que es la literal para una estimación de trabajo, y se reporta la otra
lectura como piso. La conclusión no depende del supuesto:

| Lectura de S-3 | 8 días | 15 días | Banda |
| :---- | :--: | :--: | :---- |
| Días hábiles (principal) | 52 h | 97.5 h | **52 a 98 horas-persona** |
| Días calendario (piso) | 37 h | 70 h | 37 a 70 horas-persona |

En las dos lecturas el arranque está en el orden de **una a dos semanas y media de trabajo efectivo de una sola
persona**.

## 6. Qué no hay, y por eso no se reporta

- **Corroboración publicable del autoreporte.** No la hay, y la razón es el historial de los proyectos
  anteriores es material privado que no entra al expediente, ni completo ni anonimizado, y además el acceso se
  perdió. **Nota del 2026-11-07:** sí existe una corroboración que el autor conoce —la banda es consistente con
  los registros de tiempo con que el contexto mide su propio trabajo—, y el doc 1 §6 la menciona
  declarando que no cuenta como evidencia. No se transcribe nada de ese material, no se identifica ningún
  proyecto y no se reporta ninguna de sus cifras.
- **Cuántos repositorios hay que tocar** para propagar un cambio de una capacidad compartida. Las entrevistas
  dan el costo percibido, no el conteo.
- **Horas cargadas o tickets** del arranque de un proyecto concreto. No se dispone de ese rastro.
- **Un tercer punto de dato del contexto estudiado.** No se levanta autoreporte nuevo: el equipo ya conoce la
  herramienta, de modo que una respuesta de hoy no mediría el proceso anterior.
