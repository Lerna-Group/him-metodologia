# Template de Spec HIM

> El artefacto central de HIM. Un spec describe una unidad de funcionalidad en Gherkin con metadata. Es el contrato entre el humano (Especificador) y la IA (Ejecutor).

---

## Estructura

```yaml
---
id: HIM-XXX
titulo: [nombre corto]
feature: [feature a la que pertenece]
fase: [concepcion | elaboracion]
prioridad: [alta | media | baja]
dependencias:
  - HIM-XXX
estimacion: [1 | 2 | 3 | 5 | 8 | 13]
estimacion_real: [completar en Transición]
autor: [nombre]
fecha: [YYYY-MM-DD]
estado: [borrador | validado | en_construccion | completado | rechazado]
version: 1
---
```

```gherkin
Como [rol de usuario]
Quiero [acción o funcionalidad]
Para [beneficio o razón]

Escenario: [nombre del escenario]
  Dado [contexto inicial]
  Cuando [evento o acción]
  Entonces [resultado esperado]

Escenario: [escenario de error]
  Dado [contexto]
  Cuando [acción que provoca error]
  Entonces [resultado esperado para el error]
```

---

## Campos de metadata

| Campo | Obligatorio | Descripción |
|-------|-------------|-------------|
| `id` | Sí | Identificador único del spec (HIM-001, HIM-002...) |
| `titulo` | Sí | Nombre corto y descriptivo |
| `feature` | Sí | Feature a la que pertenece (agrupa specs relacionados) |
| `fase` | Sí | Fase en la que se creó el spec |
| `prioridad` | Sí | Alta, media o baja |
| `dependencias` | No | IDs de specs de los que depende este |
| `estimacion` | Sí | Puntos de complejidad (ver `guias/estimacion.md`) |
| `estimacion_real` | No | Se completa al cerrar el spec en Transición |
| `autor` | Sí | Quién escribió el spec |
| `fecha` | Sí | Fecha de creación o última modificación |
| `estado` | Sí | Estado actual del spec en el ciclo de vida |
| `version` | Sí | Número de versión (incrementa con cada modificación) |

---

## Historia de usuario

Formato estándar:

```
Como [rol]
Quiero [acción]
Para [beneficio]
```

Los 3 campos son obligatorios. Si falta alguno, la validación lo marcará como warning.

---

## Escenarios Gherkin

Cada escenario sigue la estructura **Dado-Cuando-Entonces**:

- **Dado:** contexto o estado inicial del sistema
- **Cuando:** acción que ejecuta el usuario o el sistema
- **Entonces:** resultado observable y verificable

### Tipos de escenarios requeridos

| Tipo | Obligatorio | Descripción |
|------|-------------|-------------|
| Caso feliz | Sí | El flujo principal, cuando todo funciona correctamente |
| Caso de error | Recomendado | Qué pasa cuando algo sale mal |
| Caso borde | Recomendado | Valores límite o condiciones especiales |

En Modo Lite: mínimo 3 escenarios. En Modo Completo: mínimo 5.

---

## Notas técnicas (opcional)

Sección libre para información que la IA necesita saber para implementar:

- APIs o servicios involucrados
- Reglas de negocio complejas
- Consideraciones de rendimiento o seguridad

---

## Criterios de validación

Checklist para el revisor humano antes de aprobar el spec:

- [ ] Los 3 campos de la historia de usuario están completos
- [ ] Los escenarios cubren el comportamiento esperado
- [ ] Los casos borde y error están contemplados
- [ ] El lenguaje es preciso y no ambiguo
- [ ] Una IA puede implementar a partir de este spec sin aclaraciones externas
- [ ] La estimación en puntos es coherente con la complejidad

---

## Ejemplo mínimo

```yaml
---
id: HIM-001
titulo: Autenticación de usuario
feature: Auth
fase: elaboracion
prioridad: alta
dependencias: []
estimacion: 5
autor: Henry
fecha: 2026-07-05
estado: validado
version: 1
---
```

```gherkin
Como usuario registrado
Quiero iniciar sesión con mi correo y contraseña
Para acceder a mi cuenta

Escenario: Inicio de sesión exitoso
  Dado que estoy en la página de login
  Cuando ingreso credenciales válidas y presiono "Iniciar sesión"
  Entonces soy redirigido al dashboard

Escenario: Contraseña incorrecta
  Dado que estoy en la página de login
  Cuando ingreso una contraseña incorrecta
  Entonces veo un mensaje "Credenciales inválidas"
```

---

> Ver `ejemplos/docker-log-cleaner.md` para un spec completo.
