# Ready Skill Modules

These files are the portable Ready Product Leader Skill Pack. They are
project-agnostic standard resources, not a project's authority policy.

- [ready-skill.md](ready-skill.md) - entrypoint and router.
- [modules/evidence-resource-review.md](modules/evidence-resource-review.md) - evidence,
  samples, public resources, generated fixtures, and user-only information.
- [modules/access-readiness.md](modules/access-readiness.md) - accounts, credentials,
  environments, secret-location references, and setup verification.
- [modules/design-artifact-readiness.md](modules/design-artifact-readiness.md) - design,
  mockup, flow, component, snippet, and visual proof readiness.
- [modules/coding-handoff-readiness.md](modules/coding-handoff-readiness.md) - claimable flag
  and work-package readiness for coding agents.
- [modules/perspective-review.md](modules/perspective-review.md) - psychological, physical,
  logical, evidence, design, and access challenge review.
- [modules/standard-update.md](modules/standard-update.md) - sync the latest
  Ready standard package into a product tree and migrate the tree.

The Ready Skill is the entrypoint. Load only the modules that match the current
gap, and record loaded module ids and hashes in the agent context manifest.

## Portable Package

[manifest.yaml](manifest.yaml) describes the portable package. To pass the
skills to another agent or project, copy this whole directory or the exact files
listed in `portable_files`. Paths are repo-relative so a receiving agent can copy
the package without resolving working-directory assumptions. Do not include
local cache, raw transcripts, private samples, secrets, or project-specific
artifacts.

The receiving project should keep the copied package at `ready/standard/` and
point `ready/manifest.yaml` at that local package. Treat the copied package as
source text that can be reviewed and versioned. Agents should update it only
when asked to migrate the project to a newer Ready standard version.
