# Agent Compatibility Matrix: Resetting Context

Each AI agent has its own way of managing context. This matrix shows how to force a "compaction boundary" to maintain FIC effectiveness.

| Agent | Entry Point | Reset Method | FIC Effectiveness |
| :--- | :--- | :--- | :--- |
| **Claude Chat** | `CLAUDE.md` | New Chat / Conversation | High |
| **Claude Code** | `CLAUDE.md` | `/compact` or New Shell | Very High |
| **Gemini** | `GEMINI.md` | New Conversation | Medium (Persistent Memory) |
| **Codex (via IDE)** | `AGENTS.md` | Clear Chat / New Session | High (Stateless) |

## Reset Procedures

### Claude (Chat & Code)
Claude is highly sensitive to context.
- **Claude Chat**: Manually open a new conversation. Use the "Mandatory first message" from `README.md`.
- **Claude Code**: Use the `/compact` command to summarize and then `/init` (if supported) or start a new session.

### Gemini
Gemini tends to retain some "shadow" context between conversations.
- Use explicit imperative commands: "Forget all previous instructions. This is the only valid context."
- Be more direct than with Claude or Codex.

### Codex
Codex is typically stateless per call.
- Ensure you are not sending back the entire message history when starting a new task.
- Use a fresh session in your IDE plugin.
