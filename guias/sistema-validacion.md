# Guía: Sistema de Validación de Specs

> Reglas con las que el sistema asiste al humano validando que un spec está bien formado, completo, consistente y sin ambigüedades.

---

## Niveles de alerta

| Nivel | Significado | Acción |
|-------|-------------|--------|
| **Error** | El spec no puede pasar a Construcción | Bloquea el gate |
| **Warning** | Problema no crítico que el humano debería revisar | No bloquea |
| **Info** | Observación o sugerencia | No bloquea |

---

## 1. Validación sintáctica

| Regla | Nivel | Descripción |
|-------|-------|-------------|
| Gherkin bien formado | Error | Escenarios deben tener Dado/Cuando/Entonces |
| Metadata completa | Error | Todos los campos requeridos del YAML deben estar presentes |
| IDs únicos | Error | No puede haber dos specs con el mismo ID |
| Versión presente | Warning | Si no hay `version`, se sugiere agregarlo |

## 2. Validación de completitud

| Regla | Nivel | Descripción |
|-------|-------|-------------|
| Escenario feliz presente | Error | Debe existir al menos 1 escenario del caso principal |
| Escenario de error presente | Warning | Si puede fallar, debe tener escenario de error |
| Escenario borde presente | Warning | Si hay valores límite, debe tener escenario que los cubra |
| Criterios vacíos | Error | No se acepta un spec sin escenarios |
| Historia incompleta | Warning | Debe tener Como/Quiero/Para completos |
| Mínimo escenarios | Warning | Completo: < 5. Lite: < 3 |

## 3. Validación de ambigüedad

| Regla | Nivel | Descripción |
|-------|-------|-------------|
| Términos vagos | Warning | "rápido", "eficiente", "seguro", "bonito" sin medida concreta |
| Tiempos sin métrica | Warning | "debe responder rápido" → sugerir "en menos de X ms" |
| Cantidades sin unidad | Warning | "no debe pesar mucho" → sugerir "menos de X MB" |
| "Entre otros" / "etc" | Warning | Lista incompleta. Sugerir hacerla explícita |
| Sujeto ambiguo | Warning | "Se procesa y se envía" → ¿quién? Sugerir sujeto explícito |

## 4. Validación de consistencia entre specs

| Regla | Nivel | Descripción |
|-------|-------|-------------|
| Feature duplicada | Warning | Dos specs tienen el mismo valor en `feature` |
| Dependencia inexistente | Error | `dependencias` referencia un spec ID que no existe |
| Dependencia circular | Error | A depende de B que depende de A |
| Términos contradictorios | Info | Mismo término con distinto significado entre specs |

## 5. Validación de testabilidad

| Regla | Nivel | Descripción |
|-------|-------|-------------|
| "Entonces" no verificable | Warning | "El usuario debe sentir que..." no es verificable. Reformular como comportamiento observable |
| "Dado" sin estado previo | Info | Asume un estado no definido en ningún spec |
| Condiciones imposibles | Error | Dado/Cuando contradictorios |

---

## Reporte de validación

El sistema devuelve un reporte estructurado:

```
spec_id: HIM-042
estado: NO_APROBADO
errores: 2
warnings: 3
info: 1
detalle:
  - regla: Gherkin bien formado
    nivel: error
    mensaje: "El Escenario 1 no tiene 'Cuando'"
    linea: 12
  - regla: Términos vagos
    nivel: warning
    mensaje: "'rápido' en línea 18 no tiene métrica"
    sugerencia: "Reemplazar por 'en menos de 2 segundos'"
```

---

## Flujo de validación

```
Humano escribe/edita spec
       ↓
Sistema valida en tiempo real (mientras escribe)
       ↓
Humano pide validación explícita (botón "Validar")
       ↓
Sistema genera reporte
       ↓
Humano revisa el reporte
       ↓
[Si hay errores] → Corrige → Vuelve a validar
[Si solo warnings] → Decide si pasa o corrige
[Sin errores] → Spec validado → Listo para Construcción
```
