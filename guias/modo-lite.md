# Guía: Modo Lite

> Adaptación de HIM para proyectos pequeños. Mantiene las 4 fases pero con duración exprés y artefactos mínimos.

---

## Cuándo usar Modo Lite

- Scripts de automatización
- Utilidades de línea de comandos
- Herramientas internas de 1 propósito
- Prototipos rápidos
- Proyectos estimados en **3-10 días totales**

**No usar** si: múltiples usuarios, persistencia de datos compleja, integración con múltiples sistemas externos, o clientes reales.

---

## Las 4 fases exprés

| Fase | Duración máx | Artefactos |
|------|-------------|------------|
| **Concepción** | 2 horas | 1 párrafo de visión dentro del spec. Sin Project Vision separada. |
| **Elaboración** | 4 horas | Spec mínimo: 3-5 escenarios Gherkin. Sin ADRs ni prototipo. |
| **Construcción** | 2 días | IA implementa. Humano revisa 1 vez. Review: solo Pasa/No Pasa. |
| **Transición** | 1 hora | Puesta en marcha. Release note de 1 línea. Sin guía de operación. |

---

## Artefactos: qué se omite vs Modo Completo

| Artefacto | Modo Completo | Modo Lite |
|-----------|--------------|-----------|
| Project Vision | Documento 1 pág | 1 párrafo dentro del spec |
| User Types | Documento separado | No aplica (1 usuario) |
| Risk List | Tabla con mitigaciones | 1 línea si aplica |
| Glosario | Documento separado | No aplica |
| Feature Map | Lista priorizada | Feature única |
| ADRs | Documento formal | No aplica |
| Mapa dependencias | Diagrama/lista | No aplica |
| Prototipo visual | Wireframes | No aplica |
| Review Records | Registro formal | Solo Pasa/No Pasa |
| Guía de operación | Documento completo | No aplica |

---

## Project Vision Lite

No se crea archivo separado. Se escribe al inicio del spec:

```
Script: [nombre]
Qué hace: [una línea]
Para qué: [problema que resuelve]
Quién lo usa: [normalmente "yo" o "el equipo"]
Riesgo principal: [si aplica]
```

---

## Regla de escalado

Si durante Concepción Lite detectas que el proyecto necesita más de 10 días o involucra más de lo previsto (varios usuarios, DB, integraciones externas), **escala a Modo Completo**. No hay penalización: lo que avanzaste en Lite se migra al Project Vision completo.

---

> Ver `ejemplos/docker-log-cleaner.md` para un ejemplo real de Modo Lite.
