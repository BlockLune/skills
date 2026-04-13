---
name: codebase-to-tutorial
description: Transform an existing codebase into a guided tutorial for learning and clean-room reimplementation from first principles. Use when the user wants to study a repository deeply, turn a codebase into lessons, create a reimplementation tutorial, or generate tutorial files from an existing project, especially when the lessons should be stored in Obsidian via the obsidian-cli workflow.
---

# Codebase To Tutorial

Use this skill when the user wants to learn a real codebase by rebuilding it from the ground up.

## Workflow

1. Explore the target codebase before proposing lesson structure.

2. If the DeepWiki MCP server is available and the codebase is in a GitHub repository, use it early to learn the project structure, architecture, and major subsystems. Treat DeepWiki as a supplement to direct code reading, not a replacement.

3. Read the local codebase directly. Identify:
- the product goal
- the main runtime entrypoints
- the core architectural layers
- the highest-value modules to reimplement in sequence
- the likely difficulty level for a learner

4. Ask the user how many lessons they want. Do not skip this. Give a concrete recommendation based on the exploration, for example:
- 5-12 lessons for a compact architecture or narrow subsystem
- 12-24 lessons for a medium-sized app or library
- 24+ lessons for a large or highly layered codebase

5. Ask the user how to map the generated lessons into their Obsidian workflow. Default to storing the lessons in an Obsidian vault via the `obsidian-cli` skill. If the user does not want Obsidian, fall back to `tutorials/` under the target codebase root.

6. After the user confirms lesson count and storage location, create an outline that matches that lesson count exactly. The outline should move from fundamentals to architecture to implementation details, ending with integration and reimplementation guidance.

7. Present the outline for confirmation or adjustment before writing all lesson files.

8. Write the tutorial files step by step. Each lesson should be self-contained but build on the previous ones.

9. Add YAML front matter to every generated Markdown file. Include the `aigc` tag in front matter for all files. Use `tags: [aigc]` unless the target workflow requires another equivalent YAML list form.

## Lesson design rules

Each lesson should help the learner both understand and rebuild the system. For each lesson, include:
- what part of the codebase is being studied
- why this part exists
- the key concepts and abstractions
- a suggested reimplementation plan from scratch
- checkpoints or exercises
- links or references to the relevant source files or modules

Prefer practical explanations over exhaustive paraphrase. The learner should come away knowing what to build next and why.

## Output structure

Unless the user requests a different format, generate Markdown files with YAML front matter that includes `tags: [aigc]`.

Default storage mode:
- use the `obsidian-cli` skill and create the curriculum inside the user's Obsidian vault
- ask for the vault and destination folder only when they are not already known from context

Unless the user requests a different format, generate:
- `00-overview.md` with the full curriculum
- one file per lesson, ordered with zero-padded numbers such as `01-intro.md`, `02-runtime.md`
- an optional final file for recap, exercises, or next steps

## Quality bar

- Do not invent architecture that is not supported by the codebase.
- Keep the lesson order teachable; avoid jumping into low-level details too early.
- Call out uncertainty when the codebase is ambiguous.
- Optimize for learning and reimplementation, not for line-by-line code commentary.
