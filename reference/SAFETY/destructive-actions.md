# Destructive Action Safety

> **Pattern:** Directional Stimulus Prompting | Clear constraints prevent data loss

---

## The Mandate

**Never delete without verification.**

| Action | Required Verification |
|--------|----------------------|
| Delete a file | Verify nothing else references it |
| Undo code changes | Confirm you won't destroy unsaved work |
| Push to shared repo | Explicit user instruction required |
| Force push | **Never** without explicit authorization |

---

## The Protocols

### File Deletion

```markdown
## Before Deleting Any File

1. [ ] Search for imports: `grep -r "from './filename'" src/`
2. [ ] Search for dynamic imports: `grep -r "import('./filename')" src/`
3. [ ] Search for references: `grep -r "filename" src/`
4. [ ] Check test files: `grep -r "filename" **/*.test.ts`
5. [ ] Verify barrel exports: Check index.ts, index.js
6. [ ] Confirm with user if uncertain
```

### Undoing Changes

```markdown
## Before Undoing Code Changes

1. [ ] Check for uncommitted work: `git status`
2. [ ] Verify no staged changes will be lost
3. [ ] Confirm no new files will be deleted
4. [ ] Consider `git stash` instead of discard
```

### Shared Repository Actions

```markdown
## Repository Safety Rules

- [ ] Never push unless explicitly told to
- [ ] Never force push to main/master
- [ ] Never delete remote branches without confirmation
- [ ] Verify branch state before destructive operations
```

---

## Directional Stimulus

The constraints act as **directional stimuli** that:

- Prevent accidental data loss
- Force verification steps
- Require explicit authorization
- Protect shared state

---

## Anti-Patterns

| ❌ Wrong | ✅ Right |
|----------|----------|
| Delete file because "it's not used here" | Search entire codebase for references |
| `git checkout .` without checking status | Review changes before discarding |
| Force push to "fix" history | Ask user for authorization |
| Remove code that "looks unused" | Verify with search tools |

---

## Remember

> Data loss is permanent.
>
> Verification is cheap.
>
> Ask if uncertain.
