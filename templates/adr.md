# Template: ADR (Architecture Decision Record)

> Registro ligero de decisiones arquitectónicas. Se crea en Elaboración para decisiones con impacto significativo.

---

## Formato

```markdown
# ADR-[ID]: [Título corto]

**Fecha:** YYYY-MM-DD
**Status:** [Propuesto | Aceptado | Reemplazado]

## Contexto
¿Qué problema estábamos resolviendo? ¿Qué opciones consideramos? ¿Qué restricciones había?

## Decisión
¿Qué elegimos y por qué?

## Consecuencias
- Positivas: ¿qué ganamos?
- Negativas: ¿qué perdemos o comprometemos?
- Técnicas: ¿cómo afecta al código/arquitectura?

## Alternativas consideradas
- Opción A: [descripción breve + por qué no se eligió]
- Opción B: [descripción breve + por qué no se eligió]
```

---

## Reglas de uso

- Se crean en **Elaboración** y se revisan si aplican cambios en Construcción.
- No toda decisión merece ADR. Solo las de impacto significativo: stack, base de datos, arquitectura, APIs externas, patrones.
- Si la decisión es obvia o reversible en minutos, no se documenta.
- Si un ADR queda obsoleto, se marca como `Reemplazado` y se referencia el nuevo.

## Cuándo escribir un ADR

| Situación | ¿ADR? |
|-----------|-------|
| Elegir base de datos | Sí |
| Decidir patrón de diseño | Sí |
| Framework o librería principal | Sí |
| Nombre de variable interna | No |
| Color de un botón | No |
| Estructura de directorios | Depende (si es crítica para la arquitectura, sí) |

---

## Ejemplo

```markdown
# ADR-001: PostgreSQL como base de datos principal

**Fecha:** 2026-07-05
**Status:** Aceptado

## Contexto
Necesitamos una base de datos. Los datos son relacionales. El equipo conoce PostgreSQL.

Opciones: PostgreSQL, SQLite, MySQL.

## Decisión
Usamos PostgreSQL 16. Es la que el equipo conoce mejor y soporta lo que necesitamos.

## Consecuencias
- Positivas: madurez, conocida, buena documentación
- Negativas: más pesada que SQLite para desarrollo local
- Técnicas: usaremos SQLAlchemy async como ORM

## Alternativas consideradas
- SQLite: no soporta la concurrencia que necesitamos
- MySQL: conocida pero PostgreSQL tiene mejor soporte de tipos y extensiones
```
