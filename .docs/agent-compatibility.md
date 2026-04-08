# Agent Compatibility Matrix: Resetting Context

Each AI agent has its own way of managing context. This matrix shows how to force a "compaction boundary" to maintain FIC effectiveness.

## Volatile Guidance

This document describes operational behavior that may change as tools evolve.
Treat these notes as working guidance, not a permanent contract.
If an agent command, reset flow, or IDE behavior changes, update this file after revalidating the current behavior.

| Agent | Entry Point | Reset Method | FIC Effectiveness |
| :--- | :--- | :--- | :--- |
| **Claude Code** | `CLAUDE.md` | `/compact` or New Shell | Very High |
| **Gemini** | `GEMINI.md` | New Conversation | Medium (Persistent Memory) |
| **Codex (via IDE)** | `AGENTS.md` | Clear Chat / New Session | High (Stateless) |

## Reset Procedures

### Claude Code
Claude is highly sensitive to context.
- **Claude Code**: Use the `/compact` command to summarize and then `/init` (if supported) or start a new session.

### Gemini
Gemini tends to retain some "shadow" context between conversations.
- Use explicit imperative commands: "Forget all previous instructions. This is the only valid context."
- Be more direct than with Claude or Codex.

### Codex
Codex is typically stateless per call.
- Ensure you are not sending back the entire message history when starting a new task.
- Use a fresh session in your IDE plugin.
