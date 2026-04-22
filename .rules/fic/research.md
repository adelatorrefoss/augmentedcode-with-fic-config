# FIC research phase

## Alias
- `fic-research: <topic or task>`

## Phase boundary
Do Research only. Do not plan implementation steps beyond the next deliverable and do not change product or configuration files.

## Procedure
1. Read the prompt and relevant repository context.
2. Summarize only the next deliverable and open decisions.
3. Identify the behavioral seam that must remain stable during the next slice.
4. Identify the highest test seam that can protect that behavior without entering infrastructure.
5. Explicitly check whether any "port" in the candidate seam is only a proxy service over a repository or external dependency.
6. Ask users any questions. Do not guess.
7. Persist the summary in `.thoughts/shared/research/<YYYYMMDDHHMM-topic>.md` using `.thoughts/templates/research.md` as a guide.

## Output
- One research artifact under `.thoughts/shared/research/`.
- Clear next deliverable.
- Explicit open decisions or confirmation that no decisions remain open.

## Compaction
After Research, clear or reset context before moving to the next phase.
