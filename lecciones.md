# Lecciones y Buenas Prácticas — Diseño Contractual v3

## Principios clave
- **Contratos antes que diagramas**: primero definir qué existe y qué no; luego dibujar.
- **Contrato Base = invariantes**: fija límites globales y garantías. No ejecuta.
- **Contratos específicos = concreción**: pueden **restringir más** y/o **introducir excepciones explícitas**, sin violar los invariantes del Base.
- **Idioma del sistema**: todo en español; el input es opaco (no se traduce).
- **Determinismo y pureza**: sin memoria, sin efectos colaterales, sin inferencias.

## Alcance v3 (revisor gobernado)
- Sin semántica, sin normalización correctiva, sin retries, sin loops.
- Ante incoherencias: **ABORTAR** (no corregir, no reintentar).
- **Anti-invención** garantizada con validador final.

## Conjunto de contratos v3 (cerrado)
0. `Contrato_Base_Revisor_Documental_v3`
1. `Contrato_Puerta_Entrada_v3`
2. `Contrato_Indexador_Literal_v3`
3. `Contrato_Detector_Mecánico_v3`
4. `Contrato_Emisor_v3`
5. `Contrato_Validador_Salida_v3`

> Regla: todos **heredan del Base** (los específicos pueden ser más restrictivos o habilitar excepciones explícitas).

## Responsabilidades (límites claros)
- **Puerta de Entrada**: valida forma (texto, no vacío, `doc_id` literal). No lee contenido.
- **Indexador Literal**: extrae **strings literales** (docs, referencias, versiones). No compara ni interpreta.
- **Detector Mecánico**: aplica reglas cerradas sobre índices. Sin priorizar ni evaluar.
- **Emisor**: formatea salida contractual (1:1 hallazgo–sugerencia).
- **Validador de Salida**: verifica trazabilidad 1:1 y **anti-invención**. OK o ABORT.

## Artefactos entre nodos
- Usar **paquetes únicos** entre nodos (una flecha = un artefacto).
- Evitar múltiples salidas paralelas.

## Diagrama de contratos — buenas prácticas
- **Bloques = contratos** (nombres exactos).
- **Flechas = artefactos** (sin lógica).
- **Herencia** con flecha discontinua desde el Base a todos.
- **Arriba → abajo** (pipeline).
- Sin decisiones visuales ni colores semánticos.
- Última salida: `informe_validado.md | ABORT` (sin nodo extra).

## Reglas duras
- Si algo describe **qué hacer**, no va en el Base.
- Un contrato específico puede **restringir más** o **habilitar excepciones explícitas** sin romper invariantes.
- Si el diagrama **sugiere comportamiento**, está mal.

Notas para README — Lecciones y mejoras (acumulativo)
El Base no explica, impone: toda explicación va fuera del contrato.
Lenguaje de enforcement > lenguaje descriptivo (“aplicable” es blando).
Eliminar palabras contaminadas (p. ej. inferencia, pureza).
Determinismo ≠ cardinalidad: estabilidad no implica 1→1.
Forma mínima: todo lo que no añade enforcement sobra.
Herencia debe ser normativa, no solo gráfica.
Separar capas: invariantes en Base; cardinalidad y estructura en contratos específicos.
ABORT como mecanismo de seguridad, no como fallback.
Cierre de mundo explícito para evitar fuga semántica.
Cuando dos frases expresan la misma frontera, se fusionan en una sola regla más fuerte.
Menos líneas = menos superficies de fuga.
Nunca usar verbos que impliquen juicio (“corregir”, “mejorar”) en contratos base.
Las prohibiciones deben ser mecánicas, no semánticas.
Si una regla solo introduce una excepción, no merece un invariante propio.
Eliminar invariantes cuyo título no añade un eje nuevo de control.
/

Lecciones aprendidas — Contrato Base v3
1. El contrato base no explica, impone
Todo lo explicativo debilita.
Si una regla necesita explicación para entenderse, no es apta para el Base.
2. Menos reglas = más control
Cada invariante adicional es una nueva superficie de fuga.
Eliminar redundancias endurece el sistema.
3. Un eje, un guardián
Nunca mezclar:
datos,
juicios,
emisión,
arquitectura
en la misma regla.
Cada eje debe estar controlado por un único invariante.
4. Lenguaje blando es deuda técnica
Términos como:
aplicable,
puede,
normalmente,
semántica,
introducen interpretación. Se eliminan.
5. El Base no negocia
Si un contrato superior menciona excepciones, deben existir y estar definidas.
Si no existen, no se mencionan.
6. Congelar es una decisión técnica
Un contrato congelado:
no se embellece,
no se “hace más legible”,
no se ajusta “un poco”.
Cualquier cambio ⇒ versión mayor.
7. Determinismo ≠ cardinalidad
Estabilidad del resultado no implica 1→1.
La cardinalidad se define más abajo, nunca en el Base.
8. Diagramas describen, contratos gobiernan
El diagrama ayuda a humanos.
El contrato decide qué es válido.
9. La aridez es una señal positiva
Un contrato cómodo suele ser débil.
Un contrato incómodo suele ser preciso.
10. Si resiste agentes, es estable
Si un agente no puede:
reordenarlo,
“mejorarlo”,
hacerlo más bonito
sin romper reglas, el texto está cerca de su forma canónica.
11. Espacio > palabras
La legibilidad contractual se gana con espaciado, no con texto nuevo.
12. El Base no conoce el futuro
No anticipar v4.
No prometer excepciones.
No dejar puertas entreabiertas.

Verbos permitidos (duros)
determinar
verificar
comprobar
aplicar
emitir
rechazar
aceptar (solo si es binario)
abortar
Verbos peligrosos (evitar)
evaluar
validar (salvo que lo fijes bien)
analizar
interpretar
inferir
considerar
decidir
corregir
mejorar
Sustantivos seguros
contrato
regla
límite
artefacto
entrada / output
violación
subconjunto
colección
Sustantivos contaminados
contexto
semántica
significado
calidad
intención
coherencia (salvo mecánica)
normalización
enriquecimiento
Adjetivos a eliminar
estricto
mínimo
adecuado
correcto
suficiente
razonable
Frases clave (úsalas mucho)
Todo lo no listado ⇒ PROHIBIDO
Cualquier violación ⇒ ABORT
Exclusivamente
De forma literal
Sin excepción


LECCIONES CONTRATO PUERTA ENTRADA

Menos texto = más control.
Cada línea extra es una superficie de fuga.
El Base impone; el específico concreta.
No repetir invariantes del Base en contratos específicos.
Autorreflexividad gana.
“Cumplen este contrato” cierra mejor que criterios externos.
Lenguaje mecánico > lenguaje correcto.
Determinar > validar > evaluar. Repetir verbos es bueno.
Prohibir exactamente lo que no haces.
No prohíbas lo necesario; delimita el acceso mínimo real.
Separar ejes evita contradicciones.
Admisión/rechazo en Reglas normativas; operación en Límites.
Output pobre es virtud.
Propaga solo lo imprescindible; lo demás desaparece.
ABORT explícito y con OR declarado.
Sin operadores lógicos explícitos hay ambigüedad.
Evitar términos evaluativos y adjetivos.
“estricto”, “mínimo”, “adecuado” sobran.
Auditorías producen falsos positivos.
Revisar hallazgos: no todo “redundante” lo es; concretar ≠ repetir.
Monotonía léxica es enforcement.
Variar palabras introduce interpretación.
Un contrato por chat.
Aislar contexto mejora rigor y congelación.
Listo. Si quieres, las guardamos como lecciones_v3.md.





# Lecciones aprendidas — Diseño contractual (Indexador v3)

> Documento humano.  
> No gobierna ejecución.  
> Fuente de verdad: contratos YAML.

---

## 1. Comprensiones clave (insights)
- Un contrato **no guía al modelo**, gobierna el sistema.
- YAML **no describe**, **constriñe**.
- No todo gobierno es binario (`if`): existe gobierno por **frontera**.
- `puede / no_puede` define **superficie de acción**, no checks.
- Las invariantes se **declaran**; el runtime las **comprueba después**.

## 2. Errores cometidos
- Mezclar explicación humana y gobierno en el mismo artefacto.
- Intentar hacer ejecutable todo lo que aparece en el contrato.
- Aceptar auditorías automáticas sin cuestionar su modelo mental.
- Duplicar invariantes como reglas y como acciones prohibidas.

## 3. Decisiones correctas
- Separar contrato en **YAML (ley)** y **Markdown (explicación)**.
- Congelar el contrato antes de pensar en runtime.
- Tratar los auditores como herramientas, no como autoridad.
- Mantener invariantes atómicas y explícitas.

## 4. Decisiones descartadas (y por qué)
- Convertir `puede / no_puede` en predicados ejecutables → rompe diseño.
- Eliminar herencia del contrato base → perder invariantes globales.
- Simplificar invariantes para “contentar” al auditor → empeora el contrato.

## 5. Reglas mentales consolidadas
- Si puede evaluarse true/false → YAML.
- Si explica o justifica → Markdown.
- Si el sistema funciona sin el MD → está bien diseñado.
- Primero la ley, luego el policía.

## 6. Patrones que funcionan
- Invariantes declaradas como flags binarios.
- Schema de output cerrado y exclusivo.
- Herencia solo para reglas transversales.
- Congelación temprana para evitar deriva.

## 7. Antipatrones detectados
- Texto libre en reglas normativas.
- Verbos con payload implícito (`Leer: X`).
- Redundancia semántica entre secciones.
- Auditores que infieren intención.

## 8. Sobre auditores automáticos
- Qué detectan bien:
  - Redundancias literales reales.
  - Violaciones claras de herencia.
- Falsos positivos recurrentes:
  - Invariantes atómicas.
  - Herencia de contratos base.
  - Capacidades declarativas.
- Qué NO deben evaluar:
  - `puede / no_puede`
  - Semántica implícita
  - Intención del diseñador

## 9. Separación correcta de capas
- YAML:
  - Ley del sistema
  - Frontera y restricciones
  - Invariantes declaradas
- Markdown:
  - Contexto
  - Alcance
  - Decisiones de diseño
- Runtime:
  - Predicados
  - Checks
  - Abort efectivo

## 10. Lenguaje contractual
### Verbos a usar
- leer
- emitir
- asignar
- heredar
- abortar

### Verbos a evitar
- interpretar
- evaluar
- considerar
- garantizar (si no es comprobable)

## 11. Qué NO hacer en la próxima versión
- No ampliar el contrato sin un rol nuevo claro.
- No adaptar el contrato a tooling defectuoso.
- No introducir checks de runtime prematuramente.

## 12. Qué sí llegará en versiones futuras (NO ahora)
- Tests contractuales automáticos.
- Runtime mínimo que haga cumplir invariantes.
- Auditorías cruzadas entre contratos (indexador → detector).

# Lecciones aprendidas — Diseño contractual (Indexador v3)

> Documento humano.  
> No gobierna ejecución.  
> Fuente de verdad: contratos YAML.

---

## 1. Comprensiones clave (insights)
- Un contrato **no guía al modelo**, gobierna el sistema.
- YAML **no describe**, **constriñe**.
- No todo gobierno es binario (`if`): existe gobierno por **frontera**.
- `puede / no_puede` define **superficie de acción**, no checks.
- Las invariantes se **declaran**; el runtime las **comprueba después**.

## 2. Errores cometidos
- Mezclar explicación humana y gobierno en el mismo artefacto.
- Intentar hacer ejecutable todo lo que aparece en el contrato.
- Aceptar auditorías automáticas sin cuestionar su modelo mental.
- Duplicar invariantes como reglas y como acciones prohibidas.

## 3. Decisiones correctas
- Separar contrato en **YAML (ley)** y **Markdown (explicación)**.
- Congelar el contrato antes de pensar en runtime.
- Tratar los auditores como herramientas, no como autoridad.
- Mantener invariantes atómicas y explícitas.

## 4. Decisiones descartadas (y por qué)
- Convertir `puede / no_puede` en predicados ejecutables → rompe diseño.
- Eliminar herencia del contrato base → perder invariantes globales.
- Simplificar invariantes para “contentar” al auditor → empeora el contrato.

## 5. Reglas mentales consolidadas
- Si puede evaluarse true/false → YAML.
- Si explica o justifica → Markdown.
- Si el sistema funciona sin el MD → está bien diseñado.
- Primero la ley, luego el policía.

## 6. Patrones que funcionan
- Invariantes declaradas como flags binarios.
- Schema de output cerrado y exclusivo.
- Herencia solo para reglas transversales.
- Congelación temprana para evitar deriva.

## 7. Antipatrones detectados
- Texto libre en reglas normativas.
- Verbos con payload implícito (`Leer: X`).
- Redundancia semántica entre secciones.
- Auditores que infieren intención.

## 8. Sobre auditores automáticos
- Qué detectan bien:
  - Redundancias literales reales.
  - Violaciones claras de herencia.
- Falsos positivos recurrentes:
  - Invariantes atómicas.
  - Herencia de contratos base.
  - Capacidades declarativas.
- Qué NO deben evaluar:
  - `puede / no_puede`
  - Semántica implícita
  - Intención del diseñador

## 9. Separación correcta de capas
- YAML:
  - Ley del sistema
  - Frontera y restricciones
  - Invariantes declaradas
- Markdown:
  - Contexto
  - Alcance
  - Decisiones de diseño
- Runtime:
  - Predicados
  - Checks
  - Abort efectivo

## 10. Lenguaje contractual
### Verbos a usar
- leer
- emitir
- asignar
- heredar
- abortar

### Verbos a evitar
- interpretar
- evaluar
- considerar
- garantizar (si no es comprobable)

## 11. Qué NO hacer en la próxima versión
- No ampliar el contrato sin un rol nuevo claro.
- No adaptar el contrato a tooling defectuoso.
- No introducir checks de runtime prematuramente.

## 12. Qué sí llegará en versiones futuras (NO ahora)
- Tests contractuales automáticos.
- Runtime mínimo que haga cumplir invariantes.
- Auditorías cruzadas entre contratos (indexador → detector).

---

## Cierre
- Estado del contrato: **FROZEN**
- Motivo de congelación:
  - El contrato gobierna correctamente y los hallazgos restantes son límites del tooling.


1️⃣ El contrato gobierna, no ayuda
Un contrato no explica ni mejora resultados.
Define qué está permitido y qué está prohibido.
Si algo “ayuda” → no es contrato.
2️⃣ YAML es la ley, Markdown es el comentario
Si borras el Markdown y el sistema sigue funcionando, está bien hecho.
YAML: constriñe
MD: contextualiza
Nunca al revés.
3️⃣ No todo gobierno es un if
Hay reglas que existen para que el if no exista.
puede / no_puede → frontera
invariantes → checks
runtime → ejecución
No mezclar capas.
4️⃣ Una propiedad se declara una sola vez
Si una idea aparece dos veces, sobra una.
Invariante o
acción prohibida
Nunca ambas.
5️⃣ Congelar es una decisión técnica
Seguir tocando un contrato correcto lo empeora.
Cuando los problemas vienen del tooling:
se documenta
se congela
se avanza

DECLARAR SIEMPRE LOS ABORTS, SI HEREDAN, INDICARLO

# Lecciones aprendidas – Diseño contractual v3

Este documento recoge aprendizajes prácticos derivados de la construcción,
auditoría y prueba de contratos ejecutables en el flujo v3.

No son principios teóricos: son decisiones tomadas tras errores reales.

---

## 1. Un contrato no describe capacidades, describe estados prohibidos

Listar lo que un agente “puede hacer” no aporta control operativo.
El control real se ejerce definiendo **invariantes verificables** y **ABORT**.

**Aprendizaje**
- `puede` no es evaluable → ruido.
- `no_puede` + invariantes → control real.

---

## 2. Todo lo que no sea evaluable binariamente no es contrato ejecutable

Si una regla no puede reducirse a `true / false` comparando input y output,
no puede ser auditada ni abortar ejecución.

**Aprendizaje**
- Reglas semánticas = decoración.
- Reglas contables / comparables = gobernanza.

---

## 3. El contrato base gobierna; el contrato específico no debe repetirlo

Repetir invariantes globales (no interpretación, trazabilidad literal, etc.)
en contratos específicos introduce ruido y falsos positivos en auditorías.

**Aprendizaje**
- El contrato específico solo restringe tentaciones propias de su rol.
- Si no añade restricción nueva, es mejor no añadir nada.

---

## 4. La herencia contractual no implica herencia funcional

Heredar del contrato base:
- NO añade capacidades.
- SOLO impone prohibiciones globales.

Auditores que confunden herencia normativa con funcional están mal diseñados.

**Aprendizaje**
- Heredar invariantes refuerza fronteras, no las mezcla.

---

## 5. El ABORT heredado no es comportamiento, es enforcement

El ABORT no define “qué hace” un contrato,
define **qué ocurre cuando se viola**.

Duplicar ABORTs específicos sin necesidad es ruido.

**Aprendizaje**
- Si el contrato base ya aborta, el específico debe heredar, no redeclarar.

---

## 6. Un artefacto se nombra por autoridad, no por forma ni contenido

Dos artefactos pueden ser idénticos en datos y forma,
pero si los emite una autoridad contractual distinta,
**deben tener nombres distintos**.

**Aprendizaje**
- Mismo nombre ⇒ misma autoridad.
- Autoridad distinta ⇒ nombre distinto, aunque los datos sean iguales.

---

## 7. Verbo ≠ artefacto

- Los **verbos** describen capacidades genéricas.
- Los **sustantivos** describen fronteras y autoridad.

Un verbo como output es una violación de diseño.

**Aprendizaje**
- El verbo nunca codifica gobernanza.
- El artefacto sí.

---

## 8. Un contrato puede no transformar nada y seguir siendo necesario

Algunos contratos no existen para transformar datos,
sino para:
- fijar fronteras de gobernanza,
- permitir auditorías,
- aislar responsabilidades,
- habilitar pruebas adversarias.

**Aprendizaje**
- Transformación ≠ utilidad.
- Gobernanza también justifica un contrato.

---

## 9. Un contrato no se congela cuando “parece correcto”

Un contrato solo se congela tras:
- auditoría sin hallazgos,
- pruebas con output real del contrato anterior,
- pruebas adversarias (orden, cardinalidad, mutación, campos extra).

**Aprendizaje**
- “Suena bien” no es criterio de congelación.

---

## 10. Contrato sin prompt deja el runtime implícito

El contrato gobierna qué es válido.
El prompt gobierna **cómo se ejecuta** el contrato en el LLM.

Sin prompt explícito:
- no hay reproducibilidad,
- no hay auditoría operativa.

**Aprendizaje**
- Contrato + prompt + prueba mínima → congelable.
- Sin prompt, el control es incompleto.

---

## 11. Iterar contrato → prompt → prueba es correcto en fase de diseño

El enfoque batch (todos los contratos primero) propaga errores estructurales.
La iteración corta reduce deuda y revela fallos conceptuales antes.

**Aprendizaje**
- Iterar lento al principio acelera el sistema completo.

---

## 12. Sensación de “esto no hace nada” suele indicar buen diseño

Cuando un contrato empieza a parecer inútil,
probablemente está bien diseñado:
ha eliminado toda semántica innecesaria.

**Aprendizaje**
- La incomodidad suele marcar la frontera correcta.

---
