# Bug Autopsy

> **Pattern:** Reflexion | Self-reflection for continuous improvement

---

## The Process

After fixing a bug:

1. **Explain why it happened**
2. **Identify what could prevent it**
3. **Document the guardrail**

Don't just fix and move on - every bug is a potential guardrail.

---

## Reflexion Framework

```
┌─────────────────────────────────────┐
│  BUG IDENTIFIED                     │
└──────────────┬──────────────────────┘
               │
               v
┌─────────────────────────────────────┐
│  1. FIX THE BUG                     │
│     Implement the solution          │
└──────────────┬──────────────────────┘
               │
               v
┌─────────────────────────────────────┐
│  2. ANALYZE THE CAUSE               │
│     Why did this happen?            │
│     - Root cause identification     │
│     - Contributing factors          │
└──────────────┬──────────────────────┘
               │
               v
┌─────────────────────────────────────┐
│  3. PREVENTION ANALYSIS             │
│     What could catch this?          │
│     - Type system?                  │
│     - Lint rule?                    │
│     - Test pattern?                 │
│     - Process change?               │
└──────────────┬──────────────────────┘
               │
               v
┌─────────────────────────────────────┐
│  4. DOCUMENT IN GOTCHAS.MD          │
│     Convert to strict rule          │
└─────────────────────────────────────┘
```

---

## The Questions

### Root Cause Analysis
- What was the immediate cause?
- What was the underlying cause?
- What assumption was wrong?
- What context was missing?

### Prevention
- Could TypeScript have caught this?
- Could a test pattern detect this?
- Could a lint rule prevent this?
- Could a process change avoid this?
- Is there a tool that would flag this?

---

## Documentation Template

```markdown
## Bug Autopsy: [Brief Description]

### What Happened
[Describe the bug and its impact]

### Root Cause
[Explain why it happened]

### Prevention
[What could prevent this category in the future]

### Applied Guardrail
[What was implemented to prevent recurrence]
```

---

## Reflexion Application

```
1. OBSERVE: Bug was fixed
     |
     v
2. REFLECT: Why did this happen?
     |
     v
3. GENERALIZE: Pattern that could prevent
     |
     v
4. IMPLEMENT: Guardrail in gotchas.md
     |
     v
5. ITERATE: Apply to future work
```

---

## Example

### Bug
Function called with wrong argument order - `updateUser(id, data)` vs `updateUser(data, id)`

### Autopsy
```markdown
## Bug Autopsy: Argument Order Confusion

### What Happened
Called updateUser with arguments in wrong order,
resulting in data being treated as ID.

### Root Cause
- Similar types (string, object) made swap invisible
- No named parameters to enforce clarity
- Pattern inconsistent across codebase

### Prevention
- Use object parameters for 2+ arguments: `updateUser({ id, data })`
- Add stricter types that would fail on swap
- Consistent parameter order convention

### Applied Guardrail
Added to gotchas.md: "Functions with 2+ params 
should use object destructuring for clarity"
```

---

## Remember

> Every bug is a lesson.
>
> Every lesson is a guardrail.
>
> Document in gotchas.md.
