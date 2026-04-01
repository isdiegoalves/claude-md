# Verify Before Reporting

> Technique: **ReAct** (Reasoning + Acting + Verification)

---

## The ReAct Verification Cycle

Before declaring any task "done", run the complete ReAct cycle:

```
[Reason]  Why am I verifying?
    |
    v
[Act]     Re-read everything modified
    |
    v
[Observe] What changed? What remains?
    |
    v
[Verify]  Final confirmation
    |
    v
[Report]  Only then: "Done!"
```

---

## Pre-Report Verification Checklist

### Content Review
- [ ] Nothing references something that no longer exists
- [ ] Nothing is unused (dead code)
- [ ] Logic flows correctly
- [ ] Imports/exports are consistent

### Technical Review
- [ ] Type-check: `npx tsc --noEmit` - CLEAN
- [ ] Lint: `npx eslint . --quiet` - CLEAN
- [ ] Tests pass (if applicable)
- [ ] Build successful (if applicable)

### Context Review
- [ ] Commit messages are clear and descriptive
- [ ] All relevant files were verified
- [ ] No "lost" files in the changes

---

## Report Template

```markdown
## Task Complete: [Task Name]

### Modified Files
1. `src/file1.ts` - [change]
2. `src/file2.ts` - [change]

### Verification Performed
- [x] Type-check: CLEAN
- [x] Lint: CLEAN
- [x] Tests: [X/Y passed]

### What was verified
- Nothing references removed symbols
- All imports are resolved
- Main logic works as expected

**Status: Ready for review**
```

---

## Anti-Patterns

❌ **NEVER report:**
- "Done!" without verifying
- "I think it's good" (subjective)
- "Seems to work" (without confirmation)

✅ **ALWAYS report:**
- "Verified: type-check and lint passed"
- "Re-read all modified files"
- "Status: [specific to what was verified]"
