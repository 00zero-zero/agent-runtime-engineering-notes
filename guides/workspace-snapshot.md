# Workspace Snapshot

A workspace snapshot captures the mutable execution state needed to inspect, resume, or reproduce a trial without confusing it with durable artifacts.

## Scope

Define which paths belong to the workspace and which are external mounts, caches, secrets, or generated artifacts. A snapshot should not accidentally absorb host-global state.

## Consistency

Coordinate snapshot creation with writers. Use filesystem-native snapshots, copy-on-write layers, or a quiescence barrier so related files represent one logical point in execution.

## Identity

Assign a snapshot identity and content or manifest digest. Record the parent snapshot when using incremental storage.

## Secrets

Exclude or separately encrypt materialized secrets. The snapshot manifest may record that a secret binding existed without storing its value.

## Resume

A resume operation should restore the matching environment and runtime schema before mounting the snapshot. Workspace bytes alone are not a complete checkpoint.

## Evidence

Record snapshot time, journal position, environment identity, included paths, excluded classes, and verification digest.

## Invariants

A sound snapshot mechanism guarantees:

- the captured path set is explicit;
- related writes are captured consistently;
- secret policy is enforced;
- resume checks environment compatibility;
- snapshot identity can be tied to a journal position.

Workspace snapshots support recovery and debugging while remaining distinct from published artifacts and checkpoints.