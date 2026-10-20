---
name: git-commit
description: Commit changes using user's preferred conventions.
disable-model-invocation: true
---

Review the current changes and create atomic, cherry-pickable Conventional Commits.

Rules:

- Commit only files related to the current task.
- Keep the title concise and imperative, and include a description body.
- State the problem context and user-visible impact first, then the solution; explain why the change was made rather than restating the code diff.
- Omit self-referential phrases (such as "This commit fixes...") and compliance declarations.
- Run relevant checks before committing, and push only when explicitly asked.
