# Demand Elegance (Balanced)

> **Pattern:** Self-Consistency | Quality standards over speed

---

## The Prompt

For non-trivial changes, pause and ask:

> "Is there a more elegant way?"

---

## The Balance

| Scenario | Approach |
|----------|----------|
| Simple, obvious fix | Skip - just implement |
| Complex, hacky feeling fix | Pause and reconsider |
| Multiple similar workarounds | Find the pattern |
| "This feels wrong" | Trust instinct, refactor |

---

## When to Demand Elegance

**ACTIVATE when:**
- Fix feels hacky or workaround-ish
- Code requires extensive comments to explain
- You're copying patterns that feel off
- The solution is more complex than the problem

**SKIP when:**
- Simple, obvious fix for clear bug
- Standard, idiomatic solution
- Three experienced devs would write it the same way

---

## The Process

```
1. IMPLEMENT: First solution
2. EVALUATE: "Knowing everything I know now..."
3. CHALLENGE: Is this elegant?
4. REFACTOR: Implement the clean solution
5. VERIFY: Would three senior devs write it this way?
```

---

## Self-Consistency Check

### Before Submitting

```markdown
## Elegance Review

- [ ] Is this the most straightforward solution?
- [ ] Does it require minimal explanation?
- [ ] Would others naturally write it this way?
- [ ] Is the complexity proportional to the problem?
- [ ] Could I explain this to a junior dev easily?

If any are "no" → consider a cleaner approach.
```

---

## Examples

### ❌ Hacky
```typescript
// Workaround with nested conditionals
if (data && data.items && data.items.length > 0 && data.items[0].name) {
  // ...
}
```

### ✅ Elegant
```typescript
// Clean with optional chaining and early return
const firstName = data?.items?.[0]?.name;
if (!firstName) return null;
// ...
```

---

## Remember

> Elegance is not about cleverness.
>
> It's about clarity, simplicity, and maintainability.
