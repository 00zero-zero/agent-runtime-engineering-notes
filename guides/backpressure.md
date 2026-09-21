# Runtime backpressure

Backpressure prevents admission from outrunning the capacity of models, tools, environments, or storage.

Expose bounded queues and explicit saturation signals instead of allowing unbounded buffering. Admission should understand capacity but must not silently weaken scientific requirements to keep throughput high.

When capacity is exhausted, return a typed operational outcome that can be retried or scheduled later without changing trial identity.

Queue length, wait time, and rejection reason are useful provenance for diagnosing throughput without becoming scientific authority.
