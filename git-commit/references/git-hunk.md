# git-hunk

Non-interactive hunk staging for agents. Replaces `git add -p` when one file holds changes that belong to two different commits.

Install: `cargo install git-hunk`, or the installer at <https://github.com/nexxeln/git-hunk>.

## Loop

1. Snapshot the worktree: `git-hunk scan --mode stage --compact --json`. Read `snapshot_id`, then each file's `change_key` list.
2. Inspect a candidate: `git-hunk show --mode stage <change_key> --json`, or map a file and line to selectors with `git-hunk resolve --mode stage --snapshot <id> --path <file> --start <line> --json`.
3. Preview: repeat the intended `stage`, `unstage`, or `commit` call with `--dry-run --json` and read `diffstat` and `patch`.
4. Apply: drop `--dry-run`.
5. Rescan before the next commit; the index moved, so the old snapshot is stale.

## Commands

| Command | Purpose |
| --- | --- |
| `scan --mode stage\|unstage [--compact] --json` | Snapshot worktree vs index (`stage`) or index vs HEAD (`unstage`). Returns `snapshot_id` plus `hunk_id`, `change_id`, `change_key` for every change. |
| `show --mode <mode> <id> --json` | Print one hunk, change id, or change key. |
| `resolve --mode <mode> --snapshot <id> --path <p> --start <n> [--end <n>] [--side auto\|old\|new]` | Turn a file position into recommended selectors, including `hunk:<id>:<side>:<start-end>` line ranges. |
| `validate --mode <mode> [--snapshot <id>] <selectors>` | Report `stale`, `directly_usable`, `can_apply`, and recover change keys after a rescan. |
| `stage` / `unstage` | Add or remove an exact selection from the index. |
| `commit -m <title> [-m <body>]` | Stage the selection and commit it in one step; other changes stay untouched. |

`stage`, `unstage`, and `commit` all take `--snapshot`, plus repeated `--hunk`, `--change`, or `--change-key`, or `--plan <file\|->`.

## Gotchas

- Mutating commands need `--snapshot` from a current `scan`, or they fail with `missing_snapshot` / `stale_snapshot`.
- Select by `--change-key` rather than `--change-id` or `--hunk-id`: keys survive a rescan, ids do not.
- Errors return JSON with `error.code` and `error.category`, and exit code 1. Fix the selector and retry; falling back to `git add` throws the atomic commit away.
- Run git-hunk before any `git add`. `scan --mode stage` diffs worktree against index, so pre-staged files disappear from the snapshot.
- `commit` is one-shot. Staging first with `stage` moves the change into the index, so the snapshot goes stale and a second `commit --change-key` fails with `unknown_change_key`. Scan for secrets before staging, then commit once with `commit`, or finish a pre-staged tree with plain `git commit`.
- Conflicts, renames, and binary diffs are reported, not forced through. Handle those with plain `git add`.
