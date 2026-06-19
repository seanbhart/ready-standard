---
name: ready-evidence-resource-review
version: 0.1.0
description: Gather evidence, sample data, public resources, generated fixtures, and user-only information needed to make a Ready tree buildable.
---

# Evidence Resource Review

Use this module when a Ready tree needs evidence, sample data, expected outputs,
source-shape references, public resources, or private information that only the
user can provide.

## Responsibilities

- Inventory every product-logic primitive, service, decision/workflow primitive,
  and evidence/artifact primitive that depends on a
  sample, resource, data source, screenshot, export, document, benchmark,
  external API shape, or expected output.
- Gather safe public resources when they can answer the gap. Prefer official
  docs, public datasets, open-source examples, published schemas, API specs,
  standards bodies, and permissively licensed sources.
- Generate synthetic fixtures when the product behavior can be proven without
  private or real user data.
- Ask the user for private or user-only material only when it materially changes
  the next stage.
- Store resources as evidence/artifact primitive records or safe references,
  not as hidden chat memory.
- Record source, license or terms risk, retrieval date, privacy state,
  freshness, generation method, schema, and expected outputs.

## User Support

Assume the user is busy or tired. Do not say "send sample data" without help.
Provide a short, concrete ask:

- what to export or capture;
- where to find it;
- which format is best;
- what fields can be redacted;
- what not to include;
- a safe filename or artifact target;
- how the sample will be used;
- what happens if the user cannot provide it.

When several asks exist, rank them by implementation value. Ask for the one or
two samples that most reduce coding-agent ambiguity.

## Sample Types

Use at least these categories:

- happy-path input sample;
- expected output for that input;
- difficult edge case;
- failure or unavailable state;
- empty or first-run state;
- permission or access-denied state;
- stale, malformed, or conflicting source state;
- proof evidence that should close a flag;
- proof evidence that should not close a flag.

## Sample Purposes

Keep sample purposes distinct:

- development samples help coding agents build and debug locally;
- qualification samples prove the product behavior is correct enough for review;
- health samples support ongoing checks after the feature exists.

One file can serve more than one purpose only when that does not hide coverage
gaps. If the same sample is reused, name every purpose it serves.

## Storage Rules

- Put generated and sanitized fixture files under the milestone artifact tree.
- Use `samples/` for typed sample data, `resources/` for gathered reference
  resources, `manifests/` for machine-readable support manifests, `designs/` for
  visual artifacts, and `snippets/` for intentional handoff code or component
  contracts. Each reusable item should have an evidence/artifact primitive
  record when tools need to address, search, link, or validate it directly.
- Do not commit raw customer data, private transcripts, provider secrets,
- browser cookies, sensitive raw logs, large binary assets, or copied source
  excerpts.
- Use sanitized excerpts, generated summaries, hashes, paths, or evidence refs
  when proof needs log or trace evidence.
- Use safe refs for bulky, sensitive, licensed, or private resources.

## Online Resources

When online research is needed, gather current information before relying on it.
Record the URL, publisher, retrieval date, license or terms concern, and the
specific product decision it supports. If source authority is unclear, keep the
result as evidence with lower confidence instead of product truth.

## Completion Check

The module is complete when every build-critical primitive or flag has one of:

- attached sample/resource artifact primitives;
- generated fixtures with expected outputs;
- public-source references with provenance;
- a precise user-only ask;
- a blocked flag or question card explaining why the gap remains.
