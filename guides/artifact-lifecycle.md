# Artifact Lifecycle

Artifacts are durable runtime outputs such as patches, reports, traces, screenshots, checkpoints, datasets, and evaluation files. They need a lifecycle distinct from transient workspace state.

## Identity

Give each artifact a stable identity independent of its local path. Record the producing run/attempt, logical role, content digest, media type or schema, and producer component.

A digest prevents silent replacement under the same logical name.

## Staging and publication

Write into attempt-local staging first. Incomplete outputs must not appear as published artifacts.

Publication is an explicit state transition. Consumers should reference immutable artifact identity rather than a mutable workspace filename. Mutable aliases, when needed, should point to immutable versions.

## Retries and provenance

Retries may produce different artifacts. Preserve each attempt instead of silently overwriting prior output.

Provenance should connect an artifact to the method/program version, runtime/environment identity, input artifacts, relevant effect receipts, and producing operation.

## Retention and export

Differentiate mandatory evidence, user deliverables, diagnostics, and disposable intermediates. Export across sandbox or machine boundaries should verify the final digest and record the destination.

## Invariants

A robust artifact system guarantees:

- published artifacts are immutable by identity;
- incomplete staging objects are never consumed;
- retries do not erase prior attempts;
- every artifact has a producer and provenance path;
- retention preserves evidence required to interpret results.

Treating artifacts as first-class runtime objects prevents durable outputs from being confused with disposable workspace files.