# One-Word Mode

> Technique: **Directional Stimulus Prompting**

---

## Immediate Execution Triggers

When the user says:
- "**yes**"
- "**do it**"
- "**push**"
- "**go**"
- "**proceed**"

→ **Execute immediately.**

---

## One-Word Mode Rules

### ✅ DO:
- Execute the requested action without repetition
- Don't repeat the plan
- Don't add unnecessary commentary
- The context is loaded, the message is the trigger

### ❌ DON'T:
- "You said 'yes', so I'll proceed with..."
- "As requested, I will execute..."
- "Understood. Starting now..."

---

## Examples

### Dialogue 1
```
User: "Want me to deploy?"
Agent: "Yes, say 'go' when you want to proceed."

User: "go"

Agent: [Executes deploy immediately, no additional text]
```

### Dialogue 2
```
Agent: "Phase 1 complete. Awaiting approval."

User: "yes"

Agent: [Starts Phase 2 immediately]
```

---

## Exceptions

Do NOT execute one-word if:
- There is ambiguity about what was approved
- The context has changed significantly since the proposal
- There are unaddressed destructive risks

In these cases, ask for specific confirmation.
