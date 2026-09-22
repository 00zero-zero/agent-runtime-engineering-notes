# Priority Inversion

Priority inversion occurs when high-priority work is blocked behind lower-priority work that owns a resource it needs. Agent runtimes can trigger this through model slots, browser sessions, locks, GPUs, or tool leases.

## Detection

Record the waiter, owner, resource, priority class, wait start, and dependency chain. The scheduler should distinguish ordinary queueing from inversion caused by a lower-priority owner.

## Mitigation

Possible mechanisms include priority inheritance, bounded lease preemption, resource partitioning, or admission rules that prevent incompatible priority mixes.

Mitigation must preserve ownership semantics. Preempting a resource without reconciling in-flight effects can create duplicated actions or corrupt workspace state.

## Evidence

Persist inversion events and the policy applied. Experiments should be able to explain whether latency came from method behavior or runtime scheduling interference.

## Invariants

A robust runtime ensures:

- inversion is observable rather than inferred from latency;
- mitigation cannot bypass effect reconciliation;
- inherited priority is temporary and scoped;
- resource ownership remains explicit;
- trial metrics separate inversion delay from execution time.

Priority handling is part of the scheduler contract, not a hidden optimization.