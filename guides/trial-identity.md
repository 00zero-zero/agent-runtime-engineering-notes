# Trial Identity

A trial is a single experimental unit with a stable identity that ties method, task, environment, configuration, and repetition together.

## Construction

Derive trial identity from experiment definition plus task instance and repetition index. Runtime retries belong beneath the same trial rather than creating a new trial silently.

## Boundaries

A trial owns its workspace, journal, checkpoints, resource leases, model accounting, evaluator outputs, and terminal outcome.

## Retries

Infrastructure recovery may create new attempts inside a trial. Re-running the complete trial after terminal failure should receive a new execution identity while retaining linkage to the same experimental cell.

## Evidence

Record treatment, task identity, repetition, seed derivation, environment binding, and execution attempts.

## Invariants

Trial identity ensures:

- results cannot be mixed across experimental cells;
- retries remain subordinate to the original trial;
- repeated executions are distinguishable;
- all evidence can be joined through one stable key;
- aggregation does not rely on filenames or timestamps.

Trial identity is the backbone of experiment provenance.