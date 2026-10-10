---
name: ux-validate
description: Validate wireframes, HTML prototypes, final Figma designs, or existing implementation against the problem, requirements, usability, accessibility, design system, and available real evidence. Never invent user research results.
---

# UX Validate

Use this skill as an evidence-oriented gate between design and implementation.

## Invocation contract

The user only needs to name a target when it cannot be inferred. Determine the active initiative and whether the target is a wireframe, prototype, final design, or implementation, then apply the appropriate criteria internally.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an evidence-led review skill, not an interview phase. Inspect the design, spec, and available evidence, then report findings. Ask only for missing review-target information that cannot be determined from the repository or request. Do not turn critique into a preference questionnaire; identify hypotheses as requiring user evidence rather than asking the requester to confirm them.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal preference, otherwise English. Do not infer note language from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve and reload the initiative

Resolve active-chat or personal requirements, then start with the target artifact and its relevant success/acceptance criteria. Treat supplied screenshots, Figma links, prototype URLs, research notes, and implementation links as potential target or evidence. Load product context, system rules, Figma, prototype, implementation, or local instructions only when needed to substantiate a specific finding. Do not rely on prior chat conclusions.

A fresh chat is beneficial but not required.

Follow [workflow governance](../references/workflow-governance.md). This skill owns validation findings and their initiative consequences; it updates system documentation only when a reusable system issue is demonstrated.

## 2. Separate expert review from empirical validation

Never simulate or invent user evidence.

Label findings as one of:

- **Observed design issue:** supported by the design/prototype itself.
- **Standards/system issue:** conflicts with accessibility, product, or design-system requirements.
- **Hypothesis requiring user evidence:** plausible concern that cannot be settled by inspection.
- **User evidence:** only when actual research/analytics/support/testing evidence was provided or retrieved.

Do not say “users will…” without evidence.

## 3. Expert review

Review the design against the active problem and requirements, focusing on material issues.

Evaluate as relevant:

- problem/outcome alignment;
- information architecture;
- clarity and information scent;
- hierarchy and action priority;
- cognitive load;
- affordances and feedback;
- error prevention and recovery;
- consistency with product/design-system patterns;
- content clarity and terminology;
- trust/safety cues where relevant;
- accessibility;
- responsive behavior;
- loading/empty/error/permission/destructive states;
- important edge cases;
- feasibility constraints already documented.

Do not turn the review into a list of cosmetic preferences.

For each material issue, state:

- issue;
- evidence/location;
- likely user impact;
- severity (`critical`, `high`, `medium`, `low`);
- recommended direction, without over-prescribing when multiple solutions are valid.

## 4. Decide what needs empirical validation

From the spec risks and review findings, identify the smallest set of questions that require real user evidence.

When user testing is appropriate, prepare a concise plan in the spec:

- objective/hypothesis;
- target participants;
- realistic tasks/scenarios;
- success/behavior signals;
- moderator prompts;
- what not to lead participants toward.

Prefer behavioral tasks over preference questions.

Do not require usability testing for every trivial design change.

## 5. Synthesize real validation evidence

When the user provides notes, transcripts, analytics, support evidence, or test results:

- preserve traceability to the evidence;
- identify patterns and contradictions;
- distinguish frequency from severity;
- distinguish observation from interpretation;
- record confidence;
- recommend changes proportional to evidence.

A useful finding contains:

```text
Finding
Evidence
Frequency / confidence
Impact
Likely cause (clearly labeled as interpretation)
Recommended change or next question
```

## 6. Keep findings in chat or personal notes

Report validation questions, methods, observed findings, resulting decisions, remaining risks, and next action. If another chat needs them, save a concise personal note. Do not update repository `SPEC.md`, `design/DESIGN_SYSTEM.md`, or workflow state for personal process. A reusable design-system gap should be reported for `ux-design-system`.

## 7. Validation gate

Mark the initiative ready for build only when:

- no unresolved critical/high issue invalidates the primary flow;
- material requirements have a designed behavior;
- important accessibility/responsive/state concerns are addressed or explicitly accepted;
- remaining assumptions/risks are visible;
- acceptance criteria reflect the validated design.

Do not require certainty that is impossible or disproportionate to the change.

## 8. Finish the phase

Report concisely, in the conversation language:

- highest-severity findings;
- evidence status (expert vs real user evidence);
- changes made/recommended;
- remaining risks;
- whether to return to the relevant UX design skill or hand off to `dev-discovery`.

Do not automatically invoke another skill.

## Definition of Done

The task is complete when the target and relevant criteria have been reviewed, findings distinguish inspection from real user evidence, material issues are prioritized and grounded in evidence, resulting decisions/risks are reported in chat or useful personal notes, and the next action is explicit.
