# Cancellation semantics

Cancellation should be explicit, journaled, and propagated through the runtime tree.

A parent cancellation request should identify which child operations are interruptible, which effects must finish atomically, and which external resources require cleanup. The runtime should record the request, acknowledgement, and final termination state.

Cancellation is not equivalent to failure. Evaluation and recovery logic should preserve that distinction.

Resuming a cancelled run should require an explicit policy decision rather than silently continuing from partial state.
