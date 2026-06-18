# Product Process

Project: `{{PRODUCT_ID}}`

This document defines how product truth is created, changed, approved, and
handed to coding agents for this project.

## Source Of Truth

- Durable product truth lives in `ready/`.
- Primitive source records are `.ready.yml`.
- Generated views compile from primitives, flags, services, standards, and
  artifacts.
- Chat and local cache are evidence until promoted into the tree.

## Discovery

Start with the product-user problem, need, desire, constraint, or success
condition. Capture premises before solutioning. Preserve unresolved ambiguity as
question cards or discovery flags.

## Evidence And Resources

Every build-critical intent or service should have sample data, expected
outputs, public resources, user-only asks, or explicit blockers. Store safe
resources under the milestone artifact tree and sensitive material as refs.

## Access And Services

Every required service should name account owner, access state, credential
location reference, setup path, verification check, simulation policy, and
failure modes. Never commit raw secrets.

## Design And Artifacts

UI or interaction work should have enough mockups, flows, states, copy, assets,
component snippets, or design refs for coding agents to implement faithfully.

## Coding Handoff

Seed and delta flags become claimable only when scope, non-scope, required
standards, services, artifacts, setup, samples, expected outputs, Completion
Proof, and blocker policy are clear.

## Review

Product agents close flags only after proof passes. Coding agents attach
evidence and request review; they do not decide product completion.
