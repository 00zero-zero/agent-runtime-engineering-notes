# Effect idempotency

Resumable runtimes must prevent replay from duplicating external side effects.

Assign every intended effect a stable identity, persist the intent before execution, and persist a receipt after the provider confirms completion. Pass an idempotency key to providers that support one.

On recovery, reconcile the intended effect against stored receipts before issuing it again. When the provider lacks idempotency support, the adapter needs an explicit reconciliation protocol.

Internal control-flow replay must never imply automatic replay of payments, messages, writes, or other irreversible actions.
