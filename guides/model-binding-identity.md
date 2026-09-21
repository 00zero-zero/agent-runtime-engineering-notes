# Model binding identity

A model role is part of scientific configuration; a deployment replica is usually infrastructure.

Freeze the semantic model identifier, revision, context policy, decoding parameters, tool/schema capabilities, and any routing policy that can change outputs before execution.

At runtime, a scheduler may place that frozen binding on equivalent replicas without changing trial identity.

If failover changes the actual model semantics, it should create a different binding or fail closed rather than masquerading as transparent infrastructure recovery.
