# Nested Runtime Ownership

A runtime may launch another runtime as a child operation. Without explicit ownership, nested execution can leak resources, duplicate authority, and confuse evidence.

## Parent contract

The parent assigns child identity, budget, capability scope, workspace boundary, and cancellation relationship before launch.

## Authority

A child receives only delegated capabilities. It must not inherit host-global credentials or resource access merely because it runs inside the same process or machine.

## Lifecycle

Parent completion should wait for owned children unless they are explicitly detached and transferred to a new owner.

Cancellation, deadlines, checkpoints, and cleanup should propagate according to the declared ownership relation.

## Evidence

Record parent/child linkage, delegated capabilities, allocated budget, child terminal state, and exported artifacts.

## Invariants

Nested ownership guarantees:

- every child runtime has one accountable owner;
- delegated authority is explicit;
- parent shutdown cannot leave unknown children;
- child evidence remains joinable to the parent trial;
- detached work requires an explicit ownership transfer.

Nested runtimes should compose through contracts, not shared global state.