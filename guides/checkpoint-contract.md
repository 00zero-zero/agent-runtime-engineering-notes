# Checkpoint contract

A checkpoint is a coordinated recovery boundary, not just a serialized process object.

It should identify the run, journal position, participant states, environment state, progress counters, external resource references, and schema versions needed for resume. Every component should state whether its state is restorable, reconnectable, or non-recoverable.

Resume must validate that the checkpoint belongs to the same frozen scientific run and that required external resources can be restored consistently.

If exact restoration is impossible, fail explicitly rather than silently starting fresh state.
