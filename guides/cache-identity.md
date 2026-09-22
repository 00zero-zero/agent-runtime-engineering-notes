# Cache Identity

A cache is correct only when its key captures every semantic input that can change the result. Incomplete identity turns an optimization into cross-run contamination.

## Key dimensions

Depending on the cached object, identity may include method/version, model binding, tool schema, environment revision, normalized input, authorization scope, and relevant configuration.

Do not key semantic results only by a convenient filename or prompt string.

## Canonicalization

Normalize structured inputs deterministically before hashing. Canonicalization rules are part of the cache contract and should be versioned.

## Authority

A cache hit reuses prior computation; it does not become new evidence that the underlying provider was contacted. Record hit/miss and the source artifact or receipt identity.

## Invariants

- all semantic inputs participate in the key;
- tenant or credential scope cannot cross accidentally;
- key canonicalization is deterministic;
- cache hits are distinguishable from fresh execution;
- cache schema/version changes invalidate incompatible entries.

Cache identity determines whether reuse is reproducible or corrupting.