# FIC implement phase

## Alias
- `fic-implement: <topic or task>`

## Phase boundary
Do Implement only. Execute the approved plan for the same topic in small steps and do not switch back into research or planning mode unless blocked.

## Procedure
1. Read the approved plan for the same topic.
2. Execute the plan in micro-steps.
3. Prefer TDD: red, green, refactor, tiny commits.
4. Before writing the first test, re-check that the chosen seam is not anchored on a proxy service when a lower repository boundary is the real source of behavior.
5. Keep changes scoped to the approved slice.
6. If the plan is ambiguous or blocked, stop and ask for the smallest missing decision.

## Output
- Implemented changes for the approved slice.
- Local verification appropriate to the slice.
- A concise implementation summary.

## Compaction
After Implement, clear or reset context before moving to the next phase.
