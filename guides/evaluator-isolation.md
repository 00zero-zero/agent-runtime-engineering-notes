# Evaluator Isolation

Evaluation code should measure a run without gaining accidental authority over the system it scores.

## Boundary

Run evaluators in a separate authority domain from the agent when practical. They may read declared outputs and evidence but should not mutate agent state or repair results before scoring.

## Inputs

Define exactly which artifacts, traces, environment state, and reference data the evaluator may inspect.

## Secrets

Reference answers, hidden tests, and evaluator credentials must not leak into the agent execution environment.

## Failure

Evaluator failure is distinct from agent failure. Preserve the candidate output and record evaluation failure so rerunning the evaluator does not require rerunning the agent.

## Invariants

Evaluator isolation guarantees:

- hidden references cannot reach the agent;
- scoring cannot mutate candidate state;
- evaluator retries do not change agent execution;
- score provenance identifies evaluator version and inputs;
- evaluation failures remain separately classifiable.

Isolation keeps measurement from contaminating the system being measured.