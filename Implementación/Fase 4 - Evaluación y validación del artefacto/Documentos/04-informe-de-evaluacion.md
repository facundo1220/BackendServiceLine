# Informe de evaluación

El resultado esperado 4 del anteproyecto: el informe de evaluación del proceso de creación de
proyectos y del mecanismo de módulos reutilizables, con los resultados obtenidos, la comparación
contra el proceso actual y **los hallazgos sobre su aplicación práctica**. Interpreta lo que midieron
el doc 3; no vuelve a medir.

No es un veredicto de éxito ni una defensa del artefacto. El propósito quedó fijado antes de
medir: viabilidad, usabilidad, oportunidades de mejora y recomendaciones de adopción. Un resultado
adverso es resultado, y acá pesa lo mismo que uno favorable.

**Convención.** Lo marcado *(pendiente)* se completa cuando existan las mediciones. La estructura, las escalas
y las reglas de interpretación están decididas antes, para que el resultado no elija cómo se lo mide.

---

## 1. En qué condiciones se evaluó

Se dice primero, porque condiciona todo lo que sigue.

| Qué | Valor |
| :---- | :---- |
| Qué se evaluó | La línea de producto: la herramienta, el activo base y los dos módulos del catálogo, instalados del feed |
| Versiones | *(pendiente)* |
| Quiénes participaron | Cuatro `PE-xx`, caracterizados en el doc 2 §2: el autor, el desarrollador interno, el líder técnico con mirada de negocio y el desarrollador externo autor de la rúbrica |
| Cómo | Tres llamadas de una hora, conversadas, con instrumento escrito al cierre, más una sesión de uso con las manos |
| Qué **no** fue | El caso de estudio del laboratorio que el anteproyecto comprometía. El doc 2 declara por qué y qué se perdió con eso |

## 2. Los tres criterios del objetivo 4

| # | Criterio | Referencia | Resultado | Dónde está la evidencia |
| :-- | :---- | :---- | :---- | :---- |
| 1 | Tiempo requerido para la generación de un proyecto | 8 a 15 días · 52 a 98 horas-persona | *(pendiente)* | Doc 3 §1 |
| 2 | Correcta incorporación de un módulo reutilizable | Copia de carpetas sin vínculo con el origen | *(pendiente)* | Doc 3 §2 |
| 3 | Inicio de implementación de lógica de negocio | El andamio del producto derivado | *(pendiente)* | Doc 3 §3 |

**La comparación del criterio 1 se reporta en dos lecturas**, como lo exige la regla de las tres cubetas
del doc 1: sobre las 23 tareas que la herramienta cubre, y sobre el arranque completo, que incluye las 6 que no
cubre. Leer solo la primera exagera; leer solo la segunda esconde lo que la herramienta hace.

## 3. La rúbrica externa

| Qué | Antes, `0.2.1` | Después | Dónde |
| :---- | :---- | :---- | :---- |
| Criterios que cumplen, de nueve | 0 | *(pendiente)* | Doc 3 §4.2 |
| Discrepancias con lo que el autor declaraba | — | *(pendiente)* | Doc 3 §4.3 |
| El noveno criterio, respondido por la mirada de negocio | Falla | *(pendiente)* | Doc 3 §4.4 |

## 4. Hallazgos

Un hallazgo es algo que la evaluación encontró y que nadie había anotado: un defecto, una fricción, una
expectativa incumplida o un supuesto equivocado. Se identifican con **`HE-xx`**, serie propia de esta fase, para
no confundirlos con los `H-xx` del informe externo de octubre.

**Escala de severidad**, fijada antes de tener hallazgos:

| Severidad | Qué significa |
| :---- | :---- |
| **Bloquea** | Sin resolverlo, el equipo no puede adoptar la línea |
| **Encarece** | Se puede adoptar, pero el costo de uso es mayor que el previsto |
| **Molesta** | No impide nada; empeora la experiencia o la claridad |
| **Hallazgo de método** | No es del artefacto: es de cómo se evaluó, y afecta a lo que esta fase puede concluir |

| ID | Hallazgo | Severidad | De quién salió | Qué lo evidencia |
| :-- | :---- | :---- | :---- | :---- |
| *(pendiente)* | | | | |

**Regla de interpretación.** Un hallazgo no es un fracaso de la fase: es su producto. Y no se corrige antes de
reportarlo. Si alguno se corrige después, la corrección es otra ronda con su ADR, y este informe seguirá
diciendo que la medición se hizo sobre la versión anterior.

## 5. Recomendaciones

Priorizadas, con destinatario. Salen de los hallazgos, del bloque 3 del instrumento —*«¿qué le falta para que
lo adoptes?»* y *«si solo pudieras pedir un cambio, ¿cuál sería?»*— y de la conversación de cada llamada.

| # | Recomendación | Qué hallazgo atiende | A quién le toca | Costo estimado |
| :-- | :---- | :---- | :---- | :---- |
| *(pendiente)* | | | | |

Se separan tres destinos, porque confundirlos es lo que deja una recomendación sin dueño: lo que **la línea**
debe cambiar, lo que **el equipo que adopta** debe resolver de su lado, y lo que es **trabajo futuro** fuera
del alcance de este trabajo de grado.

## 6. Viabilidad y adopción

Es lo que el autor pidió que esta fase respondiera, y no está en el objetivo 4 con esas palabras.

| Pregunta | Respuesta | De dónde sale |
| :---- | :---- | :---- |
| ¿Es viable usarla en el equipo? | *(pendiente)* | Ítem N6 del instrumento, de los tres participantes |
| ¿Qué habría que resolver antes de adoptarla? | *(pendiente)* | Hallazgos que **bloquean**, y la pregunta 2 del bloque 3 |
| ¿Se entiende qué produce y qué no? | *(pendiente)* | Ítem N1 y el noveno criterio de la rúbrica |
| ¿Hay quien sostenga el catálogo? | *(pendiente)* | El juicio de `PE-02` sobre RF-16, en el doc 3 §2.5 |
| ¿Se sostiene fuera de este contexto? | *(pendiente)* | `PE-04`, y su ítem de transferibilidad |

## 7. El antes y el después, en una tabla

Los seis ítems que las entrevistas de agosto de 2026 ya habían tomado, ahora sobre el artefacto. Es la
comparación más directa del proyecto, porque es la misma escala y las mismas personas.

| Ítem | `PE-02` antes | `PE-02` después | `PE-03` antes | `PE-03` después |
| :---- | :--: | :--: | :--: | :--: |
| Dificultad del arranque | 3 | *(pendiente)* | 5 | *(pendiente)* |
| Tiempo hasta que el proyecto corre | 15 días | *(pendiente)* | 8 días | *(pendiente)* |
| Frecuencia de reutilizar por copia | 3 | *(pendiente)* | 4 | *(pendiente)* |
| Costo de propagar un cambio | 4 | *(pendiente)* | 5 | *(pendiente)* |
| Divergencia entre proyectos | 2 | *(pendiente)* | 3 | *(pendiente)* |
| Utilidad: esperada antes, comprobada después | 5 | *(pendiente)* | 5 | *(pendiente)* |

**Advertencia de lectura.** Son dos personas. No hay promedio, no hay dispersión y no hay significancia: se
reporta cada uno con su rol. Un movimiento en estos valores es indicio, no prueba.

## 8. Pertinencia del artefacto

La pregunta final del anteproyecto, y la única que exige un juicio y no una medición: **¿era este el artefacto
que el problema pedía?**

Se responde contra lo que la Fase 1 documentó, no contra lo que el artefacto hace:

| Qué documentó la Fase 1 | Qué dice la evaluación |
| :---- | :---- |
| El arranque es manual y recae en una sola persona (T-01) | *(pendiente)* |
| Reutilizar es copiar, porque no hay mecanismo formal (T-04) | *(pendiente)* |
| Propagar un cambio es manual y el contrato es su punto frágil (T-05) | *(pendiente)* |
| El costo técnico se paga en alcance de negocio (T-03) | *(pendiente)* |
| Adoptar exige ganancia real con uso mínimo (T-14) | *(pendiente)* |

## 9. Límites de este informe

- **Tres llamadas de una hora no miden adopción.** Miden uso informado, en sesión.
- **Una persona por rol.** Ningún dato admite generalización.
- **El autor construyó, condujo y escribe.** Lo que lo contiene está en el doc 2 —qué sesga cada
  participación, y el instrumento escrito e individual—, no en la buena voluntad de quien redacta.
- **No hubo tester ni líder de producto.** La consistencia entre productos y el costo en alcance de negocio no
  se midieron.
- **La línea base es autoreporte con n=2.** La comparación del criterio 1 hereda esa debilidad, declarada en el
  doc 1 §9.
- **Se evaluó una versión.** Lo que se corrija después no está evaluado.
- **Se evaluó una de las dos plantillas.** Agregado el 2026-11-09. La sesión mide
  `nestjs-hexagonal-api`, que es la que la línea base compara y la única con módulos que la sirvan.
  **`azure-functions-api` se muestra y no se mide**, y su arranque no lo comprueba ninguna puerta del
  repositorio, porque exige las Azure Functions Core Tools. Lo que el informe puede decir de ella es
  que existe, que deriva un producto que pasa su propia verificación y que **ningún módulo del
  catálogo la sirve todavía**; nada sobre su uso.

### 9.1 Las divergencias respecto del anteproyecto, declaradas

Agregada el 2026-11-09. Un informe que reporta tres criterios cumplidos y calla que el piso de
Node no es el prometido no es un informe honesto, así que el informe las lleva. Ninguna invalida un
requerimiento de la Fase 1: los 22 se miden contra su propio criterio de aceptación y ese veredicto no se toca.
Lo que esta tabla reporta es el **cumplimiento del anteproyecto**, que es otra cosa.

| Qué promete el anteproyecto | Qué pasó |
| :---- | :---- |
| Objetivo general y alcance: «entornos Node.js (v22–v24)» | El piso real es **24**, y el punto de entrada rechaza v22 y v23 con código 2. Se eligió entregar un producto verificable en una versión antes que uno no verificable en tres |
| Objetivo general y objetivo 1: «alineados con … BIAN e **ISO 20022**» | ISO 20022 **no se cumple**: opera en la capa de mensajería, que el artefacto no produce. BIAN sí, en **5 de las 46** capacidades extraídas, y solo `Term Deposit` transcrita de su documento oficial |
| Alcance: «documentación openAPI **basada en los módulos**» | **Incumplible por diseño**, porque un módulo no aporta adaptadores de entrada. Lo que se cumple es la cláusula de la metodología del propio anteproyecto: «basada en la estructura del proyecto generado» |
| Alcance: «**desarrollo** de un sistema de almacenamiento de plantillas» | Cumplido **por adopción y no por desarrollo**: el almacén existe —catálogo con tipo `template`, manifiesto por plantilla, `bsl templates list`— y el servicio que guarda los bytes es el registro de la organización, porque RF-15 pide que no haya canal propio de distribución |
| Objetivo 4: «en el contexto del **Laboratorio Digital del Banco W**» | La evaluación se hizo **con las personas de ese contexto y en sus entornos**, no como caso de estudio institucional, porque el autor salió del laboratorio |
| Riesgo ético 3: «documentación accesible orientada a **distintos niveles de experiencia**» | **No se construyó.** Se rechazó en la Fase 3 por un argumento de oportunidad, sin ver que era un compromiso ético. Pasa a ser la primera recomendación de adopción de §5 |
| Riesgo ético 4: «modelo de gobernanza **distribuido** con procesos participativos» | **El mecanismo está, el ejercicio no**: responsable por activo, `CODEOWNERS`, procedimiento de incorporación con condiciones verificables… y un solo participante. La documentación exhaustiva que el mismo compromiso pide **sí** está: 190 decisiones registradas |
| Riesgo ético 2: revisiones especializadas para módulos con lógica financiera | **No se materializó**: ninguno de los dos módulos lleva lógica financiera, porque el marco reparte lo técnico al módulo y el dominio al producto. Queda la condición de reactivación escrita |
| Riesgo ético 1: separación entre estructura y valores sensibles | **Cumplido y verificado por ejecución**: configuración por variable de entorno validada por esquema, barrido de valores fijos en el circuito, redacción por nombre de clave en el log |

**Dos cláusulas que **sí** se cerraron, y conviene decirlo junto a las demás.** El plural de «plantillas
configurables» del objetivo 2 quedó cumplido el 2026-11-09 con el almacén de plantillas, y el «compartidos entre proyectos»
del objetivo 3 y del resultado 3 quedó comprobado **por ejecución** el mismo día. Las dos
estaban incumplidas cuando esta fase se abrió, y las dos se cerraron antes de medir.

**Y una del método, que el informe también declara.** Ninguna de estas divergencias la detectó el mecanismo de
evolución del marco, ni los logs por fase, ni la tabla de pendientes, ni la auditoría de cierre: los cuatro
comparan lo construido contra el **expediente** y ninguno contra el **compromiso original**. La causa mecánica
estaba en el índice de la fase de esta fase, que medía contra una lista de objetivos reescrita. Queda como recomendación
de método: una auditoría de cumplimiento del anteproyecto es un paso de cierre de **cada** fase.

## 10. Qué queda como trabajo futuro

*(pendiente: sale de las recomendaciones cuyo destino es «fuera del alcance», y se consolida en el índice de la fase)*
