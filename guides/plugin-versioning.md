# Plugin Versioning

Plugins extend runtime behavior across process and package boundaries. Their compatibility contract must be explicit.

## Identity

Record plugin name, package version, ABI or protocol version, build digest when available, and declared capabilities.

## Loading

Validate compatibility before activation. A plugin that imports successfully is not necessarily compatible with the current runtime contract.

## Isolation

Prefer narrow interfaces and explicit dependency injection. Plugins should not mutate unrelated global runtime state.

## Upgrade

Upgrades should define whether checkpoints, cached values, and durable plugin state require migration.

## Failure

Plugin load and execution failures should remain distinguishable from method failures.

## Invariants

A plugin system ensures:

- loaded implementations have stable identity;
- incompatible versions fail before work starts;
- durable state migrations are explicit;
- plugin authority is bounded;
- provenance links outputs to the concrete plugin version.

Versioned plugin contracts keep extensibility from becoming hidden coupling.