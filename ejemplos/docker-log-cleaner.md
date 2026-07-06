# Ejemplo: Spec HIM completo (Modo Lite)

> Script: docker-log-cleaner — elimina logs de contenedores Docker con más de 30 días.

Este ejemplo muestra un spec completo de principio a fin, usando **Modo Lite** (ver `guias/modo-lite.md`).

---

## Fase 1: Concepción exprés

### Project Vision Lite

```
Script: docker-log-cleaner
Qué hace: Elimina logs de contenedores Docker con más de 30 días
Para qué: Liberar espacio en disco del servidor sin hacerlo manual
Quién lo usa: Henry (admin del servidor)
Riesgo: Borrar logs que aún se necesitan para debug
```

---

## Fase 2: Elaboración exprés

### Spec HIM-001: Limpiar logs Docker antiguos

```yaml
---
id: HIM-001
titulo: Limpiar logs Docker antiguos
feature: docker-log-cleaner
fase: elaboracion
prioridad: alta
dependencias: []
estimacion: 3
estimacion_real: 2
autor: Henry
fecha: 2026-07-05
estado: completado
version: 1
---
```

**Historia de usuario**

> **Como** administrador del servidor
> **Quiero** ejecutar un script que elimine logs de Docker con más de 30 días
> **Para** liberar espacio en disco sin revisar cada contenedor manualmente

**Escenarios**

```gherkin
Escenario: Limpieza normal de logs antiguos
  Dado que hay contenedores Docker con logs de más de 30 días
  Cuando ejecuto el script sin argumentos
  Entonces el script elimina los logs con fecha anterior a 30 días
  Y muestra un resumen de cuánto espacio liberó

Escenario: No hay logs antiguos
  Dado que todos los logs Docker tienen menos de 30 días
  Cuando ejecuto el script
  Entonces el script informa que no hay logs que limpiar
  Y termina con código 0

Escenario: Límite de días personalizado
  Dado que quiero conservar logs de solo 7 días
  Cuando ejecuto el script con --days 7
  Entonces el script elimina logs con más de 7 días

Escenario: Modo dry-run
  Dado que quiero ver qué se borraría antes de hacerlo
  Cuando ejecuto el script con --dry-run
  Entonces el script muestra qué archivos eliminaría
  Y no elimina ningún archivo

Escenario: Error: directorio de logs no existe
  Dado que el directorio /var/lib/docker no existe o no es accesible
  Cuando ejecuto el script
  Entonces el script muestra un mensaje de error claro
  Y termina con código 1
```

**Validación**

- [x] Escenario feliz presente
- [x] Escenario de error presente (directorio no existe)
- [x] Escenarios borde presentes (sin logs, dry-run, días personalizado)
- [x] Lenguaje preciso y no ambiguo
- [x] Una IA puede implementar sin aclaraciones externas

---

## Fase 3: Construcción

IA implementa según el spec. Humano revisa.

**Review:** Pasa. Implementación cumple los 5 escenarios. Se agregó logging adicional sugerido por la IA, el humano lo aprobó por útil.

---

## Fase 4: Transición exprés

**Release note:** `docker-log-cleaner v1 — Script que limpia logs Docker >30 días. Uso: python clean_logs.py [--days N] [--dry-run]`

**Instalación:** Copiado a `~/scripts/docker-log-cleaner/`.

---

> Ver `templates/spec-him.md` para el template usado.
