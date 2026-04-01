# Sub-Agent Swarming

> Technique: **Prompt Chaining** | Source: CLAUDE.md §4

---

## When to Use

**ACTIVATE when:** Task touches >5 independent files

**REQUIRED for:**
- Multi-file refactors
- Adding features that affect multiple modules
- Changes across the entire codebase

**NOT optional.** One agent processing 20 files sequentially guarantees context decay.

---

## How to Partition

### Golden Rule: 5-8 files per agent

| Total Files | Agents Required | Available Tokens |
|-------------|-----------------|------------------|
| 6-8 | 1 | ~167K |
| 9-16 | 2 | ~334K |
| 17-25 | 3-4 | ~501K-668K |
| 25+ | 5+ | 835K+ |

### Partitioning Strategies

**By Domain (Recommended)**
```
Agent A: UI components (5-8 .tsx files)
Agent B: Business logic (5-8 .ts files)
Agent C: Utilities and helpers (5-8 files)
```

**By Dependency**
```
Agent A: Interfaces and types (base files)
Agent B: Implementations that depend on A
Agent C: Tests and mocks
```

**By Location**
```
Agent A: src/features/auth/*
Agent B: src/features/dashboard/*
Agent C: src/shared/*
```

---

## Orchestration Workflow

### Phase 1: Analysis and Planning
1. Map all affected files
2. Group by logical cohesion
3. Define dependency order
4. Create a brief for each agent

### Phase 2: Parallel Execution
```
+-----------------------------------------+
| Orchestrator Agent                      |
| ( maintains global view )               |
+--------------+--------------------------+
       |     |     |
       v     v     v
   +------+ +------+ +------+
   |Agent | |Agent | |Agent |
   |  A   | |  B   | |  C   |
   | 5-8  | | 5-8  | | 5-8  |
   | files| | files| | files|
   +--+---+ +--+---+ +--+---+
      |        |        |
      +--------|--------+
               v
        +----------------+
        | Merge &        |
        | Verification   |
        +----------------+
```

### Phase 3: Integration
1. Check for conflicts between results
2. Validate shared interfaces
3. Run end-to-end tests
4. Confirm global type-check

---

## Orchestration Checklist

### Pre-Flight
- [ ] List EXACTLY which files will be modified
- [ ] Group into batches of 5-8 files
- [ ] Identify dependencies between batches
- [ ] Define which agent runs first (if there are deps)

### For Each Agent
- [ ] Clear brief with defined scope
- [ ] Sufficient context (don't overload)
- [ ] Integration point defined
- [ ] Clear success criteria

### Post-Execution
- [ ] All batches completed?
- [ ] Interfaces between batches consistent?
- [ ] `npx tsc --noEmit` passes?
- [ ] Tests pass?

---

## Practical Example

**Scenario:** Refactor 15 authentication files

```
❌ WRONG:
   1 agent processes all 15 files sequentially
   → Context decay at file 10+
   → Bugs in later files

✅ CORRECT:
   Agent A: Types, interfaces, contracts (3 files)
   Agent B: Auth hooks and services (6 files)
   Agent C: Login UI components (6 files)

   → Parallel execution
   → 3 × 167K = 501K effective tokens
   → Each file with fresh context
```

---

## Anti-Patterns

| Problem | Solution |
|---------|----------|
| Single agent with >8 files | Split into multiple agents |
| Batches without clear criteria | Group by domain/dependency |
| Context overlap between agents | Define clear interfaces |
| Unnecessary synchronous orchestration | Run independent tasks in parallel |
