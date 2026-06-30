# Ready Skill Modules

These files are the portable Ready Product Leader Skill Bundle. They are
project-agnostic standard resources, not a project's authority policy.

- [SKILL.md](SKILL.md) - installable skill entrypoint.
- [ready-skill.md](ready-skill.md) - authoritative Ready Skill router.
- [modules/evidence-resource-review.md](modules/evidence-resource-review.md) - evidence,
  samples, public resources, generated fixtures, and user-only information.
- [modules/access-readiness.md](modules/access-readiness.md) - accounts, credentials,
  environments, secret-location references, and setup verification.
- [modules/design-artifact-readiness.md](modules/design-artifact-readiness.md) - design,
  mockup, flow, component, snippet, and visual proof readiness.
- [modules/coding-handoff-readiness.md](modules/coding-handoff-readiness.md) - claimable flag
  and resolved target-state handoff readiness for coding agents.
- [modules/perspective-review.md](modules/perspective-review.md) - psychological, physical,
  logical, evidence, design, and access challenge review.
- [modules/standard-update.md](modules/standard-update.md) - sync the latest
  Ready Standard bundle into a product tree and migrate the tree.

The Ready Skill is the entrypoint. Load only the modules that match the current
gap, and record loaded module ids and hashes in the agent context manifest.

## Portable Bundle

[`manifest.yaml`](manifest.yaml) describes this portable skill bundle. To pass
only the skill bundle to another agent or project, copy this whole directory or the
exact files listed in `portable_files`. Paths in this skill manifest are
relative to the `skills/` bundle root. Do not include local cache, raw
transcripts, private samples, secrets, or project-specific artifacts.

A complete Ready Standard bundle also includes root files such as
`manifest.yaml` and `vocabulary.yaml`. Product repos should keep that full
bundle at `ready/standard/` and point `ready/manifest.yaml` at the local
bundle. Treat the copied bundle as source text that can be reviewed and
versioned. Agents should update it only when asked to migrate the project to a
newer Ready Standard version.
