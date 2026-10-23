# 🧠 Skills — Repositorio de Skills para Agentes de IA

Este repositorio contiene definiciones de **skills** listas para usar en agentes de IA (Pi, Claude, OpenCode, Cline, etc.). Cada skill es un conjunto de instrucciones, herramientas conceptuales y flujos de trabajo que le dan a un agente capacidades específicas.

## 📦 Skills disponibles

| Skill | Descripción |
|-------|-------------|
| [Socrates](./socrates/) | Facilitación estructurada de pensamiento crítico y creativo usando los Seis Sombreros, Mayéutica Socrática, Pensamiento Lateral, Brainstorming y Design Thinking |
| [Firefly Breakdown](./firefly-breakdown/) | Parte tareas complejas en un primer paso de 60 s + subtareas con tiempo estimado y las crea en Todoist (con OK). Para Cronos |

## 🚀 Cómo usar una skill

### En Pi (recomendado)
1. Copiá el contenido de `SKILL.md` de la skill que quieras
2. Incluilo en el prompt del agente o como parte de su system prompt
3. Activá la skill mencionando su **trigger** (ej: "socrates", "seis sombreros")

### En OpenCode / Cline / Claude
- Incluí el `SKILL.md` como parte del contexto del sistema
- Usá las instrucciones de activación detalladas en cada skill

## 📁 Estructura

```
skills/
├── README.md              ← Este archivo
├── LICENSE                ← MIT
├── socrates/              ← Skill: pensamiento crítico
│   ├── README.md          ← Descripción, uso y capacidades
│   └── SKILL.md           ← Definición completa de la skill
├── firefly-breakdown/     ← Skill: desglose de tareas (Cronos)
│   ├── README.md
│   └── SKILL.md
└── ... (más skills)
```

## 📜 Licencia

MIT
