# Load Shedding

When demand exceeds safe capacity, a runtime should reject work deliberately instead of accepting everything and failing unpredictably later.

## Admission point

Shed load before expensive work begins. Admission should consider queue depth, concurrency, memory pressure, accelerator availability, downstream capacity, and request deadlines.

## Priority

If workloads have priority classes, make them explicit. Priority should describe operational importance or experiment policy, not emerge from accidental queue ordering.

## Rejection

Return a typed overload outcome that distinguishes shedding from method failure, timeout, or provider error. Include retry guidance only when the runtime has evidence that retrying later is meaningful.

## Deadlines

Requests that cannot plausibly start and finish before their deadline should be rejected early. Waiting until deadline expiry consumes capacity without producing useful work.

## Fairness

Shedding should avoid starving low-volume tenants or experiment lanes. Per-lane quotas and fair queues can preserve diversity under saturation.

## Evidence

Record the admission snapshot, limiter identity, queue depth, selected policy, and rejection reason.

## Invariants

A sound load-shedding layer guarantees:

- overload is detected before deep resource consumption;
- rejected work is classified explicitly;
- priority policy is visible;
- one noisy lane cannot consume all capacity;
- experiment failures remain distinguishable from infrastructure saturation.

Load shedding protects the runtime's useful throughput by refusing work it cannot serve responsibly.