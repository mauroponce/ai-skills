---
name: ux-discovery
description: Understand a product-design problem before solution work. Inspect the repo and existing Figma/context first, interview only about meaningful unknowns, and create or update minimal durable product/design artifacts. Use for greenfield or existing products when requirements need clarification or documentation.
---

# UX Discovery

Use this skill to turn a product/design request into a shared, evidence-aware understanding that downstream design work can trust.

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

**Investigate facts. Ask for decisions. Never make the user answer a question that the repository, existing product, Figma, or available project documentation can answer reliably.**

Do not start by generating polished screens or implementation code. Conceptual flows may be used to clarify scope; use `ux-wireframe` for low-fidelity Figma exploration.

## User interaction

This is a decision-oriented skill intended to start in Plan mode (`/plan`). It cannot switch the host's mode. See [the shared interaction policy](../references/interactive-decision-policy.md) for the Codex and Claude Code interaction rules, including when to leave read-only Plan mode to save artifacts.

Investigate existing UX, application behavior, specs, and Figma before interviewing. Keep questions focused on unresolved product decisions such as target user/outcome, workflow behavior, information hierarchy, material states, permissions, navigation, success criteria, and scope. Leave visual-style preferences to `ux-visual-direction`. Use native structured questions when available, recommend evidence-supported options, and stop once design can proceed without guessing core behavior.

## 1. Resolve the working context

Determine whether this is:

- a new project;
- an existing project with a new initiative;
- an existing initiative that already has a `SPEC.md`.

Resolve the active initiative from, in order:

1. an explicit file/path/slug in the user's request;
2. the current conversation;
3. a single clearly active `work/*/SPEC.md`;
4. otherwise ask the user which initiative to use.

Do not create a duplicate initiative when a suitable one already exists.

## 2. Inspect before interviewing

For an existing repository, inspect only what is relevant to the request, including as appropriate:

- `AGENTS.md` and local agent instructions;
- README/project docs;
- `product/CONTEXT.md` or equivalent;
- `design/DESIGN_SYSTEM.md` or equivalent;
- existing `work/*/SPEC.md` files;
- routes/navigation;
- domain models and permissions;
- relevant views/screens/components;
- design tokens and UI component libraries;
- localization/product copy;
- analytics/event hooks;
- tests that describe current behavior;
- APIs/data contracts relevant to the flow;
- linked Figma files/frames when available.

Do not read the entire repository by default. Follow the request to the relevant seams.

For a new project, inspect whatever files already exist before assuming it is truly blank.

## 3. Build an evidence ledger

Internally classify important statements as:

- **Known:** directly supported by repo/Figma/docs/user evidence.
- **Inferred:** strongly suggested by existing evidence but not explicit.
- **Assumed:** a temporary working assumption.
- **Unknown:** information not available.
- **Conflicting:** sources disagree.

Do not present an inference or assumption as a fact.

## 4. Reframe solution requests into problems

If the user requests a specific UI solution, capture it as a candidate solution, not automatically as the requirement.

Example:

```text
Requested solution: add a dropdown to filter projects
Underlying problem to verify: users with many projects cannot efficiently locate the project they need
```

Preserve explicit business constraints, but challenge accidental solution lock-in.

## 5. Interview the user

Ask questions only after inspection.

Interview rules:

- Prefer one consequential question at a time.
- Ask a small numbered group only when the questions are genuinely independent.
- Explain briefly why a question matters when it is not obvious.
- When useful, include a recommended default and its trade-off.
- Do not ask the user to choose low-impact implementation details during discovery.
- Do not block on reversible, low-risk ambiguity: make a reasonable assumption, label it, and record it.
- Do ask when ambiguity changes user behavior, scope, permissions, business rules, success criteria, data sensitivity, accessibility, or a costly-to-reverse direction.
- If the user does not know, help narrow the decision with options rather than repeatedly asking the same question.

Cover only what is relevant, typically:

- user/segment;
- problem and context;
- current behavior;
- evidence;
- desired user outcome;
- business outcome;
- success signals/metrics;
- scope and non-goals;
- business/domain rules;
- roles and permissions;
- constraints;
- critical edge cases;
- product content language when unresolved;
- major risks: value, usability, feasibility, viability;
- open questions that need later research or validation.

## 6. Create or update durable project context

Prefer existing project conventions. Do not create parallel docs when an existing file already fulfills the same purpose.

When needed, use the templates bundled with this skill.

### `AGENTS.md`

If absent, create a lean root `AGENTS.md` using `assets/AGENTS.product-design-section.md` as guidance.

If present:

- preserve existing instructions;
- add only missing durable product/design guidance;
- never replace the whole file;
- keep it concise and link to context instead of copying context into it.

### `product/CONTEXT.md`

Create/update stable product context using `assets/CONTEXT.template.md` as guidance.

Do not fill unknown sections with invented content. Mark meaningful unknowns explicitly or omit irrelevant sections.

### `design/DESIGN_SYSTEM.md`

If a design system exists, document its actual structure, links, tokens, component/code mappings, and conventions.

If no design system exists yet, create a minimal file using `assets/DESIGN_SYSTEM.template.md` and mark its status clearly as not established. Do not invent tokens/components merely to complete the template.

### `work/<initiative>/SPEC.md`

Create or update the initiative source of truth using `assets/SPEC.template.md`.

The spec must separate:

- evidence/facts;
- decisions/requirements;
- assumptions;
- open questions.

Do not duplicate stable project context that belongs in `CONTEXT.md` or `DESIGN_SYSTEM.md`; link/reference it instead.

## 7. Discovery completion gate

Discovery is sufficiently complete when downstream design can proceed without guessing the core problem or product behavior.

Before declaring it ready, verify that the spec has, when applicable:

- a clear problem statement;
- target user/context;
- desired outcome;
- success criteria or a stated reason they cannot yet be measured;
- scope and non-goals;
- material requirements/business rules;
- known constraints;
- important assumptions;
- unresolved questions clearly marked;
- risks that require validation;
- current workflow status set to `Discovery: complete` and `Design: not-started` or equivalent.

Do not force false certainty. A spec can be ready for design with explicitly documented research questions.

## 8. Finish the phase

Report concisely, in the conversation language:

- what the agent learned from the repository/Figma;
- which decisions the user made;
- which files were created or updated;
- remaining material unknowns;
- whether the initiative is ready for `ux-wireframe`, `ux-final-design`, or another appropriate next task.

Do not automatically invoke another skill.
