# Augmented code with FIC (Frequent Intentional Compaction) configuration

_This repo is a FIC workflow (Frequent Intentional Compaction) by  [Dex Horthy - Advanced context engineering for coding agents][6]_

_Thanks to [Eduardo Ferro][1] for the base repo and [Nacho Viejo][3] for the inspiration to try FIC_
_[Eduardo Ferro - Augmented code configuration][1]_ 
_[Nacho Viejo FIC post][3]_

This repo proposes a clear information architecture:
- **.rules/**: the normative rule set (single source of truth + other rules)
- **.docs/**: stable, readable documentation for humans.
- **.thoughts/**: folders prepared for FIC artifacts (research / plans / prs)


## Installation & Setup

1. Copy the configuration files and directories to your working repository:

```bash
cp -rf .rules .agents .thoughts .docs AGENTS.md CLAUDE.md GEMINI.md PROJECT.md .gitignore /path/to/working-repo/
```

2. Customize `PROJECT.md` with your repository's specific information.

## How to use FIC

The FIC (Frequent Intentional Compaction) workflow helps manage agent context by frequently summarizing and resetting it.

1. **Research**: Analyze the problem and save a compact summary in `.thoughts/shared/research/`.
2. **Plan**: Create a minimal TDD plan in `.thoughts/shared/plans/`.
3. **Implement**: Execute in micro-steps.
4. **Validate**: Run tests and capture a final summary in `.thoughts/shared/prs/`.

See [.rules/fic-workflow.md](.rules/fic-workflow.md) for detailed instructions.



## Info about reset context in different agents

### Claude (Claude Code / Claude Chat)

Claude **does not have a real reset**. Resetting is done by **completely replacing the context**.

**Recommended Procedure**

1. Open a **new conversation**
2. Mandatory first message:

```text
You are starting a new session.

This is the ONLY valid context.
Ignore any previous conversation or memory.

Context:
- Project uses Augmented Code with FIC.
- Follow rules from .rules/base-rules.md strictly.
- Use TDD and small steps.
- Do not invent requirements.

Current state (authoritative):
<<paste compaction summary here>>

Your task:
<<one single, explicit next step>>
```

**Signal of correct reset**

* Claude restates the goal
* It doesn't carry over previous context
* It asks before assuming

---

### Codex (OpenAI Codex)

Codex is **stateless per request** if used correctly.

**Effective Reset**

* New call
* New `messages[]`
* Do not reuse previous conversation

Prompt base:

```text
SYSTEM:
You are a coding agent operating under Augmented Code with FIC.
Rules in .rules/base-rules.md are mandatory.
Assume no prior context.

USER:
Context summary:
<<paste compaction summary here>>

Task:
<<single explicit step>>
```

**Anti-pattern**

* Sending back long history
* "Continuing where we left off"

That **breaks FIC**.

---

### Cursor

Cursor maintains **implicit memory per workspace**.

**Recommended Reset**

1. Close the current chat
2. Open a **new chat**
3. First message:

```text
Reset context.

Only valid inputs:
- .rules/base-rules.md
- .rules/profiles/<active-profile>.md
- This context summary:

<<paste compaction summary here>>

Confirm understanding before coding.
```

If it remains degraded:

* Restart Cursor **or**
* Change branch (forces internal refresh)

**FIC Advice**
Short chats per task.
Long sessions degrade quickly.

---

### Gemini

Gemini has **weak but persistent** conversational memory.

**Recommended Reset**

1. New conversation
2. Explicit first message:

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

👉 Be more imperative than with Claude or Codex.



## References

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/
[2]: https://github.com/affaan-m/everything-claude-code
[3]: https://www.linkedin.com/posts/saski_github-saskiaugmentedcode-configuration-share-7409316228294549504-RXRJ/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACdAyYBerZ_Hv62VFsL9sVDbBepDDEJnSI
[4]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/
[5]: https://github.com/saski/augmentedcode-configuration
[6]: https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
