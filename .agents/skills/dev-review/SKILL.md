---
name: dev-review
description: Independently review a branch/diff against both the initiative spec and engineering quality. Inspect actual code and tests, run relevant verification, prioritize concrete correctness/security/data/performance/maintainability findings, and report actionable findings by severity. Use after implementation or on an existing PR/branch.
---

# DEV Review

Use this skill as an independent engineering review, ideally in a fresh agent session.

## Invocation contract

The user can invoke this without naming routine review dimensions. Recover the active initiative, diff/base, active-chat or personal requirements and plan when available, changed code, tests, and relevant conventions; ask only if the review target cannot be inferred safely.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an independent review skill, not an interview phase. Inspect the actual diff and relevant sources, then report evidence-based findings. Do not question the user while reviewing; ask only for essential target/base information that cannot be inferred safely, and never use clarification as a substitute for repository investigation.

Follow [workflow governance](../references/workflow-governance.md). This skill reports findings in chat by default; save a concise personal note only when a cross-chat handoff needs it. Default review does not modify the target repository.

Read the [engineering router](../references/engineering/README.md), detect the changed stack and risk areas, and load only applicable cross-cutting references. Verify material version-specific behavior with authoritative sources. Review with the source precedence of correctness/security/data integrity, explicit initiative decisions, repository conventions, demonstrated architectural pressure, framework/database idioms, then general preference. Existing conventions do not excuse a demonstrated flaw.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal initiative preference, otherwise English. Record a cross-chat preference only if useful. Never infer note language merely from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Establish the review target

Start with:

- the diff/branch/PR and comparison base;
- active-chat or personal requirements and plan when present, plus any existing project-owned spec;
- changed implementation and relevant tests.

Load architecture, design context, and local instructions only when they bear on a potential finding.

If the user provides a specific diff/commit range, use it.

Otherwise infer the normal repository base safely (for example the merge base with the default branch) and state what was reviewed.

Review the actual diff and relevant surrounding code. Do not review only a summary written by the implementer.

## 2. Review on two mandatory axes

### Axis A — Spec compliance

Verify:

- required behavior is implemented;
- acceptance criteria are satisfied;
- required states/failure behavior exist;
- no requirement was silently changed or omitted;
- scope/non-goals were respected;
- intentional deviations are documented;
- relevant approved Figma/design behavior is preserved for UI work.

For a bug fix, also determine from the observable bug scenario, code, tests, and any durable context whether the change eliminates the diagnosed cause or only masks the symptom. Do not require a `DEBUG.md` or prior chat transcript to perform this check; ask for the minimal missing symptom/context only when repository evidence cannot reconstruct it.

### Axis B — Engineering quality

Inspect material risk in categories that apply:

- correctness and edge cases;
- data integrity and migration safety;
- authorization/authentication/security/privacy;
- concurrency/idempotency;
- error handling/retries/recovery;
- API/backward compatibility;
- performance/resource behavior;
- observability/operability;
- test coverage at meaningful seams;
- maintainability/module boundaries;
- repository conventions;
- UI accessibility/design-system reuse where relevant.

Do not invent theoretical issues detached from this diff's realistic behavior.

Apply selected expert lenses independently using project evidence and the [engineering router](../references/engineering/README.md): framework modeling, transactions, queries, jobs, auth, and concurrency; frontend state, effects, async behavior, accessibility, and design-system reuse; the detected database's constraints, indexes, locking, query and migration behavior; security; production compatibility; and testing quality. Keep review relevance-based: a styling-only change does not require transaction analysis.

## RED FLAGS

- Reviewing an implementer summary without the actual diff.
- Treating green tests as proof of specification compliance.
- Inventing generic security or performance findings with no plausible path through this change.
- Applying a version-sensitive recommendation without confirming installed behavior.

## 3. Verification

Run relevant existing checks when possible:

- targeted tests;
- broader tests appropriate to risk;
- lint/typecheck/build;
- static/security checks;
- runtime/manual reproduction for important behavior.

Inspect tests for what they actually prove. A green test suite is evidence, not a substitute for code review.

Do not claim verification was run when it was not.

## 4. Findings format

Prioritize findings over praise or summary.

Use severity:

- **Critical:** likely severe security/data-loss/outage or fundamentally wrong required behavior.
- **High:** correctness/security/data/compatibility defect likely to affect users or deployment materially.
- **Medium:** real defect/risk with narrower impact or important maintainability/operability concern.
- **Low:** concrete minor issue worth fixing; avoid style-only nitpicks.

For every finding provide:

- severity;
- location (file/line or precise symbol/path when possible);
- issue;
- why it matters / failure scenario;
- recommended direction.

Do not inflate severity.

## 5. Avoid low-value review behavior

Do not:

- demand unrelated refactors;
- enforce personal style preferences when project conventions permit the code;
- flag hypothetical race/security/performance issues without a plausible execution path;
- duplicate lint output as review findings unless it exposes material risk;
- praise every correct decision before listing issues.

If there are no material findings, say so clearly and still report what verification was performed and any residual uncertainty.

## 6. Fix mode

Default behavior is **review only**.

Do not modify code unless the user explicitly asks to fix findings as part of the invocation.

If fix mode is requested:

1. report/confirm the finding through evidence;
2. apply the smallest correct fix;
3. add/update regression coverage where appropriate;
4. rerun relevant verification;
5. report what changed.

Do not use fix mode to redesign requirements.

## 7. Documentation

Do not create `REVIEW.md` by default.

Do not create or update repository review, SPEC, PLAN, or workflow-state files. For cross-chat continuation, record only material findings, accepted deviations, and readiness in a personal note. Explain why a significant finding matters at its actual boundary.

## 8. Finish the phase

Report, in the conversation language:

1. findings ordered by severity;
2. verification run and results;
3. residual unverified areas;
4. whether the change is ready to merge from the review perspective.

For a ready change, recommend the next skill and execution tier using [execution policy](../references/execution-policy.md).

## Definition of Done

The review is complete when implementation has been checked against confirmed behavior and any current plan, applicable correctness/security/data/production/test risks have been examined, findings are impact-prioritized and evidence-based, blockers are explicit, and personal handoff context is saved only when useful.
