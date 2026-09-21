# Shutdown ordering

Structured shutdown should preserve evidence before releasing the resources needed to produce it.

Stop new admissions first, allow or cancel in-flight work according to policy, flush journals and effect receipts, finalize result artifacts, stop background controllers, and then release external resources and leases.

Cleanup should be idempotent so repeated shutdown attempts do not corrupt state.

Failures during cleanup should be recorded separately from the scientific outcome of work that already completed.
