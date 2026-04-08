# Augmented code with FIC (Frequent Intentional Compaction) configuration

_This repo is a FIC workflow (Frequent Intentional Compaction) by  [Dex Horthy - Advanced context engineering for coding agents][6]_

_Thanks to [Eduardo Ferro][1] for the base repo and [Nacho Viejo][3] for the inspiration to try FIC_
_[Eduardo Ferro - Augmented code configuration][1]_ 
_[Nacho Viejo FIC post][3]_

This repo proposes a clear information architecture:
- **.rules/**: the normative rule set (single source of truth + other rules)
- **.docs/**: stable, readable documentation for humans.
- **.thoughts/**: folders prepared for FIC artifacts (research / plans / prs)


## How to config

1. Copy ai-repo files to working directory.

```
cp -rf AGENTS.md GEMINI.md .rules .agents .thoughts /to/working-repo
```

## How to use FIC

// TODO
// EXPLAin workflow


### FIC Rule of Thumb (añadir a .rules/base.md)

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



## Info about reset context in different agents

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
- Follow rules from .rules/base.md strictly.
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
Rules in .rules/base.md are mandatory.
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
- .rules/base.md
- .rules/profiles/<active-profile>.md
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



## References

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/
[2]: https://github.com/affaan-m/everything-claude-code
[3]: https://www.linkedin.com/posts/saski_github-saskiaugmentedcode-configuration-share-7409316228294549504-RXRJ/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACdAyYBerZ_Hv62VFsL9sVDbBepDDEJnSI
[4]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/
[5]: https://github.com/saski/augmentedcode-configuration
[6]: https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
