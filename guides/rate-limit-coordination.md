# Rate-Limit Coordination

Rate limits are shared-capacity constraints. Independent callers that each retry locally can amplify overload and create avoidable throttling.

## Shared authority

Coordinate limits at the provider or credential boundary. The runtime should maintain shared knowledge of request, token, and concurrency budgets for callers using the same constrained resource.

## Feedback

Prefer provider-supplied reset times and remaining-budget headers when available. Local estimates may fill gaps but should not override authoritative feedback without evidence.

## Queueing

When capacity is exhausted, queue or reject requests before dispatch. Preserve request deadlines so work that can no longer finish is not allowed to wait indefinitely.

## Retry

A 429 or equivalent response should update shared capacity state. Retry delay belongs to the same deadline and experiment accounting as the original call.

Jitter may reduce synchronized retries, but the random source and policy should be controlled for reproducibility when experiments compare runtime behavior.

## Multiple credentials

If multiple credentials or endpoints are available, routing must respect authorization boundaries and record which binding was selected. Capacity balancing must never become implicit credential escalation.

## Evidence

Record admission time, queue delay, limiter identity, provider feedback, retry delay, and final dispatch time.

## Invariants

A coordinated limiter ensures:

- callers do not independently oversubscribe the same capacity;
- provider feedback affects all relevant callers;
- retries consume the original budget;
- routing decisions remain observable;
- deadlines can fail before dispatch instead of after wasteful waiting.

Rate-limit coordination is therefore part of scheduling, not merely HTTP error handling.