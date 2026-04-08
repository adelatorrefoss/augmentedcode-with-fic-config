# FIC workflow (Frequent Intentional Compaction)

## Phases
1. **Research**
   - Read the prompt/repo.
   - Summarize *only* the next deliverable + open decisions.
   - Ask users any questions. DO NOT GUESS!
   - Persist the summary in `.thoughts/shared/research/<YYYYMMDDHHMM-topic>.md` (use `.thoughts/templates/research.md` as a guide).
   - Create or update `TASKS.md` checklist with findings.

2. **Plan**
   - Propose the smallest viable plan for the next slice.
   - Write the plan in `.thoughts/shared/plans/<YYYYMMDDHHMM-topic>.md` (use `.thoughts/templates/plan.md` as a guide).

3. **Implement**
   - Execute the plan in micro-steps.
   - Prefer TDD: red → green → refactor, tiny commits.

4. **Validate**
   - Run tests + basic quality gates.
   - Check test quality, coverage, assertions, and test quality gates.
   - Critique the unit test vs. integration test split.
   - Check constraints are still satisfied.
   - Capture the final compact summary (what changed, why) in `.thoughts/shared/prs/<YYYYMMDDHHMM-topic>.md` (use `.thoughts/templates/validation.md` as a guide).

## Phase aliases

These shorthand prompts are first-class repo conventions.
When an agent sees one of these aliases, it should treat it as a workflow command, not as an informal label.

- `fic-research`: do Research only, do not implement, and save the result in `.thoughts/shared/research/<YYYYMMDDHHMM-topic>.md`.
- `fic-plan`: do Plan only, propose the smallest viable next slice, and save the result in `.thoughts/shared/plans/<YYYYMMDDHHMM-topic>.md`.
- `fic-implement`: do Implement only, execute the approved plan in small steps, and prefer TDD.
- `fic-validate`: do Validate only, run checks, summarize what changed and what comes next, and save the result in `.thoughts/shared/prs/<YYYYMMDDHHMM-topic>.md`.

## Compaction rule of thumb
- After Research → clear/reset context
- After Plan → clear/reset context
- If you notice drift/looping → stop, compact again, reset

## “FIC light” prompts (copy/paste)
### Research
- “Read the problem and repo. Summarize only the next slice of requirements and pending decisions. Do not implement. Save to `.thoughts/shared/research/<YYYYMMDDHHMM-topic>.md` using the `.thoughts/templates/research.md` template.”

### Plan
- “Propose a minimal design and a step-by-step TDD plan for the next slice. Save to `.thoughts/shared/plans/<YYYYMMDDHHMM-topic>.md` using the `.thoughts/templates/plan.md` template.”

### Implement
- “Execute the plan in tiny steps. One failing test at a time. No scope creep.”

### Validate
- “Run tests, remove duplication, verify constraints. Summarize results in `.thoughts/shared/prs/<YYYYMMDDHHMM-topic>.md` using the `.thoughts/templates/validation.md` template.”
