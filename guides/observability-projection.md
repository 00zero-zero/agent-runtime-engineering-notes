# Observability as a projection

Metrics and dashboards should be derived from authoritative runtime facts instead of maintaining a second mutable truth.

Emit canonical events once, then build counters, traces, health views, and summaries as replayable projections. Each projection should retain enough source identity to be rebuilt after corruption or schema changes.

Operational UIs may issue commands through explicit control APIs, but they should not mutate scientific state by editing derived counters.

If an observability database is lost, execution truth should remain intact.
