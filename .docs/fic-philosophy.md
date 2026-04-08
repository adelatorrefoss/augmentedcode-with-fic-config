# FIC Philosophy: Frequent Intentional Compaction

## The Core Problem: Context Drift and Hallucination
As AI agents engage in long conversations, their "context window" fills with irrelevant details, failed attempts, and historical noise. This leading to:
- **Rule Erosion**: The agent stops following early instructions.
- **Hallucination**: The agent "remembers" things that never happened or invents constraints.
- **Verbosity**: The agent produces increasingly long and less useful responses.

## The Solution: Frequent Intentional Compaction (FIC)
FIC is a methodology designed to maintain high performance in agentic workflows by treating **context as a scarce resource** that must be managed.

### 1. Context Hygiene
Think of context like a physical workspace. If you never clean it, you can't find your tools.
- **Summarize Often**: Instead of carrying the whole history, we carry only the *current state* and the *next goal*.
- **Hard Resets**: We frequently start fresh sessions with only the essential "compacted" information.

### 2. Information Architecture
To support FIC, the repository uses a structured layout:
- **`.rules/`**: Normative logic (The "How").
- **`.docs/`**: Stable documentation (The "What").
- **`.thoughts/`**: Transient work (The "Current").

### 3. The Context Reset Rule
If an agent begins to drift, stop immediately. Do not try to fix the agent's logic incrementally. Compact the state, start a new session, and resume from the clean summary.

## Goals of FIC
- **Reliability**: Consistent adherence to rules.
- **Efficiency**: Fewer tokens wasted on irrelevant history.
- **Sustainability**: Enabling agents to work on complex projects over long periods without performance degradation.
