# Plan: Multi-CLI FIC Skill Migration
**Date**: 2026-04-22 10:41 CEST
**Research Source**: `.thoughts/shared/research/202604152349-skill-migration-multicli.md`
**Research Recheck**: 2026-04-22 update confirms Codex repository skills belong under `.agents/skills`; `.codex/skills` is not a target path for this slice. Codex plugins are a future distribution mechanism, not part of the repo-local migration.
**User Decisions**: Keep `.rules/` as canonical source. Use `.gemini/commands/` for Gemini support.

## Objective
Extract the FIC phase workflow into canonical reusable specs and add thin multi-CLI adapters without changing the current root entry-point contract.

## Scope Decision
- ✅ **In scope for the next slice**: FIC workflow only (`fic-research`, `fic-plan`, `fic-implement`, `fic-validate`).
- ✅ **In scope for the next slice**: Codex repository skills under `.agents/skills` and Claude skill adapters under `.claude/skills`.
- ✅ **In scope for the next slice**: Gemini command mapping under `.gemini/commands/`, but not Gemini command implementation.
- ❌ **Out of scope for the next slice**: TDD, refactoring, feedback-loop skill migration, root entry-point trimming, Codex plugin packaging, and a full Gemini extension package.

## Behavioral Seam
The stable behavior is the FIC workflow contract:
- entry-point guidance still sends agents through `.rules/base-rules.md` and `.rules/fic-workflow.md`;
- the four phase aliases remain discoverable and keep the same meanings;
- artifacts still land in `.thoughts/shared/research`, `.thoughts/shared/plans`, `.thoughts/shared/prs`, or implementation changes as appropriate;
- `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` remain symbolic links to `.rules/entry.md`.

## Protection Seam
This is an instruction/configuration migration, not production code.

Use document-level compatibility checks instead of unit tests:
- verify root symlinks are preserved;
- verify every FIC alias appears in the canonical workflow and in the relevant adapter metadata;
- verify adapters are thin and point back to canonical FIC phase specs;
- verify no platform adapter becomes the semantic source of truth.

## Design
1. **Canonical FIC specs**
   - Keep `.rules/` as the canonical source instead of introducing a new `.agent-os/` layer.
   - Add a small canonical phase-spec layer under `.rules/fic/`:
     - `.rules/fic/research.md`
     - `.rules/fic/plan.md`
     - `.rules/fic/implement.md`
     - `.rules/fic/validate.md`
   - Each file owns one phase procedure, including artifact path, phase boundary, required seam checks, and expected output.
   - Keep `.rules/fic-workflow.md` as the shared index and phase-alias contract.

2. **Codex repository skill adapters**
   - Add one `SKILL.md` adapter per FIC phase in the existing repo skill area:
     - `.agents/skills/fic-research/SKILL.md`
     - `.agents/skills/fic-plan/SKILL.md`
     - `.agents/skills/fic-implement/SKILL.md`
     - `.agents/skills/fic-validate/SKILL.md`
   - Keep each adapter concise: frontmatter trigger metadata plus imperative instructions to read the matching canonical `.rules/fic/*.md` file.
   - Do not duplicate the full workflow body in the adapter.
   - Do not add a `.codex/skills/` mirror unless a future official Codex source documents that path.
   - Do not create Codex plugin metadata in this slice; plugin packaging is only needed for distribution outside this repo.

3. **Claude skill adapters**
   - Add one thin Claude skill adapter per FIC phase:
     - `.claude/skills/fic-research/SKILL.md`
     - `.claude/skills/fic-plan/SKILL.md`
     - `.claude/skills/fic-implement/SKILL.md`
     - `.claude/skills/fic-validate/SKILL.md`
   - Keep the adapter content equivalent to the Codex repository adapters, with no Claude-only semantics unless the platform needs them.

4. **Gemini command mapping**
   - Document the intended Gemini command mapping:
     - `.gemini/commands/fic/research.toml`
     - `.gemini/commands/fic/plan.toml`
     - `.gemini/commands/fic/implement.toml`
     - `.gemini/commands/fic/validate.toml`
   - Do not implement these TOML commands in the next slice; keep the first slice focused on canonical extraction, `SKILL.md` adapters, and a precise Gemini command map.

5. **Entry-point preservation**
   - Do not replace root `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md`.
   - Do not break their symbolic links to `.rules/entry.md`.
   - Only update `.rules/entry.md` if implementation reveals a minimal wording change is required to point agents at the new FIC skill/spec structure.

## Step-by-Step Plan
1. [x] **🔎 1/7 - Baseline checks**
   - Confirm `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` are still symbolic links to `.rules/entry.md`.
   - Confirm current FIC alias text in `.rules/fic-workflow.md` before editing.

2. [x] **🧭 2/7 - Extract canonical phase specs**
   - Create `.rules/fic/research.md`, `.rules/fic/plan.md`, `.rules/fic/implement.md`, and `.rules/fic/validate.md`.
   - Move phase-specific procedure text from `.rules/fic-workflow.md` into those files.
   - Keep shared behavior, phase boundaries, compaction rules, and artifact locations intact.

3. [x] **📌 3/7 - Reduce `.rules/fic-workflow.md` to contract plus index**
   - Keep the phase list, alias command forms, artifact locations, and links to the new phase spec files.
   - Avoid making `.rules/fic-workflow.md` a second copy of the phase procedures.

4. [ ] **🧩 4/7 - Add Codex repository FIC skill adapters**
   - Create the four `.agents/skills/fic-*/SKILL.md` files.
   - Use lowercase hyphenated skill names.
   - Write frontmatter descriptions that explicitly trigger on the matching `fic-*:` alias and planning/research/implementation/validation intent.
   - Keep bodies under 100 lines each and point to the canonical `.rules/fic/*.md` file.
   - Do not create `.codex/skills` or Codex plugin files in this slice.

5. [ ] **🧩 5/7 - Add Claude FIC skill adapters**
   - Create the four `.claude/skills/fic-*/SKILL.md` files.
   - Mirror the same phase semantics as the Codex repository adapters.
   - Do not add Claude-specific behavior unless required for basic invocation.

6. [ ] **📝 6/7 - Capture Gemini command mapping**
   - Add a short Gemini mapping section to `.rules/fic-workflow.md` or a follow-up plan note.
   - Specify intended command names, canonical source files, artifact destinations, and explicit non-implementation status for this slice.

7. [ ] **✅ 7/7 - Validate instruction compatibility**
   - Run text checks for all four aliases across `.rules/fic-workflow.md`, `.rules/fic/*.md`, `.agents/skills`, and `.claude/skills`.
   - Check that each `SKILL.md` has only `name` and `description` frontmatter fields.
   - Check that no adapter contains a full duplicated copy of the canonical phase procedure.
   - Check that root symlinks are unchanged.

## Verification Strategy
- `test -L AGENTS.md && test -L CLAUDE.md && test -L GEMINI.md`
- `readlink AGENTS.md && readlink CLAUDE.md && readlink GEMINI.md`
- `rg "fic-(research|plan|implement|validate)" .rules .agents .claude`
- `rg "^name:|^description:" .agents/skills .claude/skills`
- Manual review that:
  - canonical phase behavior lives under `.rules/fic/`;
  - `.rules/fic-workflow.md` is an index/contract, not a duplicate procedure store;
  - adapter files are thin;
  - Codex repo-local adapters exist only under `.agents/skills`;
  - Gemini remains design-only in this slice.

## Risks And Mitigations
- **Risk**: Duplicating workflow semantics across adapters.
  - **Mitigation**: Adapters must reference canonical `.rules/fic/*.md` files and contain only trigger/usage instructions.
- **Risk**: Breaking the existing shared root entry model.
  - **Mitigation**: Do not edit root symlink files; validate symlink targets before and after.
- **Risk**: Codex project-skill discovery guidance changes again.
  - **Mitigation**: Treat `.agents/skills` as the current official repo skill source; re-check official Codex docs before introducing any mirror path.
- **Risk**: Introducing a new `.agent-os/` canonical layer contradicts the chosen migration path.
  - **Mitigation**: Keep `.rules/` canonical and do not create `.agent-os/` in this migration.
- **Risk**: Codex plugin packaging gets mixed into repo-local migration.
  - **Mitigation**: Treat plugins as future distribution work after repo-local skills are validated.
- **Risk**: Implementing Gemini commands prematurely broadens the slice.
  - **Mitigation**: Record the `.gemini/commands/` mapping only; defer TOML files to a separate implementation slice.

## Next Slice Exit Criteria
- 4 canonical FIC phase files exist under `.rules/fic/`.
- 4 Codex repository FIC skill adapters exist under `.agents/skills/`.
- 4 Claude FIC skill adapters exist under `.claude/skills/`.
- `.rules/fic-workflow.md` remains the FIC contract and points to the canonical phase files.
- Root entry symlinks remain unchanged.
- No `.codex/skills` or Codex plugin files are introduced by this slice.
- Gemini command mapping is documented but not implemented.
