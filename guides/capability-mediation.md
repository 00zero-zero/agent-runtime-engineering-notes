# Capability Mediation

Agent methods should request capabilities rather than directly owning transports, credentials, or provider-specific clients. A mediation layer keeps semantic intent separate from effectful execution.

## Request contract

A request identifies the operation, typed arguments, caller identity, runtime/trial identity, required authority, and a stable effect identity when side effects are possible.

The method states what it wants done. The mediator decides whether and how execution is allowed.

## Platform responsibilities

Reusable policy belongs at the mediation boundary:

- authorization and schema validation;
- rate, concurrency, and quota enforcement;
- credential and provider selection;
- evidence capture and redaction;
- effect receipts and retry identity.

Method-specific reasoning stays outside this layer.

## Late binding

Bind semantic capability to a concrete provider as late as practical. Record the chosen provider, version, configuration, and environment identity so runs remain reproducible.

## Failure semantics

A policy denial is distinct from a provider failure. Provider-specific exceptions should be normalized into a stable runtime taxonomy while preserving original diagnostics as evidence.

## Invariants

A strong mediator guarantees:

- methods cannot bypass centralized policy;
- effect identity survives retries;
- provider choice is observable;
- credentials never become method-owned state;
- the same method can run against different concrete environments.

Capability mediation is therefore the runtime's effect boundary: methods state intent while the platform owns safe execution.