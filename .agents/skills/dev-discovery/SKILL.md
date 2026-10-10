---
name: dev-discovery
description: Understand a software change before planning or coding. Inspect the repository and existing product/design specs first, resolve facts from code, interview the user only about consequential unknowns, and clarify the change in chat or concise personal notes when cross-chat continuity is useful. Use for new projects, features, refactors, integrations, or non-trivial bug work.
---

# DEV Discovery

Use this skill to establish shared technical understanding before an implementation plan is written.

## Invocation contract

The user only needs to state the intended software change and relevant task-specific facts. If `dev-explore` already mapped this area in the same Codex conversation, use that map as context and verify the relevant current code rather than repeating basic reconnaissance. Exploration remains an input; this skill still defines the requested change and its constraints. Recover the active initiative, relevant technical context, production implications, and material questions from the repository.

The user's explicit instructions take precedence over workflow defaults in this skill.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal initiative preference, otherwise English. Record a cross-chat preference only if useful. Never infer note language merely from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## Core rule

**Facts are the agent's job to investigate. Decisions that cannot be derived safely are the user's job to make with the agent's help.**

Do not modify the target repository during discovery. A trivial, sufficiently defined change may move directly to `dev-implement` in the same chat.

Follow [workflow governance](../references/workflow-governance.md): begin with high-signal project context and leave same-chat results in conversation. Save only useful cross-chat context in the personal workspace. This skill does not modify the target repository.

Use the [engineering router](../references/engineering/README.md). Detect the stack from high-signal repository evidence, then load only cross-cutting references applicable to the task's security, production, testing, or other risks. Verify material version-specific behavior with authoritative sources; do not research unrelated areas for a local low-risk change.

## User interaction

Use [the Codex interactive decision policy](../references/interactive-decision-policy.md) for consequential questions and the active session's Plan-mode/write boundary. Do not require a slash command before using this skill.

Investigate code, tests, configuration, documentation, and current behavior before asking. Treat supplied issue links, documents, API references, logs, and code links as additional evidence; verify them against the repository where appropriate. Ask only about unresolved externally visible behavior or material business, security, data, API, compatibility, rollout, or hard-to-reverse architecture decisions. Recommend an option when repository evidence supports it. Do not ask the user where something is implemented; search the repository.

## 1. Resolve the task and existing sources of truth

Resolve the active initiative from the user request, active conversation, relevant personal workspace notes, and current project evidence.

Start with the active behavior context (if any), local instructions/README, relevant architecture documentation, and implementation surfaces named by the request. Expand into only relevant sources such as:

- root/local `AGENTS.md`;
- relevant personal specification or existing project-owned spec;
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

Start with high-signal stack files when present: dependency manifests and lockfiles, runtime and framework configuration, routes, schema/migrations, frontend entry points, tests/CI, deployment files, job configuration, and auth/authorization/observability seams. Determine only facts useful beyond this feature:

- backend runtime/framework/version and application shape;
- authentication, authorization, jobs, cache, storage, and local architecture conventions;
- frontend integration/version/build/state/component/testing conventions;
- database engine/version when discoverable, schema format, important extensions/constraints/index conventions;
- testing frameworks and CI execution;
- stable production/deployment, queue, feature-flag, and monitoring constraints.

If useful across chats, keep stable findings and feature decisions in concise personal notes. Read existing architecture docs as evidence; do not update them for personal workflow or create an inventory for its own sake.

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
Requested implementation: add distributed locking
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

## 7. Preserve only useful personal context

For same-chat work, report the problem, desired behavior, confirmed decisions, constraints, open questions, relevant code, and next step in conversation. For long or cross-chat work, save a minimal personal specification under the project workspace. Existing project specs, ADRs, and architecture docs are evidence, not automatic write targets. Read `AGENTS.md` if present; never create or rewrite it for this workflow. Do not create repository `SPEC.md`, `PLAN.md`, `engineering/ARCHITECTURE.md`, ADRs, or workflow state. Use `assets/SPEC.template.md` only as optional structure for a personal note; omit unused sections.

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
- personal notes saved, if any;
- remaining risks/unknowns;
- whether the initiative is ready for `dev-plan`.

Do not automatically invoke another skill. For a ready initiative, recommend the next step and execution tier using [execution policy](../references/execution-policy.md).

## Definition of Done

The task is complete when relevant stack, context, and implementation seams are understood; material behavior, security/data, and production constraints are explicit; remaining questions are visible; and a next chat can continue from concise personal context when needed. Explain how significant requirements and constraints shape the implementation when useful.
