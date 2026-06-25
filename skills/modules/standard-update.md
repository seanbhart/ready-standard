---
name: ready-standard-update
version: 0.1.0
description: Sync the latest Ready standard package into a product Ready tree and migrate the tree to that version.
---

# Ready Standard Update

Use this module when a user asks to update, upgrade, or migrate a product Ready
tree to the latest Ready standard or to a named Ready standard version.

## Authority

Before changing a product repo, read that project's authority document and
confirm the agent is allowed to edit the Ready tree. If the standard source repo
does not have an authority document, say so and keep source-repo edits limited
to the explicitly requested standard package or docs work.

## Inputs

- Source standard repo or released standard package.
- Target product repo with `ready/manifest.yaml`.
- Target project authority and governance files.

## Process

1. Read the source standard `manifest.yaml` and `skills/manifest.yaml`.
2. Confirm the source standard version is newer than the target
   `ready_standard.version` or the target `ready/standard/manifest.yaml`
   version. If the target is already current, still verify the local package
   matches the source package.
3. Sync the portable package into `ready/standard/`.
   - Include `README.md`, `manifest.yaml`, `skills/`, and `templates/`.
   - Exclude `docs/`, `.git/`, `.gitignore`, local cache, raw logs, transcripts,
     private samples, and secrets.
4. Update `ready/manifest.yaml` so `ready_standard` points at the local package:

   ```yaml
   ready_standard:
     version: "<STANDARD_VERSION>"
     repository: "https://github.com/seanbhart/ready-standard"
     package_path: "ready/standard"
     package_manifest: "ready/standard/manifest.yaml"
     docs_source: "https://github.com/seanbhart/ready-standard/tree/<STANDARD_VERSION>/docs"
   ```

5. Update product manifests that carry standard metadata to the same version and
   local package path.
6. Read the new local `ready/standard/skills/ready-skill.md` and modules needed
   for the migration.
7. Migrate product records to the new standard. For the current standard:
   - Flag and Decision records use top-level `type`, `claimable`, `blocked_by`,
     and `completion_proof`.
   - Legacy unresolved-decision records migrate to `type: decision`, stable `XD-*` ids,
     `fields.safe_default`, structured `fields.proposals`, and
     `fields.decision_needed`; remove deprecated answer and owner-decision
     fields.
   - Intent `completion_proof` is the durable Definition of Done. It must
     contain concrete observable proof, not a one-word status.
   - Flag `completion_proof` is closure criteria for a temporary workflow
     record, not the canonical product DoD.
   - Store one structural edge per relationship in `refs`; do not mirror inverse
     refs.
   - Any primitive type may relate to any other primitive type when the
     structural relationship is true.
   - Approved stored roles are `peer`, `parent`, and `child`. In compact refs,
     the role describes the target primitive's position relative to the current
     primitive.
   - Semantic verbs such as `serves`, `requires`, `governed_by`,
     `contains_premise`, and `questions` are derived reader labels, not stored
     ref roles.
   - Valid vocabulary lives in `ready/standard/vocabulary.yaml`.
   - Semantic relationship display lookups in vocabulary.yaml include both
     source-to-target and target-to-source phrases for the same stored edge,
     such as `serves` / `served by`.
   - Standards that govern premises, intents, services, flags, or other standards
     should usually migrate to `peer` refs. Keep `child` standard refs only when
     preserving older fallback semantics or intentional nesting.
8. Preserve project-specific governance and product truth. Do not rewrite
   product meaning merely to fit a template.
9. Verify the migrated tree:
   - no stale standard versions or deprecated fields;
   - every record has a unique id;
   - every structural ref points to an existing id;
   - no duplicate structural edges;
   - no inverse duplicate edges and no semantic roles left in `refs`;
   - every flag has top-level `type`, `claimable`, and non-empty concrete
     `completion_proof`;
   - the vendored package differs from the source package only by intentionally
     excluded source-repo files.
10. Report the source version, target package path, migration changes, and
    verification commands.

## Agent Rule

For ordinary product-tree edits, agents read the target repo's local
`ready/standard/` package. They fetch from the source standard repo only when
the task explicitly asks for a latest-version or named-version standard update.
