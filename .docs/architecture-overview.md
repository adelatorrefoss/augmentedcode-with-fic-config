# Architecture Overview: Agentic Workspace Structure

The repository organizes information into distinct layers based on their stability and purpose. This separation allows the AI agent to consume only what is necessary at each stage of a task.

## Information Layers

### 1. `.rules/` (The "How"): Normative Logic
This layer contains the system's "constitution." It defines the behavior and constraints for the AI agent.
- **`base-rules.md`**: Global rules (single source of truth).
- **`entry.md`**: Entry point that tells the agent which other rules are important.
- **`fic-workflow.md`**: Detailed instructions for the research-plan-implement-validate loop.
- **Specialized Rules**: (e.g., `tdd-with-agents.md`, `refactoring-planner.md`) loaded only when needed.

### 2. `.docs/` (The "What"): Stable Documentation
Human-readable documentation that provides context for both humans and agents. Unlike rules, these are not normative instructions but shared knowledge.
- High-level architecture and philosophy.
- Domain-specific glossaries.
- System setup and maintenance guides.

### 3. `.thoughts/` (The "Now"): Transient State
This is the workspace where the agent records its active process. It is the primary location for **Compaction Artifacts**.
- **`shared/research/`**: Findings and open questions for a task.
- **`shared/plans/`**: Minimal, step-by-step TDD plans.
- **`shared/prs/`**: Summaries of work performed for review or compaction.

## Interaction Model

The agent starts with `.rules/` to understand its behavior. It may consult `.docs/` for background knowledge. Then it executes the FIC workflow, recording its progress in `.thoughts/`.

At each compaction boundary (e.g., after research or a major plan completion), the agent resets its context. It then consumes only the **Compacted Summary** from `.thoughts/` to resume work in a fresh session.
