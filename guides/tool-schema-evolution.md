# Tool Schema Evolution

Tool interfaces evolve. Renamed fields, new enum values, stricter validation, or changed result shapes can silently alter agent behavior even when the tool name stays the same.

## Versioned contract

Treat the callable schema as a versioned interface. Record the schema identity presented to the model and the concrete provider implementation bound behind it.

Breaking changes should create a new schema version rather than relying on runtime guesswork.

## Compatibility adapters

Compatibility belongs at an explicit boundary. An adapter may translate an older request into a newer provider call, but the translation rule should be deterministic, tested, and visible in provenance.

Do not silently drop unknown fields or invent missing required values.

## Model view

Prompt/tool descriptions are part of the semantic interface. A schema migration that changes descriptions, defaults, or enum meanings may affect model decisions even if JSON validation still succeeds.

## Evidence

Record schema version, adapter version, validation result, and provider binding for each call.

## Invariants

- every invocation can identify the schema shown to the model;
- breaking changes are explicit;
- adapters are deterministic and observable;
- validation occurs before effectful dispatch;
- provider changes cannot silently mutate tool semantics.

Versioning tool schemas keeps interface drift from becoming hidden method drift.