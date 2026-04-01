# Forced Verification

> Prompting Technique: **Self-Consistency** - Systematic multiple verification until convergence

---

## The Problem: The Illusion of Success

Your internal tool marks file writes as "successful" as soon as the bytes hit disk. **That doesn't mean the code compiles.** Many agents report "Done!" only for TypeScript or ESLint errors to be discovered immediately afterward.

### Chain-of-Thought: Why does this happen?

1. **Mistaken belief**: "The file was saved" != "The code is correct"
2. **Lack of feedback loop**: Without automatic verification, errors persist
3. **Insufficient commitment**: Premature completion reports

---

## The Mandate: Required Verification

**You are FORBIDDEN from reporting a task as complete until you have run:**

### Required Commands

```bash
# Type checking (required if project uses TypeScript)
npx tsc --noEmit

# Linting (required if ESLint is configured)
npx eslint . --quiet
```

### Explicit Feedback Cycle

```
+-----------------+
|   RUN CHECKS    | <-- Start: run the commands
+--------+--------+
         |
         v
+-----------------+
|   ANY ERRORS?   | <-- Carefully analyze output
+--------+--------+
         |
    +----+----+
    |         |
    v         v
+-------+  +---------+
|  YES  |  |   NO    |
+---+---+  +----+----+
    |           |
    v           v
+-----------+  +---------------+
| FIX ALL   |  | STATE: CLEAN  |
| ERRORS    |  +---------------+
+-----+-----+         |
      |               v
      |        +---------------+
      |        | REPORT DONE   | <-- Only now can you report success
      |        +---------------+
      |
      +--------+
               v
        +-------------+
        | REPEAT LOOP | <-- Return to start, re-run everything
        +-------------+
```

### Golden Rule

> **Repeat the cycle until the output is completely clean.** There's no such thing as "just a warning". There's no "I'll fix it later". Clean = zero errors.

---

## Verification Template

Before declaring "Done!", fill out this checklist:

```markdown
## Verification Checklist

- [ ] `npx tsc --noEmit` run
- [ ] `npx eslint . --quiet` run (if configured)
- [ ] All TypeScript errors fixed
- [ ] All ESLint errors fixed
- [ ] Final output: **CLEAN**

### Special Case: No Type-Checker

If the project doesn't have TypeScript configured:

- [ ] Type-checker: **NOT CONFIGURED** (explicit)
- [ ] ESLint run: [YES/NO]
- [ ] Status: [CLEAN/NOT APPLICABLE]

**Important:** Never say "Done!" with pending errors. If there's no type-checker, state that explicitly instead of faking success.
```

---

## Anti-Pattern Examples

### ❌ Wrong: Premature report

```
User: Create a Button component

Claude: [edits 3 files]

Done! I created the Button component.
```

**Problem**: No verification was done. There may be import errors, incorrect types, etc.

### ✅ Correct: Complete verification

```
User: Create a Button component

Claude: [edits 3 files]

[Running verifications...]
- npx tsc --noEmit: 2 errors found
  - src/Button.tsx:15 - Type 'string' is not assignable to type 'ButtonVariant'
  - src/Button.tsx:23 - Cannot find module './styles'

Fixing...

[Re-running...]
- npx tsc --noEmit: CLEAN ✓
- npx eslint . --quiet: CLEAN ✓

Done! Button component created and verified.
```

---

## Self-Consistency in Action

The **Self-Consistency** technique requires that you:

1. **Verify multiple times** - One run isn't enough; re-run after fixes
2. **Be systematic** - Same process every time, no exceptions
3. **Converge to zero** - Continue until there are no more errors
4. **Document the state** - Explicitly declare whether it's clean or not

> **Remember**: "Your code doesn't exist until it compiles without errors."
