# Spec-Based Development

> **Pattern:** Chain-of-Thought Prompting | Structured reasoning before action

---

## When to Use

**REQUIRED for:** Non-trivial features (3+ steps or architectural decisions)

**ACTIVATE when:**
- Feature involves multiple components
- User asks to "make a plan" or "think about this first"
- Architectural decisions are needed
- Implementation approach is unclear

---

## The Process

### Phase 1: Discovery Interview

Use the `AskUserQuestion` tool to interview the user about:

| Topic | Questions to Ask |
|-------|-----------------|
| **Technical Implementation** | What approach? What technologies? |
| **UX** | User flow? Edge cases? |
| **Concerns** | Performance? Security? Maintainability? |
| **Tradeoffs** | Speed vs quality? Short vs long term? |

### Phase 2: Write the Spec

The spec becomes the **contract** - execute against it, not assumptions.

```markdown
## Feature Spec: [Name]

### Overview
[Brief description]

### Technical Decisions
- [Decision 1]: [Rationale]
- [Decision 2]: [Rationale]

### Implementation Steps
1. [Step 1 with file paths]
2. [Step 2 with file paths]
3. [Step 3 with file paths]

### Edge Cases
- [Case 1]: [Handling]
- [Case 2]: [Handling]

### Verification Criteria
- [ ] Criterion 1
- [ ] Criterion 2
```

### Phase 3: Approval

Present the spec and **wait for explicit approval** before writing code.

---

## Golden Rules

1. **Strip away all assumptions** before touching code
2. **No code until user says go** - output only the plan
3. **Follow the spec exactly** - don't improvise if user provided a written plan
4. **Flag real problems** - if you spot an issue, flag it and wait

---

## Anti-Patterns

| ❌ Wrong | ✅ Right |
|----------|----------|
| Start building from vague instructions | Interview first, spec second, code third |
| Assume implementation details | Document decisions in spec |
| Change the plan mid-implementation without approval | Flag issues and wait for direction |
| Skip spec for "simple" features that span 3+ files | Always spec when complexity threshold met |
