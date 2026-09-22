# Trace Correlation

Observability is useful only when events from different runtime layers can be joined without guessing. Correlation identifiers should therefore be part of the execution contract.

## Identity hierarchy

Use stable identifiers for run, trial, attempt, operation, effect, model call, tool call, and environment action.

Each child event records its parent identity. This gives traces a causal tree even when execution is concurrent.

## Propagation

Correlation metadata should cross process, sandbox, queue, and RPC boundaries. Transport-specific trace headers may be derived from runtime identities, but transport tracing must not become the source of truth for experiment identity.

## Retries

A retry keeps the logical operation identity and receives a new attempt identity. This lets analysis group attempts without hiding that multiple executions occurred.

## External effects

Effect identity should correlate intent, dispatch, receipt, reconciliation, and recovery. This is especially important when a response is lost after the external system has already applied the effect.

## Logs and metrics

Every structured log and metric sample should include the minimum identities required to map it back to the authoritative run state.

Avoid placing sensitive prompt or artifact content in correlation tags.

## Invariants

A correlated runtime ensures:

- every child event has a discoverable parent;
- retries are grouped but remain individually visible;
- traces can be joined with journals and receipts;
- transport tracing can be replaced without changing experiment identity;
- concurrent execution never relies on timestamps alone to infer causality.

Correlation turns observability from a pile of records into a queryable execution graph.