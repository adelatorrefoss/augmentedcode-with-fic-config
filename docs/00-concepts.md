# Concepts: why structure matters

This repo is easier to adopt if it cleanly separates:
1) **Content** (rules & docs)
2) **Workflow discipline** (FIC / compaction)
3) **Tool adapters** (Claude/Cursor/Codex entry points)

## Context engineering
Long coding sessions degrade when:
- intent drifts
- the model forgets constraints
- you carry too much irrelevant context

A practical mitigation is **Frequent Intentional Compaction (FIC)**:
- short research burst
- deliberate plan
- focused implementation
- explicit validation
- repeated compaction + resets between phases

See `docs/10-fic-workflow.md`.
