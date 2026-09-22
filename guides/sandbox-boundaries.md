# Sandbox Boundaries

A sandbox is an authority boundary, not merely a temporary directory or subprocess wrapper. Its contract defines what an agent may read, write, execute, and reach over the network.

## Declared authority

Define before execution:

- filesystem roots and mount modes;
- process execution policy;
- network access;
- environment variables and secrets;
- device access;
- CPU, memory, disk, accelerator, and time limits.

Default-deny is easier to reason about than broad access followed by scattered filtering.

## Ownership

The sandbox owns every descendant process it creates. Shutdown must terminate or reap the complete process tree. Background daemons require explicit ownership or they can survive a trial and contaminate later experiments.

## Evidence

Record image/rootfs digest, mounts, network policy, resource limits, capability classes, and runtime version. Do not record secret values.

## Cleanup

Cleanup verifies that owned processes are gone, writable mounts are detached, and temporary state is either deliberately exported or destroyed.

A failed cleanup is itself a runtime fault because it can invalidate later trials.

## Invariants

A robust sandbox guarantees:

- undeclared host resources remain inaccessible;
- every descendant process has an owner;
- resource limits are observable;
- environment identity is reproducible;
- cleanup restores isolation.

The sandbox contract protects both security and experimental validity.