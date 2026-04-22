---
name: fic-plan
description: Use when the user invokes `fic-plan:` or asks to run the FIC Plan phase only. Produce a plan artifact under `.thoughts/shared/plans/` by following the canonical `.rules/fic/plan.md` procedure.
---

## Goal

Run only the FIC Plan phase for the requested topic.

## Workflow

1. Read `.rules/base-rules.md`.
2. Read `.rules/fic-workflow.md`.
3. Read `.rules/fic/plan.md` and follow it as the canonical procedure.
4. Read `PROJECT.md` if it exists.
5. Produce the required `.thoughts/shared/plans/` artifact.

## Guardrails

- Do not implement or validate the plan.
- Do not continue into the next FIC phase.
- Preserve the root `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` symbolic links.
