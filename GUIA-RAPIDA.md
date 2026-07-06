# Guía Rápida HIM

> Human-In-the-loop Methodology — RUP + Spec-Driven + IA. El humano decide, la IA ejecuta.

---

## Las 4 fases

```
Concepción → Elaboración → Construcción → Transición
  2-5 días     3-10 días     5-20 días      2-5 días
```

Cada fase tiene un **gate** que debe cumplirse para avanzar.

---

## Artefactos por fase

| Fase | Artefactos |
|------|------------|
| **Concepción** | Project Vision, User Types, Feature Map (Gherkin), Risk List, Glosario |
| **Elaboración** | Specs detallados (Gherkin + metadata), ADRs, Mapa de dependencias |
| **Construcción** | Código, Tests, Review Records |
| **Transición** | Release Notes, Guía de operación, Cierre de iteración |

---

## El spec (artefacto central)

```yaml
id: HIM-001
feature: [nombre]
prioridad: [alta|media|baja]
estimacion: [1-13 puntos]
estado: [borrador|validado|...]
```

```gherkin
Como [rol]
Quiero [acción]
Para [beneficio]

Escenario: [nombre]
  Dado [contexto]
  Cuando [acción]
  Entonces [resultado]
```

---

## Modo Lite (scripts pequeños)

4 fases exprés: Concepción (2h) → Elaboración (4h) → Construcción (2d) → Transición (1h)

Omite: ADRs, prototipos, User Types, glosario, Review Records, guía de operación.

---

## Roles

| Rol | Quién | Qué hace |
|-----|-------|----------|
| Especificador | Humano | Escribe specs |
| Ejecutor | IA | Implementa specs |
| Validador | Humano | Revisa y aprueba |
| Arquitecto | Humano + IA | Decide arquitectura |

---

## Validación rápida

| Alerta | Significado |
|--------|-------------|
| Error | Bloquea, debe corregirse |
| Warning | Revisar, no bloquea |
| Info | Observación |

---

## Principios

1. El humano siempre decide
2. Sin spec aprobado no hay construcción
3. Documentación justa (ni mucha ni poca)
4. Escalable (script → sistema grande)
5. Traza completa
6. Iterativo

---

> Documentación completa en `fundamentos/definicion.md`
> Templates en `templates/`
> Guías detalladas en `guias/`
