---
name: dev-discovery
description: Understand a software change before planning or coding. Inspect the repository and existing product/design specs first, resolve facts from code, interview the user only about consequential unknowns, and create/update minimal durable engineering context and the initiative spec. Use for new projects, features, refactors, integrations, or non-trivial bug work.
---

# DEV Discovery

Use this skill to establish shared technical understanding before an implementation plan is written.

## Invocation contract

The user only needs to state the intended software change and relevant task-specific facts. If `dev-explore` already mapped this area in the same Codex conversation, use that map as context and verify the relevant current code rather than repeating basic reconnaissance. Exploration remains an input; this skill still defines the requested change and its constraints. Recover the active initiative, relevant technical context, production implications, and material questions from the repository.

The user's explicit instructions take precedence over workflow defaults in this skill.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## Core rule

**Facts are the agent's job to investigate. Decisions that cannot be derived safely are the user's job to make with the agent's help.**

Do not start implementation during discovery unless the user explicitly asks to collapse phases for a trivial task.

Follow [workflow governance](../references/workflow-governance.md): begin with high-signal project context, persist only durable technical knowledge, and update initiative workflow state when discovery materially changes it.

Use the [stack-aware engineering router](../references/engineering/README.md). Detect the stack from high-signal repository evidence, then load only the applicable Rails, React, PostgreSQL/MySQL, security, production-safety, and testing playbooks. Do not load an irrelevant handbook for a local low-risk change.

## User interaction

Use [the Codex interactive decision policy](../references/interactive-decision-policy.md) for consequential questions and the active session's Plan-mode/write boundary. Do not require a slash command before using this skill.

Investigate code, tests, configuration, documentation, and current behavior before asking. Treat supplied issue links, documents, API references, logs, and code links as additional evidence; verify them against the repository where appropriate. Ask only about unresolved externally visible behavior or material business, security, data, API, compatibility, rollout, or hard-to-reverse architecture decisions. Recommend an option when repository evidence supports it. Do not ask the user where something is implemented; search the repository.

## 1. Resolve the task and existing sources of truth

Resolve the active initiative from the user request, current context, or an existing `work/*/SPEC.md`.

Start with the active SPEC (if any), local instructions/README, relevant architecture documentation, and the implementation surfaces named by the request. Expand into only relevant durable context such as:

- root/local `AGENTS.md`;
- existing `work/<initiative>/SPEC.md`;
- `product/CONTEXT.md`;
- `design/DESIGN_SYSTEM.md` when UI/design behavior matters;
- `engineering/ARCHITECTURE.md` or equivalent;
- README/developer docs;
- relevant ADRs;
- relevant code/tests/configuration.

If a UX/product spec already defines behavior, treat it as an input. Do not create a second competing requirements document.

## 2. Inspect the repository before asking questions

Follow the relevant execution path through the codebase. Inspect as appropriate:

- entry points/routes/controllers/handlers;
- domain/service/module boundaries;
- data models/schema/migrations;
- authorization/authentication;
- external APIs/integrations;
- jobs/queues/events;
- error handling;
- tests and fixtures;
- configuration/environment;
- observability/logging/metrics;
- deployment/runtime constraints;
- recent relevant git history when it clarifies intent.

Do not perform a full-repo archaeology pass when the change is local.

For a new/greenfield repo, inspect existing scaffolding before interviewing about stack choices.

## 3. Build or refresh the technical profile

Start with high-signal stack files when present: `.ruby-version`, `Gemfile`/lockfile, Rails config/routes, `config/database.yml`, schema/migrations, `package.json`/lockfiles/build config, frontend entry points, tests/CI, deployment files, job configuration, and auth/authorization/observability seams. Determine only facts useful beyond this feature:

- backend runtime/framework/version and application shape;
- authentication, authorization, jobs, cache, storage, and local architecture conventions;
- frontend integration/version/build/state/component/testing conventions;
- database engine/version when discoverable, schema format, important extensions/constraints/index conventions;
- testing frameworks and CI execution;
- stable production/deployment, queue, feature-flag, and monitoring constraints.

Persist stable findings in `engineering/ARCHITECTURE.md` when it exists or the information will guide future work. Keep feature decisions in SPEC/PLAN; do not create an infrastructure inventory for its own sake.

## 4. Build a technical evidence ledger

Internally distinguish:

- **Known:** directly supported by code/config/docs/tests/user input.
- **Inferred:** strongly suggested by evidence.
- **Assumed:** temporary choice pending confirmation.
- **Unknown:** unresolved.
- **Conflicting:** sources disagree.

Never disguise a guess as architecture.

## 5. Recover the real requirement

If the request is phrased as an implementation instruction, identify the behavior/outcome behind it.

Example:

```text
Requested implementation: add Redis locking
Underlying requirement to verify: prevent duplicate concurrent processing of the same webhook
```

Preserve hard constraints, but do not mistake a proposed mechanism for the requirement unless it is explicitly fixed.

## 6. Interview only on consequential unknowns

Prefer one question at a time. Group only independent decisions.

Do not ask about facts the repo can answer.

Ask when ambiguity materially affects:

- externally observable behavior;
- domain/business rules;
- API/data contracts;
- authorization/security/privacy;
- consistency/concurrency/idempotency;
- durability/data loss risk;
- migration/backward compatibility;
- performance/SLO expectations;
- rollout/operational constraints;
- architecture that is expensive to reverse;
- scope/non-goals.

For each non-obvious technical decision, offer a recommended option and concise trade-off when possible.

Do not block on low-risk reversible choices that are already guided by repository convention.

## 7. Maintain minimal durable engineering context

Prefer existing documentation conventions.

### `AGENTS.md`

Create or modify it only when a stable repository-wide engineering rule is genuinely missing. If absent, create a lean root file or merge in the guidance from `assets/AGENTS.engineering-section.md`.

If present, preserve it and add only missing durable guidance. Do not copy an entire architecture guide into `AGENTS.md`.

### `engineering/ARCHITECTURE.md`

Create/update it only when stable architectural knowledge would help future work. Use `assets/ARCHITECTURE.template.md` as guidance.

Do not invent sections or details merely to complete the template.

### `work/<initiative>/SPEC.md`

If an initiative spec already exists from product/UX work, enrich it only where necessary to make engineering requirements/constraints explicit. Do not rewrite validated product intent into a separate technical version.

If no suitable spec exists, create one using `assets/SPEC.template.md`.

Keep implementation sequencing out of the spec; that belongs in `dev-plan` / `PLAN.md` for non-trivial work.

### ADRs / durable decisions

Create an ADR under `engineering/decisions/` only when a decision is:

- materially expensive to reverse;
- non-obvious without context;
- a genuine trade-off with durable architectural consequences.

Most discovery sessions should create zero ADRs. Do not create ADRs for ordinary reversible implementation choices.

## RED FLAGS

- Planning from generic stack assumptions before inspecting the repository.
- Treating an unusual design as a mistake without checking relevant Git history.
- Persisting transient guesses or feature requirements in `AGENTS.md`.
- Recommending a version-sensitive framework behavior from memory when it changes the decision.

## 8. Discovery completion gate

Discovery is ready for planning when:

- desired behavior/outcome is clear;
- relevant current architecture/code paths are understood;
- relevant stack and production constraints are detected where they affect the task;
- material constraints are known;
- significant unknowns are either resolved or explicitly listed;
- acceptance criteria are testable enough to plan against;
- no hidden product decision is being smuggled into an implementation detail.

## 9. Finish the phase

Report concisely, in the conversation language:

- current-system findings;
- decisions made;
- relevant files/modules likely involved;
- durable docs created/updated;
- remaining risks/unknowns;
- whether the initiative is ready for `dev-plan`.

Do not automatically invoke another skill. For a ready initiative, recommend the next step and execution tier using [execution policy](../references/execution-policy.md).

## Definition of Done

The task is complete when relevant stack, technical context, and implementation seams are understood; material behavior, security/data, and production constraints are explicit; the shared SPEC and stable architecture context are updated only where warranted; and workflow state gives a fresh chat a viable planning next step.
