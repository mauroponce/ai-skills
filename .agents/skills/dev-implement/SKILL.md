---
name: dev-implement
description: Implement a sufficiently defined software change in small verified slices without reopening settled product decisions. Use existing repository patterns, test behavior as you go, keep useful personal progress current, and finish with real verification. Use after dev-plan or directly for a trivial well-defined change.
---

# DEV Implement

Use this skill to build work that has already been sufficiently decided.

## Invocation contract

The user can invoke this after planning, an immediately preceding `dev-debug` diagnosis, or a narrow `dev-audit` finding without repeating details. Recover the active-chat or personal behavior context and plan when present, active diagnosis or selected `AUDIT-###` findings from this chat, target code, and material implementation constraints internally.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an execution skill, not an interview phase. Consume confirmed decisions in the active-chat or personal context/plan and make routine implementation choices using repository conventions. Do not reopen settled decisions or ask about ordinary implementation details. If repository reality exposes a material decision that cannot be resolved safely, pause only the affected work and ask one concise question; otherwise document a reasonable assumption and proceed.

Follow [workflow governance](../references/workflow-governance.md). This skill changes task-required project code, tests, migrations, configuration, and explicitly requested project docs. Track material progress or deviations in chat or a useful personal plan; never add repository workflow artifacts.

Read the [engineering router](../references/engineering/README.md) when implementation touches a technology or risk area, then load only relevant cross-cutting references and verify material version-specific behavior. Follow the precedence of correctness/security/data integrity, explicit initiative decisions, repository conventions, demonstrated architectural pressure, framework/database idioms, then general preference. Do not reproduce a demonstrated dangerous convention.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal initiative preference, otherwise English. Record a cross-chat preference only if useful. Never infer note language merely from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve implementation scope

Start with:

- active behavior contract in chat or personal notes;
- active-chat or personal plan when present;
- the immediately preceding `dev-debug` diagnosis or selected `dev-audit` findings when intentionally chained in the same chat;
- actual target code/tests.

Load local instructions, architecture/ADRs, and product/design sources only when they constrain the target change.

If the user specifies a particular plan slice, implement only that slice unless adjacent changes are required for correctness.

If there is no plan, use a preceding diagnosis or selected audit finding as evidence, verify the repository still supports it, and determine whether remediation is narrow and unambiguous. Implement a narrow, sufficiently defined correction directly with relevant regression verification. If the finding needs material architecture, product-behavior, data/migration, caching, job, transaction, or integration decisions, recommend `dev-plan` rather than inventing them. A `MEASURE FIRST` candidate needs discriminating evidence before implementation. Do not create a planning artifact merely for a trivial correction.

An architecture finding that names a possible operation, query, state, or integration boundary is directional; it does not alone settle ownership, migration order, or trade-offs. Use a current plan for consequential extraction, while retaining direct implementation for a narrow finding whose behavior and repository seam are already clear.

## 2. Do not redesign settled behavior during implementation

Treat confirmed behavior as the contract and a current plan as the intended implementation path; recheck personal notes against repository and Git state.

If repository reality invalidates part of the plan:

- investigate the mismatch;
- choose an equivalent local adjustment when behavior and architecture intent remain unchanged;
- explain the adjustment in chat and update a personal plan only if it remains useful across chats;
- if the mismatch requires a material product, security, data-contract, or costly architecture decision, stop that part and surface the decision instead of guessing.

## 3. Implement in small feedback-driven slices

For each slice:

1. identify the observable behavior/seam;
2. add or update a focused failing test first when practical and valuable;
3. make the smallest coherent implementation change;
4. run the focused verification;
5. refactor only as needed while tests stay green;
6. track material progress in chat or an existing useful personal plan for long work.

Test-first is preferred at stable behavioral seams, but do not write meaningless tests merely to satisfy a ritual.

## 4. Follow the repository

Prefer:

- existing abstractions/components;
- existing error/result patterns;
- established dependency boundaries;
- established test conventions;
- existing configuration/observability mechanisms.

Avoid:

- unrelated cleanup;
- speculative abstractions;
- new dependencies without clear need;
- broad renames/refactors mixed into feature behavior;
- hardcoded secrets or environment-specific values;
- silently weakening validation/security to make tests pass.

## 5. Engineering correctness

Address relevant concerns from the spec/plan, including when applicable:

- authorization/authentication;
- validation;
- transactions/atomicity;
- concurrency/idempotency;
- retry/error semantics;
- backward compatibility;
- migrations and safe deploy ordering;
- data integrity;
- resource/performance impact;
- logs/metrics/auditability;
- accessibility and design-system compliance for UI code.

Use project evidence and the [engineering router](../references/engineering/README.md) to address framework, frontend, database, security, production-safety, and testing concerns only when the target change activates them. In particular, do not rely on application validation alone for a concurrency-sensitive data invariant; do not introduce framework abstractions/dependencies unless existing primitives and repository patterns are insufficient; and surface material plan contradictions before inventing architecture.

## RED FLAGS

- Calling a small change too obvious to verify.
- Ignoring repository conventions because the edit is local.
- Deferring verification until after claiming completion.
- Substituting a preferred design for a settled plan without recording a real mismatch.

## 6. Verification

Run the most relevant verification after each slice and final broader checks appropriate to risk.

Use actual repository commands. Typical categories:

- targeted tests;
- full/relevant suite;
- lint/format;
- typecheck;
- build;
- static/security checks;
- migration checks;
- runtime/manual behavior verification.

Do not claim a command passed unless it was actually run successfully.

If a required check cannot run, report exactly why and what remains unverified.

## 7. Keep documentation proportional

Change only task-required project files: application code, tests, migrations, configuration, and product documentation explicitly requested as part of the task. Keep plan progress, clarified behavior, decisions, and review handoff in chat or a concise personal note if another session needs them. Do not create or update repository `SPEC.md`, `PLAN.md`, `engineering/ARCHITECTURE.md`, ADRs, or implementation diaries for this harness.

## 8. Completion gate

Before declaring implementation complete:

- all in-scope acceptance criteria are implemented or explicitly deferred;
- relevant planned slices are complete;
- relevant tests were added or updated where behavior warrants them and actually run;
- applicable lint, type, static, or build checks used by this repository were run, or their omission is explained;
- expected behavior was verified with observable evidence, not “looks correct” or “should work”;
- tests/checks are green or remaining failures are clearly explained;
- no known critical correctness/security/data issue remains hidden;
- migrations/rollout steps are documented when needed;
- implementation does not knowingly contradict approved Figma/design for relevant UI work.

Do not perform an independent code review inside this skill beyond normal self-checking; `dev-review` is the dedicated reviewer phase.

## 9. Finish the phase

Report concisely, in the conversation language:

- implemented slices/behavior;
- important files/areas changed;
- verification actually run and results;
- any plan deviations and why;
- remaining known risks/issues;
- whether the branch is ready for `dev-review`.

At handoff, recommend an independent fresh-chat `dev-review` and an execution tier using [execution policy](../references/execution-policy.md).

## Definition of Done

The task is complete when in-scope acceptance criteria and relevant slices are implemented or explicitly deferred, applicable correctness concerns are addressed, verification has run or its limit is explicit, material deviations and rollout concerns are reported, and a fresh reviewer can inspect the current diff and tests. Save a concise personal handoff only when needed; explain significant implementation trade-offs without a tutorial.
