# Parallel Batch Changes

> Technique: **Prompt Chaining**

---

## The Principle

When the same edit needs to happen across many files, suggest **parallel batches**.

- Verify each change in context
- Reckless bulk edits break things silently
- Splitting into batches allows verification between steps

---

## Batch Strategy

### Split by Type

```
Batch A: UI components (5-8 .tsx files)
Batch B: Services/API (5-8 .ts files)
Batch C: Tests (5-8 .test.ts files)
```

### Split by Dependency

```
Batch 1: Interfaces and types (base)
Batch 2: Implementations that depend on Batch 1
Batch 3: Components that depend on Batch 2
```

---

## Batch Checklist

### Before
- [ ] Identified all affected files
- [ ] Grouped into batches of at most 5-8 files
- [ ] Defined dependency order between batches

### During
- [ ] Ran technical verification after each batch
- [ ] Confirmed nothing broken from the previous batch
- [ ] Documented changes for the next batch

### After
- [ ] Final verification across all modified files
- [ ] Tests pass
- [ ] Type-check clean

---

## Example: Mass Rename

**Scenario:** Rename `getUser` to `fetchUser` across 20 files

```
❌ WRONG: Edit all 20 files at once

✅ CORRECT:
  Batch 1: API layer (api/user.ts, api/client.ts)
  Batch 2: Hooks (hooks/useUser.ts)
  Batch 3: Components (components/User*.tsx)
  Batch 4: Tests (*.test.ts)

  [Verification between each batch]
```
