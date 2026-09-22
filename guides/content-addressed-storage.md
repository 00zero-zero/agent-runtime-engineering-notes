# Content-Addressed Storage

Content-addressed storage identifies immutable data by digest. It can simplify artifact deduplication, integrity checking, and replay.

## Digest

Choose a stable cryptographic digest and define exactly which bytes are hashed. Metadata that changes independently should live outside the content identity.

## Immutability

Objects addressed by digest must be immutable. Mutable logical names should resolve to immutable digests.

## Verification

Verify content when ingesting from untrusted or remote storage and after transfer across machine boundaries.

## Garbage collection

Reference tracking and retention policy should determine liveness. Deleting an alias must not remove an object still referenced by evidence or another artifact.

## Provenance

Record producer, logical role, digest, size, media type, and storage location separately.

## Invariants

A content-addressed store guarantees:

- equal digests refer to equal byte content under the declared hash;
- objects cannot mutate under an existing identity;
- transfer corruption is detectable;
- retention respects references;
- aliases do not replace provenance.

Content identity provides a stable bridge between workspaces, artifacts, caches, and evidence.