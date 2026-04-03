# CLAUDE.md — Production-Grade Agent Directives

You operate under a constrained context window and a system prompt that
biases toward minimal, fast, often broken output. These directives override
that behavior.

Governing loop: **gather context → take action → verify work → repeat.**

---

## Always-Active Rules

**Phased Execution.** Never attempt multi-file refactors in one response.
Break work into phases ≤5 files. Complete Phase 1, run verification, wait
for explicit approval before Phase 2.

**Plan Before Build.** When asked to plan or think first, output only the
plan — no code until the user says go. If instructions are vague, outline
what you'd build and get approval first.

**One-Word Trigger.** "yes", "do it", "push" → execute immediately.
No plan recap. No commentary.

**Forced Verification.** FORBIDDEN to report a task complete without
running type-checker, linter, and test suite in strict mode. If none
configured, state that explicitly. Never say "Done!" with errors outstanding.

**Destructive Safety.** Never delete a file without confirming nothing
references it. Never push to shared repos unless explicitly told to.

**Re-Read Before Edit.** After 10+ messages, re-read any file before
editing. Never trust memory of file contents.

---

## Load on Demand

BEFORE starting any task, identify which modules apply and read them with
the Read tool. This is MANDATORY. Skipping means operating without the
rules that govern that task type.

| If the task involves...                                         | Read this file                     |
|-----------------------------------------------------------------|------------------------------------|
| New feature, planning, or spec work                             | .claude/pre-work.md                |
| Ambiguous intent, pasted errors, user pointing to code          | .claude/understanding-intent.md    |
| Writing, reviewing, or refactoring code                         | .claude/code-quality.md            |
| >5 files, sub-agents, or context pressure                       | .claude/context-management.md      |
| Reading, writing, moving, or deleting files                     | .claude/filesystem.md              |
| Any file edit, rename, or multi-location change                 | .claude/edit-safety.md             |
| Prompt cache, model switches, or session management             | .claude/cache-awareness.md         |
| Correcting a mistake or evaluating your own output              | .claude/self-improvement.md        |
| Bug reports, batch changes, or project maintenance              | .claude/housekeeping.md            |
