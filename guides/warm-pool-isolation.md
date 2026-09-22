# Warm Pool Isolation

Pre-warmed workers reduce startup latency, but reuse creates a risk that one task observes state left by another.

## Baseline

A warm worker should have a declared clean baseline covering filesystem, process state, environment variables, loaded credentials, caches, and network sessions.

## Checkout

Before assignment, validate worker generation and reset task-local state. A failed reset removes the worker from the pool.

## Return

On return, revoke task-scoped credentials, terminate descendants, clear writable workspace, and verify readiness before reuse.

## Shared caches

Any intentionally retained cache must be declared shared infrastructure and keyed strongly enough to avoid cross-task semantic contamination.

## Invariants

A warm pool guarantees:

- task-local state cannot survive reuse;
- credentials are revoked before return;
- reset failure prevents reassignment;
- shared caches are explicit;
- worker generation and baseline are observable.

Warm pools should trade startup latency, not isolation.