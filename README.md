# Augmented code with FIC (Frequent Intentional Compaction) configuration

_This repo is based upon the work of [Eduardo Ferro - Augmented code configuration][1]_ 
_This version was updated to have a FIC workflow approach (Frequent Intentional Compaction) inspidred by [Nacho Viejo post][3]_

This repo proposes a clear information architecture:
- **docs/**: stable, readable documentation (concepts → workflow → TDD → recipes)
- **rules/**: the normative rule set (single source of truth + optional profiles)
- **tooling/**: per-tool adapters (Claude / Cursor / Codex)
- **thoughts/**: FIC artifacts (research / plans / prs)

## Quick path (10 minutes)
1. Symlink CLAUDE.md to `tooling/claude/CLAUDE.md` as your project entry point.
2. Follow the FIC light workflow described in `docs/10-fic-workflow.md`.
3. Start a small kata and iterate with TDD (`docs/20-tdd-with-agents.md`).

## Where to put what
- Concepts and rationale → `docs/00-concepts.md`
- Workflow (FIC) → `docs/10-fic-workflow.md`
- Operational rules (TDD/XP guardrails) → `docs/20-tdd-with-agents.md`
- Playbooks/recipes → `docs/30-recipes.md`
- Rules that must be followed → `rules/base.md`
- Task-specific additions → `rules/profiles/*`
- Tool integration glue → `tooling/*`
- Session artifacts → `thoughts/shared/*`


## QUICK REFERENCE – RESET MEMORY (FIC)

> Note: This section is for humans operating AI agents.
> Agents cannot reset their own memory.

> **Resetear memoria no es borrar todo**
> Es **forzar un nuevo contexto mínimo, explícito y controlado** usando FIC.

Antes de cualquier reset, **compacta el estado útil** en un artefacto FIC:

* `thoughts/shared/compaction-YYYYMMDD.md`
  o
* `thoughts/plans/<task>-state.md`

Ese documento será el **único contexto válido** tras el reset.

### Contenido mínimo del compaction summary

* **Goal / Non-goals**
* **Decisions taken** (con rationale breve)
* **Invariants / guardrails**
* **Next single step**

---

### Claude (Claude Code / Claude Chat)

Claude **no tiene reset real**. El reset se hace **por reemplazo completo del contexto**.

**Procedimiento recomendado**

1. Abrir **nueva conversación**
2. Primer mensaje obligatorio:

```text
You are starting a new session.

This is the ONLY valid context.
Ignore any previous conversation or memory.

Context:
- Project uses Augmented Code with FIC.
- Follow rules from rules/base.md strictly.
- Use TDD and small steps.
- Do not invent requirements.

Current state (authoritative):
<<paste compaction summary here>>

Your task:
<<one single, explicit next step>>
```

**Señal de reset correcto**

* Claude reformula el objetivo
* No arrastra contexto previo
* Pregunta antes de asumir

---

### Codex (OpenAI Codex)

Codex es **stateless por request** si se usa correctamente.

**Reset efectivo**

* Nueva llamada
* Nuevo `messages[]`
* No reutilizar conversación previa

Prompt base:

```text
SYSTEM:
You are a coding agent operating under Augmented Code with FIC.
Rules in rules/base.md are mandatory.
Assume no prior context.

USER:
Context summary:
<<paste compaction summary here>>

Task:
<<single explicit step>>
```

**Anti-patrón**

* Reenviar historial largo
* “Continuamos donde lo dejamos”

Eso **rompe FIC**.

---

### Cursor

Cursor mantiene **memoria implícita por workspace**.

**Reset recomendado**

1. Cerrar el chat actual
2. Abrir **nuevo chat**
3. Primer mensaje:

```text
Reset context.

Only valid inputs:
- rules/base.md
- rules/profiles/<active-profile>.md
- This context summary:

<<paste compaction summary here>>

Confirm understanding before coding.
```

Si sigue degradado:

* Reiniciar Cursor **o**
* Cambiar de rama (fuerza refresco interno)

**Consejo FIC**
Chats cortos por tarea.
Sesiones largas degradan rápido.

---

### Gemini

Gemini tiene memoria conversacional **débil pero persistente**.

**Reset recomendado**

1. Nueva conversación
2. Primer mensaje explícito:

```text
Forget any previous context.
Start from scratch.

Authoritative context:
<<paste compaction summary here>>

Constraints:
- Follow TDD
- Ask before assuming
- Small, reversible steps only
```

👉 Sé más imperativo que con Claude o Codex.

---

## FIC Rule of Thumb (añadir a rules/base.md)

```md
## Context reset rule

If the agent shows:
- repeated misunderstandings
- rule violations
- hallucinated constraints
- excessive verbosity

STOP immediately.

Perform a context reset using a compaction summary.
Never try to fix a drifting agent incrementally.
```

---

## Recommended next step (optional)

Estandarizar los resets en `tooling/`:

```
tooling/
 └── reset-prompts/
     ├── claude-reset.md
     ├── codex-reset.md
     ├── cursor-reset.md
     └── gemini-reset.md
```

Convierte el reset en **procedimiento**, no en conocimiento tribal.



## References

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/
[2]: https://github.com/affaan-m/everything-claude-code
[3]: https://www.linkedin.com/posts/saski_github-saskiaugmentedcode-configuration-share-7409316228294549504-RXRJ/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACdAyYBerZ_Hv62VFsL9sVDbBepDDEJnSI
[4]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/
[5]: https://github.com/saski/augmentedcode-configuration


## TODO
- ai-feedback-learning-loop.md  ??
- all below /commands ??
