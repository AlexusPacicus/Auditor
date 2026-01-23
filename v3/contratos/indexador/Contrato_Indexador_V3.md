# Contrato_Indexador_v3

## Identidad
- **Contract ID:** contrato_indexador_v3
- **Versión:** 3.0
- **Estado:** CONGELADO

## Rol
Indexador determinista de documentos validados.

## Propósito
Producir un índice plano e inmutable a partir de documentos ya validados, sin análisis, interpretación ni enriquecimiento.

## Alcance
Este contrato define exclusivamente:
- Las capacidades permitidas del indexador.
- Los límites estrictos de su comportamiento.
- La forma del artefacto de salida que consume el detector mecánico.

No define reglas de detección ni análisis de contenido.

## Límites del contrato

### Puede
- Leer `documentos_aceptados`.
- Asignar identificadores internos deterministas.
- Emitir `entradas_indice`.

### No puede
- Aceptar documentos por criterios distintos a la forma definida.
- Garantizar ningún orden en el índice emitido.
- Modificar, actualizar o eliminar el índice una vez emitido.

## Inputs
- **Artefacto consumido:** `documentos_aceptados`  
  (validado previamente por el contrato `contrato_puerta_entrada_v3`.)

## Output
- **Artefacto emitido:** `entradas_indice`

Cada entrada contiene exclusivamente:
- `index_id`
- `doc_id`
- `contenido`

## Reglas normativas
- Correspondencia **uno a uno** entre documentos aceptados y entradas de índice.
- **Unicidad** de `index_id`.
- El índice es **inmutable** una vez emitido.

## Gobierno contractual
Este contrato hereda íntegramente de `Contrato_Base_Revisor_Documental_v3`.  
Ante cualquier violación de las reglas definidas en el contrato YAML: **ABORT**.

El archivo `Contrato_Indexador_v3.yaml` es la **fuente de verdad ejecutable** de este contrato.

## Herencia y precedencia
- **Hereda de:** `Contrato_Base_Revisor_Documental_v3`

**Orden de precedencia:**
1. Contrato_Base_Revisor_Documental_v3
2. contrato_indexador_v3
