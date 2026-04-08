# Maintenance Guide: Managing Agent Rules

To keep the agentic workspace sustainable, the rules and configuration must be maintained like code.

## 1. Minimal Rule Set
The more rules you add, the more context is consumed.
- **Rule of Thumb**: Only add rules that solve a recurring problem.
- **Deprecation**: If a rule is consistently followed or no longer needed, remove it.

## 2. Refactoring Rules
When rule files become too long:
- Split them into specific concern-based files (e.g., `tdd-with-agents.md`, `refactoring-planner.md`).
- Link them from the central `entry.md` only when they are needed for the current task.

## 3. FIC Performance Check
If the agent consistently misses a specific rule, don't just repeat it.
- **Analysis**: Is the rule unclear? Is it conflicting with another rule?
- **Action**: Rewrite the rule to be more imperative or use a concrete example.

## 4. Documentation vs Rules
- **`.rules/`**: Rules are normative and tell the agent *how* to act.
- **`.docs/`**: Documentation is descriptive and tells the agent *what* exists.
- **Avoid Duplication**: Do not put the same information in both places. Rules should point to documentation for domain-specific details.

## 5. Maintenance Loop
Review the workspace after each project or major feature.
- Update `PROJECT.md` for new repo context.
- Archive old `.thoughts/` artifacts to keep the directory clean.
- Update the `base-rules.md` if your team's best practices have evolved.
