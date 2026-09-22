# Human Intervention Boundary

Human input can be part of a method, an operational recovery path, or an external approval. These roles should not be conflated.

## Classification

Record whether an intervention is experimental method semantics, safety approval, infrastructure recovery, or administrative control.

## Pause semantics

When waiting for a human, persist the runtime state and declare how deadlines, leases, and external effects behave during the pause.

## Authority

The human action should identify the decision being authorized and the scope it changes. Free-form operator access should not silently mutate unrelated runtime state.

## Evidence

Record request time, response time, intervention class, authorized action, and resulting state transition. Sensitive human content may require redaction.

## Invariants

A sound intervention boundary ensures:

- human help is visible in experimental evidence;
- operational recovery is not misreported as autonomous method behavior;
- approvals have bounded scope;
- pause/resume semantics are explicit;
- intervention does not erase prior machine decisions.

Human involvement should be modeled as an auditable runtime event.