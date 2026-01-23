# Contrato_Validador_v3

## Identidad
- **Contract ID:** contrato_validador_v3
- **Versión:** 3.0
- **Estado:** CONGELADO

## Propósito
Garantizar que **no ha habido contaminación de datos** entre los hallazgos del Mecánico y los hallazgos del Emisor.

## Rol
Validador binario de coherencia entre artefactos.

## Límites del contrato
- Opera exclusivamente como **gate binario**.
- No transforma ni re-emite artefactos.
- No normaliza ni interpreta contenido.
- No agrega metadata ni mensajes.
- No explica fallos.

## Inputs
- `hallazgos_mecanicos`
- `hallazgos_emisor`

## Output
- `ok` (binario)

Si no se emite `ok`, el contrato **no se cumple** ⇒ **ABORT**.

## Reglas normativas
- Comparación por **igualdad literal**.
- Correspondencia **uno a uno**.
- **Orden relevante**.
- **Incremento de cardinalidad no permitido**.

## Herencia y precedencia
- **Hereda de:** `Contrato_Base_Revisor_Documental_v3`

**Orden de precedencia:**
1. Contrato_Base_Revisor_Documental_v3
2. contrato_validador_v3
