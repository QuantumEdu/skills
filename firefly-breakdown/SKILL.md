---
name: firefly-breakdown
description: >
  Parte tareas complejas o vagas en un primer paso de 60 segundos + 3–5 subtareas con
  tiempo estimado, y (solo con OK explícito) las crea como subtareas en Todoist bajo la
  tarea madre. Pensada para Cronos. Inspirada en firefly (mikaelaldy, MIT).
  Trigger: "parte esta tarea", "desglosa", "breakdown", "firefly", "primer paso",
  "no sé por dónde empezar", o cuando Cronos agrega una tarea que parece compleja.
license: MIT
metadata:
  author: QuantumEdu
  version: "1.0"
  inspired_by: https://github.com/mikaelaldy/firefly
---

## Cuando Usar

| Situación | Acción |
|-----------|--------|
| El usuario pide partir/desglosar una tarea | Evaluar y proponer |
| Cronos agrega una tarea que parece compleja | **Preguntar** primero: "¿La parto en pasos?" |
| La tarea es simple y concreta | No hacer nada (decirlo en una línea) |

**No usar cuando**: la tarea ya tiene subtareas, es una cita/evento con hora, o es un recordatorio de una sola acción.

---

## 1. Detectar complejidad

Una tarea es **compleja** si cumple al menos uno:
- **Vaga**: no dice qué entregable ni qué acción física/digital ("tesis", "ver lo del gym").
- **Varios verbos/acciones**: "cotizar, comparar y comprar…".
- **Duración probable > ~30 min**.

Si no cumple ninguno → **no-op**: `"«Comprar limones» ya es un paso concreto; no la parto."`

---

## 2. Prompt de descomposición (adaptado)

Usar internamente (redacción propia, idea de firefly: primer paso mínimo + siguientes acciones + margen):

```
Eres un coach de arranque para personas que se bloquean ante tareas grandes.
Tarea: «{titulo}»  Contexto: {descripcion, proyecto, fecha, etiquetas}
1. Primer paso: UNA acción minúscula, concreta y física o digital que se pueda
   hacer en ≤60 segundos (abrir, escribir una línea, buscar, juntar material).
   Nada de "planear" o "pensar".
2. Siguientes acciones: 3 a 5 subtareas en orden, cada una con verbo en
   infinitivo, resultado verificable y estimación en minutos (5–45).
3. Total estimado + margen sugerido (~25 %) por imprevistos.
No inventes datos del usuario; si falta info clave, haz 1 pregunta.
```

---

## 3. Formato de propuesta (mostrar al usuario)

```
🪄 «{tarea madre}» — propuesta de desglose
⚡ Primer paso (60 s): {acción}
1. {subtarea} — ~{n} min
2. {subtarea} — ~{n} min
3. {subtarea} — ~{n} min
⏱️ Total: ~{suma} min (+{margen} min de margen)
¿Creo estas subtareas en Todoist bajo la tarea madre? (sí / ajustar / no)
```

---

## 4. Crear en Todoist (solo con OK explícito)

- Esperar un "sí"/OK claro. "Ajustar" → regenerar; "no" → no tocar nada.
- Crear cada subtarea con `parentId` (`parent_id` en la API REST) = id de la tarea madre.
- El primer paso de 60 s va como **primera** subtarea (prefijo `⚡`).
- Heredar `projectId`/sección y etiquetas de la madre; estimación en la descripción
  o en `duration` si se usa.
- **No** poner fechas a las hijas salvo que el usuario lo pida.
- Confirmar con la lista creada (y link si existe).

---

## 5. Guardrails

- Nunca quitar ni cambiar la fecha ni la recurrencia de la madre.
- Nunca completar, mover ni borrar la madre.
- Nada se escribe en Todoist sin OK explícito del usuario.
- Máximo 5 subtareas; si hace falta más, proponer partir en dos tareas madre.
- Idioma: el del usuario (español por defecto). Tono breve, sin culpa.

---

## 6. Ejemplos

**Complejo** — «Cotizar tesis»
```
⚡ Primer paso (60 s): abrir una nota y escribir el tema de la tesis en una línea
1. Listar 3 asesores o servicios a contactar — ~15 min
2. Redactar mensaje de cotización (alcance, plazos) — ~15 min
3. Enviar mensaje a los 3 — ~10 min
4. Comparar respuestas en una tabla — ~20 min
⏱️ Total: ~60 min (+15 min de margen)
¿Creo estas subtareas en Todoist? (sí / ajustar / no)
```

**Simple (no-op)** — «Comprar agua garrafón»
```
«Comprar agua garrafón» ya es una acción concreta; no la parto.
```

---

## Atribución

Lógica e ideas de descomposición (primer paso de 60 s + siguientes acciones +
margen de tiempo) inspiradas en **[firefly](https://github.com/mikaelaldy/firefly)**
de **mikaelaldy**, licencia MIT. No se copia código; el prompt está redactado de nuevo.

> MIT License — Copyright (c) mikaelaldy. Se concede permiso, libre de cargos, para usar,
> copiar, modificar… sujeto a incluir el aviso de copyright y de permiso.
