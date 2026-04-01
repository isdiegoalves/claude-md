# Tool Result Blindness

> **Pattern:** Chain-of-Thought Prompting | Explicit reasoning about output limitations

---

## The Problem

Tool results over **50,000 characters** are silently truncated to a **2,000-byte preview**.

You may be making decisions based on incomplete data.

---

## The Mandate

**When any search or command returns suspiciously few results:**

1. Re-run with narrower scope
2. State when you suspect truncation occurred
3. Verify with additional, more specific queries

---

## Chain-of-Thought Analysis

```
1. RUN: Search or command
   |
   v
2. EVALUATE: "Does this match expectations?"
   |
   +---> [Fewer results than expected]
   |           |
   |           v
   |     3. SUSPECT: Truncation
   |           |
   |           v
   |     4. MITIGATE: Narrow scope
   |           |
   |           v
   |     5. RE-RUN: Specific query
   |
   +---> [Results match expectations]
               |
               v
         6. PROCEED: With confidence
```

---

## Truncation Indicators

| Sign | Likely Cause | Action |
|------|--------------|--------|
| Large search returns 10 results | Truncation | Narrow with specific path |
| File glob missing expected files | Pattern too broad | Use stricter glob |
| Grep results cut off mid-line | Output limit | Use head/tail with context |
| "Suspiciously few results" | Silent truncation | Re-run with narrower scope |

---

## Mitigation Strategies

### 1. Narrow by Directory
```bash
# Instead of:
grep -r "pattern" .

# Use:
grep -r "pattern" src/components/
```

### 2. Stricter Glob Patterns
```bash
# Instead of:
**/*.ts

# Use:
src/**/*.service.ts
```

### 3. Use Offset and Limit
```
Read file with offset/limit for large files
```

### 4. Chain Specific Queries
```bash
# First: Find relevant files
glob "src/**/*Controller.ts"

# Then: Search within results
grep "pattern" src/controllers/
```

---

## Required Transparency

**Always state when truncation might have occurred:**

> "Results seem truncated. Re-running with narrower scope..."

> "Search returned fewer results than expected for this codebase size. Verifying..."

---

## Remember

> Silent truncation produces silent bugs.
>
> Suspect, verify, then proceed.
