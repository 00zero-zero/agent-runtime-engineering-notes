# Context Budgeting

Context is a bounded runtime resource. A robust agent runtime should allocate, account for, and compact context explicitly instead of treating model input length as an incidental prompt-building detail.

## Budget ownership

The runtime should own the total context budget for a model invocation. Prompt components consume named slices: system policy, method state, tool schemas, conversation history, retrieved memory, environment observations, and reserved generation headroom.

Downstream methods may request allocations, but they should not silently overrun the model's declared limit.

## Admission

Before invocation, estimate token cost using the selected model's tokenizer or a conservative approximation. Reject or compact before dispatch when the request cannot fit.

A model-provider truncation is not an acceptable primary policy because it hides which evidence was dropped.

## Compaction

Compaction should be explicit and attributable. Useful operations include selecting relevant history, summarizing bounded regions, replacing raw artifacts with references, and dropping reproducible boilerplate.

Every compaction step should preserve source references so the runtime can explain what information the model actually saw.

## Reserved headroom

Reserve output tokens and provider-specific overhead before filling the input budget. Retry prompts, tool-call envelopes, and structured-output schemas may require additional reserve.

## Evidence

Record the pre-compaction input set, compaction decisions, final token estimate, model limit, and actual usage returned by the provider.

## Invariants

A good context system guarantees:

- no invocation exceeds the declared budget by construction;
- dropped information is an explicit decision;
- compaction is reproducible from recorded inputs;
- output headroom is reserved before dispatch;
- token accounting is tied to the concrete model binding.

Context budgeting turns prompt overflow from an opaque provider failure into a controlled runtime decision.