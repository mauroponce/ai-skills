---
name: dev-plan
description: Convert a sufficiently defined software initiative into an executable repository-aware engineering plan. Inspect the actual code, choose appropriate seams, break work into small vertical slices, define tests/verification and rollout, and write PLAN.md for non-trivial work. Use after dev-discovery and before implementation.
---

# DEV Plan

Use this skill to decide **how** to implement already-understood behavior.

## Invocation contract

The user can invoke this after discovery without repeating paths or conventions. Resolve the active initiative from workflow state, SPEC, and repository evidence; ask only when multiple plausible initiatives or a material decision remain unresolved.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is a decision-oriented planning skill intended to start in Plan mode (`/plan`). It cannot switch the host's mode. See [the shared interaction policy](../references/interactive-decision-policy.md) for the Codex and Claude Code interaction rules, including when to leave read-only Plan mode to save artifacts.

Consume decisions from `SPEC.md` and verified repository structure. If a material product, security, data, contract, or architecture decision remains open, investigate first and resolve it before finalizing the plan. Ask only when evidence cannot settle it; recommend a supported option. Do not interview about ordinary implementation details. A plan with an unresolved material decision is not ready for implementation.

Follow [workflow governance](../references/workflow-governance.md). This skill owns `PLAN.md` and updates the initiative workflow state when plan readiness or a material implementation decision changes.

Read the [stack-aware engineering router](../references/engineering/README.md) and load only playbooks selected by the detected stack and task risk. Apply correctness/security/data integrity before repository convention, then explicit initiative decisions, repository architecture, framework/database idioms, and general preference. Surface a dangerous local convention rather than reproducing it.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve inputs

Resolve the active initiative and start with:

- active `SPEC.md`;
- relevant implementation code and tests;
- applicable architecture/documentation for the target seams.

Load `AGENTS.md`, ADRs, and product/design context only when they constrain the change.

Do not plan from the spec alone when the repository exists. Verify the proposed seams against actual code.

## 2. Recheck the planning gate

Planning may proceed with minor unknowns, but do not bury unresolved product/behavior/security/data decisions inside the plan.

If a material decision is still open:

- investigate facts first;
- ask the user only if a decision remains;
- update the spec before finalizing the plan.

## 3. Choose the smallest coherent design

Prefer:

- existing module boundaries;
- existing patterns/framework conventions;
- simple changes with clear ownership;
- deep modules / narrow interfaces where a new abstraction is genuinely needed;
- local changes over new cross-cutting infrastructure.

Avoid speculative abstraction, premature generalization, and architecture rewrites not required by the initiative.

When a requested implementation mechanism is unnecessary, propose the simpler mechanism and explain the trade-off rather than blindly planning the requested technology.

## 4. Plan vertical slices

Break non-trivial work into small, independently verifiable slices that move through the required layers rather than large horizontal phases.

Prefer slices like:

```text
accept webhook → persist dedupe key → test duplicate behavior
```

rather than:

```text
build all models → build all services → build all controllers → write tests later
```

Each slice should state:

- intended behavior;
- relevant files/modules or seams;
- dependencies/blockers;
- tests/verification;
- completion signal.

Order slices so early work reduces uncertainty and establishes usable feedback loops.

## 5. Cover relevant engineering concerns

Include only what applies:

- module/API changes;
- schema/data changes;
- migrations/backfills;
- authorization/security/privacy;
- external contracts;
- async jobs/events;
- concurrency/idempotency;
- failure/retry/recovery behavior;
- performance/caching;
- observability;
- feature flags/rollout;
- backward compatibility;
- cleanup/deprecation;
- test strategy;
- documentation changes.

For applicable Rails, React, database, security, production, and testing lenses, record the decision or verification needed in the plan rather than pasting a generic checklist. Treat schema changes in production as migration-safety work; treat auth, OAuth/OIDC, payments, jobs, multi-tenancy, public contracts, and concurrency as elevated-risk triggers.

## 6. Use disposable experiments when facts require execution

If a technical question cannot be settled by reading/docs and a small executable experiment can settle it:

- create a narrowly scoped disposable spike under `.scratch/<initiative>/` or the repository's existing scratch convention;
- clearly label it non-production;
- record the conclusion/evidence in the plan;
- do not let spike code silently become production implementation.

Do not create a spike for questions that ordinary code reading or a small test can answer.

## 7. Decide whether a PLAN file is warranted

For a genuinely tiny, local, low-risk change, a separate `PLAN.md` may be unnecessary. In that case:

- state explicitly that the change is small enough to implement directly;
- put only minimal implementation notes in the existing spec if useful;
- do not create process documents for their own sake.

For non-trivial work, create/update:

```text
work/<initiative>/PLAN.md
```

using `assets/PLAN.template.md` as guidance.

The plan must be self-contained enough that a fresh agent session can execute it by reading the repository plus `SPEC.md`/`PLAN.md`.

## 8. Define verification before implementation

For each slice and for final completion, specify actual commands/checks where they can be inferred from the repo:

- targeted tests;
- integration/system tests;
- lint/format;
- typecheck;
- build;
- migration checks;
- security/static analysis;
- manual/runtime verification when necessary.

Do not invent command names; derive them from the repo or mark them to be resolved by implementation.

## 9. Plan status

Update the SPEC workflow state with plan reference, material implementation decisions/open questions, and the next action. Do not record implementation progress during planning.

## 10. Finish the phase

Report concisely, in the conversation language:

- planned approach;
- key technical decisions/trade-offs;
- number/order of slices;
- important risks/rollout concerns;
- plan path;
- whether the work is ready for `dev-implement`.

Do not automatically invoke another skill.

## Definition of Done

The task is complete when the plan is grounded in the active SPEC, repository seams, and applicable stack guidance; material security/data/production decisions are resolved or explicit; slices and verification are executable by a fresh chat; `PLAN.md` is current when warranted; and SPEC workflow state identifies implementation readiness.
