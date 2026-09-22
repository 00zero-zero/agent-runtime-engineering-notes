# Accelerator Allocation

GPUs and other accelerators are scarce, stateful resources. Allocation should be modeled as a lease rather than an implicit environment variable.

## Identity

Record device identity, partition or MIG slice, driver/runtime version, memory capacity, and lease generation.

## Admission

Check memory and concurrency requirements before launching work. Oversubscription policy should be explicit.

## Isolation

A lease defines which process tree may access the device. Shared use should declare memory and scheduling policy.

## Cleanup

On release, terminate owned device processes, clear task-local state when feasible, and verify the lease generation before reassignment.

## Evidence

Record allocation time, wait duration, device binding, utilization summaries, and release outcome.

## Invariants

Accelerator allocation guarantees:

- device ownership is explicit;
- stale owners are fenced before reuse;
- limits are part of run evidence;
- scheduling delay is distinguishable from execution latency;
- experiments can reproduce the resource class used.

Accelerators belong in the resource authority model, not only deployment configuration.