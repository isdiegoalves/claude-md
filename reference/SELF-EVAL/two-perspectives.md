# Two-Perspective Review

> Technique: **Self-Consistency** - Multiple quality verification

---

## The Two-Perspective Technique

When evaluating your own work, present **two opposing views**:

1. **The Perfectionist's Perspective** - What would they criticize?
2. **The Pragmatist's Perspective** - What would they accept?

---

## Analysis Framework

### The Perfectionist's Perspective

"If I were an ultra-rigorous code reviewer, what would I criticize?"

- Could naming be clearer?
- Are there unhandled edge cases?
- Could the architecture be cleaner?
- Could tests be more comprehensive?

### The Pragmatist's Perspective

"If I had a tight deadline, what actually matters?"

- Does the main functionality work?
- Did it not introduce obvious bugs?
- Is the code maintainable enough?
- Is documentation sufficient for the context?

---

## Review Template

```markdown
## Two-Perspective Evaluation

### 👁️ Perfectionist's Perspective
**Criticisms:**
- [Point 1 that could be better]
- [Point 2 that could be more elegant]
- [Point 3 about architecture]

**Severity:** [Low/Medium/High]

### ⚖️ Pragmatist's Perspective
**Acceptances:**
- Delivered functionality works correctly
- Code doesn't introduce serious technical debt
- Within requested scope

**Acceptable Trade-offs:**
- [What is acceptable to not be perfect]

### 🎯 Recommendation
[Which perspective should prevail in this case]

**Justification:**
[Why we are choosing this trade-off]
```

---

## Complete Example

```markdown
## Evaluation: CSV Export Feature

### Perfectionist's Perspective
- CSV could have more robust formatting (comma escaping)
- Should support UTF-8 BOM encoding for Excel
- Architecture mixes UI with export logic

### Pragmatist's Perspective
- Export works for 95% of use cases
- Code is readable and maintainable
- Within original scope (simple export)

### Decision
Adopt pragmatic perspective, but document future improvements.
```

---

## When to Use Each Perspective

| Context | Perspective | Why? |
|---------|-------------|------|
| MVP/Prototype | Pragmatist | Speed > Perfection |
| Core System | Perfectionist | Quality is critical |
| Bug Fix | Pragmatist | Quick fix matters more |
| Refactor | Perfectionist | Moment to improve |
