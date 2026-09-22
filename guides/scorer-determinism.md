# Scorer Determinism

A scorer should produce stable results for the same declared inputs whenever its semantics are deterministic.

## Input identity

Record candidate artifact digest, reference data version, scorer version, configuration, and any external model binding.

## Randomness

If scoring uses sampling or randomized tests, derive and record seeds. If an external model remains nondeterministic, declare that limitation and use repeated estimates when appropriate.

## Numeric stability

Specify tolerances, rounding, and aggregation order for floating-point metrics. Parallel reduction should not silently alter reported scores.

## External dependencies

Network-backed or model-based scorers need the same binding and accounting discipline as agent calls.

## Invariants

A scorer system guarantees:

- deterministic scorers are replayable;
- stochastic sources are explicit;
- numeric tolerances are versioned;
- scorer upgrades create new provenance;
- identical candidate/reference identities can be compared meaningfully.

Scorer determinism makes evaluation differences attributable instead of mysterious.