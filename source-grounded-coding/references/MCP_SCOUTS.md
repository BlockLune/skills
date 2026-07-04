# MCP Scouts

Use MCP as source-grounded support. MCP results do not outrank current source or exact-version dependency source.

## MCPs and use cases

- DeepWiki: public GitHub repository architecture, major subsystems, candidate files, and high-level repository Q&A. Verify answers in source before relying on them.
- Context7: library or framework docs, setup steps, API signatures, migration notes, and version-specific examples. Prefer exact library IDs and versions.
- gh_grep (grep.app): real-world code patterns across public GitHub. Search literal code patterns and treat results as external examples, not current-project facts.

## When unavailable

If the current environment does not expose the needed MCP, tell the user which MCP to install or configure:

- DeepWiki for repository architecture and Q&A.
- Context7 for library and framework docs.
- gh_grep (grep.app) for public code pattern search.

Do not invent MCP results. Continue from local source only when that is enough for the task.
