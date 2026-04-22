# Plan: Codex FIC Skill Adapters
**Date**: 2026-04-22 14:14 CEST
**Parent Plan**: `.thoughts/shared/plans/202604221041-skill-migration-multicli.md`
**Step**: 4/7 - Add Codex repository FIC skill adapters

## Objective
Create four repo-local Codex skill adapters under `.agents/skills/` for the FIC phase aliases, with each adapter delegating procedure details to the canonical `.rules/fic/*.md` files.

## Scope Decision
- ✅ **In scope**: `.agents/skills/fic-research/SKILL.md`
- ✅ **In scope**: `.agents/skills/fic-plan/SKILL.md`
- ✅ **In scope**: `.agents/skills/fic-implement/SKILL.md`
- ✅ **In scope**: `.agents/skills/fic-validate/SKILL.md`
- ❌ **Out of scope**: `.claude/skills`, `.gemini/commands`, `.codex/skills`, Codex plugin metadata, and changes to root entry symlinks.

## Behavioral Seam
The stable behavior is Codex discovery and execution of the existing FIC contract:
- the four `fic-*` aliases remain the trigger language;
- `.rules/fic-workflow.md` remains the workflow index;
- `.rules/fic/*.md` remains the canonical procedure source;
- artifacts still land in the existing `.thoughts/shared/...` phase directories.

## Test/Protection Seam
This is a document/configuration slice, not production code.

Use document-level compatibility checks:
- validate each skill has required YAML frontmatter with only `name` and `description`;
- validate each skill name is lowercase hyphen-case;
- validate every description mentions the matching `fic-*:` alias;
- validate every body points to the matching `.rules/fic/*.md`;
- validate skill bodies do not duplicate the full canonical phase procedure;
- validate no `.codex/skills` or plugin files are created.

## Design
1. **Skill structure**
   - Create one folder per phase:
     - `.agents/skills/fic-research/`
     - `.agents/skills/fic-plan/`
     - `.agents/skills/fic-implement/`
     - `.agents/skills/fic-validate/`
   - Each folder contains only `SKILL.md`.
   - Do not add scripts, references, assets, README files, or generated metadata in this slice.

2. **Frontmatter**
   - Use only:
     - `name`
     - `description`
   - Descriptions must be explicit enough to trigger on:
     - direct alias prompts such as `fic-plan: topic`;
     - natural-language requests to run that FIC phase;
     - requests to create the expected `.thoughts/shared/...` artifact.

3. **Body**
   - Keep each body short and imperative.
   - Tell Codex to read:
     - `.rules/base-rules.md`;
     - `.rules/fic-workflow.md`;
     - the matching `.rules/fic/<phase>.md`;
     - `PROJECT.md` if present.
   - Restate only the adapter-specific guardrails:
     - execute only the named phase;
     - write the expected artifact when the phase requires one;
     - do not continue into the next phase;
     - preserve root symlinks.

4. **No semantic duplication**
   - Do not copy the full phase procedure into `SKILL.md`.
   - The adapter exists to trigger and route; `.rules/fic/*.md` remains authoritative.

## Step-by-Step Plan
1. [x] **🔎 1/6 - Baseline checks**
   - Confirm `.agents/skills/intellij-navigation/SKILL.md` remains untouched.
   - Confirm `.rules/fic/research.md`, `.rules/fic/plan.md`, `.rules/fic/implement.md`, and `.rules/fic/validate.md` exist.
   - Confirm no `.agents/skills/fic-*` folders already exist.

2. [x] **🧩 2/6 - Create `fic-research` adapter**
   - Add `.agents/skills/fic-research/SKILL.md`.
   - Trigger on `fic-research:` and research-only FIC requests.
   - Point to `.rules/fic/research.md`.

3. [x] **🧩 3/6 - Create `fic-plan` adapter**
   - Add `.agents/skills/fic-plan/SKILL.md`.
   - Trigger on `fic-plan:` and plan-only FIC requests.
   - Point to `.rules/fic/plan.md`.

4. [x] **🧩 4/6 - Create `fic-implement` adapter**
   - Add `.agents/skills/fic-implement/SKILL.md`.
   - Trigger on `fic-implement:` and implementation-only FIC requests.
   - Point to `.rules/fic/implement.md`.

5. [x] **🧩 5/6 - Create `fic-validate` adapter**
   - Add `.agents/skills/fic-validate/SKILL.md`.
   - Trigger on `fic-validate:` and validation-only FIC requests.
   - Point to `.rules/fic/validate.md`.

6. [x] **✅ 6/6 - Validate adapter compatibility**
   - Check all four adapters contain only `name` and `description` frontmatter fields.
   - Check all four aliases appear in `.agents/skills/fic-*/SKILL.md`.
   - Check every adapter references its canonical `.rules/fic/*.md` file.
   - Check no `.codex/skills`, `.claude/skills`, or `.gemini/commands` files were introduced.

## Verification Strategy
- `find .agents/skills -maxdepth 2 -name SKILL.md | sort`
- `rg -n "^name:|^description:|fic-(research|plan|implement|validate)|\\.rules/fic/" .agents/skills/fic-*`
- `find .codex .claude .gemini -maxdepth 3 -type f -print 2>/dev/null`
- `git diff --check -- .agents/skills .thoughts/shared/plans/202604221041-skill-migration-multicli.md`
- Manual review that each adapter is thin and does not copy a full phase procedure.

## Exit Criteria
- 4 Codex repository FIC skill adapters exist under `.agents/skills/fic-*`.
- Each adapter triggers on the matching `fic-*:` alias.
- Each adapter points to the matching `.rules/fic/*.md` canonical source.
- Existing `.agents/skills/intellij-navigation/SKILL.md` is unchanged.
- No out-of-scope platform adapter files are introduced.
