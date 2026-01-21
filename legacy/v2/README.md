# Revisor de Documentación Técnica v2

## 1. Qué es

Un proceso que transforma documentación técnica en un informe estructurado de hallazgos y sugerencias.

Opera bajo reglas fijas definidas en el contrato `contrato_revisor_documentacion_tecnica_v2`.

## 2. Qué no es

- No es un auditor.
- No es un validador técnico del sistema.
- No es un evaluador de calidad.
- No toma decisiones arquitectónicas.
- No reescribe ni corrige documentación.

## 3. Input esperado

- **Artefacto:** Documentación del proyecto.
- **Forma:** Texto plano.
- **Validación:**
  - Solo documentos no vacíos.
  - Solo documentos accesibles en texto plano.
  - Documentos ausentes o duplicados se omiten.
- **Regla:** Solo se considera información explícitamente presente en el artefacto.

## 4. Output esperado

- **Artefacto:** Informe de hallazgos y sugerencias.
- **Formato:** Markdown estructurado.

### Estructura

```
Hallazgos:
  - categoria
  - referencia_explicita
  - descripcion_breve
  - estado: {presente | propuesto}

Sugerencias:
  - hallazgo_id_ref
  - accion_documental
```

### Reglas del output

- `estado=propuesto` solo si el documento lo indica explícitamente.
- Cada sugerencia requiere un hallazgo (relación 1:1).
- Sugerencias solo documentales.
- Sin comparación de estados.
- Sin evaluación de impactos.

## 5. Reglas clave

**Operaciones permitidas:**
- Lectura literal del artefacto de entrada.
- Aplicación de checklist fija.
- Extracción de referencias explícitas.
- Emisión de output estructurado según contrato.

**Checklist aplicada:**
- Coherencia interna del documento.
- Correspondencia entre afirmaciones y referencias explícitas.
- Consistencia de versiones si se mencionan.
- Presencia de secciones anunciadas en el documento.

**Prohibiciones:**
- Crear conocimiento no presente en el input.
- Inferir, interpretar, completar, introducir, suplir o deducir información.
- Proponer o rediseñar arquitectura, flujos o decisiones técnicas.
- Usar fuentes externas.
- Reutilizar ejecuciones previas.
- Priorizar hallazgos o sugerencias.
- Asignar severidad, impacto o riesgo.
- Inferir intención, planificación o evolución futura.
- Emitir razonamiento explícito o texto fuera del formato.

**Determinismo:**
- Mismo input produce mismo output.

## 6. Diferencias v1 → v2

| Aspecto | v1 | v2 |
|---------|----|----|
| Validación de input | Implícita | Explícita (vacíos, accesibilidad, duplicados) |
| Campo `estado` en hallazgos | No existe | `{presente \| propuesto}` |
| Reglas de output | Genéricas | Reglas duras específicas |
| Prohibiciones | 7 reglas | 10 reglas (añade priorización, severidad, intención) |
| Checklist | 5 puntos (incluye precisión técnica, omisiones) | 4 puntos (incluye secciones anunciadas) |
| Formato de salida | No especificado | Salida única, sin texto fuera de formato |

## 7. Limitaciones explícitas

- No cubre auditoría.
- No cubre validación técnica del sistema.
- No cubre evaluación de calidad del modelo.
- No cubre decisiones arquitectónicas.
- Toda operación no listada como permitida está prohibida.
