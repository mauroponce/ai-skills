---
name: dev-plan
description: Convert a sufficiently defined software initiative into an executable repository-aware engineering plan. Inspect the actual code, choose appropriate seams, break work into small vertical slices, define tests/verification and rollout, and keep the plan in chat or personal local notes when another session needs it. Use after dev-discovery and before implementation.
---

# DEV Plan

Use this skill to decide **how** to implement already-understood behavior.

## Invocation contract

The user can invoke this after discovery, an active `dev-debug` diagnosis, or selected `dev-rails-audit` findings without repeating paths, conventions, or finding text. Resolve the active initiative from active-chat or personal context, current repository evidence, and any active diagnosis or `RAILS-###` IDs in the same conversation. Verify finding evidence against current code; ask only when multiple plausible initiatives or a material decision remain unresolved.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

Use [the Codex interactive decision policy](../references/interactive-decision-policy.md) for consequential questions and the active session's Plan-mode/write boundary. Do not require a slash command before using this skill.

Consume confirmed requirements from active chat, personal notes, or existing project documentation, an active diagnosis or selected audit findings when intentionally chained in the same chat, and verified repository structure. For audit findings, preserve the cited evidence, uncertainty, production constraints, and measurement needed; do not repeat a discovery questionnaire or treat a candidate as confirmed. For a diagnosed bug, plan root-cause elimination, regression prevention, relevant tests, and rollout/migration concerns rather than repeating discovery. If a material product, security, data, contract, or architecture decision remains open, investigate first and resolve it before finalizing the plan. Ask only when evidence cannot settle it; recommend a supported option. Do not interview about ordinary implementation details. A plan with an unresolved material decision is not ready for implementation.

For a selected architecture finding, compare the smallest Rails/repository-native correction with the proposed boundary, state the pressure each addresses and its carrying cost, and plan incremental migration, behavior preservation, transaction/async safety, and verification where relevant. Do not turn the audit's directional recommendation into an unexamined global style rule.

Follow [workflow governance](../references/workflow-governance.md). This skill produces the implementation plan in chat by default; save it in the personal workspace only when cross-chat use is likely. It does not modify the target repository.

Read the [stack-aware engineering router](../references/engineering/README.md) and load only playbooks selected by the detected stack and task risk. Apply correctness/security/data integrity first, then explicit initiative decisions, repository architecture and conventions, demonstrated architectural pressure, framework/database idioms, and general preference. Surface a dangerous local convention rather than reproducing it.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal initiative preference, otherwise English. Record a cross-chat preference only if useful. Never infer note language merely from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve inputs

Resolve the active initiative and start with:

- active behavior contract in chat or personal notes;
- relevant implementation code and tests;
- applicable architecture/documentation for the target seams.

Load `AGENTS.md`, ADRs, and product/design context only when they constrain the change.

Do not plan from the spec alone when the repository exists. Verify the proposed seams against actual code.

## 2. Recheck the planning gate

Planning may proceed with minor unknowns, but do not bury unresolved product/behavior/security/data decisions inside the plan.

If a material decision is still open:

- investigate facts first;
- ask the user only if a decision remains;
- clarify the active behavior contract in chat or personal notes before finalizing the plan.

## RED FLAGS

- Recommending a gem without checking existing capabilities or repository conventions.
- Proposing schema changes without inspecting schema and migration history.
- Using version-sensitive Rails patterns without checking the installed version and authoritative source when needed.
- Planning from generic best practices while implementation still needs major invention.
- Ignoring migration, rollback, or old/new code compatibility for production data changes.

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

- use an outside-repository disposable location or an isolated test environment;
- clearly label it non-production;
- record the conclusion/evidence in the chat plan or personal note;
- do not let spike code silently become production implementation.

Do not create a spike for questions that ordinary code reading or a small test can answer.

## 7. Keep the plan in the right place

For a same-chat handoff, provide an executable plan in conversation without creating a file. For a long task or planned new chat, save a concise personal plan under `~/.codex/workspaces/<project-key>/plans/`, optionally using `assets/PLAN.template.md` as a guide. Include confirmed behavior, ordered vertical slices, relevant files, tests, rollout constraints, open risks, and the current Git revision. Do not create or update repository `PLAN.md`, `SPEC.md`, or workflow state.

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

For cross-chat work, note the material decisions, current Git revision, open questions, and next action in the personal plan. Same-chat work needs no workflow-state file. Revalidate the plan before implementation.

## 10. Finish the phase

Report concisely, in the conversation language:

- planned approach;
- key technical decisions/trade-offs;
- number/order of slices;
- important risks/rollout concerns;
- personal plan path, only if one was useful;
- whether the work is ready for `dev-implement`.

Do not automatically invoke another skill.

At handoff, recommend the next skill and execution tier using [execution policy](../references/execution-policy.md). A strong plan may make the implementation cheaper than planning.

## Definition of Done

The task is complete when the plan is grounded in confirmed requirements, current repository seams, and applicable stack guidance; material security/data/production decisions are resolved or explicit; slices and verification are executable; and cross-chat context is saved personally only when useful. Explain significant architecture, data integrity, failure, or production trade-offs concisely.
