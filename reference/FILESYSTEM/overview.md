# File System as State

> **Pattern:** Chain-of-Thought Prompting | Progressive disclosure through file organization

---

## The Principle

The file system is your most powerful general-purpose tool. Stop holding everything in context.

---

## Active File System Usage

### 1. Selective Reading

**Don't dump large files into context.**

```bash
# Use bash to grep, search, tail
# Agentic search beats passive context loading
```

### 2. Write Intermediate Results

```markdown
## Analysis Results: [Task Name]

### Files Affected
- src/components/Button.tsx
- src/utils/helpers.ts

### Decisions
1. [Decision made]

### Next Steps
1. [Step to take]
```

### 3. Process Large Data with Bash Tools

```bash
# Use grep, jq, awk for scripting
grep "pattern" results.json | jq '.data[]'
```

### 4. Memory Across Sessions

```markdown
## Session Memory: [Topic]

### Key Decisions
- Decision 1

### Pending Work
- Task 1

### References
- [Link to file]
```

### 5. Debugging Artifacts

```markdown
## Debug Log: [Issue]

### Error
[Error message]

### Attempts
1. [Attempt 1]: [Result]
```

### 6. Progressive Disclosure

```
context-log.md
  ├── references/
  │     ├── decision-1.md
  │     └── decision-2.md
  └── summary.md
```

---

## File System Strategies

| Strategy | Use Case |
|----------|----------|
| **Grep First** | Find relevant content before reading |
| **Write Summaries** | Compact context for future reference |
| **Chain Bash** | Process data without loading into context |
| **Structured Directories** | Enable progressive disclosure |
| **Log to Files** | Reproducible debugging artifacts |

---

## Remember

> The file system is your external memory.
>
> Use it actively. Don't hoard context.
