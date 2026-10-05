---
name: ux-validate
description: Validate an existing product design against its problem, requirements, usability, accessibility, design system, and available real user evidence. Use after ux-design, after an HTML prototype, or to revalidate a changed design. Never invent user research results.
---

# UX Validate

Use this skill as an evidence-oriented gate between design and implementation.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an evidence-led review skill, not an interview phase. Inspect the design, spec, and available evidence, then report findings. Ask only for missing review-target information that cannot be determined from the repository or request. Do not turn critique into a preference questionnaire; identify hypotheses as requiring user evidence rather than asking the requester to confirm them.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve and reload the initiative

Resolve the active `SPEC.md`, then read relevant durable context from disk and Figma rather than relying on prior chat conclusions.

Read as relevant:

- `AGENTS.md`;
- active `SPEC.md`;
- `product/CONTEXT.md`;
- `design/DESIGN_SYSTEM.md`;
- relevant Figma frames/prototype;
- `prototype/<initiative>/prototype.html` if it exists and is relevant;
- existing implementation if validating a redesign of live behavior.

A fresh chat is beneficial but not required.

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

## 6. Update durable artifacts

Update `SPEC.md` with:

- validation questions/method;
- actual findings;
- changes resulting from validation;
- remaining risks;
- workflow status.

If validation reveals a reusable design-system problem, update `design/DESIGN_SYSTEM.md` or record the gap there.

If material product behavior changes, ensure the requirements/acceptance criteria reflect the new decision rather than leaving contradictory sections.

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
- whether to return to `ux-design` or proceed to `ux-build`.

Do not automatically invoke another skill.
