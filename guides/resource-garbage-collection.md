# Resource Garbage Collection

Long-running runtimes accumulate snapshots, artifacts, cache entries, leases, images, temporary workspaces, and remote resources. Collection must preserve everything still required by active work or evidence.

## Roots

Define durable roots such as active runs, retained experiment records, published artifacts, checkpoints, and pinned references.

## Reachability

Prefer reference or reachability analysis when possible. Age alone is insufficient because old evidence may still be required while recent temporary data may already be disposable.

## Safety window

Use a quarantine or grace period before destructive deletion when concurrent writers or delayed references are possible.

## Remote resources

Garbage collection for cloud or external resources needs ownership tags and fencing so stale cleanup cannot delete reassigned resources.

## Evidence

Record collection generation, selected objects, retention reason, deletion outcome, and unresolved references.

## Invariants

A collector guarantees:

- rooted evidence is never deleted;
- active owners are fenced from stale cleanup;
- deletion is auditable;
- retention policy is explicit;
- collection can be retried safely.

Garbage collection should reclaim cost without weakening reproducibility.