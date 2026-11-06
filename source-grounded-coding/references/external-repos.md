# External Repositories

Use this when required source is not already in the active workspace.

## Choose location

- Active workspace: use when the source already exists there.
- `repos/<name>`: use for long-lived dependency source the project will revisit. Ask before adding it.
- `~/.explore/repos/<owner>__<repo>`: use for one-off exploration outside the workspace.
- Web or MCP: use only as a scout when source cannot be fetched or must first be located.

Completion: the chosen location and its reason are clear.

## Source packet

Before relying on an external checkout, record:

- local path
- remote URL
- branch/tag/ref and commit
- project dependency version or lockfile evidence, if relevant
- whether the match is exact or approximate

Completion: external facts can be traced to a specific checkout.

## Exploration cache

Cache root: `~/.explore/repos`.

```bash
mkdir -p ~/.explore/repos
ls -la ~/.explore/repos
```

Use `owner__repo` as the directory name. If the repo is already cached, inspect it before trusting it:

```bash
git -C ~/.explore/repos/<owner>__<repo> remote -v
git -C ~/.explore/repos/<owner>__<repo> rev-parse HEAD
git -C ~/.explore/repos/<owner>__<repo> branch --show-current
git -C ~/.explore/repos/<owner>__<repo> tag --points-at HEAD
```

If absent, clone to an explicit destination:

```bash
git clone <repo-url> ~/.explore/repos/<owner>__<repo>
```

If a branch, tag, or commit matters, check it out explicitly before using it as evidence.

## Match dependency versions

Read project dependency evidence first: lockfiles, package manifests, module files, build config, vendored metadata, or generated manifests.

Use exact-version source when possible. If no exact match is found, use the closest source only as approximate evidence and say so.

## Long-lived vendored source

For important dependencies, recommend a project-local subtree:

```bash
git subtree add --prefix=repos/<name> <repo-url> <ref> --squash
git subtree pull --prefix=repos/<name> <repo-url> <ref> --squash
```

Do not run subtree commands without user approval. If added, document that `repos/` is read-only reference and application code should keep importing normal package dependencies.
