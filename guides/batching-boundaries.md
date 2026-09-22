# Batching Boundaries

Batching can improve throughput, but it changes failure, latency, and accounting semantics. A runtime should make batch formation an explicit scheduling decision.

## Eligibility

Only requests with compatible provider binding, schema, policy, and deadline class should share a batch.

## Deadlines

A slow or distant-deadline item should not force urgent work to wait. Batch formation needs a bounded collection window and per-item deadline checks.

## Failure

Provider-level batch failure and item-level failure are different. Preserve per-item identity, retry state, and evidence even when transport is shared.

## Accounting

Allocate shared transport cost and latency without losing the fact that each item is an independent logical operation.

## Invariants

A correct batcher guarantees:

- incompatible requests never share execution;
- every item retains independent identity and outcome;
- batching never silently resets deadlines;
- retries can split a failed batch;
- observability can reconstruct batch membership.

Batching belongs in the scheduler, not inside opaque provider glue.