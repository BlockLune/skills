---
name: no-comments
description: Audit comments in scope, delete redundant or historical ones, and encode constraints into types or tests.
disable-model-invocation: true
---

# No comments

Audit every comment and lint/type suppression in the named files or current diff against `main`. Make the code express its own meaning, encode checkable constraints, and keep only verified external rationale.

## Classification and actions

- DELETE: restates what the code literally does; narrates modification history ("previously X, now Y", "原来用 X，现改为 Y"); commented-out code; chat residue; crutch comments excusing unclear names or tangled control flow; unproved lint or type suppressions.
  Action: remove the comment. When a crutch comment explains a confusing name or condition in code we own, rename the symbol or simplify the logic within scope first.
- ENCODE: states an internal constraint ("do not delete", "keep in sync with Y", "must call before X") that a type, assertion, unit test, or lint rule can enforce.
  Action: encode the constraint and delete the comment; if encoding is non-trivial or out of scope, propose the simplest approach and ask for approval.
- KEEP: states a non-obvious why or external constraint the code cannot express on its own (protocol/OS/hardware quirk, third-party bug workaround, performance trap, public contract), verified against the current code.
  Action: keep and trim to the current rationale only.

Report the deleted count, kept comments (with one-line reason why code cannot express each), code simplifications made, and constraints encoded or awaiting approval.
