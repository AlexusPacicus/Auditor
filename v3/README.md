# Capa Contractual v3

**Estado:** CONGELADO

---

## Qué es esta capa

Capa de gobernanza contractual.

Define una base estable y controlada mediante contratos que regulan ejecución.
---

## Principios arquitectónicos

1. **Determinismo absoluto.** Mismo input válido produce mismo resultado observable o mismo ABORT.

2. **Aislamiento total.** Sin memoria, sin estado persistente, sin dependencia entre ejecuciones.

3. **Dominio cerrado.** Solo se opera sobre datos explícitamente presentes en artefactos de entrada o dependencias exógenas declaradas.

4. **Prohibición de interpretación.** No se evalúa intención, calidad ni adecuación.

5. **Trazabilidad literal.** Todo elemento emitido es trazable 1:1 a contenido literal de entrada.

6. **Silencio explicativo.** Prohibida emisión de razonamiento o justificación fuera del artefacto contractual.

7. **ABORT como resultado válido.** ABORT no es error. Es resultado contractual ante violación o imposibilidad de cumplimiento.

---

## Topología contractual

```
Entrada → Indexador → Mecánico → Emisor → Validador
                          ↑
                   reglas_mecanicas
                   (dependencia exógena)
```
Flujo acíclico y determinista.

Los artefactos se producen de forma secuencial hasta el Emisor.
El Validador consume múltiples artefactos previos para verificación de coherencia.

No existen ciclos ni flujos alternativos de ejecución.

---

## Roles contractuales

| Contrato | Rol | Artefacto consumido | Artefacto emitido |
|----------|-----|---------------------|-------------------|
| Puerta de Entrada | Gate de admisión formal | colección de documentos | `documentos_aceptados` |
| Indexador | Indexación determinista | `documentos_aceptados` | `entradas_indice` |
| Detector Mecánico | Detección literal por reglas | `entradas_indice` | `hallazgos_mecanicos` |
| Emisor | Reemisión bajo autoridad contractual distinta | `hallazgos_mecanicos` | `hallazgos_emisor` |
| Validador | Gate binario de coherencia | `hallazgos_mecanicos`, `hallazgos_emisor` | `ok` (binario) |

---

## Gobernanza y precedencia

Existe un Contrato Base: `Contrato_Base_Revisor_Documental_v3`.

Todo contrato v3 hereda íntegramente del Contrato Base.

**Orden de precedencia (invariable):**

1. `Contrato_Base_Revisor_Documental_v3`
2. Contrato específico

Los contratos específicos pueden restringir invariantes del Contrato Base.

Los contratos específicos no pueden relajar invariantes del Contrato Base.

Conflicto entre contrato específico y Contrato Base se resuelve aplicando Contrato Base.

Violación del Contrato Base ⇒ ABORT.

---

## Dependencias exógenas

| Artefacto | Consumido por | Producido por |
|-----------|---------------|---------------|
| `reglas_mecanicas` | Detector Mecánico | Ningún contrato v3 |

Las dependencias exógenas son de solo lectura.

No son modificables.

No son derivables.

---

## Qué NO es este sistema

- No es un pipeline de procesamiento flexible.
- No es una arquitectura extensible por plugins.
- No es un sistema de reglas de negocio.
- No es un sistema de análisis semántico.
- No es un sistema que interpreta, infiere o explica.
- No es un sistema que propone decisiones.
- No es un sistema que evalúa calidad.

---

## Estado de la versión

Todos los contratos v3 están en estado **CONGELADO**.

No se aceptan modificaciones sin versionado explícito.

---

## Fuente de verdad

Cada contrato tiene dos manifestaciones:

- Documento Markdown: descripción contractual legible.
- Documento YAML: fuente de verdad ejecutable.

En caso de discrepancia: prevalece el YAML.

---

## Criterio de calidad

Un contrato v3 es correcto si:

1. Hereda íntegramente del Contrato Base.
2. No relaja ningún invariante del Contrato Base.
3. Define explícitamente sus límites.
4. Define explícitamente sus artefactos de entrada y salida.
5. Define condiciones de ABORT o las hereda del Contrato Base.
6. Tiene manifestación YAML como fuente de verdad.
7. Está en estado CONGELADO.

Una ejecución es correcta si:

1. Termina en artefacto de salida válido.
2. Termina en ABORT.

No existen otros estados terminales válidos.
