---
name: ready-access-readiness
version: 0.1.0
description: Make accounts, credentials, environments, secret storage, and service setup ready for coding agents without committing secrets.
---

# Access Readiness

Use this module when a Ready tree depends on accounts, API keys, OAuth apps,
provider sessions, databases, queues, deployment targets, CLIs, local
environment files, or other service access.

## Responsibilities

- Identify every service, account, credential, environment, permission, and CLI
  login needed for the intended product.
- Record service readiness as product truth, not as a private assumption.
- Create or request `.env.example` entries for variable names and non-secret
  setup hints.
- Direct the user to put real secrets in a safe, accessible place: untracked
  `.env.local`, OS keychain, 1Password, Vault, Supabase/Vercel/GitHub secret
  stores, provider-owned sessions, or another approved secret store accessible
  through a CLI or official SDK.
- Record safe secret-location references only: variable name, storage system,
  owner, required scope, setup status, and verification command.
- Create blocked flags when access is missing and coding would stall.

## Safety Rules

- Do not ask the user to paste raw secrets into chat.
- Do not commit tokens, cookies, private keys, API keys, OAuth secrets, database
  passwords, personal access tokens, or raw credential files.
- Do not store secrets in primitives, artifacts, samples, logs, screenshots, or
  generated coding handoffs.
- If a credential is accidentally exposed, stop and tell the user to rotate it.

## Account Readiness Checklist

For each required service, capture:

- service name and environment;
- account owner;
- top-level service `status`;
- blockers when status is blocked, draft, or not currently usable;
- credential type and safe storage location;
- current evidence;
- proof required;
- input and output types plus representative sample refs;
- implementation instructions or external setup docs;
- off-limits work;
- required scopes or permissions;
- setup steps the user must complete;
- setup steps the agent can complete safely;
- verification command or UI check;
- fallback or simulation policy;
- failure modes that coding agents should expect.

## User Support

Make account setup easy for a distracted user:

- provide exact steps in the smallest useful order;
- say which account they should use;
- say what not to paste into chat;
- provide the variable names to add;
- provide the command to confirm access;
- explain what coding work is blocked until the step is done.

## Completion Check

The module is complete when every required service has a top-level status,
credential-location reference or blocked reason, setup path, verification check,
implementation instructions, and coding-agent-visible failure policy.
