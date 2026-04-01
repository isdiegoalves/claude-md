# Don't Over-Engineer

> **Pattern:** Directional Stimulus Prompting | Clear constraints prevent drift

---

## The Rule

**Don't build for imaginary scenarios.**

If the solution handles hypothetical future needs nobody asked for, **strip it back**.

---

## The Principle

> Simple and correct beats elaborate and speculative.

---

## When to Apply

| ❌ Over-Engineering | ✅ Just Right |
|---------------------|---------------|
| Abstractions for "future flexibility" | Concrete implementations for current needs |
| Configuration for hypothetical use cases | Hardcoded values for actual requirements |
| Generic solutions for specific problems | Specific solutions that can be generalized later |
| Complex state management for simple UI | Local state that can be lifted when needed |
| Microservices for a monolith-sized problem | Monolith that can be split when scale demands |

---

## The Test

Ask yourself:

1. **Is this needed now?** (YAGNI - You Aren't Gonna Need It)
2. **Does the user ask for this?**
3. **Is there a concrete use case?**
4. **Can this be added later without breaking changes?**

If the answer is "no" to most, **strip it back**.

---

## Directional Stimulus

The directive "Don't Over-Engineer" acts as a **directional stimulus** that keeps solutions focused:

- **Constrains** the solution space
- **Prevents** speculative abstractions
- **Focuses** on immediate requirements
- **Enables** future extension without premature complexity

---

## Examples

### ❌ Over-Engineered
```typescript
// Generic plugin system for a single integration
interface Plugin<TConfig, TInput, TOutput> {
  configure: (config: TConfig) => void;
  execute: (input: TInput) => Promise<TOutput>;
}

// 50 lines of boilerplate for one use case
```

### ✅ Just Right
```typescript
// Simple function for the current need
async function integrateWithService(data: Data): Promise<Result> {
  // Direct implementation
}

// Can be abstracted later when there are 2+ integrations
```

---

## Remember

> Solve the problem in front of you.
>
> Future problems will have future context.
