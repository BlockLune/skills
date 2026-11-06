# Pattern Files

Use a pattern file when a source-grounded pattern is likely to be reused.

## Create or update when

- The same dependency, module, API, or architecture pattern will likely recur.
- The pattern required multi-file tracing and would be costly to rediscover.
- Future agents need a compact project-local reference.

Do not create one for a one-off implementation detail.

Completion: the pattern is reusable enough to justify a project artifact.

## Location and shape

Use `agent-patterns/<topic>.md`.

```markdown
# <Pattern Name>

Source packet:
- repo/package:
- version/ref/commit:
- inspected files:

## When to use

## Idioms to follow

## Example

## Avoid

## Open questions
```

Rules:

- Prefer `path:line` or `path:symbol` over broad prose.
- Keep examples short and license-safe; adapt instead of copying when unsure.
- Update an existing pattern file instead of creating a duplicate.
- Keep it practical, not exhaustive.

Completion: future agents can apply the pattern without repeating the original trace, while still seeing the source packet behind it.
