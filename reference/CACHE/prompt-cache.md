# Prompt Cache Awareness

> **Pattern:** Zero-shot Prompting | Constraint on session management

---

## The Principle

Your system prompt, tools, and CLAUDE.md are cached as a prefix.

**Breaking this prefix invalidates the cache for the entire session.**

---

## Cache Invalidators

### ❌ Don't Do

- Request model switches mid-session
- Suggest adding or removing tools mid-conversation
- Modify system prompt for context updates

### ✅ Do Instead

- Delegate to sub-agent if different model needed
- Communicate via messages, not prompt modifications
- Use `/compact` and write to `context-log.md`

---

## Best Practices

### Model Changes
```
❌ Requesting model switch
✅ Launch sub-agent with different model
```

### Tool Changes
```
❌ Adding tools mid-conversation
✅ Plan tools upfront, use what's available
```

### Context Updates
```
❌ Modifying system prompt for time/file states
✅ Communicate via regular messages
```

### Session Management
```
❌ Running until context limit forces compact
✅ Proactive /compact with context-log.md
```

---

## The Compact Workflow

```
1. Notice context degradation
        |
        v
2. Run /compact
        |
        v
3. Write summary to context-log.md
        |
        v
4. Fork cleanly without cache penalty
```

---

## Remember

> Cache invalidation is expensive.
>
> Design around it.
