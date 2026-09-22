# Circuit Breaker Policy

Repeatedly calling a failing dependency wastes deadlines and can amplify an outage. A circuit breaker converts recent failure evidence into temporary admission policy.

## States

Use explicit states such as closed, open, and half-open. State transitions should be driven by bounded windows of typed failures rather than raw exception counts alone.

## Scope

Breakers should be scoped to the failing dependency identity: provider, endpoint, region, model binding, tool backend, or service instance. One unhealthy route should not disable unrelated capacity.

## Opening

Only failures that indicate dependency health should contribute. Method-level validation errors, policy denials, and user cancellation should not trip an infrastructure breaker.

## Half-open probes

After a bounded cool-down, allow a small number of probe requests. Probe ownership and results should be recorded so concurrent callers do not all probe simultaneously.

## Interaction with fallback

Fallback routing may use breaker state, but selection must remain observable. A fallback changes infrastructure binding and may affect experiment interpretation.

## Recovery

Breaker state should not become hidden global memory. Persist enough state or evidence to explain why admission changed during a run.

## Invariants

A robust breaker guarantees:

- only relevant failure classes affect health state;
- state is scoped to a concrete dependency;
- half-open probes are bounded;
- fallback decisions are recorded;
- breaker policy cannot silently change method semantics.

Circuit breakers are a runtime reliability mechanism, not a substitute for method-level recovery logic.