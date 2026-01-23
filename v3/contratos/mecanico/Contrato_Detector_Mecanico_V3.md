# Contrato_Detector_Mecanico_v3

## Identidad
- Contract ID: contrato_mecanico_v3
- Versión: 3.0
- Estado: CONGELADO

## Rol
Detector mecánico determinista de hallazgos literales.

## Propósito
Emitir hallazgos literales conforme a reglas mecánicas explícitas.

## Alcance
Este contrato define exclusivamente la aplicación de reglas mecánicas explícitas para la emisión de hallazgos literales.

No evalúa ausencia de señales, no interpreta contenido y no emite juicios ni conclusiones.


## Límites del contrato

### Puede
- Leer el artefacto `entradas_indice`.
- Leer el artefacto `reglas_mecanicas`.
- Emitir hallazgos mecánicos.

### No puede
- Modificar el artefacto `entradas_indice`.
- Modificar el artefacto `reglas_mecanicas`.

## Inputs
- `entradas_indice` (requerido)


## Dependencias exógenas

- **Artefacto:** `reglas_mecanicas`
- **Tipo:** dependencia exógena
- **Producción:** no producida por ningún contrato v3
- **Modo de acceso:** solo lectura
- **Modificable:** no
- **Derivable:** no

## Reglas normativas
- La emisión de hallazgos se ejecuta exclusivamente mediante `reglas_mecanicas`.
- La emisión de hallazgos solo puede producirse por match literal.


## Output
- Artefacto emitido: `hallazgos_mecanicos`

Cada hallazgo contiene exclusivamente:
- `hallazgo_id`
- `regla_id`
- `index_id`
- `doc_id`
- `evidencia_literal`

## Gobierno contractual
Este contrato hereda íntegramente de `Contrato_Base_Revisor_Documental_v3`.  
Ante cualquier violación de las reglas definidas en el contrato YAML: **ABORT**.

El archivo `Contrato_Detector_Mecanico_v3.yaml` es la **fuente de verdad ejecutable** de este contrato.

