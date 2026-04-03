# CLAUDE.md

Production-grade agent directives for Claude Code. Reverse-engineered
from the source, refined against billions of tokens of real agent logs,
and incorporating patterns from Anthropic's own engineering team.

## What This Is

Claude Code has structural bottlenecks that cause predictable failures:
context compaction destroys working memory mid-refactor, file reads
silently truncate at 2,000 lines, tool results get cut to 2,000-byte
previews, the default system prompt biases toward minimal output over
correct output, and the agent has no built-in verification loop between
editing code and reporting success.

This CLAUDE.md overrides all of it using a **three-level Progressive
Disclosure** architecture — the agent only loads the context it needs,
exactly when it needs it.

## Structure

```
CLAUDE.md                        ← always loaded (~53 lines, always-active rules)
  └── .claude/[category].md      ← loaded on demand (one per task type)
        └── reference/[TOPIC]/   ← deep reference, read only when needed
```

**Level 1 — `CLAUDE.md`** holds always-active rules and a load-on-demand
table. The agent reads this at session start. ~53 lines total.

**Level 2 — `.claude/[category].md`** — nine category files, each ~30
lines. The agent reads only the one(s) relevant to the current task
(pre-work, code quality, context management, etc.).

**Level 3 — `reference/[CATEGORY]/[topic].md`** — granular rules the
agent reads only when it needs full detail on a specific behavior. Each
category file ends with `> Deep reference: reference/CATEGORY/`.

## Install

**Minimal** — always-active rules only, no on-demand loading:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/iamfakeguru/claude-md/main/CLAUDE.md
```

**Full** — all three Progressive Disclosure levels:

```bash
git clone https://github.com/iamfakeguru/claude-md.git
cp claude-md/CLAUDE.md /path/to/your/project/
cp -r claude-md/.claude /path/to/your/project/
cp -r claude-md/reference /path/to/your/project/
```

Claude Code reads CLAUDE.md from the project root automatically.

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
| Agent builds before understanding | No plan/build separation by default | Spec-Based Development |
| Same mistakes every session | No cross-session learning | Self-Improvement Loop |
| Context lost between sessions | Starting fresh every time | Session Continuity |
| Agent asks for hand-holding on bugs | Default passivity | Autonomous Bug Fixing |

## Going Further

The nine load-on-demand category files cover the general case. Each links
to a `reference/` subfolder for rules the agent reads on demand:

| `.claude/` file | Covers | Deep reference |
|---|---|---|
| `pre-work.md` | Delete-first, spec-based development | `reference/PREWORK/` |
| `understanding-intent.md` | References, raw data, one-word triggers | `reference/INTENT/` |
| `code-quality.md` | Senior override, style, elegance | `reference/QUALITY/` |
| `context-management.md` | Sub-agents, decay, compaction | `reference/CONTEXT/` |
| `filesystem.md` | File system as state | `reference/FILESYSTEM/` |
| `edit-safety.md` | Edit integrity, semantic search, one source of truth | `reference/SAFETY/` |
| `cache-awareness.md` | Prompt cache, session management | `reference/CACHE/` |
| `self-improvement.md` | Mistake logging, bug autopsy, failure recovery | `reference/SELF-EVAL/` |
| `housekeeping.md` | Guardrails, batch changes, file hygiene | `reference/MAINTENANCE/` |

For per-filetype rules (test files, migrations, etc.), Claude Code supports
`.claude/rules/*.md` with YAML frontmatter — separate from the on-demand
category files above:

```markdown
# .claude/rules/tests.md
---
paths:
  - "**/*.test.ts"
  - "**/*.spec.ts"
---
When modifying test files:
- Do not modify production code from this context.
- Use AskUserQuestion if the mocked data schema is unclear.
- Run the specific test file after changes, not the full suite.
```

You can also set up hooks in `~/.claude/settings.json` to auto-format
or block dangerous commands:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "hooks": [
          {
            "type": "command",
            "command": "python -m black \"$file\""
          }
        ]
      }
    ]
  }
}
```

For the full configuration system (permissions, hooks, custom slash
commands, MCP servers), see the
[Anthropic docs](https://docs.anthropic.com/en/docs/claude-code/overview).

## Works With

- **Claude Code** - reads CLAUDE.md natively
- **Cursor** - paste into `.cursorrules`
- **Other agents** - paste into whatever rules/system prompt file your
  tool uses

## Context

Built by [@fakeguru](https://x.com/iamfakeguru). AI agent
infrastructure. Advisor [@OpenServAI](https://x.com/openservai).

## License

MIT.
