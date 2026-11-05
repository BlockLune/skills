---
name: git-commit
description: Commit changes using user's preferred conventions.
---

Review the current changes and create atomic, cherry-pickable Conventional Commits.

Rules:

- Commit only files related to the current task.
- Write the title and description in English unless the user asks for another language.
- Keep the title concise and imperative, and include a description body.
- State the problem context and user-visible impact first, then the solution; explain why the change was made rather than restating the code diff.
- Omit self-referential phrases (such as "This commit fixes...") and compliance declarations.
- Run relevant checks before committing, and push only when explicitly asked.

Tools:

Probe each with `command -v <tool>`. Read its reference before the first use; when the tool is missing, take the install line from that reference, report it once, and continue without the tool.

| Tool | Use it for | Reference |
| --- | --- | --- |
| `git-hunk` | splitting one file's changes across commits | [git-hunk.md](references/git-hunk.md) |
| `difft` | reading the diff before writing the description | [difft.md](references/difft.md) |
| `gitleaks` | blocking secrets before the commit exists | [gitleaks.md](references/gitleaks.md) |
