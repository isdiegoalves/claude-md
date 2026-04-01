# One Source of Truth

> **Pattern:** Zero-shot Prompting | Clear constraint prevents data duplication

---

## The Rule

**Never fix a display problem by duplicating data or state.**

One source. Everything else reads from it.

---

## The Anti-Pattern

```typescript
// ❌ WRONG: Duplicating state to fix a rendering bug
const [items, setItems] = useState([]);
const [displayItems, setDisplayItems] = useState([]); // Duplication!

// "Fixing" a display bug by copying state
useEffect(() => {
  setDisplayItems(items.filter(i => i.visible));
}, [items]);
```

**Problem:** You're solving the wrong problem.

---

## The Right Solution

```typescript
// ✅ CORRECT: Single source, computed values
const [items, setItems] = useState([]);

// Derived from single source - no duplication
const displayItems = useMemo(
  () => items.filter(i => i.visible),
  [items]
);
```

---

## Zero-Shot Constraint

The directive "One Source of Truth" acts as a **zero-shot prompt** that prevents:

- State duplication
- Sync bugs between copies
- Inconsistent data states
- Unnecessary complexity

---

## When Tempted to Duplicate

| Temptation | Correct Approach |
|------------|-----------------|
| "I need a filtered version" | Compute from source |
| "I need a transformed version" | Compute from source |
| "I need local state for UX" | Use the source, add UI state only |
| "I need a cache" | Ensure cache invalidation is automatic |

---

## The Test

Ask yourself:

1. **Is this data derived from somewhere else?** → Use a computed value
2. **Could this get out of sync with the source?** → You're duplicating
3. **Am I copying state to fix a bug?** → Fix the root cause

---

## Examples

### ❌ Duplication
```typescript
// Component with local copy
function UserProfile({ user }) {
  const [name, setName] = useState(user.name); // Duplication!

  useEffect(() => {
    setName(user.name); // Trying to sync
  }, [user.name]);
}
```

### ✅ Single Source
```typescript
// Read from source, transform as needed
function UserProfile({ user }) {
  // Direct from source
  const displayName = useMemo(
    () => user.name || 'Anonymous',
    [user.name]
  );
}
```

---

## Remember

> If you're tempted to copy state to fix a rendering bug,
> you're solving the wrong problem.
>
> Find the root cause. Keep one source.
