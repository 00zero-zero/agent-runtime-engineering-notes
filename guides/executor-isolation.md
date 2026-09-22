# Executor Isolation

Executors run untrusted or failure-prone work on behalf of the runtime. Their resource and failure boundaries should be explicit.

## Scope

An executor owns a bounded process tree, workspace, environment variables, resource quota, and capability set.

## Failure containment

Crashes, memory leaks, and deadlocks inside one executor should not corrupt scheduler or journal authority. Supervisors should detect executor loss and classify affected operations.

## Reuse

Reusable workers must reset task-local state before accepting a new operation. Persistent caches and connections should be declared shared state rather than accidental residue.

## Evidence

Record executor identity, image or binary version, assigned operation, resource limits, and terminal disposition.

## Invariants

Executor isolation guarantees:

- task-local state does not leak across unrelated operations;
- executor failure is contained;
- reused workers pass a reset boundary;
- resource usage is attributable;
- scheduler authority remains outside worker processes.

Executors should be replaceable workers, not hidden control planes.