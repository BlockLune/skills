# difftastic

Structural diff: compares syntax trees, so moved or reindented code reads as unchanged instead of a delete plus an add. Use it to see the shape of a change before writing the commit description.

Install: `brew install difftastic`. The binary is `difft`.

## Reading a change

git reaches it through `GIT_EXTERNAL_DIFF`:

```shell
DFT_DISPLAY=inline DFT_COLOR=never DFT_WIDTH=100 GIT_EXTERNAL_DIFF=difft git diff
DFT_DISPLAY=inline DFT_COLOR=never DFT_WIDTH=100 GIT_EXTERNAL_DIFF=difft git diff --staged
```

Each file is labelled `path --- 1/2 --- <language>`, with the old and new line numbers in one column.

## Settings through `DFT_*`, not flags

`GIT_EXTERNAL_DIFF` hands the program a file pair and no flags, so every option travels as an environment variable. Assign them per command rather than `export`:

- `DFT_DISPLAY=inline` — one column. The default `side-by-side` splits each line across two columns and wraps badly at narrow widths.
- `DFT_COLOR=never` — no ANSI escapes.
- `DFT_WIDTH=100` — fixes wrapping. Without a TTY there is no terminal width to detect.
- `DFT_CONTEXT=<lines>` — widen context when the description needs the surrounding structure.

`DFT_DISPLAY=json` needs `DFT_UNSTABLE=yes` and emits token-level highlight spans; the inline text is easier to read.

## Gotchas

- Language detection can miss: the output then falls back to a byte diff, correctly but without structural alignment. `difft --list-languages` shows what is supported.
- An exported `GIT_EXTERNAL_DIFF` reaches every `git diff` in the shell. `git-hunk scan` and `gitleaks` both pass `--no-ext-diff`, so they ignore it, but per-command assignment keeps the blast radius at one call.
- `difft --check-only` answers "did anything change" faster than rendering the diff; use it in loops, not before writing a description.
