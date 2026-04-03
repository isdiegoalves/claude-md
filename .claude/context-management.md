# Context Management

### Sub-Agent Swarming
For tasks touching >5 independent files, you MUST launch parallel
sub-agents (5-8 files per agent). Each agent gets its own context window
(~167K tokens). This is not optional. One agent processing 20 files
sequentially guarantees context decay. Five agents = 835K tokens of working
memory.

Use the appropriate execution model:
- **Fork**: inherits parent context, cache-optimized, for related subtasks
- **Worktree**: gets own git worktree, isolated branch, for independent
  parallel work across the same repo
- **/batch**: for massive changesets, fans out to as many worktree agents
  as needed

One task per sub-agent for focused execution. Offload research,
exploration, and parallel analysis to sub-agents to keep the main context
window clean. Use `run_in_background` for long-running tasks so the main
agent can continue other work while sub-agents execute. Do NOT poll a
background agent's output file mid-run - this pulls internal tool noise
into your context. Wait for the completion notification.

### Context Decay Awareness
After 10+ messages in a conversation, you MUST re-read any file before
editing it. Do not trust your memory of file contents. Auto-compaction may
have silently destroyed that context. You will edit against stale state and
produce broken output.

### Proactive Compaction
If you notice context degradation (forgetting file structures, referencing
nonexistent variables), run `/compact` proactively. Treat it like a save
point. Do not wait for auto-compact to fire unpredictably at ~167K tokens.
Summarize the session state into a `context-log.md` so future sessions or
forks can pick up cleanly.

### File Read Budget
Each file read is capped at 2,000 lines. For files over 500 LOC, you MUST
use offset and limit parameters to read in sequential chunks. Never assume
you have seen a complete file from a single read.

### Tool Result Blindness
Tool results over 50,000 characters are silently truncated to a 2,000-byte
preview. If any search or command returns suspiciously few results, re-run
with narrower scope (single directory, stricter glob). State when you
suspect truncation occurred.

### Session Continuity
Always prefer `--continue` to resume the last session rather than starting
fresh. All context, workflow state, and session memory is preserved. When
exploring two different approaches, use `--fork-session` to branch the
conversation and preserve both contexts independently.

> Deep reference: reference/CONTEXT/
