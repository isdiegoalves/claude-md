# Phased Execution

**Pattern:** Prompt Chaining
**Source:** CLAUDE.md Section 1 - Pre-Work

> Never attempt multi-file refactors in a single response. Break work into explicit phases. Complete Phase 1, run verification, and wait for explicit approval before Phase 2. Each phase must touch no more than 5 files.

---

## Copyable Checklist Template

### Phase Checklist

```markdown
## Phase [N]: [Phase Name]

**Objective:** [Describe the objective of this phase]
**Files:** [List maximum 5 files]

### Execution Checklist

- [ ] 1. [First task of the phase]
- [ ] 2. [Second task of the phase]
- [ ] 3. [Third task of the phase]
- [ ] 4. [Fourth task of the phase]
- [ ] 5. [Fifth task of the phase]

### Required Verification

- [ ] Run `npx tsc --noEmit` (type-check)
- [ ] Run `npx eslint . --quiet` (lint)
- [ ] All errors fixed
- [ ] Tests pass (if applicable)

### Awaiting Approval

- [ ] User reviewed the changes
- [ ] User approved next phase
- [ ] Proceed to Phase [N+1]
```

---

## Fundamental Rules

### 5-File Limit per Phase

| Rule | Description | Why? |
|------|-------------|------|
| **Hard limit** | Maximum 5 files modified per phase | Keeps context under control |
| **Independence** | Phases should be independent when possible | Allows isolated review |
| **Atomicity** | Each phase must leave code in a functional state | Don't break builds between phases |

### Examples of Phase Splits

**Scenario: Refactor 15 files**

```
❌ Wrong: Single phase modifying all 15 files at once
✅ Correct:
   - Phase 1: Files 1-5 (preparation)
   - Phase 2: Files 6-10 (main migration)
   - Phase 3: Files 11-15 (cleanup and finalization)
```

**Scenario: Add a complex new feature**

```
❌ Wrong: Everything in one response
✅ Correct:
   - Phase 1: Setup and interfaces (types, contracts)
   - Phase 2: Core implementation (main logic)
   - Phase 3: Integration and UI (components, views)
   - Phase 4: Tests and documentation
```

---

## Verification Process Between Phases

### Verification Checklist

Before requesting approval for the next phase:

```markdown
## Post-Phase Verification

### Technical Validation
- [ ] Type-check: `npx tsc --noEmit`
- [ ] Lint: `npx eslint . --quiet`
- [ ] Tests: `npm test` (or equivalent)
- [ ] Build: `npm run build` (if applicable)

### Quality Validation
- [ ] No dead code introduced
- [ ] No debug console.log
- [ ] Code follows project patterns
- [ ] States are consistent

### Context Validation
- [ ] Clear commit messages
- [ ] No broken references
- [ ] Imports/exports consistent
```

---

## Approval Protocol

### What to Expect from the User

1. **Review**: User should review the current phase changes
2. **Feedback**: User may request adjustments before the next phase
3. **Explicit approval**: Wait for "yes", "go", "do it", "proceed" or similar
4. **Never assume**: Don't start the next phase without clear confirmation

### Example Dialogue

```markdown
Agent: Phase 1 complete. Modified:
  - src/types/user.ts
  - src/api/user.ts
  - src/hooks/useUser.ts

Verification: Type-check and lint passed.
Awaiting your approval to start Phase 2.

User: go

Agent: [Starts Phase 2 immediately, without repeating the plan]
```

---

## Complete Workflow

```text
+--------------------------------------------------------------+
|  START: Task identified (e.g.: multi-file refactor)          |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  1. PLANNING                                                 |
|     • Break into phases                                      |
|     • Maximum 5 files per phase                              |
|     • Define dependency order                                |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  2. EXECUTE PHASE N                                          |
|     • Modify phase files                                     |
|     • Run technical verifications                            |
|     • Ensure functional state                                |
+--------------------------------------------------------------+
                               |
                               v
+--------------------------------------------------------------+
|  3. PRESENT RESULTS                                          |
|     • List modified files                                    |
|     • Summary of changes                                     |
|     • Verification status                                    |
|     • Ask: "Approve for next phase?"                         |
+--------------------------------------------------------------+
                               |
                               v
                    +--------------------+
                    |  Awaiting Input    |
                    +--------------------+
                               |
              +----------------+----------------+
              |                                 |
              v                                 v
+-------------------------+        +-------------------------+
|  "yes/go/do it/proceed" |        |  "adjust X" / feedback  |
+-------------------------+        +-------------------------+
              |                                 |
              v                                 v
+-------------------------+        +-------------------------+
|  Start Phase N+1        |        |  Make adjustments       |
|  (don't repeat plan)    |        |  Re-verify              |
+-------------------------+        +-------------------------+
```

---

## Prompt Template for Agents

Use this prompt to instruct any agent on this workflow:

```markdown
## Prompt Chaining: Phased Execution

For multi-file tasks:

1. Break the work into explicit phases
2. Each phase must touch NO MORE THAN 5 files
3. Complete the current phase entirely
4. Run technical verification (type-check, lint)
5. Wait for explicit user approval before the next phase
6. Upon receiving "yes/go/do it", proceed immediately without repeating the plan

Never attempt multi-file refactors in a single response.
```
