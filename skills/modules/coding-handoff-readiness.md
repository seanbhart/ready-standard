---
name: ready-coding-handoff-readiness
version: 0.1.0
description: Ensure Ready target-state handoffs are complete enough for coding agents to claim, build, verify, and return evidence without avoidable blockers.
---

# Coding Handoff Readiness

Use this module before any seed or change flag is made claimable.

## Responsibilities

- Compile product truth into coding-agent-ready resolved target-state handoffs
  without turning the product agent into the coding agent.
- Ensure every claimable flag names scope, non-scope, dependencies, required
  standards, required services, required artifacts, setup needs, acceptance
  proof, and blocker policy.
- Ensure every required sample, resource, design, snippet, manifest, credential
  location, or environment setup reference is visible to the coding agent.
- Keep non-blocked seed flags non-ready until product leadership intentionally
  starts implementation.
- Allow blocked flags to be ready only when `blocked_by` prevents coding claims.
- Require concrete top-level Completion Proof before review and closure.

## Target-State Handoff Checklist

A coding agent should receive:

- the decision/workflow flag id when a stored flag gates the work;
- the resolved intended product state, not just a delta;
- the product-logic primitive ids, standards, services, artifacts, and proof
  gates that define that target state;
- scope and non-scope;
- user-facing and system-facing acceptance criteria;
- required services with status, blockers, access, proof, and instructions;
- setup and verification commands;
- required artifacts and sample ids;
- design, snippet, or component references when applicable;
- data shapes and expected outputs;
- failure modes and edge cases;
- relevant standards;
- privacy, security, and authority limits;
- Completion Proof;
- how to report blockers and attach evidence.

## What Not To Do

- Do not prescribe internal file edits unless a standard, interface, architecture
  decision, or user instruction requires it.
- The coding environment chooses implementation strategy inside the product,
  service, authority, and proof constraints.
- Do not hand coding agents only a diff or change instruction. Diffs,
  implementation evidence, and prior commits are context; the claimable target is
  the resolved intended state.
- Do not make a flag claimable because the prose sounds clear while access,
  samples, designs, or proof are missing.
- Do not treat one-word statuses such as `ready`, `done`, or `complete` as
  Completion Proof.
- Do not close flags based on coding-agent self-report.

## Completion Check

The module is complete when a coding agent can claim the work, set up the
environment, understand the resolved target state, choose a clean implementation
strategy within constraints, run proof, attach evidence, and know when to stop or
report a blocker.
