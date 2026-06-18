---
name: ready-perspective-review
version: 0.1.0
description: Use specialist perspectives and subagents to challenge whether the Ready tree fully understands the product and is ready for implementation.
---

# Perspective Review

Use this module before implementation handoff, after major discovery changes,
or when confidence is low. The goal is to find missing truth before coding
agents discover it by stalling or building the wrong thing.

## Review Roles

Assign distinct roles to subagents when available. A single agent may simulate
roles for small work, but substantial Ready tree creation should use real
parallel review.

Psychological reviewer:

- What motivation, fear, trust issue, desire, habit, or adoption barrier is
  missing?
- What emotional outcome does the user need?
- What would make the user reject the product even if the logic works?

Physical reviewer:

- What real-world context, device, environment, time pressure, handoff, manual
  step, or operational constraint is missing?
- What has to be true before, during, and after the product is used?
- What could go wrong because of physical or organizational reality?

Logic reviewer:

- What rules, data shapes, state transitions, permissions, edge cases, or
  failure modes are underspecified?
- What contradictions exist between premises, intents, standards, services,
  artifacts, and flags?
- What proof would catch a false-green implementation?

Evidence/resources reviewer:

- What samples, expected outputs, public resources, generated fixtures,
  licenses, or provenance are missing?
- Which facts are circular, stale, inferred, or unsupported?
- What can the agent gather safely, and what must the user provide?

Design reviewer:

- What interface states, copy, assets, flows, responsive behavior, accessibility
  expectations, or component contracts are missing?
- Which design artifacts are authoritative versus illustrative?
- What visual proof should be required?

Access/handoff reviewer:

- What account, credential, environment, CLI login, service readiness, setup
  command, or blocker would stop coding?
- What work-package instruction is ambiguous?
- Which flags should stay non-claimable?

## Review Output

Each reviewer returns:

- missing facts;
- risky assumptions;
- contradictions;
- suggested cuts;
- user-only asks;
- safe agent-gatherable resources;
- affected primitives, services, artifacts, or flags;
- readiness recommendation: ready, draft, blocked, or cut.

## Completion Check

The review is complete when every material issue becomes one of:

- a primitive edit;
- an artifact or resource task;
- a service readiness update;
- a flag change;
- a question card;
- an explicit cut from the next stage.
