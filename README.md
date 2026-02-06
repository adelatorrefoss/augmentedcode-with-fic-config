# augmentedcode-configuration — Reorg proposal (MR draft)

This branch proposes a clearer information architecture:
- **docs/**: stable, readable documentation (concepts → workflow → TDD → recipes)
- **rules/**: the normative rule set (single source of truth + optional profiles)
- **tooling/**: per-tool adapters (Claude / Cursor / Codex)
- **thoughts/**: FIC artifacts (research / plans / prs)

## Quick path (10 minutes)
1. Use `tooling/claude/CLAUDE.md` as your project entry point (symlink it into your target repo if desired).
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

> Note: contents are intentionally concise placeholders; you can copy your current material into the appropriate files.
