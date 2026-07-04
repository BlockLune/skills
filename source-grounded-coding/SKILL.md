---
name: source-grounded-coding
description: Source-grounded coding. Use when implementation or advice depends on current repo behavior, dependency internals, external repo patterns, or disputed docs.
---

# Source-Grounded Coding

Code facts first. Use memory to form search hypotheses, then ground decisions in source evidence.

## Workflow

1. Frame the source question.
   - Identify the behavior, API, dependency, generated artifact, or external pattern that matters.
   - Decide which sources must be inspected before writing or advising.
   - Completion: the needed source set is named, and missing evidence is visible.

2. Pin the evidence.
   - Prefer the active workspace. For missing dependency or external source, read [`references/EXTERNAL_REPOS.md`](references/EXTERNAL_REPOS.md).
   - Record a source packet: path, repo/package, version/ref/commit, and why it is relevant.
   - Completion: important sources are local and versioned, or explicitly marked unavailable/approximate.

3. Trace the code path.
   - Read project instructions, metadata, entrypoints, relevant modules, tests, fixtures, and examples.
   - Follow definitions and call sites far enough to explain the behavior or choose the change.
   - If maps, docs, or public examples would unblock the trace, read [`references/MCP_SCOUTS.md`](references/MCP_SCOUTS.md).
   - Completion: each key claim is backed by `path:line`, `path:symbol`, or a named gap.

4. Apply local idioms.
   - Match observed patterns for imports, errors, config, tests, naming, and public API shape.
   - For reusable non-obvious patterns, read [`references/PATTERN_FILES.md`](references/PATTERN_FILES.md).
   - Completion: implementation choices follow source evidence; exceptions are labeled as inference or assumption.

5. Verify and report.
   - Run relevant existing checks when safe and available.
   - Cite only the evidence that explains the result; do not dump the whole trace.
   - Resolve conflicts with the Truth Ladder.
   - Completion: the user can trace the important behavior or design choice to source, or see the uncertainty.

## Truth Ladder

1. Current project source and tests.
2. Current lockfiles, config, schemas, generated types, and fixtures.
3. Exact-version dependency source.
4. Same-version docs, examples, and changelogs.
5. MCP, web docs, and public code examples.
6. Semantic memory.

Code decides behavior. Docs explain public contract when versions match. MCP and public examples are scouts. Reference repos such as `repos/` and `~/.explore/repos` are read-only unless the user asks otherwise.
