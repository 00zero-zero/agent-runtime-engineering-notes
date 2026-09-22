# Temporary File Lifecycle

Temporary files often carry prompts, downloads, tool outputs, credentials, and intermediate artifacts. Their ownership and cleanup require explicit policy.

## Location

Create temporary state under a runtime-owned root rather than arbitrary system locations when possible.

## Ownership

Associate every temporary path with a run, trial, operation, or sandbox owner.

## Durability

Classify temporary data as disposable, recoverable until checkpoint, or promotable to a durable artifact. Promotion should be explicit.

## Security

Use restrictive permissions for sensitive content. Secret-bearing temporary files should have a shorter lifetime and should never be included in broad snapshots by default.

## Cleanup

Cleanup should be idempotent and should handle crashes through orphan reaping.

## Invariants

A temporary-file system guarantees:

- every path has an owner;
- sensitive files have bounded exposure;
- disposable data is not mistaken for durable evidence;
- promotion to artifact is explicit;
- crash cleanup can discover leftovers.

Temporary storage is runtime state with a lifecycle, not an untracked scratch space.