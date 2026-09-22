# Communication Visibility

Multi-agent systems need explicit rules for which messages, observations, and state each participant may see.

## Policy

Define visibility by participant, channel, message class, or shared workspace rather than relying on incidental object references.

## Delivery

A message should be admitted only if sender authority, receiver scope, and channel policy all permit it.

## Shared state

Read visibility and write authority are separate. An agent may observe shared state without permission to mutate it.

## Observability

System operators may have broader diagnostic access, but that view should not automatically become model context.

## Invariants

A communication policy guarantees:

- participant views are explicitly derived;
- hidden channels cannot leak through shared prompts or logs;
- read and write authority are distinct;
- operator observability is separated from agent visibility;
- replay reconstructs the same participant-visible history.

Visibility rules are part of method semantics whenever information access affects decisions.