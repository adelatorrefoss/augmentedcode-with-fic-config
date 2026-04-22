# FIC validate phase

## Alias
- `fic-validate: <topic or task>`

## Phase boundary
Do Validate only. Do not add new scope.

## Procedure
1. Run tests and basic quality gates appropriate to the implemented slice.
2. Check test quality, coverage, assertions, and test quality gates.
3. Critique the unit test versus integration test split.
4. Check constraints are still satisfied.
5. Capture the final compact summary in `.thoughts/shared/prs/<YYYYMMDDHHMM-topic>.md` using `.thoughts/templates/validation.md` as a guide.

## Output
- Validation results.
- Constraint check summary.
- One PR or validation artifact under `.thoughts/shared/prs/`.

## Compaction
After Validate, clear or reset context before ending or starting another phase.
