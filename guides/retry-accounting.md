# Retry accounting in agent evaluation

Retries consume real resources and can improve success probability, so evaluation must define how they affect budgets.

Model calls, tool calls, tokens, environment steps, wall time, and cost should normally include method-visible retries. Infrastructure retries that occur before an operation is accepted can be reported separately only under a predeclared transparent-recovery rule.

Log every attempt with its cause, budget impact, and final disposition.

A benchmark result should make hidden recovery work visible so treatments cannot receive unequal extra computation.
