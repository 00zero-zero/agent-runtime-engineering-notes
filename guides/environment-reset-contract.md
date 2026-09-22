# Environment Reset Contract

Repeated trials are comparable only when the environment can return to a defined baseline. Reset is therefore an explicit runtime operation, not incidental cleanup.

## Baseline identity

Define the baseline using immutable or versioned inputs: image digest, filesystem snapshot, service state, dataset revision, configuration, and external fixture identities.

A reset target should be named by identity, not by a vague command such as "clean workspace."

## Reset phases

A robust reset sequence may include:

1. stop owned processes;
2. reconcile outstanding external effects;
3. remove or archive trial-local state;
4. restore baseline filesystem or snapshot;
5. reinitialize services and credentials;
6. verify readiness.

The verification phase is essential. Completion of a reset command does not prove the environment matches the baseline.

## External systems

For remote APIs or shared simulators, define which state can be reset and which state is merely namespaced. If perfect rollback is impossible, isolate trials with unique resource identities.

## Failure

Reset failure should block the next trial. Continuing after a partial reset risks contaminating experimental results.

## Evidence

Record baseline identity, reset start and completion, verification results, residual resources, and any manual exception.

## Invariants

A reset contract guarantees:

- each trial starts from a declared baseline;
- owned processes and writable state from prior trials are absent;
- unresettable external state is namespaced;
- failed verification prevents admission of the next trial;
- reset evidence is attached to the trial boundary.

Environment reset is part of experimental validity, not just operational hygiene.