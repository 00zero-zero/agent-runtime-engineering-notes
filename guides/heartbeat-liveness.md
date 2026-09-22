# Heartbeat and Liveness

Heartbeats provide evidence of recent activity, but they are not proof that a component is healthy or dead.

## Signal design

A heartbeat should carry component identity, generation or lease epoch, monotonic sequence, and observation time.

## Failure detection

Use bounded suspicion windows rather than treating one missed heartbeat as failure. Network partitions, scheduler pauses, and overloaded control planes can delay a healthy component.

## Fencing

Before replacing a suspected owner, advance a fencing token or lease generation so an old instance cannot resume with stale authority.

## Readiness

Separate liveness from readiness. A process may be alive but unable to accept work because dependencies or capacity are unavailable.

## Evidence

Record heartbeat gaps, suspicion transitions, fencing changes, and replacement decisions.

## Invariants

A sound liveness system guarantees:

- heartbeats are generation-aware;
- suspicion is distinct from confirmed ownership loss;
- replacement is fenced;
- readiness and liveness are separately modeled;
- transient delay does not silently create duplicate owners.

Heartbeats support failure detection, but authority comes from leases and fencing.