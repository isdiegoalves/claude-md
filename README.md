# CLAUDE.md

Production-grade agent directives for Claude Code. Reverse-engineered from the source and refined against real agent failures.

## What This Is

Claude Code has predictable failure modes: context compaction destroys working memory mid-refactor, file reads silently truncate at 2,000 lines, tool results get cut to 2,000-byte previews, and the default system prompt biases toward minimal output over correct output.

This CLAUDE.md overrides all of it.

Full technical breakdown: [x.com/iamfakeguru/status/2038965567269249484](https://x.com/iamfakeguru/status/2038965567269249484)

---

## Quick Install

Drop the complete directives file into your project root:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/iamfakeguru/claude-md/main/CLAUDE.md
```

Claude Code reads `CLAUDE.md` from the project root automatically. Nothing else required.

---

## What It Fixes

| Problem | Root Cause | Directive |
|---|---|---|
| "Done!" with 40 type errors | Success = bytes on disk, no compile check | Forced Verification |
| Hallucinations after ~15 messages | Auto-compaction nukes context at ~167K tokens | Step 0 + Phased Execution |
| Band-aid fixes instead of real solutions | System prompt mandates minimal intervention | Senior Dev Override |
| Context decay on large refactors | Single agent = single 167K context window | Sub-Agent Swarming |
| Edits reference code it never saw | File reads capped at 2,000 lines | File Read Budget |
| Grep finds 3 results, there are 47 | Tool results truncated to 2,000-byte preview | Tool Result Blindness |
| Rename misses dynamic imports | Grep is text matching, not an AST | No Semantic Search |

---

## Modular Structure

Each directive is also available as a standalone file. Use these when you want to add specific guardrails to an existing `CLAUDE.md` without adopting the full set.

```
claude-md/
├── CLAUDE.md               ← Full directives (start here)
│
└── reference/              ← Standalone files per directive
    ├── PREWORK/            ← Before touching any code
    │   ├── delete-before-build.md
    │   ├── phased-execution.md
    │   └── planning.md
    │
    ├── INTENT/             ← Reading what the user actually wants
    │   ├── references.md
    │   ├── raw-data.md
    │   └── oneword.md
    │
    ├── QUALITY/            ← Code correctness and style
    │   ├── verification.md
    │   ├── architecture.md
    │   └── code-style.md
    │
    ├── CONTEXT/            ← Managing the context window
    │   ├── subagents.md
    │   └── file-reading.md
    │
    ├── SAFETY/             ← Edit safety and destructive actions
    │   ├── editing-workflow.md
    │   └── checklist.md
    │
    ├── SELF-EVAL/          ← Agent self-evaluation
    │   └── two-perspectives.md
    │
    └── MAINTENANCE/        ← Ongoing project hygiene
        ├── guardrails.md
        └── batch-changes.md
```

<details>
<summary><strong>PREWORK — Before touching any code</strong></summary>

**`delete-before-build.md`** — Step 0: Delete Before You Build  
Before any structural refactor on a file >300 LOC, remove dead props, unused exports, unused imports, and debug logs. Commit the cleanup separately. No ghosts in the project.

**`phased-execution.md`** — Phased Execution  
Never attempt multi-file refactors in a single response. Break work into explicit phases. Complete Phase 1, run verification, wait for explicit approval before Phase 2. Each phase touches no more than 5 files.

**`planning.md`** — Plan and Build Are Separate Steps  
When asked to "make a plan," output only the plan. No code until the user says go. If instructions are vague, outline what you'd build and where it goes — get approval first.

</details>

<details>
<summary><strong>INTENT — Reading what the user actually wants</strong></summary>

**`references.md`** — Follow References, Not Descriptions  
When the user points to existing code as a reference, study it before building. Match its patterns exactly. Working code is a better spec than English.

**`raw-data.md`** — Work From Raw Data  
When the user pastes error logs, work from that data. Don't guess, don't chase theories — trace the actual error.

**`oneword.md`** — One-Word Mode  
When the user says "yes," "do it," or "push" — execute. Don't repeat the plan. Don't add commentary. The trigger is the message.

</details>

<details>
<summary><strong>QUALITY — Code correctness and style</strong></summary>

**`verification.md`** — Forced Verification  
Forbidden from reporting a task as complete without running `npx tsc --noEmit` and `npx eslint . --quiet`. Fix ALL resulting errors. If no type-checker is configured, state that explicitly — never claim success with errors outstanding.

**`architecture.md`** — Senior Dev Override  
If architecture is flawed, state is duplicated, or patterns are inconsistent — propose and implement structural fixes. Ask: "What would a senior, perfectionist dev reject in code review?" Fix all of it.

**`code-style.md`** — Write Human Code / Don't Over-Engineer  
Write code that reads like a human wrote it. No robotic comment blocks, no section headers, no descriptions of obvious things. Don't build for imaginary scenarios — simple and correct beats elaborate and speculative.

</details>

<details>
<summary><strong>CONTEXT — Managing the context window</strong></summary>

**`subagents.md`** — Sub-Agent Swarming  
For tasks touching >5 independent files, launch parallel sub-agents (5-8 files per agent). Each agent gets its own ~167K context window. One agent processing 20 files sequentially guarantees context decay.

**`file-reading.md`** — File Read Budget + Context Decay Awareness  
File reads capped at 2,000 lines — use offset/limit for larger files. After 10+ messages, re-read any file before editing it. Auto-compaction may have silently destroyed that context.

</details>

<details>
<summary><strong>SAFETY — Edit safety and destructive actions</strong></summary>

**`editing-workflow.md`** — Edit Integrity + No Semantic Search  
Re-read every file before editing. After editing, read again to confirm. When renaming anything, search separately for: direct calls, type-level references, string literals, dynamic imports, re-exports, test files.

**`checklist.md`** — One Source of Truth + Destructive Action Safety  
Never fix a display problem by duplicating state. Never delete a file without verifying nothing references it. Never push to a shared repository unless explicitly told to.

</details>

<details>
<summary><strong>SELF-EVAL — Agent self-evaluation</strong></summary>

**`two-perspectives.md`** — Two-Perspective Review  
When evaluating your own work, present two opposing views: what a perfectionist would criticize and what a pragmatist would accept. Let the user decide the tradeoff.

Also covered in `CLAUDE.md`: Verify Before Reporting, Bug Autopsy, Failure Recovery, Fresh Eyes Pass.

</details>

<details>
<summary><strong>MAINTENANCE — Ongoing project hygiene</strong></summary>

**`guardrails.md`** — Proactive Guardrails  
Offer to checkpoint before risky changes. Flag files getting unwieldy. Offer basic validation once if the project has none.

**`batch-changes.md`** — Parallel Batch Changes  
When the same edit needs to happen across many files, suggest parallel batches. Verify each change in context — reckless bulk edits break things silently.

</details>

---

## Works With

- **Claude Code** — reads `CLAUDE.md` natively
- **Cursor** — paste into `.cursorrules`
- **Other agents** — paste into whatever rules/system prompt file your tool uses

---

## Context

Built by [@fakeguru](https://x.com/fakeguru). Strategic growth at [@OpenServAI](https://x.com/openservai).

## License

MIT.
