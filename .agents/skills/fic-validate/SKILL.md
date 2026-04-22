---
name: fic-validate
description: Use when the user invokes `fic-validate:` or asks to run the FIC Validate phase only. Produce a validation artifact under `.thoughts/shared/prs/` by following the canonical `.rules/fic/validate.md` procedure.
---

## Goal

Run only the FIC Validate phase for the requested topic.

## Workflow

1. Read `.rules/base-rules.md`.
2. Read `.rules/fic-workflow.md`.
3. Read `.rules/fic/validate.md` and follow it as the canonical procedure.
4. Read `PROJECT.md` if it exists.
5. Produce the required `.thoughts/shared/prs/` artifact.

## Guardrails

- Do not add new scope.
- Do not continue into another FIC phase.
- Preserve the root `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` symbolic links.
