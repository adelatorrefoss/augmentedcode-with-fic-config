# Augmented code configuration

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

## References

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/
[2]: https://github.com/affaan-m/everything-claude-code
[3]: https://www.linkedin.com/posts/saski_github-saskiaugmentedcode-configuration-share-7409316228294549504-RXRJ/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACdAyYBerZ_Hv62VFsL9sVDbBepDDEJnSI
[4]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/
[5]: https://github.com/saski/augmentedcode-configuration


## TODO
- ai-feedback-learning-loop.md  ??
- all below /commands ??
