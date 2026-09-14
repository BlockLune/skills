# Reporting a Behavior Trace

Adapt the report to the reader and trace complexity. The headings below separate facts that otherwise blur together; omit empty sections rather than filling a template.

## Main trace

Start with the direction, scenario, and stopping status. Then present one continuous sequence of nodes.

For each node, include enough of the following to make it a black box at its current level:

- **Role**: what this node owns for the scenario.
- **Receives / produces**: the meaningful event, input, state change, or result.
- **Next relationship**: call, dispatch, resolution, scheduling, consumption, or boundary.
- **Evidence**: source locations or named artifacts, with its confirmed/candidate/gap strength.
- **Context**: only the protocol, base class, framework rule, or registration needed to make this node understandable.

A forward trace normally ends at an observable effect or external boundary. A backward trace normally ends at the scenario's user, framework, job, or process entry.

## Alternatives

List alternatives outside the main trace as short leads:

```md
- `FeatureFlagX = false` selects `FallbackHandler` instead of `PrimaryHandler`.
```

Keep each lead conditional and name the deciding evidence. Trace it only on request.

## Gaps and verification

Make a gap useful:

```md
## Unresolved
- The container receives `PaymentClient`, but the active binding is absent from the checked configuration.
  Smallest verification: inspect the production composition root or observe the resolved implementation in the existing integration test.
```

Prefer a safe, existing test, log, configuration, or build artifact as verification. Request permission before adding instrumentation or changing repository code.

## Requested artifacts

The default result is conversational. When the user asks to preserve it, write the same separation—main trace, context, alternatives, and gaps—to the requested Markdown location. Keep its evidence current and scoped to the named scenario.
