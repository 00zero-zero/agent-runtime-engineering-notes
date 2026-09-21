# Durable schema migration

Durable runtime state should never rely on best-effort deserialization across incompatible versions.

Every stored contract should carry a schema identifier and version. Unsupported versions should fail with a typed migration requirement rather than guessing missing fields or applying new defaults.

A migration should be deterministic, tested, and explicit about its source and target versions. Preserve the original artifact or its immutable identity so the transformation remains auditable.

Silent compatibility fallbacks can change scientific meaning and should be avoided.
