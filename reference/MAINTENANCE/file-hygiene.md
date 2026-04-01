# File Hygiene

> **Pattern:** Zero-shot Prompting | Clear constraint on file organization

---

## The Principle

When a file gets long enough that it's hard to reason about, suggest breaking it into smaller focused files.

Keep the project navigable.

---

## The Threshold

**Soft limit:** 300 lines  
**Hard limit:** 500 lines  
**Critical:** 1000+ lines

---

## Zero-Shot Application

The directive acts as a constraint that triggers:

1. **Recognition:** File is getting unwieldy
2. **Suggestion:** Propose splitting
3. **Action:** Break into focused files
4. **Result:** Project remains navigable

---

## Splitting Strategies

### By Responsibility

```
utils.ts (500 lines)
  ├── utils/date.ts
  ├── utils/string.ts
  ├── utils/validation.ts
  └── utils/index.ts (re-exports)
```

### By Domain

```
components/
  ├── Button/
  │   ├── index.tsx
  │   ├── styles.css
  │   └── test.tsx
  └── Card/
      ├── index.tsx
      ├── styles.css
      └── test.tsx
```

### By Layer

```
services/
  ├── api/
  │   ├── client.ts
  │   └── endpoints.ts
  └── business/
      ├── validators.ts
      └── transformers.ts
```

---

## The Conversation

```markdown
User: "Add feature X to this component"

Agent: "This component is 600 lines. Before adding feature X,
I'd recommend splitting it into:

1. Component.tsx (UI only)
2. useComponent.ts (logic)
3. utils.ts (helpers)

This keeps each file focused and maintainable.

Should I proceed with the split first?"
```

---

## Remember

> Large files are a form of technical debt.
>
> Split early, split often.
>
> Keep it navigable.
