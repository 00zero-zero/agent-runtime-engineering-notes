# Multi-Agent Message Ordering

Concurrent agents may send messages whose delivery order differs from creation order. Communication semantics should therefore be explicit.

## Identity

Every message should carry sender, receiver or channel, message identity, sender-local sequence, and causal parent when applicable.

## Delivery

Define whether a channel provides FIFO per sender, FIFO per conversation, causal order, or no ordering guarantee.

## Retries

Delivery retries preserve logical message identity while recording new transport attempts. Duplicate suppression should not erase evidence of retries.

## Visibility

Recipients should only observe messages admitted by the channel's visibility policy. Hidden internal coordination must not leak through shared logs or prompts.

## Invariants

A communication layer guarantees:

- ordering claims are explicit;
- duplicates can be detected;
- causal parents remain traceable;
- transport retries do not create new logical messages;
- replay follows the declared delivery semantics.

Message ordering is part of multi-agent method semantics whenever communication affects decisions.