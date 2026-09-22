# Model Call Accounting

Model calls consume money, tokens, latency, and experiment budget. A runtime should account for them as first-class operations rather than opaque provider requests.

## Identity

Assign each logical model operation an identity and each retry an attempt identity. Record the concrete model binding, provider, endpoint class, request parameters, and runtime caller.

## Usage

Capture prompt tokens, completion tokens, cached tokens, reasoning tokens when exposed, billable units, and provider-reported cost metadata. Preserve provider raw usage alongside normalized fields.

## Retries and fallbacks

Retries and fallbacks remain visible. Do not collapse several paid requests into one apparent call. The logical operation may succeed once while still consuming multiple attempts.

## Streaming

For streaming calls, record dispatch time, first-token latency, completion time, termination reason, and whether the consumer cancelled before the provider finished.

## Budget enforcement

Admission should consider remaining token, monetary, and time budgets before dispatch. A call that exceeds policy should fail before contacting the provider.

## Evidence

Persist request identity, model binding, sampling controls, usage, latency, retry history, and normalized outcome. Sensitive prompt content can remain behind separate access controls.

## Invariants

A correct accounting layer ensures:

- every provider request belongs to one attempt;
- every attempt belongs to one logical operation;
- retries never disappear from cost totals;
- actual provider usage can be reconciled with normalized metrics;
- model cost is attributable to a run, trial, and method.

Model-call accounting is therefore part of scientific measurement as well as operations.