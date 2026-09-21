# Journal replay

A machine journal should contain enough authoritative information to reconstruct state transitions without reissuing external side effects.

Replay applies recorded results and receipts to rebuild internal state. It should not call live providers for facts that the original execution already resolved.

Version journal event schemas and fail explicitly when an event cannot be interpreted.

Snapshots may accelerate replay, but the journal position used by a snapshot must be explicit so replay can continue deterministically from that boundary.
