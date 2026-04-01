# Mistake Logging

> **Pattern:** Reflexion | Continuous improvement through error analysis

---

## The Principle

After ANY correction from the user:

1. Log the pattern to `gotchas.md`
2. Convert mistakes into strict rules
3. Review past lessons at session start
4. Iterate until error rate drops to zero

---

## The Reflexion Loop

```
┌──────────────────────────────────────┐
│  User Correction Received            │
└──────────────┬───────────────────────┘
               │
               v
┌──────────────────────────────────────┐
│  1. ANALYZE PATTERN                  │
│     What category of error?          │
│     What assumption was wrong?       │
└──────────────┬───────────────────────┘
               │
               v
┌──────────────────────────────────────┐
│  2. DOCUMENT IN GOTCHAS.MD            │
│     Convert to strict rule           │
│     Include WHY for future context   │
└──────────────┬───────────────────────┘
               │
               v
┌──────────────────────────────────────┐
│  3. REVIEW AT SESSION START           │
│     Load lessons from gotchas.md     │
│     Apply to current work            │
└──────────────┬───────────────────────┘
               │
               v
┌──────────────────────────────────────┐
│  4. ITERATE                           │
│     Track error rate                   │
│     Target: zero                     │
└──────────────────────────────────────┘
```

---

## Gotchas.md Structure

```markdown
# Gotchas

## Category: [Error Type]

### Pattern: [Description]
**Strict Rule:** [What to do instead]

**Why:** [The correction that established this rule]

**How to apply:** [When this guidance kicks in]

---

## Category: Testing

### Pattern: Mocking the database
**Strict Rule:** Integration tests must hit a real database, not mocks.

**Why:** Prior incident where mock/prod divergence masked a broken migration.

**How to apply:** When writing tests for data layer, use testcontainers or test DB.
```

---

## When to Log

| Trigger | Action |
|--------|--------|
| User says "no not that" | Log the correction |
| User says "don't" | Log the constraint |
| User says "stop doing X" | Log the rule |
| User confirms unusual approach worked | Log the validation |

---

## Remember

> Every correction is a lesson.
>
> Every lesson is a rule.
>
> Every rule prevents future errors.
