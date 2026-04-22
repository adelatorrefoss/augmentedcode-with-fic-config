# Research: Converting This Repo to Multi-CLI Skills
**Date**: 2026-04-15 23:49

## Context Analysis
- Current prompt surface is small and clean:
  - `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` are symbolic links to `.rules/entry.md`.
  - `.rules/` contains the normative behavior.
  - `.docs/` contains explanatory context.
  - `.agents/skills/` currently contains one example skill: `intellij-navigation`.
- There are no separate hidden per-agent prompt stacks inside this repo beyond the three entry-point files and the rule/docs layers.
- The current architecture already separates content by intent:
  - always-on rules in `.rules/`
  - optional explanation in `.docs/`
  - reusable extensions in `.agents/`
  - transient artifacts in `.thoughts/`
- This makes the repo a good candidate for extraction into skills, because the procedural content is already mostly isolated from the always-on entry point.

## Primary Requirement for the Migration
- Preserve the current FIC behavior:
  - minimal entry point
  - explicit `fic-research`, `fic-plan`, `fic-implement`, `fic-validate`
  - compact reusable procedures
  - repo-portable structure
- Avoid duplicating the same operational logic three times for Codex CLI, Claude Code, and Gemini CLI.

## Behavioral Seam to Keep Stable
- The stable seam is the FIC workflow contract:
  - entry point loads core rules
  - phase aliases remain discoverable
  - research/plan/implement/validate artifacts still land in `.thoughts/...`
  - project context remains separate from reusable agent behavior

## Highest Protection Seam
- Not a code-testing seam; this is a configuration/instruction migration.
- The equivalent protection seam is document-level compatibility:
  - one canonical source for FIC workflow text
  - thin per-CLI adapters
  - no divergence in phase semantics across CLIs

## Findings

### 1. Current repo state
- The repo is currently optimized for entry-point compatibility, not skill portability.
- `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` share the same entry text through symbolic links to `.rules/entry.md`; this is not file-level duplication.
- The existing `.agents/skills/intellij-navigation/SKILL.md` already matches the emerging `SKILL.md` pattern and proves the repo can host reusable capability modules.

### 2. What should remain always-on vs on-demand
- Keep always-on:
  - minimal project entry file per CLI
  - core project rules that must apply every session
  - project-specific context from `PROJECT.md`
- Move to skills:
  - FIC phase procedures
  - TDD playbook
  - refactoring planner
  - feedback loop workflow
  - specialized navigation/research helpers
  - any long checklist or multi-step operational guide

### 3. Official capability check as of 2026-04-22

Re-check result:
- The broad compatibility conclusion still holds.
- The Codex adapter path in the original 2026-04-15 recommendation needs correction:
  - current Codex docs say repository skills are discovered from `.agents/skills`, not `.codex/skills`.
  - Codex plugins are now the documented installable distribution unit for reusable skills and apps.
- Claude Code and Gemini CLI source checks did not change the adapter strategy.

#### Codex CLI
- Codex officially supports both `AGENTS.md` and skills.
- Official docs state Codex reads `AGENTS.md` files before work and layers global and project guidance.
- Official docs also state Codex skills use `SKILL.md`, are loaded via metadata first, and are available in the CLI, IDE extension, and Codex app.
- Repository-scoped Codex skills should live under `.agents/skills`.
- Codex plugins are the documented installable distribution unit when skills should be shared beyond one repo.
- This means Codex can support a split architecture cleanly:
  - `AGENTS.md` for always-on repo policy
  - `.agents/skills/<skill-name>/SKILL.md` directories for procedural workflows
  - plugins for broader distribution, if needed

#### Claude Code
- Claude officially supports `CLAUDE.md` for always-on project memory.
- Claude docs explicitly say that if a repo already uses `AGENTS.md`, `CLAUDE.md` can import `AGENTS.md`.
- Claude officially supports skills in `.claude/skills/<name>/SKILL.md`.
- Claude docs also say skills follow the Agent Skills open standard and are the preferred replacement for legacy custom commands.
- This is the cleanest target for migration because Claude already models the same split:
  - `CLAUDE.md` for persistent project guidance
  - skills for procedures and reusable workflows

#### Gemini CLI
- Gemini officially supports `GEMINI.md` as hierarchical context.
- Gemini officially supports project-level custom commands in `.gemini/commands/*.toml`.
- Gemini also supports installable extensions that bundle prompts, MCP servers, and custom commands.
- Gemini does not present `SKILL.md` as its native packaging format.
- Therefore Gemini compatibility is possible, but it is adapter-based rather than native-standard:
  - `GEMINI.md` for always-on context
  - `.gemini/commands/*.toml` or an extension package as the execution surface for reusable workflows

### 4. Compatibility conclusion
- Codex CLI and Claude Code align well around an open-skill model.
- Gemini CLI aligns at the architectural level, but not at the file-format level.
- So “one exact skill artifact for all three” is not the right target.
- The right target is:
  - one canonical workflow/spec source
  - two native skill adapters (`Codex`, `Claude`)
  - one Gemini adapter through project-level `commands`

## Recommended Target Architecture

### A. Canonical source inside the repo
- Keep the canonical workflow text in `.rules/`, not inside three platform-specific folders.
- Use `.rules/fic/` for extracted FIC phase specs:

```text
.rules/
  entry.md
  base-rules.md
  fic-workflow.md
  fic/
    research.md
    plan.md
    implement.md
    validate.md
```

- Rationale:
  - one source of truth;
  - simpler migration;
  - preserves the current mental model;
  - platform adapters can stay thin.

### B. Thin per-CLI entry files
- Keep these files in the repo root:
  - `AGENTS.md`
  - `CLAUDE.md`
  - `GEMINI.md`
- Each should be a minimal adapter, not the place where workflow logic lives.

Suggested intent:
- `AGENTS.md`
  - short project policy
  - references Codex-native skills
- `CLAUDE.md`
  - import `AGENTS.md`
  - add Claude-only notes if needed
- `GEMINI.md`
  - mirror only the always-on project guidance
  - point the user/model to `.gemini/commands/` for phase workflows

### C. Convert procedural rules into reusable skills/workflows
- Create these canonical capability modules:
  - `fic-research`
  - `fic-plan`
  - `fic-implement`
  - `fic-validate`
  - `tdd-guardrails`
  - `refactoring-planner`
  - `feedback-learning-loop`
  - `intellij-navigation`

## Recommended Adapter Strategy

### Codex CLI adapter
- Implement each capability as a Codex skill:
  - `.agents/skills/fic-research/SKILL.md`
  - `.agents/skills/fic-plan/SKILL.md`
  - etc.
- Keep `AGENTS.md` focused on:
  - startup rules
  - how to invoke the skills
  - repository-specific constraints
- Best fit:
  - FIC procedures become skills
  - core norms remain in `AGENTS.md`
  - reusable distribution, if needed outside this repo, happens through a Codex plugin rather than a repo-local skill path

### Claude Code adapter
- Implement the same capability set as Claude skills:
  - `.claude/skills/fic-research/SKILL.md`
  - `.claude/skills/fic-plan/SKILL.md`
  - etc.
- Keep `CLAUDE.md` short and import `AGENTS.md`.
- This keeps the repo synchronized while allowing Claude-only features later if needed.

### Gemini CLI adapter
- Map each workflow to a command:
  - `.gemini/commands/fic/research.toml`
  - `.gemini/commands/fic/plan.toml`
  - `.gemini/commands/fic/implement.toml`
  - `.gemini/commands/fic/validate.toml`
- Optionally package these into a Gemini extension if distribution matters.
- Gemini command prompts should reference the canonical markdown docs and tell Gemini where to write artifacts.
- For Gemini, this is functionally equivalent to skills even if the native format is TOML commands plus `GEMINI.md`.

## Proposed Migration Mapping

| Current file | Recommended destination | Notes |
| :--- | :--- | :--- |
| `.rules/base-rules.md` | stay always-on canonical guidance | Do not fully convert to skill |
| `.rules/fic-workflow.md` | split into 4 workflow skills + short always-on summary | Best procedural extraction candidate |
| `.rules/tdd-with-agents.md` | `tdd-guardrails` skill | Procedure/checklist, not startup memory |
| `.rules/refactoring-planner.md` | `refactoring-planner` skill | Strong skill candidate |
| `.rules/ai-feedback-learning-loop.md` | `feedback-learning-loop` skill | Procedure, low-frequency, on-demand |
| `.agents/skills/intellij-navigation/SKILL.md` | keep as Codex repo skill and add Claude/Gemini adapters if needed | Already in the current Codex repo skill location |
| `AGENTS.md` / `CLAUDE.md` / `GEMINI.md` | keep as symbolic links to `.rules/entry.md` unless platform-specific adapter files are needed | No duplicated entry text exists today |

## Suggested Rollout Plan

### Phase 1: Normalize the content model
- Create canonical markdown specs for:
  - base startup guidance
  - each FIC phase
  - optional workflows
- Refactor existing rule files only enough to distinguish:
  - always-on facts
  - on-demand procedures

### Phase 2: Ship Codex and Claude adapters first
- These are the most natural targets because both support `SKILL.md`.
- For Codex, use `.agents/skills`, matching the current official repository-skill discovery path.
- This phase validates the canonical split with the lowest translation cost.

### Phase 3: Add Gemini command adapters
- Build `.gemini/commands/` from the same canonical specs.
- If team sharing matters across repos later, package them as a Gemini extension in a separate distribution slice.

### Phase 4: Trim root entry files
- After skill coverage exists, reduce `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` to concise startup guidance.
- Avoid keeping long procedural checklists in root memory files.

## Decisions
- Decision 1: keep `.rules/` as the canonical source.
  - Rationale:
    - simpler migration;
    - preserves the current mental model;
    - avoids introducing a structural `.agent-os/` layer.
- Decision 2: implement Gemini support as `.gemini/commands/`.
  - Rationale:
    - faster;
    - lower maintenance;
    - sufficient for repo-local workflow compatibility.
  - A full Gemini extension remains a future distribution option, not part of the first migration slice.

## Recommended Next Deliverable
- The smallest high-value next step is a `fic-plan` for:
  - extracting the four FIC phase aliases into canonical skill specs
  - generating first-class adapters for Codex and Claude
  - designing Gemini command equivalents without implementing them yet

## Bottom-Line Recommendation
- Do not try to replace this repo with one universal `SKILL.md` tree.
- Instead, treat the repo as a canonical instruction source and generate native adapters:
  - Codex: `AGENTS.md` + `.agents/skills/<name>/SKILL.md`
  - Claude: `CLAUDE.md` + `SKILL.md`
  - Gemini: `GEMINI.md` + `.gemini/commands/`
- The repo is already close to this shape. The migration is mostly extraction and packaging, not a conceptual rewrite.

## Sources
- Repo files inspected:
  - `AGENTS.md`
  - `CLAUDE.md`
  - `GEMINI.md`
  - `.rules/base-rules.md`
  - `.rules/fic-workflow.md`
  - `.rules/tdd-with-agents.md`
  - `.rules/refactoring-planner.md`
  - `.rules/ai-feedback-learning-loop.md`
  - `.docs/architecture-overview.md`
  - `.docs/agent-compatibility.md`
  - `.docs/fic-philosophy.md`
  - `.docs/maintenance-guide.md`
  - `.agents/skills/intellij-navigation/SKILL.md`
- Official docs verified on 2026-04-15 and re-checked on 2026-04-22:
  - OpenAI Codex `AGENTS.md`: https://developers.openai.com/codex/guides/agents-md
  - OpenAI Codex skills: https://developers.openai.com/codex/skills
  - OpenAI Codex CLI overview: https://developers.openai.com/codex/cli
  - Agent Skills open standard: https://agentskills.io/
  - Claude Code memory and `CLAUDE.md`: https://code.claude.com/docs/en/memory
  - Claude Code skills: https://code.claude.com/docs/en/skills
  - Claude Code extension overview: https://code.claude.com/docs/en/features-overview
  - Gemini CLI `GEMINI.md`: https://google-gemini.github.io/gemini-cli/docs/cli/gemini-md.html
  - Gemini CLI custom commands: https://google-gemini.github.io/gemini-cli/docs/cli/custom-commands.html
  - Gemini CLI extensions: https://google-gemini.github.io/gemini-cli/docs/extensions/
