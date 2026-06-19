# Ready Standard

Ready is a file-based product tree standard for storing product truth as typed
records that can be reviewed with Git and compiled by agents into code,
design, PM, customer, or operations views.

- [docs/](docs/) - Mintlify-compatible documentation source.
- [skills/](skills/) - portable Ready Product Leader Skill Pack.
- [templates/](templates/) - project starter templates.
- [manifest.yaml](manifest.yaml) - package index for reusable resources.

This repository is project-agnostic. Ready Room is an app that reads and writes
Ready product trees; it is not the standard itself.

## Portable Package

Projects that want agents to edit a Ready tree deterministically should vendor
the portable package beside the tree at `ready/standard/`. The portable package
is:

- `README.md`
- `manifest.yaml`
- `skills/`
- `templates/`

Do not vendor `docs/` into product repos. Those files are Mintlify source for
the public standard docs, not the runtime contract agents need to edit a tree.
Do not vendor `.git/` or repo-local metadata.

Agents should read the local `ready/standard/manifest.yaml` for normal product
tree work. Pulling the latest standard from this source repo is an explicit
standard-update task, followed by syncing the portable package and migrating the
target tree to the new version.
