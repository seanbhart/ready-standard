# Product Process

Project: `{{PRODUCT_ID}}`

This document defines how product truth is created, changed, approved, and
handed to coding agents for this project.

## Source Of Truth

- Durable product truth lives in `ready/`.
- Ready primitives are typed, addressable records. Product-logic primitives use
  `.ready.yml`; flags and artifact records may use specialized Ready schemas.
- Generated views compile from product-logic, decision/workflow,
  evidence/artifact, and governance primitives.
- Chat and local cache are evidence until promoted into the tree.

## Discovery

Start with the product-user problem, need, desire, constraint, or success
condition. Capture premises before solutioning. Preserve unresolved ambiguity as
decision flags or discovery flags.

## Evidence And Resources

Every build-critical intent or service should have proof corpus inputs, expected
outputs, public resources, user-only asks, or explicit blockers. Store safe
resources as evidence/artifact primitives under the milestone artifact tree and
sensitive material as refs.

## Access And Services

Every required service should use top-level `status` for state and name
blockers, account owner, access requirements, credential location reference,
evidence, proof required, setup or implementation instructions, input/output
types and samples, off-limits work, simulation policy, and failure modes. Never
commit raw secrets.

## Design And Artifacts

UI or interaction work should have enough mockups, flows, states, copy, assets,
component snippets, or design refs for coding agents to implement faithfully.
Record the design metadata as evidence/artifact primitives; large binaries or
external sources can remain attached payloads or safe refs.

## Coding Handoff

Seed and delta flags become claimable only when scope, non-scope, required
standards, services, artifacts, setup, samples, expected outputs, Completion
Proof, and blocker policy are clear. Completion Proof is the flag's Definition
of Done and must name observable evidence, not a one-word status.

## Review

Product agents close flags only after proof passes. Coding agents attach
evidence and request review; they do not decide product completion.
