# Secret Boundaries

Secrets are runtime capabilities with confidentiality requirements. They should cross as few boundaries as possible and should never become ordinary configuration or evidence payloads.

## Scope

Bind each secret to the smallest authority scope that needs it: provider call, tool process, sandbox, or short-lived session.

Do not inject repository-wide or process-wide credentials when a narrower child process can receive a temporary credential instead.

## Representation

Runtime state should carry secret references or capability handles, not plaintext values. Logs, checkpoints, traces, prompts, and artifacts should record the reference class and redaction state without recording the secret.

## Injection

Materialize a secret only at the execution boundary that consumes it. Prefer environment variables, file descriptors, or platform secret mounts with explicit lifecycle over writing credentials into durable workspace files.

## Rotation and revocation

A long-running runtime must tolerate rotated or revoked credentials. Authentication failure should trigger re-resolution of the secret reference when policy permits, not exposure of the stale secret in diagnostics.

## Child processes

Secret inheritance must be explicit. A subprocess should receive only the credentials needed for its declared capability set.

## Evidence

Record secret class, provider, acquisition time, expiry metadata, and consumer identity. Never record the value.

## Invariants

A sound design guarantees:

- secret values do not enter journals or model prompts by default;
- child processes receive only declared credentials;
- revocation does not require rewriting durable state;
- diagnostics remain useful after redaction;
- cleanup removes materialized secret files or handles.

Secrets should behave like leased authority, not like ordinary strings.