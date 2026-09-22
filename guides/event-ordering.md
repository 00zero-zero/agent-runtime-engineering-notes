# Event Ordering

Concurrent runtimes produce events from models, tools, participants, environments, and background services. Arrival order is not automatically semantic order.

## Ordering model

Define which events require a total order and which only need causal order. Use per-stream sequence numbers or explicit parent/event links instead of relying on wall-clock timestamps.

## Concurrent producers

Each producer should allocate monotonically increasing local sequence numbers. Cross-producer relationships are established through causality: request/response links, effect identities, checkpoint boundaries, or scheduler decisions.

## Persistence

A journal should preserve the authoritative ordering metadata even if storage batches or transports reorder delivery.

## Replay

Replay should reconstruct the same semantic order from recorded metadata. If two independent events were unordered originally, replay should not invent a dependency between them.

## Evidence

Record stream identity, sequence, causal parent, ingestion timestamp, and storage position when relevant.

## Invariants

- duplicate delivery cannot create a second semantic event;
- causal predecessors never appear after their dependents in replay;
- wall-clock skew cannot reorder authoritative history;
- independent events remain explicitly unordered where appropriate;
- journal storage order is not confused with semantic order.

Explicit ordering rules make concurrent traces explainable and replayable.