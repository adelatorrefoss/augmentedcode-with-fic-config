# Base rules (single source of truth)

These rules are intended to be the base instructions for an agent.

## Working style

- Prefer small, reversible steps.
- Use tests to drive changes (TDD) unless the task is explicitly non-testable (see .rules/tdd-with-agents.md).
- Keep context minimal; compact intent frequently (see .rules/fic-workflow.md).
- **Simplicity First**: Use the simplest working solution; avoid unnecessary abstractions.
- **Question Assumptions**: Always question assumptions.
- **Seek Clarification**: If in doubt, always ask for clarification before proceeding.
- **Sequential Questions**: Only one question at a time; each question should build on previous answers.

## Tool usage

- Use Rider/IntelliJ MCP for semantic code navigation: symbols, usages, declarations, references, and structure.
- Use direct filesystem tools for known file paths, known line ranges, and simple text or filename searches.
- Prefer `rg --files`, `rg`, and ranged reads for fast repository inspection.
- Use Atlassian MCP for Jira and Confluence.

## Code changes

- Do not introduce new libraries without justification.
- Avoid large rewrites; refactor safely with tests.
- Prefer clarity to cleverness.
- **MANDATORY Validation**: Before EVERY commit, build solution and fix ALL errors. Zero tolerance.
- **High Coverage**: All code must have very high test coverage; strive for 100% where practical.
- **TDD Workflow**: Test-Driven Development (TDD) is the default workflow: always write tests first.
- **OOP Design**: Use Object-Oriented Programming (OOP) for all components and features.
- **Self-Documenting Code**: Avoid comments in code; rely on self-documenting names. Eliminate superficial comments (Arrange/Act/Assert, describing obvious code behavior, historical references that Git already manages).
- **English-Only Artifacts**: All technical artifacts must always use English.

## Context reset rule (FIC Rule of Thumb)

If the agent shows:
- repeated misunderstandings
- rule violations
- hallucinated constraints
- excessive verbosity

STOP immediately.

Perform a context reset using a compaction summary.
Never try to fix a drifting agent incrementally.

## Output

- Provide short, actionable plans.
- Track key decisions in `.thoughts`.
- **Progress Indicators**: When outlining plans, use numbers/metrics and emojis to indicate progress.
- **User-Focused README**: README.md must be user-focused, containing only information relevant to table authors and end users.


## Development Best Practices

### Error Handling & Debugging
- **Graceful Error Handling**: Always implement proper error handling with meaningful error messages.
- **Debugging First**: When encountering issues, use debugging tools and logging before asking for help.
- **Error Context**: Provide sufficient context in error messages to enable quick problem resolution.
- **Fail Fast**: Design code to fail fast and fail clearly when errors occur.


### Security Considerations
- **Security by Design**: Consider security implications in all design decisions.
- **Input Validation**: Always validate and sanitize user inputs and external data.
- **Secrets Management**: Never hardcode secrets; use proper secret management systems.
- **Dependency Security**: Regularly update dependencies and monitor for security vulnerabilities.

### Testing Strategy Distinction
- **Unit Tests**: Fast, isolated tests for individual components (the majority of the test suite). Test the functional unit, from use case to the first meaningful infrastructure port, and avoid mocking internal services unless necessary to simplify test configuration.
- **Meaningful Port Rule**: Do not stop a characterization test at a service interface if that service is only a thin proxy over another dependency. In those cases, keep the proxy service real and mock the underlying repository or external boundary where data is actually read or decisions are actually made.
- **Refactor Safety-Net Rule**: For behavior-preserving refactors, place the first safety-net test at the highest stable seam that still remains outside infrastructure. Prefer asserting the visible behavior of the functional flow over asserting an internal intermediate contract, unless the task explicitly targets that internal contract.
- **Integration Tests**: Test interactions between components and external systems (limited, focused).
- **E2E Tests**: Full system validation (minimal, critical user paths only).
- **Test Pyramid**: Follow the test pyramid - many unit tests, some integration tests, few E2E tests.

## Refactoring

When prompted for refactoring, use the rules in `./refactoring-planner.md`.

## AI Feedback learning loop

When prompted for feedback learning after a process, use the rules in `./ai-feedback-learning-loop.md`.
