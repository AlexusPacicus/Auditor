# Contrato Validador v3

## Propósito
Garantizar que **no ha habido contaminación de datos**
entre los hallazgos del Mecánico y los hallazgos del Emisor.

---

## Rol en el sistema
- Opera como **gate binario**.
- Evalúa la relación entre `hallazgos_mecanicos` y `hallazgos_emisor`.
- El control de paso se aplica en el **runner**.

---

## Qué hace
- Aplica las **reglas normativas definidas en el contrato**.
- Determina si el resultado **puede existir aguas abajo**.
- Emite `ok` o provoca **ABORT heredado**.

---

## Qué NO hace
- No transforma ni re-emite artefactos.
- No normaliza ni interpreta contenido.
- No agrega metadata ni mensajes.
- No explica fallos.

---

## Inputs
- `hallazgos_mecanicos`
- `hallazgos_emisor`

---

## Output
- `ok` (binario)

Si no se emite `ok`, el contrato **no se cumple** ⇒ **ABORT**.

---

## Reglas
Las reglas de comparación, correspondencia y cardinalidad
están definidas **exclusivamente en el contrato** (`reglas_normativas`).

---

## Relación con otros contratos
- Hereda de `Contrato_Base_Revisor_Documental_v3`.
- Valida el output de `Contrato_Emisor_v3`.

---

## Notas de diseño
- El validador es **pasivo**.
- El aislamiento se garantiza por **orquestación**.
- El diagrama del flujo es **derivado**, no normativo.
