# FIC workflow (Frequent Intentional Compaction)

## Phases
1. **Research**
   - Read the prompt/repo.
   - Summarize *only* the next deliverable + open decisions.
   - Ask users any questions. DO NOT GUESS!
   - Persist the summary in `.thoughtsshared/research/<topic>.md`.
   - Create or update `TASKS.md` checklist with findings.

2. **Plan**
   - Propose the smallest viable plan for the next slice.
   - Write the plan in `.thoughtsshared/plans/<topic>.md`.

3. **Implement**
   - Execute the plan in micro-steps.
   - Prefer TDD: red → green → refactor, tiny commits.

4. **Validate**
   - Run tests + basic quality gates.
   - Check constraints are still satisfied.
   - Capture the final compact summary (what changed, why) in `.thoughtsshared/prs/<topic>.md`.

## Compaction rule of thumb
- After Research → clear/reset context
- After Plan → clear/reset context
- If you notice drift/looping → stop, compact again, reset

## “FIC light” prompts (copy/paste)
### Research
- “Read the problem and repo. Summarize only the next slice of requirements and pending decisions. Do not implement. Save to `.thoughtsshared/research/<topic>.md`.”

### Plan
- “Propose a minimal design and a step-by-step TDD plan for the next slice. Save to `.thoughtsshared/plans/<topic>.md`.”

### Implement
- “Execute the plan in tiny steps. One failing test at a time. No scope creep.”

### Validate
- “Run tests, remove duplication, verify constraints. Summarize results in `.thoughtsshared/prs/<topic>.md`.”
