# Base rules (single source of truth)

These rules are intended to be the base to an agent

## Working style

- Prefer small, reversible steps.
- Use tests to drive changes (TDD) unless the task is explicitly non-testable (see .rules/tdd-with-agents.md).
- Keep context minimal; compact intent frequently (see .rules/fic-workflow.md).
- **Simplicity First**: Use the simplest working solution; avoid unnecessary abstractions.
- **Question Assumptions**: Always question assumptions
- **Seek Clarification**: If in doubt, always ask for clarification before proceeding.
- **Sequential Questions**: Only one question at a time; each question should build on previous answers.

## Code changes

- Do not introduce new libraries without justification.
- Avoid large rewrites; refactor safely with tests.
- Prefer clarity to cleverness.
- **MANDATORY Validation**: Before EVERY commit, build solution and fix ALL errors. Zero tolerance.
- **High Coverage**: All code must have very high test coverage; strive for 100% where practical.
- **TDD Workflow**: Test-Driven Development (TDD) is the default workflow: always write tests first.
- **OOP Design**: Use Object-Oriented Programming (OOP) for all components and features.
- **Self-Documenting Code**: Avoid comments in code; rely on self-documenting names. Eliminate superficial comments (Arrange/Act/Assert, describing obvious code behavior, historical references that Git already manages).
- **English-Only Artifacts**: All technical artifacts must always use English

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
- **Unit Tests**: Fast, isolated tests for individual components (majority of test suite).
- **Integration Tests**: Test interactions between components and external systems (limited, focused).
- **E2E Tests**: Full system validation (minimal, critical user paths only).
- **Test Pyramid**: Follow the test pyramid - many unit tests, some integration tests, few E2E tests.

## Refactoring

When prompt for refactoring use rules in ./refactoring-planner.md

## AI Feedback learning loop

When prompt for feedback learning after a process use the rules in ./ai-feedback-learning-loop.md
