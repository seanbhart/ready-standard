# Product Process

Project: `{{PRODUCT_ID}}`

This document defines how product truth is created, changed, approved, and
handed to coding agents for this project.

## Source Of Truth

- Durable product truth lives in `ready/product/`.
- Ready primitives are typed, addressable durable product-package inputs.
  Flags, governance records, settings, and manifests use their own Ready kinds.
- Generated views compile from primitives, flags, artifact primitives,
  governance records, settings, and manifests.
- Chat and local cache are evidence until promoted into the tree.

## Discovery

Start with the product-user problem, need, desire, constraint, or success
condition. Capture premises before solutioning. Preserve unresolved ambiguity as
decision flags or discovery flags.

## Evidence And Resources

Every build-critical intent or service should have proof corpus inputs, expected
outputs, public resources, user-only asks, or explicit blockers. Store safe
resources as artifact descriptors under `ready/product/artifacts/` and
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
Record the design metadata as artifact descriptors; large binaries or
external sources can remain attached payloads or safe refs.

Ready-carried artifacts may become product assets, templates, fixtures, or
manifests, but implementation must copy, transform, or compile those files into
product-owned paths or storage. The running product must not depend on
`ready/settings/` or any Ready directory for runtime artifacts.

## Coding Handoff

Seed and change flags become claimable only when the resolved target-state
handoff, scope, non-scope, required standards, services, artifacts, setup,
samples, expected outputs, intent Completion Proof, and blocker policy are
clear. A handoff gives coding agents the intended end state plus proof gates,
not a delta or edit instructions. Intent Completion Proof is the durable
Definition of Done; flag Completion Proof is only closure criteria for the
temporary flag.

## Review

Product agents close flags only after proof passes. Coding agents attach
evidence and request review; they do not decide product completion.
