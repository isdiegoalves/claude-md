# Edit Integrity

> Technique: **ReAct** (Reasoning + Acting)

---

## ReAct Checklist (Copyable)

Use this checklist in each edit cycle:

```
[ ] STEP 1 - REASON: Why am I editing this file?
    → Identify the necessary change and the reason

[ ] STEP 2 - RE-READ: Read the file BEFORE editing
    → Confirm: line X, column Y, context Z is correct?
    → Answer: Yes/No - if No, re-evaluate

[ ] STEP 3 - ACT: Execute the edit with precise old_string
    → old_string must be EXACT (including spaces, line breaks)

[ ] STEP 4 - VERIFY: Read the file again AFTER editing
    → Confirm: was the change applied correctly?
    → Answer: Yes/No - if No, investigate silent failure

[ ] STEP 5 - DECISION: Next step
    → If 3+ edits to this file → RE-READ required before continuing
    → If fewer than 3 edits → can continue (but preferably verify)
```

---

## The 3-Edit Rule

**Never batch more than 3 edits without a verification read.**

| Edits | Required Action |
|-------|-----------------|
| 1st   | Re-read after editing (best practice) |
| 2nd   | Re-read after editing (best practice) |
| 3rd   | **MANDATORY RE-READ** before 4th edit |
| 4th+  | Re-read between EACH subsequent edit |

---

## How to Detect Silent Failures

The Edit tool **fails silently** when `old_string` doesn't match.

| Symptom | Likely Cause | Solution |
|---------|--------------|---------|
| File appears unchanged | `old_string` with wrong spaces | Re-read file, copy exact text |
| Edit reports success but nothing changed | Stale context | Re-read file from scratch |
| old_string "not found" | Different line breaks | Use editor to visualize whitespace |
| Partial change applied | `old_string` partially matches | Check for multiple occurrences |

---

## ReAct Application Example

**Scenario:** Rename function `handleClick` to `handleSubmit`

```
Thought: I need to rename handleClick in components/Button.tsx
         It will affect exports and props.

Action: Read file /project/components/Button.tsx

Observation:
- Line 15: export function handleClick() {
- Line 42: onClick={handleClick}
- Line 89: const handleClick = useCallback(...)

Thought: 3 occurrences. The last one is a local variable.
         I need to change the name of the exported function.

Action: Edit file with old_string="export function handleClick()"

Observation (after edit):
- Line 15: export function handleSubmit() {
- Line 42: onClick={handleClick}  // <- still references old name

Thought: Partial failure! The reference at line 42 was not updated.
          I need one more edit.

Action: Edit file with old_string="onClick={handleClick}"

Observation (after edit):
- Line 42: onClick={handleSubmit}

Thought: Complete verification. 2 edits made. < 3, can continue.
         But I'll do a verify read to be sure.

Action: Read file again to confirm both changes
```
