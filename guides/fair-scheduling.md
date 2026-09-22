# Fair Scheduling

Concurrency alone does not guarantee fair access to runtime resources. A scheduler should prevent one workload, user, or experiment lane from monopolizing shared capacity.

## Scheduling unit

Define the schedulable unit explicitly: request, trial, model call, tool call, environment lease, or accelerator slot.

Different resources may require different schedulers.

## Fairness domains

Group work by the identity that deserves isolation, such as tenant, experiment, repository, or priority class. Use weighted fairness only when weights are declared policy.

## Queue discipline

FIFO is simple but can suffer head-of-line blocking. Deficit round-robin, fair queueing, or bounded per-domain queues can improve isolation.

The chosen discipline should be deterministic enough to analyze and should expose tie-breaking rules.

## Long-running work

Prevent long tasks from holding all scarce slots. Resource leases, preemption boundaries, or concurrency caps can protect shorter and unrelated work.

## Starvation

Track wait time and service share. Starvation protection may boost old requests, but this policy must remain observable.

## Evidence

Record enqueue time, selected queue, scheduling decision, wait duration, resource assignment, and any priority adjustment.

## Invariants

A fair scheduler ensures:

- no single domain can consume unbounded shared capacity;
- policy weights are explicit;
- starvation is detectable;
- scheduling decisions are reconstructable;
- fairness logic does not alter method semantics.

Fair scheduling turns shared infrastructure into an accountable resource rather than a race.