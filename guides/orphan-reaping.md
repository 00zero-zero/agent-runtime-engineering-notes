# Orphan Reaping

Agent runtimes create subprocesses, sandboxes, leases, temporary files, and remote resources. Crashes can leave these resources without a live owner.

## Ownership record

Every resource should record an owner identity, creation time, lease or heartbeat metadata, and cleanup strategy.

Resources without explicit ownership are difficult to distinguish from intentional long-lived state.

## Detection

A reaper should determine liveness using durable owner state, lease expiry, process ancestry, or authoritative run status. Missing heartbeats alone may be insufficient when the control plane is partitioned.

## Fencing

Before destructive cleanup, ensure the old owner cannot still act. Fencing tokens or lease generations prevent a delayed owner from resuming against a resource that has been reassigned.

## Cleanup

Cleanup should be idempotent. Deleting an already-removed resource should be safe and should not hide evidence of the original orphan.

## Evidence

Record why the resource was classified orphaned, the fencing decision, cleanup attempts, and final disposition.

## Invariants

A safe reaper guarantees:

- resources carry discoverable owners;
- cleanup never races an unfenced live owner;
- repeated cleanup is safe;
- unresolved orphans remain visible;
- reaping does not erase provenance.

Orphan reaping closes the lifecycle gap created by crashes and partial failures.