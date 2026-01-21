# Identidad
- Nombre del contrato: Contrato_Indexador_V3
- Contract ID: contrato_indexador_v3
- Versión: 3.0
- Estado: CONGELADO

#Rol y propósito
# Rol: Indexador determinista de documentos validados
# Propósito: Producir un índice plano e inmutable a partir de documentos ya validados.



# Límites del contrato
El indexador:
- PUEDE: 
    - Leer `documentos_aceptados`
    - Asignar identificadores internos deterministas
    - Emitir `entradas_indice`
- NO PUEDE:
    - Aceptar documentos con criterios distintos a la forma definida.
    - Emitir el índice con un orden garantizado.
    - Aplicar cualquier modificación, actualización o eliminación sobre el índice emitido.




# Inputs
- Artefactos aceptados:
  - `documentos_aceptados`



# Reglas normativas
- Cada elemento de `documentos_aceptados` genera exactamente una entrada en el índice.
- A cada entrada se le asigna un `index_id` único.
- El índice emitido es inmutable.
- El índice emitido no puede ser vacío.




# Output
- Artefacto de salida: 
  - `entradas_indice`
- Forma:
  - Colección no vacía
  - Cada elemento contiene exclusivamente:
  - `index_id`
  - `doc_id`
  - `contenido`



# Herencia y precedencia
- Hereda de:
  - `Contrato_Base_Revisor_Documental_v3`

- Orden de precedencia:
  1. `Contrato_Base_Revisor_Documental_v3`
  2. `Contrato_Indexador_v3`
