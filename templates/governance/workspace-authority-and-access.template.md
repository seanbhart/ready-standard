# Workspace Authority And Access

Project: `{{PRODUCT_ID}}`

This file records project-specific authority and access policy for product
agents and coding handoff.

## Owners

- Product authority: `{{PRODUCT_AUTHORITY_OWNER}}`
- Technical authority: `{{TECHNICAL_AUTHORITY_OWNER}}`
- Repository authority: `{{REPOSITORY_AUTHORITY_OWNER}}`
- Merge/release authority: `{{MERGE_RELEASE_AUTHORITY_OWNER}}`

## Allowed Actions

Two-way-door actions product agents may perform without additional approval:

- `{{REVERSIBLE_ACTION}}`

One-way-door or authority-expanding actions requiring explicit approval:

- destructive file or data changes;
- credential creation or rotation;
- shared-state changes;
- repo branch protection, merge, release, or deployment changes;
- `{{PROJECT_SPECIFIC_ONE_WAY_ACTION}}`

## Local Access

- Allowed local paths: `{{ALLOWED_LOCAL_PATHS}}`
- Required clean-tree policy: `{{CLEAN_TREE_POLICY}}`
- CLI tools allowed: `{{ALLOWED_CLI_TOOLS}}`

## Secret Handling

Never store raw secrets in `ready/`. Record safe secret-location references:
variable names, storage system, owner, required scope, setup status, and
verification command.
