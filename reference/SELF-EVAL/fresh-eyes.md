# Fresh Eyes Pass

> **Pattern:** Few-shot Prompting | Persona-based evaluation

---

## The Technique

When asked to test your own output:

**Adopt a new-user persona.**

Walk through the feature as if you've never seen the project.

---

## The Persona

```
┌──────────────────────────────────────┐
│  NEW USER PERSONA                    │
│                                      │
│  • Never seen the codebase           │
│  • Doesn't know conventions          │
│  • Has basic domain knowledge        │
│  • Wants to accomplish a task        │
│  • Gets confused easily              │
└──────────────────────────────────────┘
```

---

## What to Flag

| Category | Examples |
|----------|----------|
| **Confusing** | Unclear error messages, ambiguous naming |
| **Friction-Heavy** | Too many steps, unnecessary complexity |
| **Unclear** | Missing documentation, implicit requirements |
| **Inconsistent** | Different patterns than rest of codebase |
| **Unexpected** | Behavior that violates conventions |

---

## Few-Shot Application

The persona provides **reference points** (few-shot examples):

```
"As a new user, I would expect..."
"A new user might be confused by..."
"If I hadn't built this, I would wonder..."
```

---

## The Checklist

```markdown
## Fresh Eyes Review

### Onboarding
- [ ] Can I understand what this does without context?
- [ ] Are there clear entry points?
- [ ] Is the API intuitive?

### Usage
- [ ] Are error messages helpful?
- [ ] Do I know what went wrong?
- [ ] Is the happy path clear?

### Consistency
- [ ] Does this match the project's patterns?
- [ ] Would a new user find this predictable?

### Documentation
- [ ] Is there enough context to use this?
- [ ] Are assumptions documented?
```

---

## Example

### Builder Brain (❌)
```
This function works correctly. It handles
the edge cases I identified during implementation.
```

### Fresh Eyes (✅)
```
As a new user:
- The parameter name "opts" is vague - what options?
- No error message if I pass the wrong type
- The return format isn't documented
- The side effects aren't obvious
```

---

## Remember

> Builder-brain misses what users see.
>
> Fresh eyes catch friction.
>
> Personas reveal truth.
