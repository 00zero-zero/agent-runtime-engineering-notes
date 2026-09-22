# Environment Capability Negotiation

A method should not assume that every runtime environment exposes the same tools, devices, network access, or interaction primitives.

## Declaration

An environment publishes a typed capability set before execution: supported observations, actions, devices, network classes, filesystem semantics, and optional extensions.

## Requirements

A method or benchmark declares required and optional capabilities. Admission succeeds only when required capabilities can be bound.

## Late binding

Concrete implementations may vary across machines, but the selected capability versions and provider identities must be recorded.

## Degradation

Optional capability loss may activate an explicit fallback only when the method permits it. Silent degradation changes experimental semantics.

## Invariants

Negotiation guarantees:

- required capabilities are validated before execution;
- concrete bindings are observable;
- optional fallbacks are declared;
- environment differences cannot hide behind the same task label;
- unsupported requirements fail at admission rather than mid-run.

Capability negotiation keeps method intent portable without making environment authority ambiguous.