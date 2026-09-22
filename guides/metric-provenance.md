# Metric Provenance

A metric value is meaningful only when its source events, aggregation rule, units, and implementation version are known.

## Identity

Give each metric definition a stable name and version. Record units, aggregation window, inclusion rules, and missing-data behavior.

## Sources

Metrics should reference authoritative events or artifacts rather than scraping presentation logs when structured evidence exists.

## Aggregation

Define how retries, failed attempts, warmup periods, outliers, and partial trials contribute. Aggregation policy must be stable across compared runs.

## Derived metrics

A derived metric should retain links to its input metrics and formula version.

## Presentation

Dashboards may transform units or summarize windows, but the stored metric should remain traceable to raw evidence.

## Invariants

Metric provenance guarantees:

- values have explicit units and definitions;
- aggregation policy is versioned;
- source events are discoverable;
- derived metrics retain dependency lineage;
- presentation changes do not rewrite authoritative measurements.

Metric provenance turns numbers into auditable scientific evidence.