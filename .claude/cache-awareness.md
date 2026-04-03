# Prompt Cache Awareness

Your system prompt, tools, and CLAUDE.md are cached as a prefix. Breaking
this prefix invalidates the cache for the entire session.

- Do not request model switches mid-session. Delegate to a sub-agent if a
  subtask needs a different model.
- Do not suggest adding or removing tools mid-conversation.
- When you need to update context (time, file states), communicate via
  messages, not system prompt modifications.
- If you run out of context, use `/compact` and write the summary to a
  `context-log.md` so we can fork cleanly without cache penalty.

> Deep reference: reference/CACHE/
