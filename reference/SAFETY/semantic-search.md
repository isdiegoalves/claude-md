# No Semantic Search

> **Pattern:** Chain-of-Thought Prompting | Explicit, separate searches for comprehensive coverage

---

## The Constraint

**You have grep, not an AST.**

When renaming or changing any function/type/variable, you MUST search separately for multiple categories.

---

## The Multi-Search Protocol

Do not assume a single grep caught everything. **Assume it missed something.**

### Required Search Categories

```markdown
## Semantic Search Checklist

When renaming `foo` to `bar`:

### 1. Direct Calls and References
```bash
grep -r "foo" --include="*.ts" src/
```

### 2. Type-Level References
```bash
# Interfaces, generics, type annotations
grep -r "foo:" --include="*.ts" src/
grep -r "foo<" --include="*.ts" src/
```

### 3. String Literals
```bash
# Keys, property access, dynamic references
grep -r "\"foo\"" --include="*.ts" src/
grep -r "'foo'" --include="*.ts" src/
```

### 4. Dynamic Imports and require()
```bash
grep -r "require.*foo" --include="*.ts" src/
grep -r "import.*foo" --include="*.ts" src/
```

### 5. Re-exports and Barrel Files
```bash
grep -r "export.*foo" --include="*.ts" src/
grep -r "from.*foo" --include="*.ts" src/
```

### 6. Test Files and Mocks
```bash
grep -r "foo" --include="*.test.ts" src/
grep -r "foo" --include="*.spec.ts" src/
grep -r "mock.*foo" --include="*.ts" src/
```
```

---

## Why Separate Searches?

| Reason | Example |
|--------|---------|
| Grep is text-based, not AST-based | `foo()` vs `type Foo` vs `"foo"` |
| Different contexts need different handling | Call vs Type vs String key |
| Tests may reference differently | Mock names, spy references |
| Barrel files re-export | `export { foo } from './module'` |

---

## Chain-of-Thought Execution

```
1. IDENTIFY: What is being renamed/changed?
   |
   v
2. PLAN: Which search categories apply?
   |
   v
3. EXECUTE: Run each search separately
   |
   v
4. COMPILE: Aggregate all references
   |
   v
5. UPDATE: Modify all occurrences
   |
   v
6. VERIFY: Re-run searches to confirm zero results
```

---

## Example: Complete Rename Workflow

```bash
# Renaming function processData to transformData

# 1. Direct calls
grep -r "processData" --include="*.ts" src/ | grep -v "transformData"

# 2. Type annotations
grep -r "processData:" --include="*.ts" src/
grep -r "processData<" --include="*.ts" src/

# 3. String references (if any)
grep -r "\"processData\"" --include="*.ts" src/

# 4. Imports
grep -r "import.*processData" --include="*.ts" src/

# 5. Exports
grep -r "export.*processData" --include="*.ts" src/

# 6. Tests
grep -r "processData" --include="*.test.ts" src/

# After all edits, verify:
grep -r "processData" --include="*.ts" src/ | wc -l
# Should be 0 (or only in comments if intentionally kept)
```

---

## Remember

> One grep = incomplete picture.
>
> Six greps = confidence.
