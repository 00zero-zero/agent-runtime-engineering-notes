# Feature Flag Provenance

Feature flags can change runtime behavior without changing source code. A reproducible run must therefore record the effective flag set.

## Resolution

Resolve flags at a declared boundary: process start, run admission, trial start, or operation dispatch. Avoid ambiguous mid-operation reads.

## Identity

Record flag name, effective value, source, evaluation context, and policy version. Sensitive targeting attributes should be redacted.

## Experiments

A feature flag that changes semantics is part of the treatment definition. Infrastructure-only flags should still be recorded when they can affect latency, routing, or failure behavior.

## Dynamic changes

When live updates are allowed, version transitions and affected operations must be observable.

## Invariants

A correct flag system ensures:

- effective values are reconstructable;
- source and targeting context are attributable;
- semantic flags cannot change invisibly mid-trial;
- experiments can detect mixed configurations;
- disabled code paths do not leave hidden state.

Feature flags are configuration with time-dependent provenance.