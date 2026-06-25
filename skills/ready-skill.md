---
name: ready
version: 0.3.27
description: Lead creation of a Ready product tree from docs, code, or discovery, then make it complete enough for coding agents to build without avoidable blockers.
---

# Ready Skill

Use this skill to create or revise a Ready product tree. The skill is about the
Ready standard and about acting as a strong product leader: discover the real
problem, shape the smallest useful solution, gather the evidence and resources
needed to build it, identify the services and standards that make it safe, and
cut away what is unnecessary for the intended product version.

This is an orchestration skill. Load specialist Ready Skill modules when the
tree needs focused work:

- [modules/evidence-resource-review.md](modules/evidence-resource-review.md) -
  evidence, proof corpora, online resources, generated fixtures, and user-only
  information.
- [modules/access-readiness.md](modules/access-readiness.md) -
  accounts, credentials, environments, secret-location references, and setup
  verification.
- [modules/design-artifact-readiness.md](modules/design-artifact-readiness.md) -
  designs, mockups, screenshots, flows, component specs, and modular UI snippets.
- [modules/coding-handoff-readiness.md](modules/coding-handoff-readiness.md) -
  resolved target-state handoffs, blockers, acceptance proof, and coding-agent
  constraints.
- [modules/perspective-review.md](modules/perspective-review.md) -
  subagent review from psychological, physical, logical, evidence, design, and
  access perspectives.
- [modules/standard-update.md](modules/standard-update.md) -
  sync a newer Ready standard package into a product repo and migrate the tree.

The portable package manifest is [manifest.yaml](manifest.yaml). The canonical
vocabulary file is [vocabulary.yaml](../vocabulary.yaml). Product repos that
need deterministic agent edits should keep the portable standard package at
`ready/standard/`. Normal product agents read that local package. Pulling from
the source standard repo happens only for explicit standard-update work.

The Ready Skill does not prescribe internal code files, functions, components,
migrations, or implementation strategy unless those choices are product
constraints, standards, interfaces, artifacts, proof expectations, or user-given
requirements. Its job is to ensure coding agents know exactly what product
outcome to build and have the resources to do it.

## Outputs

The primary output is a `ready/` tree:

```text
ready/
  manifest.yaml
  governance/
    agent-guidelines.md
    product-orchestrator-charter.md
    product-process.md
    workspace-authority-and-access.md
  settings/
    product-agent-context.ready.yml
  product/
    manifest.yaml
    README.md
    premises/
    intents/
    standards/
    services/
    artifacts/
      samples/
      resources/
      snippets/
      designs/
      manifests/
  flags/
    decisions/
    blockers/
    drift/
    proof-gaps/
```

The root `manifest.yaml` must declare product, flags, governance, settings, and
standard package locations:

```yaml
schema: readyroom/product-tree-root/v1
product: example
source_root: ready
product_directory: ready/product
flags_directory: ready/flags
governance_directory: ready/governance
settings_directory: ready/settings
ready_standard:
  version: "0.3.27"
  repository: "https://github.com/seanbhart/ready-standard"
  package_path: "ready/standard"
  package_manifest: "ready/standard/manifest.yaml"
```

Use `ready/settings/` for git-tracked workspace and app settings that help tools
manage the Ready tree. Settings files should use explicit settings schemas,
avoid raw secrets, and not duplicate product truth that belongs in primitives,
governance, artifacts, or flags.

Use `ready/product/` for canonical intended product truth for this Ready tree
version, including premises, intents, standards, services, product artifacts,
and reusable proof material that may not be fully implemented yet. Use
`ready/flags/` for temporary decisions, blockers, discrepancy notes, and claim
coordination. File location is authoritative for product/workflow assignment.

Primitive source records are `.ready.yml` files with:

```yaml
schema: readyroom/primitive/v1
kind: primitive
id: I-001
type: intent
title: Human-readable title
status: draft
fields:
  statement: Concise product-truth statement
refs: []
artifacts: []
owner_notes: []
```

Reader-friendly docs, app views, resolved target-state coding handoffs, tickets,
and briefs compile from the tree. They are not the primitive source of truth.

## Product-Leadership Stance

Act like a product leader, discoverer, and practical unblocker:

- Start with the user's problem, need, desire, constraint, or success condition.
- Separate observed evidence from approved product truth.
- Ask the fewest questions that materially change the tree.
- Assume the user is busy, tired, distracted, or missing context; provide exact
  next steps, examples, and safe options instead of vague requests.
- Proactively gather public resources, generated fixtures, examples, and
  source-shape references when they can fill safe gaps.
- Direct the user only for information, samples, credentials, accounts, business
  judgment, or private resources that cannot be safely obtained another way.
- Preserve uncertainty as decision flags, draft fields, low confidence, or flags.
- Prefer a smaller coherent product version that proves the core promise.
- Cut nice-to-have work until it clearly supports the intended product version.
- Keep implementation details out of primitives unless they are true product
  constraints, interfaces, standards, artifacts, services, or proof expectations.
- Treat the Ready tree on the current branch as the intended product state for
  that branch. Use Git branches or worktrees for substantial hypothetical
  concepts instead of storing speculative fragments in canonical product truth.

Docs, code, conversation, public sources, generated samples, designs, and model
output are evidence. They do not automatically become approved product truth.

## Input Modes

Ready tree creation starts from one of three modes.

### Human Documentation Only

Use this mode when the project has planning docs, specs, decks, notes, issue
lists, design docs, or strategy prose, but no reliable codebase signal.

Process:

1. Inventory the docs and note source age, author intent, and confidence.
2. Extract premise candidates from observations, beliefs, assumptions, needs,
   problems, motivations, risks, opportunities, and success claims.
3. Extract intent candidates from product promises, observable product
   behaviors, workflows, outcomes, capabilities, experiences, safety behavior,
   failure behavior, and requirements.
4. Extract standards from constraints, explicit rules, quality bars, compliance
   needs, measurement rules, and non-negotiable behavior.
5. Extract services from dependencies needed to build, prove, run, or monitor
   the product.
6. Identify missing samples, resources, designs, accounts, credentials, and
   environments needed to make the intended product buildable.
7. Preserve conflicts instead of averaging them.
8. Ask the user to resolve only product-shaping gaps that affect the intended product.
9. Create draft or active `.ready.yml` primitives with evidence confidence.
10. Create flags or decision flags where work is not ready.

Documentation-only trees should be explicit about whether a fact is user-stated,
doc-stated, inferred, stale, generated, gathered from public sources, or
unresolved.

### Codebase Only

Use this mode when the project has code but little or no reliable product
documentation.

Process:

1. Inspect the visible product surfaces: routes, screens, commands, APIs,
   schemas, tests, fixtures, configuration, workflows, README material, design
   assets, and environment examples.
2. Infer what the product currently does.
3. Infer possible actors, outcomes, services, resources, and standards from code
   evidence.
4. Do not assume current behavior is desired behavior.
5. Mark user problems and product motivations as inferred or unknown until the
   user confirms them.
6. Ask questions that connect implementation reality to product truth: who uses
   it, what need it serves, what success looks like, what must not break, what
   resources are missing, what credentials or accounts are needed, and what
   should be cut from the intended product.
7. Create a Ready tree that separates existing behavior from approved direction.
8. Use flags or decision flags for gaps that code cannot answer.

Codebase-only trees should be conservative. They can describe observed behavior
with medium or high evidence confidence, but user need and product priority
usually remain lower confidence until confirmed.

### From Scratch Discussion

Use this mode when the product is being discovered in conversation.

Process:

1. Understand the situation.
2. Identify the user, buyer, operator, or system actor.
3. Discover the problem, need, desire, motivation, constraint, or success
   condition.
4. Understand current alternatives and why they fail.
5. Shape one or more solution candidates.
6. Choose the smallest coherent intended product version.
7. Cut scope until that product version can prove the core promise.
8. Identify standards, services, artifacts, proof corpora, resources, accounts,
   credentials, designs, and proof expectations.
9. Create the Ready tree and review it with the user.

Ask follow-up questions like a product leader, not a form. Start broad, then
become concrete. When the user seems overloaded, offer a short checklist,
default assumptions, and one or two high-leverage questions.

## Discovery Questions

Use these as a question bank. Do not ask all of them at once.

Problem and need:

- Who has the problem?
- What are they trying to accomplish?
- What is painful, slow, risky, expensive, confusing, or unsatisfying today?
- Why does this matter now?
- How often does it happen?
- What happens if it is not solved?
- What does the user already do instead?
- What emotional, operational, financial, or strategic desire is underneath it?

Success:

- What would make the user say this worked?
- What observable outcome should change?
- What must be true for the product to be trusted?
- What would make the product unacceptable even if it technically works?

Solution:

- What solution shape seems most likely?
- What workflow should the user experience first?
- What should the product decide, automate, reveal, prevent, or simplify?
- What should stay manual for now?
- What should not be built yet?

Resources and evidence:

- What real samples, screenshots, documents, exports, data, examples, or edge
  cases would help a coding agent understand the target?
- Can safe synthetic data prove the workflow, or does this need user-provided
  data?
- Are there public datasets, API docs, marketplace examples, competitor
  references, or source-shape docs that should be gathered and cited?
- What samples are privacy-sensitive, bulky, licensed, stale, or unavailable?
- What is the expected output for each important sample input?

Access and services:

- What external systems, data sources, APIs, people, models, stores, queues, or
  environments are required?
- What accounts must exist before coding starts?
- Where should credentials live so coding agents can access them safely?
- What `.env.example`, `.env.local`, secret manager, CLI login, vault, or
  provider-owned session is required?
- What command or UI check proves the service is usable enough for the intended
  product?

Design and handoff:

- What mockups, flows, screenshots, copy, states, assets, or component specs are
  needed before implementation?
- Does the coding agent need modular prototype code, snippets, fixtures, or
  component contracts?
- Which acceptance proof tells the product lead the coding work is done?

Product version:

- What is the smallest useful coherent product version?
- What does this product version need to prove?
- What can be faked, mocked, manually operated, or deferred without breaking the
  core promise?
- What must be real for the proof to matter?
- What should be removed from scope because it only serves later scale, polish,
  or automation?

## Ready Primitive Classes

Create only the primitives needed to make the intended product legible. A Ready
primitive is a typed, addressable, reusable unit of product knowledge, decision
state, workflow state, evidence, or governance context. Do not assume every
primitive has the same compiler authority.

Use these classes:

- `product_logic`: premises, intents, standards, and services that define the
  product behavior, constraints, or dependencies.
- `decision_workflow`: decision flags, blockers, drift, proof gaps, and
  readiness records. These use X-family ids because they are temporary process
  interrupts.
- `evidence_artifact`: resources, samples, snippets, designs, manifests,
  screenshots, and handoff records. These use A-family ids because they are
  durable supporting content. The artifact descriptor is the primitive; bulky or
  sensitive payload files are attachments or safe refs.
- `governance`: authority, process, agent, skill, and template records.

### Product-Logic Primitives

Premises:

- Capture why the product or feature should exist.
- Use `fields.premise_type` to clarify the discovery role. Valid values are in
  `ready/standard/vocabulary.yaml`.
- Put constraints, rules, quality bars, compliance needs, and measurement rules
  in `standard` records, not premise records.
- Include evidence provenance and confidence.
- Include product implications: what the premise requires, rules out, or
  prioritizes.
- If the premise is not clear enough to support intent work, create a discovery
  flag or decision flag.

Intents:

- Capture product promises.
- Use `fields.intent_type` to clarify the commitment shape. Valid values are in
  `ready/standard/vocabulary.yaml`.
- Keep `statement` concise, then decompose the promise into actor, trigger,
  action, expected end state, value, scope, non-scope, failure behavior,
  claim level, process decision, validation boundary, input/output types,
  input/output sample refs, required surfaces, and operating envelope.
- Use `claim_level` to name the strongest supported evidence posture, such as
  `concept`, `process_proof`, `simulation_baseline`, `fixture_validated`,
  `human_labeled_validated`, or `production_monitored`. Do not use it as
  Completion Proof.
- Put required services, governing standards, and intent dependencies in `refs`,
  not in duplicate `fields`.
- Every committed intent should trace to at least one premise unless explicitly
  marked exploratory.
- Quality-bearing or live-variable intents need an operating envelope.

Standards:

- Capture rules for implementation, behavior, measurement, judgment,
  maintenance, safety, privacy, accessibility, and proof.
- Make standards concrete enough to validate.
- Prefer `peer` refs when a standard governs a premise, intent, service, flag,
  or another standard. Use `child` standard refs only as fallback semantics for
  an older tree or when a record intentionally nests a subordinate standard.
- Avoid vague standards like "make it clean" or "good UX" unless the rule says
  what that means.
- Do not put deferred or future-only rules on active standards. Use a Ready
  branch or worktree for a coherent alternate future product. Use a flag on the
  current branch only when a decision, blocker, discrepancy, or proof gap needs
  attention.

Services:

- Capture dependencies required to build, prove, run, or monitor the product.
- Put `role` first in service fields and use top-level `status` for readiness
  state.
- Capture blockers, access requirements, credential location, evidence,
  proof required, input/output types and samples, implementation instructions,
  off-limits work, and failure modes when relevant.

### Decision/Workflow Primitives

Decision flags:

- Capture unresolved product-shaping ambiguity.
- Use them when a decision blocks product truth, proof, service readiness,
  resource readiness, access readiness, design readiness, or coding claim
  readiness.
- When decided, apply the resulting primitive or flag edits and remove the
  active decision flag.

Flags:

- Capture attention, blockers, drift, proof gaps, claim coordination, and
  Completion Proof for intended product truth that is unsatisfied or unproven.
- Keep coding readiness out of product-logic primitive bodies.
- A flag can be a primitive without being claimable implementation work, and it
  should not prescribe a coding delta.
- Seed and change flags become claimable only after status, blockers,
  top-level `claimable: true`, top-level Completion Proof, and workspace policy
  allow it.
- Intent Completion Proof is the durable Definition of Done for rebuilding the
  product. A flag's `completion_proof` is only the closure criterion for that
  temporary workflow record.
- Apps may derive unstored discrepancies by comparing Ready truth to code,
  evidence, generated views, assessments, or prior Ready commits. Store a flag
  when the discrepancy needs durable attention, blocker tracking, claim
  coordination, explicit Completion Proof, or review history.

### Evidence/Artifact Primitives

Artifact descriptors:

- Capture resources, samples, snippets, designs, manifests, screenshots,
  generated views, and handoff material.
- Name provenance, privacy state, freshness, expected use, and linked product
  or proof roles.
- Store large, binary, private, generated, or licensed payloads as attached
  files or safe refs instead of inline product truth.

### Governance Primitives

Governance records:

- Capture project authority, product process, agent behavior, skills, and
  templates.
- Constrain how other primitives may be edited, approved, claimed, or handed to
  coding agents.
- Do not store governance in artifact directories.

## Specialist Module Loading

Load modules based on gaps, not ceremony:

- Load evidence-resource review for every nontrivial product tree and any tree with
  missing samples, expected outputs, user-only data, public-source references,
  or resource provenance questions.
- Load access readiness when a service, environment, account, login, API key,
  OAuth app, provider session, CLI auth, or deployment target is required.
- Load design artifact readiness when the product has a UI, user workflow,
  visual review surface, component contract, or customer-facing copy.
- Load coding handoff readiness before making seed or change flags claimable.
- Load perspective review before implementation handoff, after major
  discovery changes, or when confidence is low.
- Load standard update when the user asks to update, upgrade, or migrate a
  product Ready tree to the latest Ready standard.

For substantial Ready tree creation, use subagents when available. Assign
distinct perspectives instead of duplicating the same review:

- psychological: motivation, trust, fear, desire, adoption, and user emotion;
- physical: real-world environment, devices, time, handoffs, manual steps, and
  operational constraints;
- logic: rules, data, state transitions, edge cases, and failure modes;
- evidence/resources: samples, public sources, generated data, licenses, and
  provenance;
- design: workflows, visual states, interaction details, assets, and component
  handoff;
- access/handoff: accounts, credentials, environments, blockers, proof, and
  coding-agent readiness.

Each subagent should state missing facts, risky assumptions, suggested cuts, and
the exact primitives, artifacts, services, or flags affected.

## Writing Rules

Use `.ready.yml` for product-logic primitive source records. Use specialized
Ready schemas such as `readyroom/flag/v1` and `readyroom/artifact/v1` when they
are the clearer machine contract for decision/workflow or evidence/artifact
primitives.

Tree directory rules:

- Use `product_directory` for `ready/product/`.
- Use `flags_directory` for `ready/flags/`.
- Use `settings_directory` for `ready/settings/`.
- Use `governance_directory` for `ready/governance/`.
- Keep canonical intended product truth in `ready/product/`.
- Keep temporary workflow records, discrepancy notes, blockers, and decisions in
  `ready/flags/`.
- Use Git commits, branches, and worktrees for product history, alternatives,
  and substantial hypothetical concepts.

Required product-logic primitive fields:

- `schema: readyroom/primitive/v1`
- `kind: primitive`
- `id`
- `type`
- `title`
- `status`
- `fields`
- `refs`

Product/workflow ownership is derived from file location under `ready/product/`
or `ready/flags/`, not from a primitive field. Settings files under
`settings_directory` are not primitive source records.

Do not add root `summary` to primitives. If summary text is truly source data,
it belongs under `fields.summary`; otherwise use the type's primary field.

Use `owner_notes` only for human product-owner annotations that should travel
with the record without becoming product truth. They are not requirements,
evidence, Completion Proof, or agent instructions. Ignore them for satisfaction
and enforcement; promote anything authoritative into typed `fields`, `refs`,
`artifacts`, or flags.

Premise evidence confidence is derived from linked evidence artifacts, not
stored on the premise. Do not write `fields.evidence_confidence` on premise
records. Every evidence artifact must carry `fields.confidence`; until weighted
evidence is defined, compiled premise confidence is the equal-weight average of
linked evidence artifact confidence values.

Artifact descriptors use `type` for the specific artifact subtype, not only a broad
storage bucket. Common artifact types include `customer_statement`,
`source_document`, `reference_resource`, `access_reference`, `review_protocol`,
`proof_corpus`, `code_snippet`, `design_artifact`, and `manifest`. Subtype data
belongs under `fields`; do not duplicate it in sibling blocks with local-only
ids.

Every artifact descriptor must carry `fields.purpose`, `fields.content`,
`fields.intended_use`, and `fields.format`. Evidence and proof descriptors must
also carry `fields.confidence` and `fields.provenance`. File-backed descriptors
must give every file a `path` and `role`.

One descriptor records one artifact purpose. A descriptor may list multiple
files only when those files are interchangeable versions or representations of
that same purpose. Files with different purposes, such as
buyer inputs, seller inputs, scoring config, expected scoring outputs, and
diagnostics, need separate descriptors.

Use `proof_corpus` for replayable inputs, configs, expected outputs, diagnostic
outputs, and negative cases used to prove or regress product behavior. Proof
corpus records must state their proof role, authority level, coverage,
dataset contract, oracle policy, replay commands, acceptance contract, and
limitations under `fields`. Do not use proof corpus success as a stronger claim
than its authority level supports.

Product and workflow records reference supporting artifacts through their own
`artifacts` lists. Artifact descriptors must not keep reverse product/workflow links
such as `linked_primitives`; artifact descriptors may relate to other artifacts
when one artifact depends on, derives from, includes, or carries the other.

Relationship rules:

- Store relationships in `refs`.
- Store structural roles only: `peer`, `parent`, and `child`.
- In compact refs, the role describes the target primitive's position relative
  to the current primitive. `parent` means the target parents the current
  record; `child` means the target is a child of the current record; `peer`
  means the target is lateral.
- If an app needs numeric relationship codes, use `0 = peer`, `1 = parent`,
  and `2 = child`. Source YAML should use the strings.
- Do not store semantic verbs such as `serves`, `requires`, `governed_by`,
  `refines`, or `questions` as ref roles.
- Derive reader phrases from source type, target type, and structural role.
  The semantic relationship display lookup lives in
  `ready/standard/vocabulary.yaml` and must include source-to-target and
  target-to-source phrases for the same stored edge. For example,
  `intent --parent--> premise` renders as the intent `serves` the premise and
  as the premise is `served by` the intent; `intent --child--> service` renders
  as `requires` / `required by`; `intent --child--> intent` renders as
  `fulfilled by` / `fulfills`; `intent --peer--> standard` renders as
  `governed by` / `governs`.
- Do not store an inverse ref for the same assertion. Choose one structural edge
  and let views invert parent/child labels when needed.
- Artifact descriptors only own artifact-to-artifact relationships. Product and
  workflow records point to artifacts through `artifacts`.
- Required services and governing standards belong in structural `refs`, not
  duplicated under intent `fields`. Standards usually govern through `peer`
  refs; existing `child` standard refs are retained as fallback display
  semantics.

Lifecycle rules:

- Do not store coding lifecycle state on product-logic primitives.
- Use decision/workflow primitives for discovery, seed, change, blocker, drift,
  proof gap, and question attention.
- Open seed and change flags are not coding-ready by default.
- A coding agent should only claim work when the relevant flag is ready,
  unblocked, claimable, and has top-level Completion Proof.

Artifact rules:

- Store proof corpora, source-shape resources, snippets, screenshots, mockups,
  manifests, and handoff material as artifact descriptors or as payloads
  referenced by those descriptors.
- Store generated or gathered proof data only when privacy, license, size, and
  provenance are acceptable, and state the proof role and authority level.
- Store sanitized excerpts, summaries, paths, hashes, or evidence refs for
  logs/traces when proof needs them; do not commit sensitive raw logs.
- Store references to bulky or sensitive materials, not copied source,
  transcripts, provider secrets, raw customer data, or diffs.
- Link artifacts to product-logic primitives, services, flags, or proof by
  descriptor id. Use raw paths only for direct source/file access.

Credential rules:

- Never commit raw secrets, tokens, cookies, private keys, or provider
  credentials into the Ready tree.
- Commit `.env.example`-style variable names and setup instructions when useful.
- Store local secrets in untracked `.env.local` files, provider-owned sessions,
  OS keychain, 1Password, Vault, Supabase/Vercel/GitHub secret stores, or another
  user-approved service accessible through a CLI or official SDK.
- Record only safe secret-location references: variable names, storage system,
  owner, required scope, setup status, and verification command.

## Cutting The Product Version

After drafting the tree, cut it down.

Keep only product truth that is required to prove the intended product version:

- the core user problem or desire;
- the minimal solution path;
- the standards that protect trust and proof;
- the services and accounts that must exist now;
- the samples, resources, designs, snippets, and artifacts needed to understand
  or prove the target;
- the flags needed to make gaps visible.

Move everything else out of the current product tree. Use a Ready branch or worktree for a
substantial hypothetical concept that should be evaluated as a coherent possible
end state. Use decision flags or flags on the current branch only when the team
needs to choose, prove, coordinate, or block against that concept.

Good cuts are explicit. Say what was removed and why.

## Completion Checklist

A Ready tree is usable when:

- The intended product version is coherent and bounded.
- Active intents trace to premises.
- Required standards and services are represented.
- Service blockers, proof required, access needs, and implementation
  instructions are visible.
- Samples, resources, expected outputs, and difficult cases exist or are blocked
  by specific user-only asks.
- Design artifacts, interaction states, copy, assets, and modular snippets exist
  when coding depends on them.
- Required accounts, credentials, environments, and secret-location references
  are available or explicitly blocked.
- Unknowns are decision flags, low-confidence fields, or flags.
- Coding agents receive the resolved intended product state rather than only
  discrepancy context.
- Claimable flags have clear scope, constraints, acceptance proof, resources,
  environment setup, and blocker policy.
- Artifact descriptors reference sensitive or bulky source safely.
- The user can review the tree and understand what is in, out, blocked, and
  deferred.

If any item is missing, keep the tree draft or blocked rather than pretending it
is ready.
