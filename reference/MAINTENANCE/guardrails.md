# Proactive Guardrails

> Technique: **Directional Stimulus Prompting** - Directional stimuli for preventive action

---

## Directional Stimuli

Offer checkpoints automatically in risky situations:

### Before Risky Changes
```
"Want me to save state before this?"
```

### When a File Grows Large
```
"This is big enough to cause pain later —
want me to split it into smaller files?"
```

### When Project Lacks Validation
```
"I notice the project doesn't have error checking configured.
Want me to add basic type-check and lint?"
```

---

## Guardrail Triggers

| Situation | Directional Stimulus |
|-----------|----------------------|
| Refactor on file >300 LOC | "Save state first?" |
| Deleting a file | "Verify references first?" |
| Change to a public API | "Maintain backward compatibility?" |
| Adding a new dependency | "Verify compatibility?" |

---

## Proactivity Checklist

- [ ] Offered checkpoint before risky change?
- [ ] Flagged when file grew too large?
- [ ] Suggested automatic validation if it doesn't exist?
- [ ] Asked before breaking compatibility?

---

## Example Dialogue

```markdown
User: "Refactor the Dashboard component, it's 600 lines"

Directional Stimulus Agent:
"This is a significant refactor on a large file.
Would you like me to:

1. First save the current state (checkpoint)?
2. Split into smaller components during the refactor?
3. Or would you prefer I propose a structure before starting?"
```
