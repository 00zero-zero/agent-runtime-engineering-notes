# Resource leases

Long-lived runtimes need explicit ownership for scarce external resources such as model replicas, simulators, browsers, and accelerator slots.

A lease should identify the resource, owner, validity interval or renewal rule, and release semantics. Losing a lease should surface as a typed runtime condition rather than being hidden by a silent rebinding.

Lease identity is infrastructure provenance unless resource choice changes scientific behavior.

Shutdown should release owned leases idempotently and record failures without corrupting the completed run record.
