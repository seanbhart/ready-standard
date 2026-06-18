---
name: ready
version: 0.3.2
description: Lead creation of a Ready product tree from docs, code, or discovery, then make it complete enough for coding agents to build without avoidable blockers.
---

# Ready Skill

Use this skill to create or revise a Ready product tree. The skill is about the
Ready standard and about acting as a strong product leader: discover the real
problem, shape the smallest useful solution, gather the evidence and resources
needed to build it, identify the services and standards that make it safe, and
cut away what is unnecessary for the next product stage.

This is an orchestration skill. Load specialist Ready Skill modules when the
tree needs focused work:

- [modules/evidence-resource-review.md](modules/evidence-resource-review.md) -
  evidence, sample data, online resources, generated fixtures, and user-only
  information.
- [modules/access-readiness.md](modules/access-readiness.md) -
  accounts, credentials, environments, secret-location references, and setup
  verification.
- [modules/design-artifact-readiness.md](modules/design-artifact-readiness.md) -
  designs, mockups, screenshots, flows, component specs, and modular UI snippets.
- [modules/coding-handoff-readiness.md](modules/coding-handoff-readiness.md) -
  work-package readiness, blockers, acceptance proof, and coding-agent
  instructions.
- [modules/perspective-review.md](modules/perspective-review.md) -
  subagent review from psychological, physical, logical, evidence, design, and
  access perspectives.

The portable package manifest is [manifest.yaml](manifest.yaml).
Use it when passing the Ready Skill set to agents in another project: copy the
entrypoint, module files, and package README, then record the copied versions in
that project's standard-resource manifest.

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
  end-state/
    manifest.yaml
    README.md
  m1/
    manifest.yaml
    README.md
    premises/
    intents/
    standards/
    services/
    flags/
    artifacts/
      samples/
      resources/
      snippets/
      designs/
      manifests/
```

The root `manifest.yaml` must include a stage registry:

```yaml
schema: readyroom/product-tree-root/v1
product: example
source_root: ready
default_stage: m1
stages:
  - id: m1
    title: M1
    path: ready/m1
    manifest: ready/m1/manifest.yaml
    kind: normal
    status: active
    order: 10
    default_candidate: true
    coding_claims_enabled: false
  - id: end-state
    title: End State
    path: ready/end-state
    manifest: ready/end-state/manifest.yaml
    kind: horizon
    status: horizon
    order: 9999
    default_candidate: false
    coding_claims_enabled: false
```

Use `kind: normal` for buildable product stages. Use `kind: horizon` for
future concept shelves such as `end-state`. Do not rely on directory names or
alphabetical order to decide the default stage.

Primitive source records are `.ready.yml` files with:

```yaml
schema: readyroom/primitive/v1
kind: primitive
id: I-001
type: intent
title: Human-readable title
milestone: m1
status: draft
summary: Concise product-truth statement
fields: {}
refs: []
artifacts: []
owner_notes: []
```

Reader-friendly docs, app views, work packages, tickets, and briefs compile from
the tree. They are not the primitive source of truth.

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
- Preserve uncertainty as question cards, draft fields, low confidence, or flags.
- Prefer a smaller next stage that proves the core promise.
- Cut nice-to-have work until it clearly supports the next stage.
- Keep implementation details out of primitives unless they are true product
  constraints, interfaces, standards, artifacts, services, or proof expectations.

Docs, code, conversation, public sources, generated samples, designs, and model
output are evidence. They do not automatically become approved product truth.

## Input Modes

Ready tree creation starts from one of three modes.

### Human Documentation Only

Use this mode when the project has planning docs, specs, decks, notes, issue
lists, design docs, or strategy prose, but no reliable codebase signal.

Process:

1. Inventory the docs and note source age, author intent, and confidence.
2. Extract premise candidates from problems, actors, contexts, constraints,
   motivations, risks, and success claims.
3. Extract intent candidates from user promises, workflows, outcomes, and
   requirements.
4. Extract standards from explicit rules, quality bars, compliance needs,
   measurement rules, and non-negotiable behavior.
5. Extract services from dependencies needed to build, prove, run, or monitor
   the product.
6. Identify missing samples, resources, designs, accounts, credentials, and
   environments needed to make the next stage buildable.
7. Preserve conflicts instead of averaging them.
8. Ask the user to resolve only product-shaping gaps that affect the next stage.
9. Create draft or active `.ready.yml` primitives with evidence confidence.
10. Create flags or question cards where work is not ready.

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
   should be cut from the next stage.
7. Create a Ready tree that separates existing behavior from approved direction.
8. Use flags or question cards for gaps that code cannot answer.

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
6. Choose the next product stage and add it to the root stage registry.
7. Cut scope until the next stage can prove the core promise.
8. Identify standards, services, artifacts, sample data, resources, accounts,
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
- What command or UI check proves the service is usable enough for the next
  stage?

Design and handoff:

- What mockups, flows, screenshots, copy, states, assets, or component specs are
  needed before implementation?
- Does the coding agent need modular prototype code, snippets, fixtures, or
  component contracts?
- Which acceptance proof tells the product lead the coding work is done?

Next stage:

- What is the smallest useful stage?
- What does this stage need to prove?
- What can be faked, mocked, manually operated, or deferred without breaking the
  core promise?
- What must be real for the proof to matter?
- What should be removed from scope because it only serves later scale, polish,
  or automation?

## Ready Primitive Types

Create only the primitives needed to make the next stage legible.

Premises:

- Capture why the product, milestone, or feature should exist.
- Include evidence provenance and confidence.
- Include product implications: what the premise requires, rules out, or
  prioritizes.
- If the premise is not clear enough to support intent work, create a discovery
  flag or question card.

Intents:

- Capture product promises.
- Name actor, trigger, action, expected end state, value, scope, non-scope,
  failure behavior, inputs, outputs, required services, required artifacts, and
  required standards when those details matter.
- Every committed intent should trace to at least one premise unless explicitly
  marked exploratory.
- Quality-bearing or live-variable intents need an operating envelope.

Standards:

- Capture rules for implementation, behavior, measurement, judgment,
  maintenance, safety, privacy, accessibility, and proof.
- Make standards concrete enough to validate.
- Avoid vague standards like "make it clean" or "good UX" unless the rule says
  what that means.

Services:

- Capture dependencies required to build, prove, run, or monitor the product.
- Name readiness by environment, access requirements, credential location,
  proof policy, failure modes, simulation rules, observability, privacy, owner,
  and readiness gaps when relevant.

Question cards:

- Capture unresolved product-shaping ambiguity.
- Use them when a decision blocks product truth, proof, service readiness,
  resource readiness, access readiness, design readiness, or coding claim
  readiness.
- When answered, apply the resulting primitive or flag edits and remove the
  active question card.

## Specialist Module Loading

Load modules based on gaps, not ceremony:

- Load evidence-resource review for every nontrivial product tree and any tree with
  missing samples, expected outputs, user-only data, public-source references,
  or resource provenance questions.
- Load access readiness when a service, environment, account, login, API key,
  OAuth app, provider session, CLI auth, or deployment target is required.
- Load design artifact readiness when the product has a UI, user workflow,
  visual review surface, component contract, or customer-facing copy.
- Load coding handoff readiness before making seed or delta flags claimable.
- Load perspective review before implementation handoff, after major
  discovery changes, or when confidence is low.

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

Use `.ready.yml` for primitive source records.

Stage registry rules:

- Use `stages` in `ready/manifest.yaml` as the authoritative list of stages.
- Give every stage `id`, `title`, `path`, `manifest`, `kind`, `status`, `order`,
  `default_candidate`, and `coding_claims_enabled`.
- Prefer stage kinds `normal`, `horizon`, `experiment`, `archive`, and
  `template`.
- Set `default_stage` when the product lead has chosen a specific stage.
- If `default_stage` is absent, tools choose the highest `order` normal stage
  with `default_candidate: true`, then the highest `order` normal stage.
- Keep `end-state` or other horizon stages as `kind: horizon` and
  `default_candidate: false`.

Required primitive fields:

- `schema: readyroom/primitive/v1`
- `kind: primitive`
- `id`
- `type`
- `title`
- `milestone` (the owning stage id; the v1 primitive field name is still
  `milestone`)
- `status`
- `summary`
- `fields`
- `refs`

Relationship rules:

- Store relationships in `refs`.
- Store one directed edge.
- Use approved roles: `serves`, `contains_premise`, `requires`, `governed_by`,
  and `questions`.
- Store primary primitive-tree relationships in canonical source direction:
  - `intent --serves--> premise`
  - `intent --contains_premise--> premise`
  - `intent --requires--> service`
  - `intent --governed_by--> standard`
- Do not store inverse tree edges such as `premise --serves--> intent`,
  `service --serves--> intent`, or `standard --serves--> intent`. Views derive
  inverse labels from the one canonical edge.
- Compact refs infer `from` as the current primitive id. Use compact refs only
  when the current primitive is the edge source; otherwise write explicit `from`
  and `to`.
- `required_services` and `required_standards` fields are reader aids; matching
  canonical refs are still required for graph traversal and validation.
- Views can derive inverse labels.

Lifecycle rules:

- Do not store coding lifecycle state on primitives.
- Use flags for discovery, seed, delta, blocker, drift, proof gap, and question
  attention.
- Open seed and delta flags are not coding-ready by default.
- A coding agent should only claim work when the relevant flag is ready,
  unblocked, claimable, and has Completion Proof.

Artifact rules:

- Store samples, source-shape resources, snippets, screenshots, mockups,
  manifests, and handoff material as artifacts.
- Store generated or gathered sample data only when privacy, license, size, and
  provenance are acceptable.
- Store sanitized excerpts, summaries, paths, hashes, or evidence refs for
  logs/traces when proof needs them; do not commit sensitive raw logs.
- Store references to bulky or sensitive materials, not copied source,
  transcripts, provider secrets, raw customer data, or diffs.
- Link artifacts to primitives, services, flags, or proof by id or path.

Credential rules:

- Never commit raw secrets, tokens, cookies, private keys, or provider
  credentials into the Ready tree.
- Commit `.env.example`-style variable names and setup instructions when useful.
- Store local secrets in untracked `.env.local` files, provider-owned sessions,
  OS keychain, 1Password, Vault, Supabase/Vercel/GitHub secret stores, or another
  user-approved service accessible through a CLI or official SDK.
- Record only safe secret-location references: variable names, storage system,
  owner, required scope, setup status, and verification command.

## Cutting The Next Stage

After drafting the tree, cut it down.

Keep only work that is required to prove the next stage:

- the core user problem or desire;
- the minimal solution path;
- the standards that protect trust and proof;
- the services and accounts that must exist now;
- the samples, resources, designs, snippets, and artifacts needed to understand
  or prove the target;
- the flags needed to make gaps visible.

Move everything else out of the next stage. Use future milestone notes, draft
primitives, question cards, or flags when the idea is useful but not needed now.
Record that future work in a later `normal` stage, an `experiment` stage, or a
`horizon` stage rather than leaving it hidden in chat.

Good cuts are explicit. Say what was removed and why.

## Completion Checklist

A Ready tree is usable when:

- The next stage is named and bounded.
- Active intents trace to premises.
- Required standards and services are represented.
- Service readiness gaps are visible.
- Samples, resources, expected outputs, and difficult cases exist or are blocked
  by specific user-only asks.
- Design artifacts, interaction states, copy, assets, and modular snippets exist
  when coding depends on them.
- Required accounts, credentials, environments, and secret-location references
  are available or explicitly blocked.
- Unknowns are question cards, low-confidence fields, or flags.
- Coding-ready work is gated by seed or delta flags, not primitive prose.
- Claimable flags have clear scope, constraints, acceptance proof, resources,
  environment setup, and blocker policy.
- Artifacts are referenced without storing sensitive or bulky source.
- The user can review the tree and understand what is in, out, blocked, and
  deferred.

If any item is missing, keep the tree draft or blocked rather than pretending it
is ready.
