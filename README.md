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

1. Copy the configuration files and directories to your working repository:

```bash
cp -rf .rules .agents .thoughts .docs AGENTS.md CLAUDE.md GEMINI.md PROJECT.md .gitignore /path/to/working-repo/
```

2. Customize `PROJECT.md` with your repository's specific information.

## How to use FIC

The FIC (Frequent Intentional Compaction) workflow helps manage agent context by frequently summarizing and resetting it.

1. **Research**: Analyze the problem and save a compact summary in `.thoughts/shared/research/`.
2. **Plan**: Create a minimal TDD plan in `.thoughts/shared/plans/`.
3. **Implement**: Execute in micro-steps.
4. **Validate**: Run tests and capture a final summary in `.thoughts/shared/prs/`.

See [.docs/fic-philosophy.md](.docs/fic-philosophy.md) for more details, and [.rules/fic-workflow.md](.rules/fic-workflow.md) for detailed instructions.

### Example Prompts

Use one small prompt per phase.

**Research**

```text
Read the problem and repo. Summarize only the next slice of requirements and open decisions. Do not implement. Save the result in `.thoughts/shared/research/<YYYYMMDDHHMM-topic>.md`.
```

**Plan**

```text
Propose the smallest viable plan for the next slice. Use TDD and keep the steps small. Save the plan in `.thoughts/shared/plans/<YYYYMMDDHHMM-topic>.md`.
```

**Implement**

```text
Execute the plan in tiny steps. One failing test at a time. No scope creep.
```

**Validate**

```text
Run tests, verify constraints, and summarize what changed and what comes next. Save the result in `.thoughts/shared/prs/<YYYYMMDDHHMM-topic>.md`.
```

## Included Files

- `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`: agent entry points linked to `.rules/entry.md`, the unique entry point
- `.rules/`: (for agents) mandatory operating rules and workflow guidance
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
