# Benchmark Binding

A benchmark name is not enough to identify the workload used in an experiment. Dataset revision, task transformation, evaluator, and environment must be bound explicitly.

## Identity

Record benchmark package/version, dataset revision or digest, split, task instance identity, preprocessing, environment image, and scorer binding.

## Adapters

Adapters may translate benchmark records into runtime tasks, but transformation code and configuration become part of the benchmark binding.

## Hidden state

Remote benchmark services should expose a stable service or protocol version when possible. If hidden data can change, record the evaluation window and service response metadata.

## Upgrades

Benchmark updates should create a new binding rather than silently replacing an old one under the same label.

## Invariants

A benchmark binding guarantees:

- task instances are version-addressable;
- preprocessing is attributable;
- evaluator identity is connected to the workload;
- environment changes are visible;
- results from incompatible benchmark revisions are not aggregated accidentally.

Explicit binding turns a benchmark label into a reproducible workload contract.