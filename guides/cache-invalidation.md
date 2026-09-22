# Cache Invalidation

A valid cache entry can become invalid when code, schemas, environments, data, policy, or provider behavior changes. Invalidation should follow explicit dependency identity rather than ad hoc deletion.

## Dependency model

Each entry should name the immutable identities it depends on. When one dependency changes, entries referencing the old identity naturally miss without a global purge.

## Time-based expiry

TTL is useful for freshness-sensitive data but is not a substitute for semantic versioning. Expiry should reflect the source's validity window, not an arbitrary cleanup interval.

## Negative cache

Cached failures or "not found" results need shorter, explicit validity because recovery or external state changes can make them obsolete quickly.

## Eviction versus invalidation

Capacity eviction removes valid entries for space. Invalidation declares an entry semantically unsafe to reuse. Keep the two reasons distinguishable in evidence.

## Invariants

- semantic changes create misses by identity;
- TTL does not hide missing version dimensions;
- negative results have bounded validity;
- eviction is not reported as invalidation;
- stale entries cannot cross environment or policy revisions.

Explicit invalidation keeps performance reuse subordinate to correctness.