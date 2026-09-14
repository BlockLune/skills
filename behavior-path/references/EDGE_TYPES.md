# Edge Types

Use the smallest bridge that makes adjacent nodes intelligibly connected. The trace remains scenario-specific: an edge explains why this behavior reaches the next node, not every relationship in the repository.

## Direct execution

A call, constructor invocation, or language-native dispatch can connect caller and callee directly. Read both ends when needed to establish the current contract and next handoff.

## Registered dispatch

Routes, UI actions, command maps, event subscribers, plugin registries, and dispatch tables connect a trigger to selected code through a key or registration.

Show the trigger, the key or selection rule, and the registered target when source establishes them. Keep registration as startup or framework context when it is not executed by the scenario itself.

## Resolution

For service location, dependency injection, reflection, or protocol/interface dispatch, follow the smallest available resolution bridge:

```text
requesting site → key or contract → binding/configuration → selected implementation
```

A static binding can confirm an implementation. A runtime-dependent binding remains a candidate until configuration, generated output, or observation selects it. If selection stays unavailable, end at a gap and name the configuration or observation that would resolve it.

## Callback and event delivery

Connect registration/subscription to invocation through the event, selector, route, or callback slot that binds them. Explain whether delivery is synchronous, queued, or framework-controlled when that changes the scenario.

## Async and cross-boundary work

Represent async work as a boundary with its own contract:

```text
schedule or publish → transport/queue/task context → resume or consume
```

Show the scheduler, message, task, or correlation mechanism that connects the two sides. A process, network, database, or platform API is a useful terminal boundary unless the user asks to trace further.

## Generated and reflective code

Inspect generated source, schemas, build configuration, metadata, or naming conventions that select the target. When those artifacts establish only a set of possible targets, report the set as candidates and retain the unresolved selection condition.

## Structural context

Inheritance, protocol conformance, imports, directory ownership, and base classes explain a node's available contract or lifecycle. Present them beside the relevant node; they become a trace hop only when source shows an actual dispatch or resolution through them.

## Evidence language

Match certainty to evidence rather than imposing a fixed citation format:

- **Confirmed**: source, configuration, generated output, or runtime observation establishes this relationship for the scenario.
- **Candidate**: source narrows the relationship but a runtime condition or missing artifact still chooses the target.
- **Gap**: available evidence cannot establish the relationship.

Use paths, symbols, and line locations at the granularity that lets the reader reproduce an important claim. Give alternatives a condition such as platform, feature flag, registration, message type, or runtime state.
