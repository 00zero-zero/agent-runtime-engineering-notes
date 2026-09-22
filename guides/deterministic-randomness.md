# Deterministic Randomness

Randomness is often part of agent research: sampling, exploration, shuffling, environment initialization, and retry jitter. Reproducibility requires explicit control over every random stream that can affect semantics.

## Seed hierarchy

Derive child seeds from stable identities such as experiment, trial, participant, and operation. Do not rely on process-global random state whose consumption order changes under concurrency.

Independent subsystems should receive independent deterministic streams.

## Concurrency

Parallel execution must not make random outcomes depend on thread or task scheduling. Allocate stream identity before dispatch rather than consuming from a shared generator after scheduling.

## External providers

When a model or environment exposes a seed parameter, record both the requested seed and whether the provider guarantees deterministic behavior. A seed request is evidence, not proof of identical output.

## Evidence

Record stream identity, derivation inputs, algorithm/version where relevant, and externally supplied seed values.

## Invariants

- every semantic random source has an owner;
- parallel scheduling cannot reorder a shared stream;
- retries either reuse or intentionally derive a new seed under explicit policy;
- seed derivation is stable across replay;
- non-deterministic providers are marked as such.

Deterministic randomness makes stochastic experiments repeatable without pretending that every external system is perfectly deterministic.