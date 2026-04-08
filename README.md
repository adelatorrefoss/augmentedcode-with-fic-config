# Augmented code with FIC (Frequent Intentional Compaction) configuration

_This repo is a FIC workflow (Frequent Intentional Compaction) by  [Dex Horthy - Advanced context engineering for coding agents][6]_

_Thanks to [Eduardo Ferro][1] for the base repo and [Nacho Viejo][3] for the inspiration to try FIC_
_[Eduardo Ferro - Augmented code configuration][1]_ 
_[Nacho Viejo FIC post][3]_

This repo proposes a clear information architecture:
- **.rules/**: the normative rule set (single source of truth + other rules) (for agents).
- **.docs/**: stable, readable documentation (for humans).
- **.thoughts/**: folders prepared for FIC artifacts (research / plans / prs).
- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`: agent entry points linked to the one and only `.rules/entry.md`.

## Core Principles

- **Context Hygiene**: Treat context as a scarce resource; frequently summarize and reset.
- **Small, Reversible Steps**: Break tasks into the smallest possible slices to minimize risk.
- **Single Source of Truth**: All normative logic resides in `.rules/`.
- **Continuous Compaction**: At every boundary (research, plan, implementation), compact the current state.


## Installation & Setup

1. Copy the generic configuration files and directories to your working repository:

```bash
cp -rf .rules .agents .thoughts .docs AGENTS.md CLAUDE.md GEMINI.md PROJECT.md .gitignore /path/to/working-repo/
```

2. Treat the copied content as follows:

- `.rules`, `.thoughts`, `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` are the core generic FIC setup.
- `.docs` is generic supporting documentation that explains the philosophy, architecture, and maintenance model.
- `.agents` contains reusable agent skills and extensions. Keep this folder generic and portable; do not put machine-local configuration here.
- `PROJECT.md` is a starter project-specific file. Replace the placeholder content with context for your target repository.
- `.gitignore` is optional. Keep it only if it matches your target repository's needs.

## How to use FIC

The FIC (Frequent Intentional Compaction) workflow helps manage agent context by frequently summarizing and resetting it.

1. **Research**: Analyze the problem and save a compact summary in `.thoughts/shared/research/`.
2. **Plan**: Create a minimal TDD plan in `.thoughts/shared/plans/`.
3. **Implement**: Execute in micro-steps.
4. **Validate**: Run tests and capture a final summary in `.thoughts/shared/prs/`.

See [.docs/fic-philosophy.md](.docs/fic-philosophy.md) for more details, and [.rules/fic-workflow.md](.rules/fic-workflow.md) for detailed instructions.

### Example Prompts

The repo also supports shorthand phase aliases: `fic-research`, `fic-plan`, `fic-implement`, and `fic-validate`.
Use one small command per phase. The alias carries the workflow behavior; the text after `:` only provides the topic or task.

**Research**

```text
fic-research: get-users-api-endpoint
```

**Plan**

```text
fic-plan: get-users-api-endpoint
```

**Implement**

```text
fic-implement: get-users-api-endpoint
```

**Validate**

```text
fic-validate: get-users-api-endpoint
```

## Included Files

- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`: agent entry points linked to `.rules/entry.md`, the unique entry point
- `.rules/`: (for agents) mandatory operating rules and workflow guidance
- `.agents/`: generic reusable skills and agent extensions
- `.docs/`: (for humans) optional reference material for architecture, compatibility, and maintenance
- `.thoughts/`: templates and folders for research, planning, and validation artifacts
- `PROJECT.md`: project-specific context to customize after copying the repo

## More Documentation

- Use [.docs/architecture-overview.md](.docs/architecture-overview.md) for the repo structure and information architecture.
- Use [.docs/fic-philosophy.md](.docs/fic-philosophy.md) for FIC guidance.
- Use [.docs/agent-compatibility.md](.docs/agent-compatibility.md) for agent-specific reset guidance.
- Use [.docs/maintenance-guide.md](.docs/maintenance-guide.md) for documentation and rule maintenance practices.

## References

[1]: https://github.com/adelatorrefoss/augmentedcode-configuration/
[2]: https://github.com/affaan-m/everything-claude-code
[3]: https://www.linkedin.com/posts/saski_github-saskiaugmentedcode-configuration-share-7409316228294549504-RXRJ/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAACdAyYBerZ_Hv62VFsL9sVDbBepDDEJnSI
[4]: https://nikeyes.github.io/tu-claude-md-no-funciona-sin-context-engineering-es/
[5]: https://github.com/saski/augmentedcode-configuration
[6]: https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
