# Base rules (single source of truth)

These rules are intended to be referenced by tool entry points (CLAUDE.md / AGENTS.md / Cursor rules).

## Working style
- Prefer small, reversible steps.
- Use tests to drive changes (TDD) unless the task is explicitly non-testable.
- Keep context minimal; compact intent frequently (see docs/10-fic-workflow.md).

## Code changes
- Do not introduce new libraries without justification.
- Avoid large rewrites; refactor safely with tests.
- Prefer clarity over cleverness.

## Output
- Provide short, actionable plans.
- Track key decisions in `thoughts/`.
