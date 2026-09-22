# Configuration Layering

Multiple configuration sources are useful only when precedence is deterministic and explainable.

## Layers

Define an ordered stack such as built-in defaults, project config, environment config, user config, CLI overrides, and runtime policy.

## Merge semantics

Specify whether nested structures merge, replace, or reject conflicts. Lists and maps need explicit rules.

## Provenance

Each effective value should retain its source layer so operators can explain why it won.

## Validation

Validate after full resolution, not each source independently, because invalid combinations may emerge only after merge.

## Invariants

A layered configuration system guarantees:

- precedence is stable;
- merge behavior is defined per data type;
- effective values retain provenance;
- invalid combinations fail before execution;
- secrets can remain references instead of copied values.

Configuration layering should reduce repetition without hiding authority.