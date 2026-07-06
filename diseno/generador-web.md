# Diseño: Generador Web de Specs HIM

> Aplicación web que guía al usuario en la creación de specs bien formados en formato HIM.

---

## Objetivo

Que el usuario pueda crear un spec HIM sin conocer el template de memoria. El sistema lo guía paso a paso, valida en tiempo real, y produce un spec listo para Construcción.

---

## Flujo del usuario (6 pasos)

### Paso 1: Nueva feature
Usuario ingresa nombre y descripción libre (1-2 párrafos).
El sistema propone historia de usuario y Feature Map inicial.

### Paso 2: Refinar historia
Usuario edita la historia propuesta (Como/Quiero/Para).
Sistema valida que los 3 campos estén completos.

### Paso 3: Agregar escenarios
Sistema guía:
- "¿Cuál es el caso feliz?" → Completa Dado/Cuando/Entonces
- "¿Qué puede salir mal?" → Escenario de error
- "¿Hay casos borde?" → Escenario borde
- Usuario escribe en lenguaje natural, sistema estructura en Gherkin

### Paso 4: Metadata
Sistema completa automáticamente:
- ID (autogenerado)
- Feature (heredado del paso 1)
- Prioridad (usuario selecciona Alta/Media/Baja)
- Dependencias (usuario selecciona de lista de specs existentes)
- Estimación (usuario selecciona puntos según tabla de complejidad)

### Paso 5: Validación
Sistema ejecuta todas las reglas de validación (ver `guias/sistema-validacion.md`).
Usuario corrige hasta que no haya errores.

### Paso 6: Aprobar
Usuario aprueba el spec → estado cambia a "validado" → listo para Construcción.

---

## Pantallas

### Dashboard
- Lista de specs agrupados por estado
- Botón "Nuevo spec"
- Filtros por fase, prioridad, feature

### Editor de spec
- Panel izquierdo: formulario guiado (pasos 1-4)
- Panel derecho: previsualización del spec completo
- Barra inferior: estado de validación en tiempo real

### Detalle de spec
- Spec completo renderizado
- Reporte de validación
- Botones: Editar, Validar, Aprobar, Archivar

### Mapa de dependencias
- Lista de qué specs dependen de cuáles
- Versión gráfica opcional (futuro)

---

## Datos que almacena

```yaml
spec:
  id: HIM-XXX
  titulo: string
  feature: string
  descripcion: text
  historia_usuario:
    como: string
    quiero: string
    para: string
  escenarios:
    - nombre: string
      dado: string
      cuando: string
      entonces: string
      tipo: [feliz | error | borde]
  metadata:
    prioridad: [alta | media | baja]
    dependencias: [HIM-XXX, ...]
    estimacion: int
    estimacion_real: int
    autor: string
    fecha_creacion: date
    fecha_actualizacion: date
    version: int
    estado: [borrador | validado | en_construccion | completado | rechazado]
  validacion:
    ultimo_reporte:
      errores: int
      warnings: int
      info: int
      detalle: [...]
  historial:
    - accion: string
      fecha: datetime
      usuario: string
```

---

## Reglas de UI

- El usuario nunca ve YAML ni Gherkin crudo si no quiere. La preview es opcional.
- Errores de validación se muestran en línea, al lado del campo correspondiente.
- El sistema sugiere correcciones con un clic para aceptar.
- Cada paso tiene "Siguiente" y "Anterior".
- Autosave mientras se edita.

---

## Lo que NO hace (por ahora)

- No es un gestor de proyectos
- No tiene integración con GitHub ni plataformas externas
- No agenda implementación ni asigna recursos
- No tiene login multi-usuario
