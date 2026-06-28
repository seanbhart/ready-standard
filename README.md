# Ready Standard

The Ready Standard defines `.ready` packages: file-based product trees for
storing product truth as typed records that can be reviewed with Git and
compiled by agents into code, design, PM, customer, or operations views.

Current source records use `.ready.yml`, the YAML serialization of the `.ready`
record format. The standard treats `.ready` as the durable package and record
identity; `.ready.yml` is the current human-readable file extension.

- Public docs are Mintlify-compatible source in this repository's `docs/`
  directory. Vendored product-local packages omit `docs/`.
- [skills/](skills/) - portable Ready Product Leader Skill Pack.
- [templates/](templates/) - project starter templates.
- [manifest.yaml](manifest.yaml) - package index for reusable resources.

This repository is project-agnostic. Ready Room is an app that reads and writes
`.ready` packages; it is not the standard itself.

## Portable Package

Projects that want agents to edit a Ready tree deterministically should vendor
the portable package beside the tree at `ready/standard/`. The portable package
is:

- `README.md`
- `manifest.yaml`
- `vocabulary.yaml`
- `skills/`
- `templates/`

Do not vendor `docs/` into product repos. The local runtime contract for agents
is the vendored `manifest.yaml`, `vocabulary.yaml`, `skills/`, and `templates/`.
Do not vendor `.git/` or repo-local metadata.

Agents should read the local `ready/standard/manifest.yaml` for normal product
tree work. Pulling the latest standard from this source repo is an explicit
standard-update task, followed by syncing the portable package and migrating the
target tree to the new version.
