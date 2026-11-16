# BackendServiceLine

Línea de producto de software para servicios backend en una entidad financiera
regulada, con la herramienta de línea de comandos que deriva sus productos y les
incorpora capacidades compartidas. Este repositorio guarda el **trabajo de grado**
que la sustenta: el expediente completo de su construcción y los dos documentos
académicos que la narran.

> **El código no vive acá.** Los activos de la línea —los contratos, las
> plantillas, los módulos y la herramienta— y el manifiesto del catálogo se
> publican en los repositorios `bsl-assets` y `bsl-catalog`, en el registro de
> paquetes de la organización. Lo que este repositorio ofrece es el registro de
> por qué cada cosa es como es.

## Qué hay acá

| Carpeta | Qué contiene |
| :-- | :-- |
| `Documentos/JorgeFacundo_AnteProyecto/` | El anteproyecto aprobado, en LaTeX. Es el compromiso original: los objetivos, el alcance y las cuatro fases de la metodología |
| `Documentos/JorgeFacundo_ProyectoGrado/` | El trabajo de grado, en LaTeX. Es la narración destilada de lo que cada fase dejó construido |
| `Implementación/` | El expediente paso a paso, una carpeta por fase. Es la fuente de verdad del proyecto, y es a lo que el trabajo de grado remite cuando dice que el detalle se conserva en los documentos de una fase |

Las dos capas no se confunden y la distinción explica el tamaño de cada una. El
expediente **registra**: cada decisión con su razón, sus alternativas y su
verificación. El trabajo de grado **narra**: el argumento y la evidencia que lo
sostiene, sin el paso a paso.

## Cómo leer el expediente

Cada fase abre con su `00-indice-de-fase.md`, y ese archivo es la puerta de
entrada. Dice qué resuelve la fase, qué documentos la componen y en qué orden
dependen unos de otros, cuál es su condición de llegada y qué narra de ella el
capítulo correspondiente del trabajo de grado.

Dentro de cada fase hay tres clases de archivo. Los **documentos** desarrollan lo
que la fase construye, numerados en orden de dependencia. El **log de decisiones**
—el archivo `01-adr-...`— registra cada decisión de arquitectura con su contexto,
su razón, las alternativas que se descartaron y cómo quedó verificada; abre con un
índice que permite responder «¿se decidió X?» sin leerlo entero. Los **insumos**
guardan el material de trabajo: los diagramas, las entrevistas, las capturas de
ejecución y las auditorías.

Las cuatro fases son la metodología Design Science Research aplicada al proyecto:

1. **Fundamentación y definición del marco de referencia.** Demuestra con
   evidencia que el problema existe y define cómo debe estructurarse la solución.
2. **Diseño y construcción del mecanismo de generación.** Construye la herramienta
   que deriva un proyecto conforme al marco.
3. **Diseño y construcción del gestor de módulos reutilizables.** Construye lo que
   incorpora una capacidad compartida a un proyecto ya en curso.
4. **Evaluación y validación del artefacto.** Mide lo construido contra la línea
   base y contra los objetivos comprometidos.

## El lenguaje de la trazabilidad

El expediente teje todo con identificadores estables, y leerlos permite seguir
cualquier afirmación hasta su origen. La cadena es
`T → B → RF/RNF → ADR → MR/MG/GM → código`.

| Código | Qué es |
| :-- | :-- |
| `T-xx` | Tema del análisis cualitativo de las entrevistas. Es el origen de todo requerimiento |
| `B-xx` | Brecha que ninguna herramienta existente cierra |
| `RF-xx` / `RNF-xx` | Requerimiento funcional o no funcional, con su prioridad y su criterio de aceptación |
| `ADR-xxx` | Decisión de arquitectura, en el log de la fase cuyo artefacto toca |
| `MR-xx` · `MG-xx` · `GM-xx` | Documento o diagrama del marco de referencia, del mecanismo de generación y del gestor de módulos |
| `PE-xx` | Participante de la evaluación, por su rol |

## Confidencialidad

El trabajo se desarrolló sobre una organización del sector financiero, y el
expediente no documenta información privada de ella. El contexto se describe por
**propiedades transferibles** a cualquier equipo que opere en un entorno regulado,
y no por datos particulares, por dos razones que alcanzan cada una por su cuenta:
la confidencialidad, y que el análisis solo es trasladable si se sostiene sobre
propiedades y no sobre detalles irrepetibles.

Los registros de entrevista identifican a cada participante **por su rol** y no por
su nombre, los hallazgos se atribuyen a roles, y los nombres de productos internos
y de proveedores se describen por su función. Las decisiones del proyecto se
sostienen sobre temas, brechas y requerimientos verificables, nunca sobre datos
privados.

## Autor

Jorge Andrés Facundo Solarte — Maestría en Ingeniería de Software, Pontificia
Universidad Javeriana, Cali.
