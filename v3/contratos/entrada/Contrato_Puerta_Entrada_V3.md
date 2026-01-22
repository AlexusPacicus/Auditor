# Identidad
- Nombre del contrato: Contrato_Puerta_Entrada_v3
- Contract ID: contrato_puerta_entrada_v3
- Versión: 3.0
- Estado: CONGELADO



# Propósito
Determinar si los artefactos de entrada cumplen este contrato.


# Límites del contrato
Este contrato:
- PUEDE:
  - Determinar la forma contractual definida en este contrato.
  - Determinar el subconjunto de documentos que cumplen este contrato.

- NO PUEDE:
  - Acceder al contenido para fines distintos a verificar que existe como string y que no está vacío.


# Inputs
- Artefactos aceptados:
  - Colección de documentos.
- Forma:
  - Cada documento debe contener:
    - `doc_id` (string literal)
    - `contenido` (string literal)
- Reglas de admisión:
  - El input no puede ser vacío.



# Reglas normativas
- Un documento cuyo `contenido` no sea un string es rechazado.
- Un documento con `contenido` vacío es rechazado.
- Un documento que requiera referencias externas no presentes es rechazado.



# Output
- Artefacto de salida:
  - Colección `documentos_aceptados`.
- Forma:
  - Cada elemento contiene exclusivamente:
    - `doc_id`
    - `contenido`


# Condiciones de ABORT
Se produce ABORT si se cumple cualquiera de las siguientes condiciones:
- El input es vacío.
- La colección `documentos_aceptados` queda vacía.
- Se viola el Contrato_Base_Revisor_Documental_v3.



# Herencia y precedencia
- Hereda de: Contrato_Base_Revisor_Documental_v3
- Orden de precedencia:
  1. Contrato_Base_Revisor_Documental_v3
  2. Contrato_Puerta_Entrada_v3
