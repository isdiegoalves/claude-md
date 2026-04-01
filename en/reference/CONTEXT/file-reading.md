# File Read Budget

> Technique: **Zero-shot Prompting** | Source: CLAUDE.md §4

---

## Fundamental Limits

```
+----------------------------------------+
|  MAXIMUM PER READ: 2,000 lines        |
|  (= ~167K context tokens)             |
+----------------------------------------+
```

**Never assume** you've seen the complete file in a single read if:
- File has >500 LOC (Lines of Code)
- Error message was truncated
- Result seems incomplete

---

## Using Offset and Limit

### Basic Syntax

```typescript
Read({
  file_path: "/abs/path/to/file.ts",
  offset: 1,      // Starting line (1-based)
  limit: 500      // Number of lines
})
```

### Navigation Pattern

```
Read 1: offset=1,    limit=500  → Lines 1-500
Read 2: offset=501,  limit=500  → Lines 501-1000
Read 3: offset=1001, limit=500  → Lines 1001-1500
Read 4: offset=1501, limit=500  → Lines 1501-2000
...and so on
```

---

## Strategies for Files >500 LOC

### Strategy 1: Targeted Search (Recommended)

**When to use:** You know what you're looking for

1. Use `Grep` to locate specific patterns
2. Read only the relevant sections with offset/limit
3. Navigate via references (imports, exports)

```typescript
// Step 1: Find where the function is
Grep({ pattern: "function handleAuth", path: "/src" })

// Step 2: Read only the relevant block
Read({ file_path: "/src/auth/handlers.ts", offset: 145, limit: 50 })
```

### Strategy 2: Sequential Chunk Reading

**When to use:** Need to understand the entire file

```
Chunk 1: Header and imports (offset 1, limit 50)
Chunk 2: Interfaces and types (offset 51, limit 100)
Chunk 3: Main functions (offset 151, limit 300)
Chunk 4: Helpers and utils (offset 451, limit 200)
...
```

---

## Reading Checklist

### Before Reading
- [ ] Estimate the file size
- [ ] Define a clear reading objective
- [ ] Choose the appropriate strategy

### During Reading
- [ ] If >500 LOC: use offset/limit
- [ ] Note lines of interest for re-reading
- [ ] Check imports/exports for navigation

### After Reading
- [ ] Confirm you've seen the necessary sections
- [ ] Navigate to referenced files if needed
- [ ] Validate assumptions with a second read if uncertain
