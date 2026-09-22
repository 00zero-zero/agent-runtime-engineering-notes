# Deadline Budgeting

Deadlines are resource budgets. Treating each runtime layer as if it owns the full user timeout creates hidden overruns, retry storms, and non-reproducible behavior.

## Absolute deadline contract

Represent a deadline as an absolute monotonic-time boundary rather than repeatedly copying a relative timeout. Each child receives the parent's remaining budget minus any explicit reserve.

A child may shorten its deadline, but it may not extend the parent's authority. Wall-clock timestamps remain useful for audit; scheduling decisions should use a monotonic clock.

## Hierarchical allocation

A practical hierarchy is:

request → runtime turn → model/tool operation → transport attempt.

The parent owns the total budget. Children receive bounded slices. Reserve time for mandatory finalization such as journal flushes, effect reconciliation, checkpoint persistence, and lease release.

## Retry accounting

Retries spend the same deadline budget. A retry policy must inspect remaining time before backoff or redispatch.

If the next sleep or attempt cannot fit, return a typed deadline outcome instead of starting work that is already impossible to finish.

## Queueing versus execution

Record queue delay separately from execution time. Saturated capacity should not be misdiagnosed as a slow model or tool.

Admission control can reject work that cannot plausibly start before its deadline, preserving capacity for requests that remain feasible.

## External calls

Transport libraries often accept relative timeouts. Convert the remaining absolute budget immediately before dispatch.

Keep separate transport limits when needed: connection, first-byte, operation, and total parent deadline. A transport timeout is an implementation event; the parent deadline is the scheduling authority.

## Pauses and human steps

Human approval may intentionally suspend execution. Persist the paused state and explicitly suspend or replace the active deadline rather than letting it expire invisibly.

## Evidence

Record parent deadline, child allocation, queue delay, execution duration, retry delay, reserve usage, and exhaustion reason.

This lets experiments distinguish algorithmic failure from insufficient runtime budget.

## Invariants

A sound runtime can assert:

- no child deadline exceeds its parent;
- retries never reset the total budget;
- cleanup has bounded reserved time;
- monotonic time drives scheduling;
- queueing and execution remain separately observable.

Deadline budgeting turns scattered timeout settings into an explicit runtime contract.