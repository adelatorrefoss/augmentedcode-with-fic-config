# Entry point

This file is the entry point for any agent (CLAUDE.md, AGENTS.md, GEMINI.md, etc).

## Entry point topology

- `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` are symbolic links to `.rules/entry.md`.
- Treat `.rules/entry.md` as the single source of truth for the shared entry text.
- Do not report those three root files as duplicated entry-point content unless their symbolic-link status has changed.
- When changing shared entry guidance, edit `.rules/entry.md` and preserve the root symbolic links.

1. Read **base rules**: `.rules/base-rules.md`.
2. Understand the **FIC workflow**: `.rules/fic-workflow.md`, including the `fic-research`, `fic-plan`, `fic-implement`, and `fic-validate` phase aliases.
3. If performing TDD: `.rules/tdd-with-agents.md`.
4. If performing Refactoring: `.rules/refactoring-planner.md`.
5. For feedback loops: `.rules/ai-feedback-learning-loop.md`.

Read project info if exists:
- PROJECT.md

Optional deeper context, only if needed for the current task:
- `.docs/fic-philosophy.md`
- `.docs/architecture-overview.md`
- `.docs/agent-compatibility.md`
- `.docs/maintenance-guide.md`
