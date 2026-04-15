# TDD with agents (guardrails)

## Default operating constraints
- Smallest step that proves value.
- One failing test → minimal change → green.
- Refactor only on green.
- Prefer pure functions / deterministic tests.
- Avoid large refactors without characterization tests.
- For behavior-preserving refactors, the first characterization test should protect the highest stable functional seam, not the most convenient internal seam.

## Definition of done (per slice)
- Tests pass locally.
- No obvious duplication.
- Naming explains intent.
- New behavior is covered.
- Commit message states the slice.
- **Complete Coverage**: Ensure every new feature or bugfix is covered by a test.
- **Refactor Tests**: Refactor tests to remove duplication and improve readability.

## Anti-patterns to stop immediately
- “Implementing ahead” of the current requirement.
- Adding abstractions without tests.
- Rewriting instead of refactoring (unless explicitly requested).
- Treating a thin proxy service as the target port of a characterization test when the real behavior comes from a lower repository or external boundary.
- Building the initial safety-net around an internal contract when the user asked to preserve visible behavior.

## Test Naming & Coverage
- **Descriptive Names**: Test function names should clearly describe the scenario and expected outcome.
- **Purpose-Driven Variables**: Use descriptive variable names that reflect their purpose in the test.
- **Incremental Coverage**: Ensure all code paths and edge cases are eventually covered by tests, but add them incrementally.

## Test Review & Refactoring
- **Post-Pass Review**: After a test passes, review for opportunities to simplify or clarify.
- **Helper Refactoring**: Refactor test helpers and fixtures as needed to keep the suite DRY and maintainable.
