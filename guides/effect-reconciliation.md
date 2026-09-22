# Effect Reconciliation

An external effect can succeed even when the runtime loses its response. Recovery must therefore reconcile uncertain effects before retrying.

## States

Track effect intent, dispatch, acknowledgement, observed receipt, and final reconciled disposition.

## Uncertainty

Timeout or connection loss after dispatch creates an unknown state, not an automatic failure.

## Reconciliation

Use provider lookup, idempotency keys, durable receipts, or domain-specific queries to determine whether the effect happened.

## Retry

Only retry when policy and evidence show that repetition is safe. Preserve the same logical effect identity across reconciliation.

## Invariants

A reconciliation system guarantees:

- uncertain effects remain explicitly uncertain;
- recovery queries before blind redispatch when possible;
- receipts and idempotency keys stay attached to the logical effect;
- duplicate side effects are minimized;
- final disposition is auditable.

Reconciliation closes the gap between local call status and real-world effect state.