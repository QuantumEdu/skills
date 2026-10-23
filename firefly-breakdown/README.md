# 🪄 Firefly Breakdown — Partir tareas complejas en pasos

Skill para **Cronos** (o cualquier agente de agenda) que convierte una tarea vaga o grande en un **primer paso de 60 segundos** + 3–5 subtareas con tiempo estimado, y solo con tu OK las crea como subtareas en Todoist bajo la tarea madre.

## 🎯 Capacidades
- Detecta complejidad (vaga, varios verbos, > ~30 min); si es simple no hace nada.
- Propone primer paso + subtareas + total con margen.
- Crea subtareas con `parentId` sin tocar fecha ni recurrencia de la madre.

## 🚀 Uso
Incluí `SKILL.md` en el contexto del agente y activá con "parte esta tarea", "desglosa", "firefly" o "primer paso".

## 🙏 Crédito
Inspirada en [firefly](https://github.com/mikaelaldy/firefly) de mikaelaldy (MIT).
