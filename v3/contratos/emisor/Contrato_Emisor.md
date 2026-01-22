# Contrato_Emisor_v3

## Identidad
- **Contract ID:** contrato_emisor_v3  
- **Versión:** 3.0  
- **Estado:** CONGELADO  

---

## Rol
Emisor contractual de hallazgos mecánicos.

---

## Propósito
Reemitir hallazgos mecánicos **sin transformación**, bajo una **autoridad contractual distinta**, fijando una frontera explícita de gobernanza.

Este contrato no analiza, no interpreta y no modifica datos.

---

## Alcance
Este contrato define exclusivamente:
- Las **prohibiciones operativas** aplicables al proceso de emisión.
- La **forma del artefacto emitido**.
- La **autoridad contractual** bajo la cual se reemiten los hallazgos.

No introduce reglas de detección ni lógica de decisión.

---

## Límites del contrato

### No puede
- Asignar identificadores nuevos.
- Alterar el orden o la cardinalidad de los hallazgos.
- Emitir el artefacto más de una vez.
- Modificar el artefacto una vez emitido.

Cualquier violación implica **ABORT**, conforme al contrato base.

---

## Inputs
- **Artefacto requerido:** `hallazgos_mecanicos`  
  Emitido previamente por el contrato `Contrato_Detector_Mecanico_v3`.

No se aceptan inputs adicionales.

---

## Output
- **Artefacto emitido:** `hallazgos_emisor`

Cada hallazgo contiene exclusivamente:
- `hallazgo_id`
- `regla_id`
- `index_id`
- `doc_id`
- `evidencia_literal`

No se permiten campos adicionales.

---

## Gobierno contractual
Este contrato hereda íntegramente de `Contrato_Base_Revisor_Documental_v3`.

- No define condiciones de ABORT propias.
- Ante cualquier violación de invariantes globales o de los límites aquí definidos: **ABORT**.

El archivo `Contrato_Emisor_V3.yaml` es la **fuente de verdad ejecutable** de este contrato.

---

## Herencia y precedencia
**Orden de precedencia:**
1. `Contrato_Base_Revisor_Documental_v3`
2. `Contrato_Emisor_v3`
