---
name: behavior-path
description: Trace one evidence-backed behavior path through a codebase, forward from a user action or business entry to an effect, or backward from a symbol to its trigger. Use when the user asks how behavior reaches code, what triggers a module, or how callbacks, indirect wiring, or async work connect.
disable-model-invocation: true
---

# Behavior Path

A **trace** is one scenario-specific, evidence-backed path. It explains a high-level behavior as connected code relationships, rather than reconstructing the repository's whole architecture.

## Trace contract

- Establish the direction, scenario, and available anchors first. Accept a natural-language behavior plus optional files, symbols, UI text, logs, or target effect.
- Trace execution and resolution relationships as the main path. Present inheritance, protocols, framework contracts, and registration as nearby black-box context when they explain a node.
- Give each node a stable abstraction level: what it receives, its responsibility in this scenario, and what it hands off or causes next. Descend into internals only when that establishes the next relationship.
- Let source evidence set the claim. A confirmed link, a viable candidate, and an unresolved gap are different results.
- Explore the selected scenario deeply. Mention alternative paths as bounded possibilities; expand one only when the user requests it.

## Steps

1. **Frame the trace.**
   - Infer `forward` for “what happens after X?” and `backward` for “what triggers X?”. Ask for the direction only when both remain plausible.
   - Identify the scenario, anchor, and desired end. For a forward trace, end at the requested observable effect or an external boundary. For a backward trace, end at the scenario's entry or boundary.
   - Completion: the trace has a direction, one scenario, and either a concrete anchor or a candidate-selection question.

2. **Locate the anchor.**
   - Read repository instructions and inspect the relevant entrypoints, metadata, configuration, tests, and source around each candidate.
   - Use the scenario, platform, and supplied anchor to select a candidate. When equally plausible candidates remain, present them briefly and wait for the user's choice.
   - Completion: the first node is tied to source evidence, or the user is choosing among equally plausible candidates.

3. **Walk the trace.**
   - At each hop, name the relationship, inspect the code that establishes it, and explain the current node as a black box before continuing.
   - For every non-direct hop—callback, event, route, service lookup, reflection, generated code, async scheduling, or process boundary—read [`references/EDGE_TYPES.md`](references/EDGE_TYPES.md) before selecting the next node.
   - Treat unresolved evidence as an explicit trace endpoint. State what is known, what would establish the connection, and the smallest useful verification.
   - Completion: the selected scenario reaches its endpoint or an explicit evidence gap, and every displayed hop has a named relationship and evidence strength.

4. **Report the trace.**
   - Answer in the user's language. Keep the main path continuous and readable; attach only the structural context needed to understand each node.
   - Include alternate paths as short, condition-bound leads. Use [`references/REPORTING.md`](references/REPORTING.md) when the trace includes alternatives, gaps, indirect dispatch, or a requested Markdown artifact.
   - Completion: a reader can distinguish the selected path, its evidence, its context, its alternatives, and its gaps without mistaking one for another.

## Interaction

Read facts from the repository instead of asking the user to supply them. Pause only for an ambiguous direction, equally plausible scenario candidates, a requested alternate path, or an evidence gap that requires a user decision. Keep tracing between those points.
