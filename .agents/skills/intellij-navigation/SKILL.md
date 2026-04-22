---
name: intellij-navigation
description: Use when navigating code, finding usages, references, or understanding structure in a JetBrains-based project using MCP. Prefer semantic navigation over text search.
---

## Goal

Perform code navigation tasks using IntelliJ MCP tools with validation and classification of results.

## Mandatory behavior

- Use IntelliJ/Rider MCP tools for semantic navigation:
- resolving symbols,
- finding usages,
- inspecting declarations,
- validating references,
- understanding code structure.
- For known file paths, prefer direct filesystem reads such as `sed -n`, `rg`, or equivalent shell commands.
- For simple filename or text searches, prefer `rg --files` and `rg`.
- Do not use IntelliJ/Rider MCP for simple path-based reads unless IDE context is specifically useful.
- Prefer semantic understanding over text matching when the task is about code relationships.

## Workflow

1. Resolve symbol
- Use `get_symbol_info` if location is known

2. Search candidates
- Use `search_in_files_by_text` or regex
- Treat results as candidates only

3. Filter noise
Exclude:
- declarations
- overloads in same class
- interface members
- comments and strings
- generated files
- coverage reports
- TestResults, bin, obj

4. Validate
- For semantic validation, use `get_symbol_info`, `search_symbol`, or targeted MCP reads.
- For already-known file paths or line ranges, use direct filesystem reads.
- Confirm actual usage before reporting it.

5. Classify
- production call site
- test call site
- internal/self call
- non-call reference

## Output

- Only validated usages
- Include file + line
- Explicitly state if no production usages exist

## Tool constraints

- Do not use unsupported parameters
- Avoid truncateMode unless known valid
