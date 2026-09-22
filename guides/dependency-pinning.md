# Dependency Pinning

Runtime reproducibility depends on more than top-level source revisions. Transitive libraries, system packages, and executable tools can change behavior.

## Pinning levels

Record lockfile state, package hashes when available, runtime language version, system image digest, and externally invoked binary versions.

## Resolution

Dependency resolution should happen before experiments begin. Re-resolving floating ranges between repetitions can create different treatments.

## Exceptions

When a dependency must remain floating, record the exact resolved version for every run and treat upgrades as configuration changes.

## Native components

Compiler, CUDA, driver, browser, and system library versions may materially affect behavior even when application packages are fixed.

## Invariants

A reproducible environment guarantees:

- resolved dependency identity is recorded;
- repeated trials do not silently re-resolve versions;
- image and package provenance are connected;
- floating dependencies are observable;
- environment upgrades are deliberate experimental changes.

Dependency pinning turns environment drift into explicit version transitions.