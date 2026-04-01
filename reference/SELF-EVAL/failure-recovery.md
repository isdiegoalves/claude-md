# Failure Recovery

> **Pattern:** Tree of Thoughts | Branching evaluation when stuck

---

## The Rule

**If a fix doesn't work after two attempts:**

1. Stop
2. Read the entire relevant section top-down
3. Figure out where your mental model was wrong
4. Say so

If the user says "step back" or "we're going in circles," **drop everything** and rethink from scratch.

---

## Tree of Thoughts for Recovery

```
                    [Fix Failed]
                         |
         +---------------+---------------+
         |                               |
    [Attempt 1]                    [Attempt 2]
         |                               |
         +---------------+---------------+
                         |
                         v
                   [Still Failing?]
                         |
             +-----------+-----------+
             |                       |
            YES                     NO
             |                       |
             v                       v
    ┌─────────────────┐    ┌─────────────────┐
    │ STOP. DIAGNOSE. │    │ Continue with   │
    │                 │    │ current fix     │
    │ 1. Read section │    └─────────────────┘
    │    top-down     │
    │ 2. Identify     │
    │    wrong model  │
    │ 3. State error  │
    │ 4. Rethink      │
    └─────────────────┘
```

---

## The Diagnosis Protocol

### Step 1: Stop
```
❌ Don't keep trying variations
❌ Don't add more workarounds
✅ Pause and assess
```

### Step 2: Read Top-Down
```
- Re-read the entire relevant file/section
- Don't trust partial context
- Look for the actual problem, not assumed problem
```

### Step 3: Identify Wrong Model
```
- What did I assume that was incorrect?
- What context was I missing?
- What edge case did I overlook?
```

### Step 4: State the Error
```
"My mental model was wrong because..."
"I assumed X but actually Y..."
```

### Step 5: Rethink from Scratch
```
- Drop the current approach entirely
- Consider fundamentally different solutions
- Propose something new
```

---

## When User Says "Step Back"

**IMMEDIATE ACTIONS:**
1. Acknowledge the signal
2. Stop current approach
3. Summarize what was tried
4. Propose fundamentally different approach

---

## Example

### Attempt 1
Added null check - didn't work

### Attempt 2
Added optional chaining - still broken

### STOP. DIAGNOSE.
```
After two attempts, the issue persists.

Re-reading the file top-down...

Realization: My mental model was wrong.
I assumed the issue was in the data access,
but actually the problem is that the data
structure itself is different than expected.

The API returns { items: [...] } but I was
treating it as if it returns the array directly.

New approach: Fix the data extraction, not the access.
```

---

## Remember

> Two failed attempts = wrong model.
>
> Admit it. State it. Fix it properly.
