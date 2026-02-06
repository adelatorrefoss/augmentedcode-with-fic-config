# TDD with agents (guardrails)

## Default operating constraints
- Smallest step that proves value.
- One failing test → minimal change → green.
- Refactor only on green.
- Prefer pure functions / deterministic tests.
- Avoid large refactors without characterization tests.

## Definition of done (per slice)
- Tests pass locally.
- No obvious duplication.
- Naming explains intent.
- New behavior is covered.
- Commit message states the slice.

## Anti-patterns to stop immediately
- “Implementing ahead” of the current requirement.
- Adding abstractions without tests.
- Rewriting instead of refactoring (unless explicitly requested).
