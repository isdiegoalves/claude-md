# Step 0: Delete Before You Build

**Pattern:** Zero-shot Prompting
**Source:** CLAUDE.md Section 1 - Pre-Work

> Dead code accelerates context compaction. Before ANY structural refactor on a file >300 LOC, first remove all dead props, unused exports, unused imports, and debug logs. Commit this cleanup separately before starting the real work. After any restructuring, delete anything now unused. No ghosts in the project.

---

## Pre-Refactor Checklist

Copy and paste this checklist before starting any structural refactor:

```markdown
## Pre-Refactor Cleanup Checklist

- [ ] Identify target file(s) >300 LOC
- [ ] Scan for dead props (unused component properties)
- [ ] Scan for unused exports (functions, constants, types)
- [ ] Scan for unused imports
- [ ] Scan for debug logs (console.log, debug statements)
- [ ] Remove all dead code identified
- [ ] Commit cleanup: `git commit -m "cleanup: remove dead code before refactor"`
- [ ] Proceed with structural refactor
```

---

## Dead Code Cleanup Rules

### What to Remove

| Category | Examples | How to Identify |
|----------|----------|-----------------|
| **Dead Props** | Props declared but never used in the component | Search for props not referenced in the component body |
| **Unused Exports** | `export const helper = ...` never imported elsewhere | Check if any other file imports the symbol |
| **Unused Imports** | `import { unused } from './module'` | Gray lines in VS Code or `organize imports` |
| **Debug Logs** | `console.log`, `console.debug`, `debugger;` | Search for `console.` and `debugger` |
| **Commented Code** | Commented-out code blocks | Search for `/* ... */` and `//` followed by code |

### Thresholds

- **300 LOC**: Critical threshold. Files larger than 300 lines must go through cleanup before any structural refactor
- Metric: Count lines of code (excluding comments and blank lines)

### Commit Process

1. **Separate commit required**: Cleanup MUST be committed separately from the refactor
2. **Standard message**: `cleanup: remove dead code before refactor`
3. Don't mix cleanup changes with logic changes in the same commit

### Post-Refactor

After any restructuring:
- Re-run the dead code check
- Verify that exported symbols moved to new files have had their originals deleted
- Ensure: **No ghosts in the project**

---

## Complete Workflow

```text
+-------------------------------------------------------------+
|  START: Identified file >300 LOC for refactor               |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  1. RUN CLEANUP CHECKLIST                                   |
|     • Dead props? → Remove                                  |
|     • Unused exports? → Remove                              |
|     • Unused imports? → Remove                              |
|     • Debug logs? → Remove                                  |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  2. SEPARATE COMMIT                                         |
|     git add .                                               |
|     git commit -m "cleanup: remove dead code before refactor" |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  3. RUN REFACTOR                                            |
|     (Now start the structural work)                         |
+-------------------------------------------------------------+
                              |
                              v
+-------------------------------------------------------------+
|  4. POST-REFACTOR VERIFICATION                              |
|     • New dead code created?                                |
|     • Old files can be deleted?                             |
|     • Final commits                                         |
+-------------------------------------------------------------+
```

---

## Prompt Template for Agents

Use this prompt to instruct any agent on this workflow:

```markdown
## Zero-Shot Instruction: Delete Before You Build

Before any structural refactor on files >300 lines, execute:

1. Identify dead code: dead props, unused exports, unused imports, debug logs
2. Remove all dead code found
3. Separate commit with message: "cleanup: remove dead code before refactor"
4. Only then proceed with the requested refactor

Threshold: 300 LOC is the critical trigger for this workflow.
```
