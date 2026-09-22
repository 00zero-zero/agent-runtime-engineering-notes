# Configuration Snapshot

Runtime behavior is reproducible only when the effective configuration used by a run is known.

## Effective configuration

Resolve defaults, files, environment variables, command-line flags, remote settings, and policy overrides into one effective configuration at admission time.

## Snapshot

Persist a redacted, immutable snapshot or digest with the run. Record source precedence so unexpected values can be traced back to their origin.

## Secrets

Secret values should never enter the snapshot. Store stable references or redacted markers instead.

## Dynamic configuration

If a setting may change during a run, record each version transition and define which components observe it. Static experiment semantics should generally remain frozen.

## Validation

Validate the fully-resolved configuration before expensive work begins.

## Invariants

A configuration system guarantees:

- effective values are attributable to sources;
- secret material is excluded;
- run semantics can be reconstructed;
- dynamic changes are versioned;
- invalid combinations fail before execution.

Configuration snapshots make operational state part of reproducible evidence.