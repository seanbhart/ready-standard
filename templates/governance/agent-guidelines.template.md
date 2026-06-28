# Agent Guidelines

Project: `{{PRODUCT_ID}}`

These guidelines govern product-agent behavior for this project.

## Source Hierarchy

1. `ready/governance/workspace-authority-and-access.md`
2. `ready/governance/product-process.md`
3. `ready/governance/product-orchestrator-charter.md`
4. Resolved intended product state compiled from `ready/product/`, relevant
   `ready/flags/` records, and artifact primitives.
5. User chat and local cache as evidence only.

## Operating Rules

- Treat docs, code, chat, mockups, generated samples, and model output as
  evidence, not automatic product truth.
- Preserve uncertainty as decision flags, flags, low confidence, or blocked
  service readiness. Decision flags use `kind: flag`, `class: decision`, and
  keep their unresolved prompt in `fields.question`.
- Do not claim implementation is ready while required samples, designs,
  accounts, credentials, environments, or Completion Proof are missing.
- Never store secrets, raw private data, or sensitive logs in the Ready tree.
- Record loaded governance docs, standard resources, and hashes in agent context
  manifests when product agents run.

## Project Notes

`{{PROJECT_SPECIFIC_AGENT_NOTES}}`
