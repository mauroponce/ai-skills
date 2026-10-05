---
name: ux-prototype
description: Create a disposable but realistic browser prototype for a product-design question as one self-contained HTML file using only HTML, inline CSS, and vanilla JavaScript. Use during UX design/validation when interaction is easier to judge in a browser. Never treat the prototype as production code.
---

# UX Prototype

Use this skill to answer a design question with a runnable browser artifact, not to build the production application.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an artifact-generation skill, not an interview phase. Use the design question and decisions already recorded in the spec. Resolve routine prototype details from product context and the design system. Ask only if the target question or a material behavior is genuinely unclear and cannot be inferred; do not reopen settled product or visual decisions.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve the initiative and prototype question

Read the active `SPEC.md`, relevant `product/CONTEXT.md`, `design/DESIGN_SYSTEM.md`, and relevant Figma frames when available.

Identify the specific uncertainty the prototype should help answer, for example:

- does the multi-step flow feel understandable?;
- is inline editing clearer than a modal?;
- how should progressive disclosure behave?;
- does the responsive interaction work?;
- which state transition is easier to understand?;
- can a usability test participant complete the target task?

Do not prototype the entire product when a smaller artifact can answer the question.

## 2. Output contract

Create exactly one primary prototype file:

```text
prototype/<initiative>/prototype.html
```

The file must be self-contained and use only:

- HTML;
- CSS inside `<style>`;
- vanilla JavaScript inside `<script>`.

Do not use:

- React;
- Vue;
- Svelte;
- npm/yarn/pnpm;
- Vite/Webpack;
- Tailwind CDN;
- Bootstrap or other external CSS/JS libraries;
- remote fonts;
- external images required for core behavior;
- backend services;
- network/API calls required for the prototype to work.

Use inline/local placeholder treatment when imagery is not essential to the question.

Start from `assets/prototype-shell.html` when useful, but adapt it to the initiative rather than keeping generic demo content.

## 3. Make the prototype behaviorally realistic

Implement enough behavior to test the design question, including as relevant:

- navigation/step progression;
- forms and validation;
- dialogs/menus;
- toggles/selections;
- loading simulation;
- success/error states;
- empty state;
- keyboard/focus behavior;
- responsive layout;
- realistic sample content/data.

Do not implement unrelated production concerns.

## 4. Respect the design system without overengineering

When an existing design system is documented/Figma-linked:

- approximate its tokens/components closely enough for the prototype question;
- do not build a full reusable component framework inside the single HTML file;
- keep the prototype easy to read and throw away.

If the design question is structural rather than visual, prefer speed and clarity over pixel-perfect styling.

## 5. Accessibility baseline

Even for a prototype, use sensible semantic HTML and basic keyboard/focus behavior so the interaction can be evaluated honestly.

## 6. Make local execution trivial

The file should work when served from the repository root with, for example:

```bash
python3 -m http.server 8000
```

If command/browser tooling is available:

- start a local server on an available port;
- smoke-test that the prototype loads;
- exercise the core interaction;
- fix runtime errors.

Do not require the user to install dependencies.

## 7. Prototype labeling

Include a visible or source-level indication that this is a prototype and not production code. Do not let the artifact masquerade as production implementation.

## 8. Update the spec

Add/update the prototype path and the question it is intended to answer in `SPEC.md`.

Do not claim the prototype validated anything until actual evaluation/user evidence exists.

## 9. Finish the phase

Report concisely, in the conversation language:

- prototype path;
- design question it addresses;
- how to run it locally;
- what interaction/states are implemented;
- what should be evaluated next, usually via `ux-validate`.
