---
name: ready-design-artifact-readiness
version: 0.1.0
description: Prepare design, mockup, flow, copy, asset, and modular component artifacts needed for product-faithful implementation.
---

# Design Artifact Readiness

Use this module when the product has a UI, workflow, customer-facing copy,
visual proof requirement, component contract, or interaction that coding agents
must implement faithfully.

## Responsibilities

- Identify every product-logic primitive and decision/workflow primitive that
  depends on a visual or interaction decision.
- Gather existing designs, screenshots, mockups, prototypes, brand assets,
  design-system references, copy, and flow diagrams.
- Create low-fidelity mockups, HTML prototypes, component specs, or generated
  visual references when no useful design exists and the intended product needs one.
- Provide modular snippets or component contracts when they reduce ambiguity for
  coding agents.
- Mark prototype code as handoff reference unless the user explicitly makes it
  production source.
- Capture responsive behavior, loading states, empty states, error states,
  permission states, accessibility expectations, and content rules.

## Artifact Guidance

Store design-support material as artifact descriptors under product artifacts:

- `designs/` for mockups, screenshots, visual references, diagrams, and design
  handoff notes;
- `snippets/` for component contracts, prototype code, copy blocks, state maps,
  and reusable reference snippets;
- `resources/` for design-system docs, public UI references, icon sources, or
  external inspiration refs;
- `samples/` for UI state fixtures and expected outputs.

Record each design artifact's authority: target, reference, evidence,
prototype, generated concept, stale, or superseded. If a design conflicts with
primitive truth, create a decision flag or primitive edit proposal instead of
silently blending them.

Do not bury design decisions in chat. Link the artifact descriptor to the
affected product-logic primitive, service, or flag.

## Design Completeness Checklist

Before a coding flag becomes claimable, check whether it needs:

- target user flow;
- screen or component inventory;
- primary, empty, loading, error, disabled, and permission states;
- responsive behavior;
- copy and labels;
- asset and icon requirements;
- accessibility requirements;
- data displayed in each state;
- interaction rules;
- visual acceptance proof;
- modular snippets or component contracts.

## Completion Check

The module is complete when coding agents can see what should be built, what
states must exist, which artifacts are authoritative, what is only reference,
and what visual proof will be reviewed.
