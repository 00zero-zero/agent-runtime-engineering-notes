# Shared State Conflicts

Multiple agents or runtime workers may update the same logical state concurrently. Conflict policy should be declared instead of delegated to last-write-wins accidents.

## Versioning

Each mutable record should carry a version, revision, or compare-and-swap token.

## Conflict detection

Writers should detect stale bases before commit. A failed compare is a typed conflict, not a generic storage error.

## Resolution

Resolution may retry, merge, serialize through a coordinator, or invoke method-specific arbitration. Generic infrastructure should not invent semantic merges it does not understand.

## Evidence

Record the competing revisions, writer identities, chosen resolution path, and resulting version.

## Invariants

A shared-state system guarantees:

- stale writes are detectable;
- merge policy is explicit;
- conflicting attempts remain observable;
- retries do not silently overwrite newer state;
- method-specific arbitration stays outside generic storage machinery.

Conflict handling preserves authority under concurrency instead of relying on timing luck.