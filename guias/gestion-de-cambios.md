# Guía: Gestión de Cambios y Rechazos

> Cómo manejar cambios durante Construcción y qué hacer cuando la IA no pasa la revisión humana.

---

## 1. Cambios durante Construcción

Si durante Construcción alguien solicita un cambio sobre un spec ya aprobado:

### Cambio menor

No invalida escenarios existentes ni cambia el alcance del spec.

Ejemplos: cambiar el mensaje de un error, agregar un campo opcional a una respuesta, renombrar un botón.

**Qué hacer:**
1. Se modifica el spec (nueva versión)
2. Se re-valida
3. La IA ajusta la implementación
4. No se retrocede de fase

### Cambio mayor

Invalida escenarios existentes o cambia el alcance.

Ejemplos: "en lugar de eliminar logs, queremos comprimirlos", "ahora también debe soportar autenticación".

**Qué hacer:**
1. El spec se congela en su estado actual
2. La implementación parcial se archiva (no se pierde)
3. El spec vuelve a Elaboración
4. Se replantea, re-valida y pasa a una nueva iteración de Construcción

### Clasificación

El humano (Especificador/Validador) decide si un cambio es menor o mayor. Si hay duda: preguntar "¿Esto invalida algún escenario existente?".
- Si la respuesta es sí → cambio mayor
- Si la respuesta es no → cambio menor

---

## 2. Rechazos durante revisión humana

Cuando la implementación de un spec **no pasa** la revisión del Validador:

### Ciclo de corrección

```
1. Humano rechaza implementación
2. Humano explica qué no cumple del spec (punto específico)
3. IA corrige
4. Humano revisa de nuevo
5. Si pasa → spec completado. Si no → repetir desde paso 2.
```

### Límite: 3 intentos

- Máximo 3 correcciones por spec en una misma iteración.
- Si tras 3 intentos el spec sigue sin pasar:
  - El spec **vuelve a Elaboración**
  - Se analiza si el spec original estaba mal definido (ambiguo, incompleto) o si el problema es técnico
  - Se reescribe el spec con más claridad y se inicia Construcción de nuevo

### Aborto definitivo

Si tras 3 intentos en Elaboración + 3 intentos en Construcción el spec no avanza:
- Se marca como **rechazado**
- Se documenta por qué no fue viable
- Se replantea en una iteración futura o se descarta

---

## 3. Diagrama completo

```
Spec aprobado en Elaboración
       ↓
Construcción: IA implementa
       ↓
Humano revisa
  ├── Pasa → Siguiente spec o Cierre
  └── No pasa → IA corrige (intento 1)
                   ↓
                Humano revisa
                  ├── Pasa → OK
                  └── No pasa → IA corrige (intento 2)
                                  ↓
                               Humano revisa
                                 ├── Pasa → OK
                                 └── No pasa → IA corrige (intento 3)
                                                 ↓
                                              Humano revisa
                                                ├── Pasa → OK
                                                └── No pasa → Spec vuelve a Elaboración

Durante Construcción llega cambio:
  ├── Menor → Modifica spec + IA ajusta directo
  └── Mayor → Spec se congela → vuelve a Elaboración
```
