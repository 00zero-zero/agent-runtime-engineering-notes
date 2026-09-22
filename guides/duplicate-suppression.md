# Duplicate Suppression

Distributed retries can deliver the same logical operation more than once. Duplicate suppression should use stable identities rather than timing heuristics.

## Identity

Assign an idempotency or message identity before first dispatch and preserve it across transport retries.

## Scope

Declare where uniqueness is enforced: process, queue, service, effect domain, or external provider.

## Storage

Suppression records need bounded retention tied to the maximum retry or replay horizon. Expiring too early can re-admit old duplicates; retaining forever creates unbounded state.

## Outcome reuse

When a duplicate arrives after a completed operation, return or reference the recorded outcome when safe instead of executing again.

## Invariants

A suppression layer guarantees:

- retries preserve logical identity;
- duplicate detection scope is explicit;
- completed outcomes can be reconciled;
- expiration policy matches replay windows;
- suppression does not erase evidence of repeated delivery attempts.

Duplicate suppression protects side effects without pretending transport is exactly-once.