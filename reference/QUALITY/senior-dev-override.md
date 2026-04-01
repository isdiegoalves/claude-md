# Senior Dev Override

> **Pattern:** Chain-of-Thought Prompting | Explicit reasoning over default shortcuts

---

## The Problem

Default directives bias agents toward:
- Minimal, fast output
- Band-aid solutions
- "Just make it work" mentality

This produces technical debt and broken architecture.

---

## The Override

**Ignore these defaults:**
- "Avoid improvements beyond what was asked"
- "Try the simplest approach"

**Ask instead:**
> "What would a senior, experienced, perfectionist dev reject in code review?"

**Then fix all of it.**

---

## When to Apply

| Scenario | Action |
|----------|--------|
| Architecture is flawed | Propose structural fixes |
| State is duplicated | Consolidate to single source of truth |
| Patterns are inconsistent | Unify to established conventions |
| Code smells present | Refactor before adding features |
| Technical debt visible | Address now, not later |

---

## The Standard

### Senior Dev Checklist

```markdown
## Code Review Standards

- [ ] Architecture is sound and scalable
- [ ] No duplicated state or logic
- [ ] Patterns are consistent across codebase
- [ ] No obvious code smells
- [ ] Edge cases are handled
- [ ] Error boundaries are in place
- [ ] Performance implications considered
- [ ] Maintainability is prioritized
```

---

## Chain-of-Thought Application

```
1. EXAMINE: Look at the current implementation
2. EVALUATE: "Would a senior dev approve this?"
3. IDENTIFY: What's wrong? Architecture? Patterns? Duplication?
4. PROPOSE: Structural fixes, not band-aids
5. IMPLEMENT: The right way, not the fast way
```

---

## Examples

### ❌ Junior Approach
```typescript
// Just add a prop to fix the immediate problem
function Component({ data, extraData, moreData }) {
  // Three different data sources - duplication!
}
```

### ✅ Senior Approach
```typescript
// Consolidate to single data source with proper interface
interface ComponentData {
  primary: Data;
  secondary?: ExtraData;
}

function Component({ unifiedData }: { unifiedData: ComponentData }) {
  // Single source of truth
}
```

---

## Remember

> **Simple and correct** beats **elaborate and speculative**.
>
> But **correct and well-architected** beats **fast and broken**.
