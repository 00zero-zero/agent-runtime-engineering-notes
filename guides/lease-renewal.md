# Resource lease renewal

Leases make temporary runtime ownership explicit for workers, model replicas, sessions, and external environments.

A lease should identify the resource, owner, validity interval, renewal policy, and fencing token or generation when concurrent owners are possible. Renewal failure must surface before the runtime continues using an ownership assumption that may no longer be valid.

Lease state is operational provenance. It should not redefine the scientific identity of the model or environment being used.

Fencing stale owners is as important as detecting expiration.
