---
name: ux-discovery
description: Understand a product-design problem before solution work. Inspect the repo and existing Figma/context first, interview only about meaningful unknowns, and clarify product/design context in chat or minimal personal notes when cross-chat continuity is useful. Use for greenfield or existing products when requirements need clarification or documentation.
---

# UX Discovery

Use this skill to turn a product/design request into a shared, evidence-aware understanding that downstream design work can trust.

## Invocation contract

The user only needs to state the product intent and any task-specific context or references. Recover the initiative, repository/Figma context, durable artifacts, language behavior, and next questions internally.

The user's explicit instructions take precedence over workflow defaults in this skill.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- For personal workflow notes, follow an explicit current language request, then a recorded personal preference, otherwise English. Do not infer note language from conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## Core rule

**Investigate facts. Ask for decisions. Never make the user answer a question that the repository, existing product, Figma, or available project documentation can answer reliably.**

Do not start by generating polished screens or implementation code. Conceptual flows may be used to clarify scope; use `ux-wireframe` for low-fidelity Figma exploration.

Follow [workflow governance](../references/workflow-governance.md): begin with the smallest useful set of repository signals, keep same-chat results in conversation, and save only useful cross-chat context in the personal workspace. Do not modify the target repository.

## User interaction

Use [the Codex interactive decision policy](../references/interactive-decision-policy.md) for consequential questions and the active session's Plan-mode/write boundary. Do not require a slash command before using this skill.

Investigate existing UX, application behavior, specs, and Figma before interviewing. Keep questions focused on unresolved product decisions such as target user/outcome, workflow behavior, information hierarchy, material states, permissions, navigation, success criteria, and scope. Leave visual-style preferences to `ux-visual-direction`. Use native structured questions when available, recommend evidence-supported options, and stop once design can proceed without guessing core behavior.

## 1. Resolve the working context

Determine whether this is:

- a new project;
- an existing project with a new initiative;
- an existing initiative described in personal notes or a project-owned spec.

Resolve the active initiative from, in order:

1. an explicit file/path/slug in the user's request;
2. the current conversation;
3. a single clearly active personal initiative note or existing project-owned spec;
4. otherwise ask the user which initiative to use.

Do not create a duplicate initiative when a suitable one already exists.

## 2. Inspect before interviewing

Start with repository structure, local instructions, README, existing product context/specs, and the implementation surfaces that express the request. Expand only when needed, for example into:

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

## 6. Keep useful context personal

Read existing project instructions, product context, specs, and design-system documentation as evidence. If `AGENTS.md` exists, respect it; never create or rewrite it for this workflow. Same-chat discovery can stay in conversation. For cross-chat work, save a concise personal problem/requirements note under the project workspace; include confirmed decisions, constraints, assumptions, open questions, and next action. `assets/SPEC.template.md` and `assets/CONTEXT.template.md` are optional personal-note guides. Do not create or update repository `SPEC.md`, `product/CONTEXT.md`, `design/DESIGN_SYSTEM.md`, or workflow state.

## 7. Discovery completion gate

Discovery is sufficiently complete when downstream design can proceed without guessing the core problem or product behavior.

Before declaring it ready, verify that the result contains, when applicable:

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
- a clear next recommended action; save it personally only if another chat needs it.

Do not force false certainty. A spec can be ready for design with explicitly documented research questions.

## 8. Finish the phase

Report concisely, in the conversation language:

- what the agent learned from the repository/Figma;
- which decisions the user made;
- which personal notes were saved, if any;
- remaining material unknowns;
- whether the initiative is ready for `ux-wireframe`, `ux-final-design`, or another appropriate next task.

Do not automatically invoke another skill.

## Definition of Done

The task is complete when the relevant repository/Figma evidence has been inspected, material product decisions and unknowns are explicit, the problem and constraints are clear in conversation or useful personal notes, and a fresh chat has the needed context when cross-chat continuation is planned.
