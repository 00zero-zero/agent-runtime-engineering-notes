# Runtime Image Identity

Container tags are mutable labels. Reproducible execution should bind to immutable runtime image identity.

## Digest

Record image repository plus content digest, not only a tag such as latest or stable.

## Build provenance

When available, retain source revision, build recipe, base image digest, and build timestamp or provenance attestation.

## Layers

Environment-specific images should declare their relationship to shared base images so changes in the base remain visible.

## Admission

Resolve tags to digests before a trial starts. Repetitions in the same experimental cell should not silently pull different image content.

## Invariants

Runtime image identity guarantees:

- executed bytes are digest-addressable;
- mutable tags cannot silently change repetitions;
- base-image lineage is traceable;
- image upgrades are explicit configuration changes;
- results can be associated with the concrete execution environment.

Image identity is part of experiment provenance, not just deployment metadata.