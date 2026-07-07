---
name: codebase-trick-hunt
description: Hunt a codebase for language-specific, non-obvious coding tricks and report them as concise tips.
disable-model-invocation: true
---

# Codebase Trick Hunt

Hunt for compact, language-specific tricks in the current codebase and report them as reusable tips.

## Trick

A trick is a small language, standard-library, framework, or type-system move that an experienced developer may know but a newcomer may miss. It must be specific enough to change code, not a general principle.

Good tricks include:

- A built-in API that replaces hand-written control flow.
- A type-system expression that extracts or constrains useful information.
- A language idiom that makes a local pattern shorter, safer, or clearer.
- A common library helper already available in the project.

Reject generic advice, style preferences, architecture opinions, and tips that do not depend on the language or project stack.

## Workflow

1. Map the stack.
   - Inspect project metadata, extensions, lockfiles, and representative source files.
   - Identify the main languages and major libraries worth hunting in.
   - Completion: every searched language or stack surface is named.

2. Mine candidates.
   - Search for loops, filtering, grouping, indexing, object/key manipulation, error handling, option/result handling, async patterns, type definitions, and repeated helper code.
   - For each language, look for both tricks already used and nearby code that could use a known built-in or idiom.
   - Completion: each main language has been checked for candidate patterns, or explicitly marked as skipped with a reason.

3. Verify the trick.
   - Confirm the API, syntax, or idiom is available in this codebase's language version or dependencies.
   - Prefer project source, config, lockfiles, and dependency docs over memory.
   - Completion: every retained trick has evidence from code, config, or exact dependency/version knowledge; uncertain tricks are dropped or labeled.

4. Compress into tips.
   - Write each trick as a short `tip` first. If it cannot fit as one sentence, add a tiny example.
   - Keep the tip actionable: name the language or library, the move, and when to use it.
   - Completion: every retained trick is expressed as a reusable tip, not a long explanation.

5. Report the list.
   - Group tips by language or stack area.
   - Include a file reference when the trick was found in or suggested by local code.
   - If no good tricks are found, report the searched surfaces and the strongest near-misses.
   - Completion: the user receives a concise list of tips with enough context to apply them.

## Tip Format

Prefer this shape:

```md
- tip: In <language/library>, use <move> when <situation> instead of <common beginner approach>. (`path/to/file.ext`)
```

Use a small example only when the tip would otherwise be ambiguous:

````md
- tip: In TypeScript, use `keyof typeof obj` to derive a union of an object's keys instead of duplicating string literals.

  ```ts
  const routes = { home: '/', settings: '/settings' } as const;
  type RouteName = keyof typeof routes; // 'home' | 'settings'
  ```
````

## Quality Bar

- Prefer five strong tips over twenty generic ones.
- A trick must be locally relevant: present in the codebase, enabled by its stack, or a clear replacement for nearby code.
- Do not present risky cleverness as a trick unless the trade-off is named.
- Do not rewrite the code unless the user asks; this skill produces tips.
