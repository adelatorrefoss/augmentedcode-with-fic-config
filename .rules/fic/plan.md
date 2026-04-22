# FIC plan phase

## Alias
- `fic-plan: <topic or task>`

## Phase boundary
Do Plan only. Propose the smallest viable next slice and do not implement it.

## Procedure
1. Read the approved research artifact or the task payload.
2. Propose the smallest viable plan for the next slice.
3. When tests are part of the slice, state explicitly:
   - the visible behavior being protected;
   - the intended test seam;
   - which collaborators will remain real;
   - which dependency is the first meaningful mocked port.
4. Keep the plan actionable and reversible.
5. Write the plan in `.thoughts/shared/plans/<YYYYMMDDHHMM-topic>.md` using `.thoughts/templates/plan.md` as a guide.

## Output
- One plan artifact under `.thoughts/shared/plans/`.
- A clear scope decision for the next slice.
- Verification criteria for the next implementation.

## Compaction
After Plan, clear or reset context before moving to the next phase.
