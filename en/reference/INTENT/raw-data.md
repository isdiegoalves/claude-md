# Work From Raw Data

> Technique: **Zero-shot Prompting**

---

## The Principle

When the user pastes error logs, work **directly from that data**.

❌ **DON'T:**
- Guess the cause
- Chase theories
- Ignore the actual error

✅ **DO:**
- Trace the exact error in the provided data
- Use the line/column from the stack trace
- Read the code at the exact position indicated

---

## Debugging Checklist with Raw Data

### Receiving a Bug Report
- [ ] Read the complete stack trace
- [ ] Identify the exact file and line of the error
- [ ] Read the code at that specific line
- [ ] Understand the state of variables at the time of the error
- [ ] DO NOT make assumptions about causes

### Requesting More Information
```
If the bug report has no error output:
"Paste the console output — raw data finds
the real problem faster."
```

---

## Example of Correct Flow

**Bug Report:**
```
TypeError: Cannot read property 'name' of undefined
    at UserProfile.render (UserProfile.tsx:42)
    at ReactDOM.render (react-dom.js:123)
```

❌ **WRONG:**
"This seems to be an issue with the UserProfile component.
I'll check the props..."

✅ **CORRECT:**
```
Analyzing error at UserProfile.tsx:42...

Reading line 42:
  return <div>{user.name}</div>;

Observation: 'user' is undefined at this point.

Checking where 'user' comes from...
[Investigation based on actual code]
```

---

## Anti-Patterns

| Anti-Pattern | Why it's bad | Solution |
|--------------|--------------|---------|
| "It seems to be..." | Assumption without data | Always check the exact code |
| "Probably..." | Theory without confirmation | Trace the error step by step |
| "Maybe it's X" | Guessing | Read the data, don't guess |
| Ignoring stack trace | Loses precious information | Use the line:column provided |
