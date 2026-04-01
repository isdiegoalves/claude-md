# Context Decay Awareness

> **Pattern:** Tree of Thoughts | Branching evaluation of context validity

---

## The Problem

After 10+ messages in a conversation, context auto-compaction may have **silently destroyed** your understanding of file contents.

You will edit against stale state and produce broken output.

---

## The Mandate

**After 10+ messages, you MUST re-read any file before editing it.**

Do not trust your memory of file contents.

---

## Tree of Thoughts Evaluation

```
                    [Need to edit file?]
                           |
           +---------------+---------------+
           |                               |
     [Messages < 10]                 [Messages >= 10]
           |                               |
           v                               v
    [Trust context?]              [MUST re-read]
           |                          BEFORE editing
     +-----+-----+
     |           |
     v           v
 [Simple]    [Complex]
 change      change
   |             |
   v             v
[Can trust]  [Re-read to
 context]     be safe]
```

---

## Warning Signs

| Symptom | Cause | Solution |
|---------|-------|----------|
| Referencing nonexistent variables | Stale context | Re-read file |
| Wrong line numbers | Context shifted | Re-read file |
| Forgotten file structure | Compaction | Re-read file |
| "I'm pretty sure..." | Memory unreliable | Re-read file |

---

## The 10-Message Rule

```markdown
## Context Decay Check

Messages in conversation: [N]

If N >= 10:
- [ ] Re-read file BEFORE any edit
- [ ] Verify line numbers
- [ ] Check variable names
- [ ] Confirm imports/exports

Remember: Auto-compaction is silent.
```

---

## Best Practices

1. **Re-read proactively** - Don't wait for errors
2. **Use offset/limit** - For large files, read relevant sections
3. **Verify after compact** - If `/compact` was run, re-read everything
4. **Keep a checklist** - Track which files you've verified

---

## Remember

> Your memory of file contents expires at 10 messages.
>
> Re-read or regret it.
