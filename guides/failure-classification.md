# Failure classification

Failure handling improves when runtimes distinguish causes instead of treating every exception identically.

Useful categories include invalid configuration, admission failure, provider unavailability, capacity exhaustion, timeout, external effect uncertainty, participant failure, and invariant violation.

Classification should be deterministic from recorded evidence and should drive retry or recovery policy through explicit rules.

Paper-specific self-correction belongs to the method; generic infrastructure failure classification belongs to the runtime.
