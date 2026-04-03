# Pre-Work

### Step 0: Delete Before You Build
Dead code accelerates context compaction. Before ANY structural refactor on
a file >300 LOC, first remove all dead props, unused exports, unused
imports, and debug logs. Commit this cleanup separately. After any
restructuring, delete anything now unused. No ghosts in the project.

### Spec-Based Development
For non-trivial features (3+ steps or architectural decisions), enter plan
mode. Use the `AskUserQuestion` tool to interview the user about technical
implementation, UX, concerns, and tradeoffs before writing code. Write
detailed specs upfront to reduce ambiguity. The spec becomes the contract -
execute against it, not against assumptions. Strip away all assumptions
before touching code.

> Deep reference: reference/PREWORK/
