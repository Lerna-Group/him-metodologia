# Guía: Estimación en HIM

> Cómo estimar el tiempo de implementación de un spec y medir precisión para mejorar con el tiempo.

---

## Unidad de estimación: puntos por spec

Cada spec se estima en **puntos** según su complejidad. No en horas. Los puntos se calibran con la experiencia.

### Tabla de complejidad

| Puntos | Tipo | Ejemplo |
|--------|------|---------|
| **1** | Trivial | Cambiar un mensaje, ajustar un color, renombrar variable |
| **2** | Simple | Agregar un campo a un formulario, un endpoint CRUD simple |
| **3** | Media | Feature con 3-5 escenarios, sin integraciones externas |
| **5** | Compleja | Feature con integración externa, lógica de varias ramas |
| **8** | Muy compleja | Feature que cruza múltiples specs, DB + API + UI |
| **13** | Incierta | No se entiende bien → requiere más análisis en Elaboración |

### Reglas

- Si un spec da más de 13 puntos, **debe dividirse** en specs más pequeños.
- Si dudas entre 3 o 5, usa 5 (mejor sobreestimar).
- Los puntos los asigna el humano (Especificador) al validar el spec.

---

## Formato en el spec

Se agrega al metadata YAML:

```yaml
---
id: HIM-XXX
titulo: ...
estimacion: 5          # puntos estimados (lo pones en Elaboración)
estimacion_real: 4     # puntos reales (lo completas en Transición)
---
```

---

## Velocidad y calibración

Después de cada Construcción/Transición se calcula la velocidad:

```
Puntos completados: [suma de puntos reales de specs aprobados]
Días hábiles: [días de la iteración]
Velocidad: [puntos / días] = [pts/día]
```

### Ejemplo de calibración

| Iteración | Puntos | Días | Velocidad |
|-----------|--------|------|-----------|
| 1 | 8 | 5 | 1.6 pts/día |
| 2 | 10 | 6 | 1.67 pts/día |
| 3 | 7 | 4 | 1.75 pts/día |

→ Velocidad estimada: **1.7 pts/día**. Un spec de 5 puntos ≈ 3 días.

---

## Cómo empezar sin datos previos

Para la primera iteración, asume:
- **1 punto ≈ 1 día** (trabajo combinado humano + IA)
- Un spec de 3 puntos ≈ 3 días
- Ajusta después de la primera iteración con datos reales

---

## Uso en el flujo HIM

| Fase | Acción |
|------|--------|
| **Elaboración** | Asignar puntos a cada spec en el metadata |
| **Construcción** | Trackear puntos completados vs días |
| **Transición** | Registrar puntos reales en el Cierre de iteración |
| **Siguiente iteración** | Usar velocidad calibrada para planificar carga |

---

> Ver `templates/cierre-iteracion.md` para el template donde se registran estos datos.
