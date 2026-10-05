---
name: dev-implement
description: Implement an approved software SPEC/PLAN in small verified slices without reopening settled product decisions. Use existing repository patterns, test behavior as you go, keep PLAN progress current, and finish with real verification. Use after dev-plan or directly for a trivial well-defined change.
---

# DEV Implement

Use this skill to build work that has already been sufficiently decided.

## Invocation contract

The user can invoke this after planning or an immediately preceding `dev-debug` diagnosis without repeating details. Recover the active SPEC, approved plan when present, active diagnostic result, target code, and material implementation constraints internally.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an execution skill, not an interview phase. Consume decisions in the spec/plan and make routine implementation choices using repository conventions. Do not reopen settled decisions or ask about ordinary implementation details. If repository reality exposes a material decision that cannot be resolved safely, pause only the affected work and ask one concise question; otherwise document a reasonable assumption and proceed.

Follow [workflow governance](../references/workflow-governance.md). This skill owns production code; it updates plan progress and initiative workflow state only for material completion, deviations, or remaining blockers.

Read the [stack-aware engineering router](../references/engineering/README.md) when implementation touches a selected technology or risk area, then load only the relevant playbooks. Follow the precedence of correctness/security/data integrity, explicit initiative decisions, repository conventions, framework/database idioms, then general preference. Do not reproduce a demonstrated dangerous convention.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve implementation scope

Start with:

- active `SPEC.md`;
- `PLAN.md` when present;
- the immediately preceding `dev-debug` diagnosis when intentionally chained in the same chat;
- actual target code/tests.

Load local instructions, architecture/ADRs, and product/design sources only when they constrain the target change.

If the user specifies a particular plan slice, implement only that slice unless adjacent changes are required for correctness.

If there is no `PLAN.md`, use a preceding diagnosis as evidence, verify the repository still supports it, and determine whether remediation is narrow and unambiguous. Implement a narrow confirmed correction directly; if it needs material architecture, data, product-behavior, migration, or integration decisions, recommend `dev-plan` rather than inventing them. Do not create a planning artifact merely for a trivial bug fix.

## 2. Do not redesign settled behavior during implementation

Treat the spec as the behavioral contract and the plan as the intended implementation path.

If repository reality invalidates part of the plan:

- investigate the mismatch;
- choose an equivalent local adjustment when behavior and architecture intent remain unchanged;
- update the plan with the reason;
- if the mismatch requires a material product, security, data-contract, or costly architecture decision, stop that part and surface the decision instead of guessing.

## 3. Implement in small feedback-driven slices

For each slice:

1. identify the observable behavior/seam;
2. add or update a focused failing test first when practical and valuable;
3. make the smallest coherent implementation change;
4. run the focused verification;
5. refactor only as needed while tests stay green;
6. update progress in `PLAN.md` for non-trivial work.

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

Apply Rails, React, PostgreSQL/MySQL, security, production-safety, and testing guidance only when the target change activates it. In particular, do not rely on application validation alone for a concurrency-sensitive data invariant; do not introduce framework abstractions/dependencies unless existing primitives and repository patterns are insufficient; and surface material plan contradictions before inventing architecture.

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

Update:

- `PLAN.md` progress;
- `SPEC.md` only for durable clarified behavior, accepted deviations, or completion status;
- `engineering/ARCHITECTURE.md` only if stable architecture actually changed;
- ADRs only for decisions that satisfy the durable-decision threshold.

Do not generate implementation diaries.

## 8. Completion gate

Before declaring implementation complete:

- all in-scope acceptance criteria are implemented or explicitly deferred;
- relevant planned slices are complete;
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

## Definition of Done

The task is complete when in-scope acceptance criteria and relevant plan slices are implemented or explicitly deferred, applicable stack-specific correctness concerns are addressed, appropriate verification has run or its limitation is explicit, material deviations and rollout concerns are durable, and SPEC/PLAN workflow state supports an independent review.
