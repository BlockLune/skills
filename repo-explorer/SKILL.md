---
name: repo-explorer
description: Explore external repositories using a reusable local clone cache. Use when answering questions about or comparing repositories outside the current workspace.
allowed-tools: Bash(mkdir -p ~/.explore/repos) Bash(ls -la ~/.explore/repos) Bash(git clone *) Bash(rg *)
---

Keep exploration clones in `~/.explore/repos`, outside the active workspace.

## Select the repository and revision

Inspect the cache before cloning. Use stable names such as `owner__repo`; include the host or namespace when needed to avoid collisions. Verify an existing clone's remote URL before reusing it.

Use the user's requested branch, tag, or commit. Otherwise, use the remote's default branch rather than assuming `master`, `main`, or the cached checkout's current branch.

## Acquire or refresh

For source-only exploration, start with a shallow, single-branch clone:

```bash
mkdir -p ~/.explore/repos
git clone --depth 1 --single-branch <repo-url> ~/.explore/repos/<owner>__<repo>
```

Add `--branch <branch-or-tag>` when specified. For an exact commit, fetch and check out that commit explicitly; verify the resolved revision before searching.

For an existing cache, check its working tree and fetch the target ref once at the start of the task, unless the user requests an offline or cached snapshot. Explore the fetched commit, preferably in a detached checkout, rather than merging remote changes into a local branch. Reuse that snapshot for subsequent searches in the same task.

Preserve local changes and existing branch history. If switching revisions would disturb ongoing work, use a separate worktree or clone; do not reset, clean, or stash someone else's work. If fetching fails, disclose that freshness is unverified before relying on the cached snapshot.

Fetch additional refs explicitly when needed: single-branch clones do not track every remote branch. Deepen or unshallow only when history analysis requires it; shallow history cannot establish that older changes do not exist.

## Explore and report

Read the repository's local instructions and project metadata, then use `rg`, `rg --files`, and targeted file reads. These search the checked-out snapshot, not every branch or the full Git history. Account for ignored or hidden files when relevant to the question.

Ground findings in file paths and line numbers. Identify the inspected ref and commit, and note any stale-cache or shallow-history limitation that affects the answer.
