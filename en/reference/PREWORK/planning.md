# Plan and Build Are Separate Steps

**Pattern:** Chain-of-Thought Prompting
**Source:** CLAUDE.md Section 1 - Pre-Work

> When asked to "make a plan" or "think about this first," output only the plan. No code until the user says go. When the user provides a written plan, follow it exactly. If you spot a real problem, flag it and wait - don't improvise. If instructions are vague (e.g. "add a settings page"), don't start building. Outline what you'd build and where it goes. Get approval first.

---

## When to Output Only the Plan

### Plan Mode Triggers

| User Request | Action | Example |
|--------------|--------|---------|
| "make a plan" | Plan only, no code | Output plan structure |
| "think about this first" | Plan only, no code | Analysis and recommendations |
| "how would you approach..." | Plan only, no code | Strategy and trade-offs |
| "outline..." | Plan only, no code | Implementation structure |

### Default Response for Plan Mode

```markdown
## Plan: [Task Name]

### Overview
[Brief description of what will be built]

### Proposed Structure

#### Files to Create
1. `path/to/file1.ts` - [Responsibility]
2. `path/to/file2.ts` - [Responsibility]
3. `path/to/file3.ts` - [Responsibility]

#### Files to Modify
1. `path/to/existing1.ts` - [Required change]
2. `path/to/existing2.ts` - [Required change]

### Dependencies
- [List of required external dependencies]

### Potential Issues
- [Identify known problems]

### Next Steps
Awaiting your confirmation with "yes", "go", or "do it" to start implementation.
```

---

## When to Wait for Approval

### Scenarios Requiring Explicit Approval

| Scenario | Why Wait? | Example of Vague Input |
|----------|-----------|------------------------|
| **Vague instructions** | No clear behavior specification | "add a settings page" |
| **Undefined scope** | Not clear what should be included | "improve the dashboard" |
| **Multiple options** | More than one valid approach | "refactor the auth" |
| **High impact** | Changes affecting many files | "migrate to new architecture" |
| **Ambiguity** | Can be interpreted multiple ways | "add theme support" |

### What to Obtain Before Building

1. **Clear specification**: What exactly needs to be done
2. **Defined scope**: Limits of what is included/not included
3. **Confirmed approach**: Which solution to adopt
4. **Explicit approval**: "yes", "go", "do it", "proceed"

---

## How to Handle Vague Instructions

### Example: "Add a settings page"

```
❌ Wrong: Start coding immediately
✅ Correct:
   1. Ask clarifying questions:
      - "What settings should be available?"
      - "Should it be a separate page or modal?"
      - "Is there an existing design/mockup to follow?"
      - "Where should the access link be?"
   2. Present an outline of what will be built
   3. Wait for approval before starting
```

### Response Template for Vague Instructions

```markdown
Before starting, I need to clarify a few points about "[vague instruction]":

## Clarifying Questions

1. [Specific question about behavior]
2. [Specific question about scope]
3. [Specific question about design/patterns]

## Preliminary Proposal

Based on what I understand, I plan to:

### What I'll build:
- [Item 1]
- [Item 2]
- [Item 3]

### Where it will go:
- `src/path/file1.ts`
- `src/path/file2.ts`

### What I will NOT include (unless specified):
- [Out-of-scope items]

Please confirm if this is correct or adjust as needed.
Say "go" when you're ready to proceed.
```

---

## Rules for Following Exact Plans

### When the User Provides a Written Plan

1. **Follow exactly**: Implement as specified
2. **Don't improvise**: Don't add unsolicited "improvements"
3. **Flag real problems**: If you find a problem, report and wait
4. **Don't bypass**: Don't ignore parts of the plan without approval

### Example of a Real Problem

```
User: "Move the calculateTotal function to utils.ts and delete the
       original file without checking dependencies"

Agent: I identified a problem: calculateTotal is imported by 5 other
       files. Deleting without updating the imports will break the code.

       Options:
       1. Move and automatically update all imports
       2. Move, keep an export redirect in the original file temporarily
       3. Reconsider the change

       How would you like to proceed?
```

---

## Decision Flow

```text
+-------------------------------------------------------------+
|  USER REQUEST                                               |
+-------------------------------------------------------------+
                              |
                              v
                    +------------------+
                    |  Is it to make   |
                    |  a plan?         |
                    +------------------+
                              |
              +---------------+---------------+
              | YES                          | NO
              v                              v
+----------------------------+   +----------------------------+
|  OUTPUT ONLY THE PLAN      |   |  Are instructions clear   |
|  • Structure               |   |  and specific?            |
|  • Files                   |   +----------------------------+
|  • Trade-offs              |                  |
|  • No code                 |         +-------+-------+
+----------------------------+         | YES           | NO
           |                         v               v
           |          +--------------------+  +--------------------+
           |          |  EXECUTE DIRECTLY  |  |  VAGUE INSTRUCTIONS|
           |          |  Follow user's     |  |  • Ask questions   |
           |          |  plan exactly      |  |  • Present outline |
           |          +--------------------+  |  • Wait for        |
           |                                  |    approval        |
           |                                  +--------------------+
           |
           v
+----------------------------+
|  WAIT FOR APPROVAL:        |
|  "yes", "go", "do it"      |
+------------------------------------+
           |
           v
+----------------------------+
|  ONLY THEN:                |
|  START IMPLEMENTATION      |
+----------------------------+
```

---

## Prompt Template for Agents

Use this prompt to instruct any agent on this workflow:

```markdown
## Chain-of-Thought: Plan and Build Are Separate

Planning rules:

1. When asked to "make a plan" or "think about this first",
   output ONLY the plan - no code
2. When the user provides a written plan, follow it exactly
3. If you find real problems, flag and wait - don't improvise
4. For vague instructions (e.g. "add a settings page"):
   - Present an outline of what you'll build
   - Specify where each file will go
   - Wait for explicit approval before starting

Clear separation: Plan first, build after the "go".
```
