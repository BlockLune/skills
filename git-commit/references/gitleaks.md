# gitleaks

Secret scanner. Run it before the commit exists, so a leaked key never enters history.

Install: `brew install gitleaks`. Without brew: `go install github.com/zricethezav/gitleaks/v8@latest` (the module path still carries the original personal namespace).

## Choosing the scan mode

| Situation | Command |
| --- | --- |
| Work not staged yet, the normal case | `gitleaks git --pre-commit --redact --no-banner` |
| Index already holds part of the work | `gitleaks git --staged --redact --no-banner` |
| New file, still untracked | `gitleaks dir <path> --redact --no-banner` |
| A commit already made | `gitleaks git --log-opts="-1"` |

`git --pre-commit` runs `git diff -U0 --no-ext-diff .`; `git --staged` adds `--staged`. Neither sees untracked files, which is why the third row exists.

## Reading the result

Exit code 1 means a finding, and a scan error also exits 1. Findings print as `RuleID  file:line:secret`.

On a finding: stop, report file, line, and rule, fix the leak, then rescan. Do not commit and clean up afterwards; rewriting history costs more than rerunning the scan.

Keep `--exit-code` at its default 1. A scan that cannot fail is not a gate.

`--redact` (bare, which means 100%) masks the secret in the output itself, so a finding can be quoted back to a human without re-leaking it.

## Gotchas

- `detect` and `protect` are deprecated since v8.19. Use `git`, `dir`, or `stdin`.
- Both git modes pass `--no-ext-diff`, so a `GIT_EXTERNAL_DIFF` set for difftastic does not distort the scan.
- A false positive goes into `.gitleaksignore`, matched by the finding's `Fingerprint` field. Read the fingerprints with `--report-format json --report-path <file>` and copy the one that fires.
- The default rule set is broad and `--config` points at a custom `gitleaks.toml`; a repo with a local config should be scanned with that config rather than the default.
