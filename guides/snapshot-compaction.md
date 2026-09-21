# Snapshot compaction

Snapshots bound replay cost but should remain derived from authoritative history.

Create a snapshot only at a known journal position and record the position plus a digest of the materialized state. Older snapshots can be compacted or deleted when a newer verified snapshot and the required journal history remain available.

Compaction must not delete the only evidence needed to audit state transitions. If journal retention is also bounded, define an explicit trust boundary where a verified snapshot becomes the new recovery root.

Snapshot lifecycle is a performance policy, not a second source of truth.
