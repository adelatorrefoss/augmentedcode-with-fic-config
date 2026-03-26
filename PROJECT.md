# Project Information

## Repository Overview
This repository contains application code, supporting libraries, tests, and operational assets.
It is intended to be adaptable across different projects, so this document focuses on reusable structure and working conventions rather than product-specific details.

## Suggested Module Organization
- `src/`: Application and domain code.
- `tests/`: Automated test suites.
- `docs/`: Project documentation and decision records.
- `scripts/`: Local development and automation scripts.
- `infra/` or `deploy/`: Infrastructure, deployment, and environment configuration.

Adjust the structure to match the repository, but keep naming and ownership clear.

## Local Dependencies
Projects may depend on local services such as:
- databases
- message brokers
- search engines
- caches
- external service emulators

If local infrastructure is required, document:
- which services are needed
- how to start them
- which ports or environment variables matter
- how to reset state for repeatable testing

Example:
```bash
docker compose up -d
```

## Build and Run Basics
Document the standard commands for:
- restoring or installing dependencies
- building the project
- running the application
- running the full test suite

Keep examples aligned with the actual stack used in the repository.

## Development Commands
List the commands contributors need most often, for example:
- fast local tests
- integration or end-to-end tests
- linting or formatting
- project-specific automation scripts

Prefer a small set of reliable commands over a long catalog.

## Contribution Guidelines

## Coding Style & Naming
Follow the conventions already established in the repository:
- use consistent indentation and formatting
- keep naming explicit and intention-revealing
- align namespaces, packages, or modules with the folder structure
- prefer clarity over cleverness

If the project has automated formatters or analyzers, treat them as the source of truth.

## Testing Expectations
- Add or update tests for behavior changes.
- Keep tests deterministic and focused on observable behavior.
- Use descriptive test names that explain scenario and expected outcome.
- Prefer fast unit tests, with narrower use of integration and end-to-end coverage.

## Testing Learnings and Future Guidelines
This section captures reusable guidance for integration and end-to-end test development.
The goal is to reduce investigation time, improve determinism, and prevent environment-driven flakiness.

## Core Principles
- Make tests deterministic and avoid timing-dependent assumptions when possible.
- Validate contracts explicitly: configuration keys, payload schemas, routes, bindings, and interfaces.
- Prefer observable failures over generic timeouts.
- Keep test setup close to production behavior while isolating external dependencies where control is needed.
- Fail fast with messages that explain what was expected and what was observed.

## Common Failure Patterns
1. Host or process lifecycle not started before assertions.
2. Configuration keys do not match the runtime binding path.
3. Dependency endpoints silently fall back to defaults.
4. Seeded data shape does not match parser or mapper expectations.
5. Background processes swallow exceptions and tests only expose downstream timeouts.

## Guidelines for Future Test Development
1. Startup and lifecycle
- Explicitly initialize the application or host before asserting side effects.
- Wait for readiness conditions when testing asynchronous components.

2. Configuration discipline
- Derive test configuration keys from application binding code, not memory.
- Verify section names before writing in-memory or fixture configuration.
- Keep one authoritative configuration block per dependency.

3. External dependency strategy
- Prefer explicit dependency injection overrides for critical integrations.
- Use containerized services or emulators with clear endpoint injection.
- Avoid relying on layered configuration precedence unless it is tested.

4. Test data contracts
- Seed data in the exact shape expected by parser, repository, or mapper layers.
- Build fixtures from domain contracts where practical to reduce drift.
- Add lightweight contract assertions around seeded inputs when useful.

5. Observability and debugging
- Enable detailed logging when reproducing failures.
- Capture service or worker logs in failing runs.
- Add intermediate assertions to narrow failure boundaries.

6. Assertions and timeouts
- Use bounded retries with clear timeout reasons.
- Keep polling intervals and timeout windows explicit.
- Assert both the presence and semantic correctness of produced outputs.

## Recommended Development Workflow for New Tests
1. Define the behavior and expected side effect.
2. Confirm application and dependency readiness.
3. Configure dependencies using exact runtime bindings.
4. Seed data according to the real contract.
5. Trigger the behavior under test.
6. Assert outputs with bounded retries where needed.
7. On failure, inspect boundaries in order: startup, configuration, connectivity, mapping, dispatch.

## Practical Checklist Before Merging Tests
- Startup is explicit and deterministic.
- Dependency endpoints are controlled by the test.
- Configuration keys are verified against runtime bindings.
- Seed data matches the expected contract.
- Timeouts are bounded and explained.
- Logs are sufficient to diagnose failures without repeating the full investigation.
