# README — Contratos Binarios y Gobierno del Sistema

## Propósito

Este documento fija **el modelo mental correcto** para diseñar contratos en sistemas con LLM.

No explica prompts, agentes ni arquitectura visual.
Define **qué es un contrato**, **para qué sirve** y **por qué debe ser binario**.

Si este README se entiende, los contratos se escriben solos.



## Idea central (no negociable)

> **El contrato existe para que el sistema pueda decir “NO” sin pensar.**

* No guía al modelo
* No razona
* No explica
* **Gobierna**

Todo lo demás es secundario.



## Separación de responsabilidades

### LLM

* Genera texto
* Aproxima
* Puede fallar
* No gobierna

### Prompt

* Maximiza probabilidad de cumplimiento
* No valida
* No decide

### Contrato

* Define lo permitido
* Define lo prohibido
* Define cuándo abortar

### Runtime

* Lee contratos
* Evalúa reglas binarias
* Decide si se ejecuta o se descarta

> El LLM propone. El sistema decide.



## Qué es un contrato (definición operativa)

Un contrato es un **filtro binario ejecutable por código** que responde solo a estas preguntas:

1. ¿El input es aceptable?
2. ¿El output es aceptable?
3. Si no lo es, ¿se aborta?

Si una regla no responde a una de estas preguntas, **no es contractual**.



## Por qué los contratos son binarios

### 1. Porque el LLM ya es blando

Si la capa de control también es blanda:

* hay ambigüedad
* hay propagación de error
* no hay gobierno

### 2. Porque el sistema debe decidir, no opinar

El runtime solo puede hacer:

* permitido
* prohibido
* ABORT

No existe el “más o menos válido”.

### 3. Porque fallar pronto es escalar

* Error temprano → local
* Error blando → sistémico

---

## Qué va en contrato (YAML / JSON)

Todo lo que **rompe el flujo** si no se cumple:

* Schema de input
* Schema de output
* Campos permitidos
* Campos obligatorios
* Enumeraciones cerradas
* Prohibiciones explícitas
* Condiciones de ABORT

Regla:

> **Si no puede evaluarse con `true / false`, no va aquí.**

---

## Qué NO va en contrato (Markdown)

* Propósito
* Contexto
* Ejemplos
* Justificación
* Rationale
* Diagramas
* Métricas suaves
* Recomendaciones

Eso explica.
No gobierna.

---

## Markdown vs YAML (regla clara)

* **YAML** → gobierna ejecución
* **Markdown** → comunica intención

Arquitectura sana:

* Contrato_X_v3.yaml
* Contrato_X_v3.md

Mismo nombre. Misma versión. Roles distintos.

---

## ABORT (pieza clave)

ABORT no es silencio.
Es una **respuesta válida del sistema**.

Ejemplo conceptual:

* status: ABORT
* reason: output_fuera_de_contrato
* source: validador_post

> Si no puedes abortar, no gobiernas.



## Capas dentro del contrato

### Capa A — Gobierno (binaria)

* Pasa / No pasa
* Ejecutable
* Dura

### Capa B — Observabilidad (no binaria)

* Warnings
* Métricas
* Scores

> **Binario en el borde. Gradual dentro.**

Nunca al revés.



## Lenguaje contractual

### Verbos permitidos

* determinar
* verificar
* comprobar
* aplicar
* emitir
* rechazar
* aceptar (solo binario)
* abortar

### Verbos prohibidos

* evaluar
* interpretar
* inferir
* considerar
* mejorar
* corregir

### Frases canónicas

* Todo lo no listado ⇒ PROHIBIDO
* Cualquier violación ⇒ ABORT
* Exclusivamente
* De forma literal
* Sin excepción

La monotonía léxica **es enforcement**.



## Señales de contrato débil

* Usa adjetivos evaluativos
* Necesita explicación para entenderse
* Introduce “normalmente”, “si tiene sentido”, “cuando aplique”
* Permite interpretación
* No define ABORT

Si es cómodo de leer, suele ser débil.



## Regla final (la que lo ordena todo)

> **El contrato no describe lo que pasa.
> Describe lo que NO se permite que pase.**

Cuando se diseña así:

* los contratos se acortan
* el YAML se vuelve obvio
* el sistema se vuelve gobernable



## Cierre

Este enfoque no es elegante.
No es flexible.
No es mágico.

Es **ingeniería de control**.

Y es el punto exacto donde se deja de hacer demos
para empezar a construir sistemas que resisten.
