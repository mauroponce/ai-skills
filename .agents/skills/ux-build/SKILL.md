---
name: ux-build
description: Implement an approved Figma/product design in the existing codebase with high design fidelity, design-system reuse, accessibility, responsive behavior, tests, and design QA. Use after ux-validate when the product behavior is sufficiently settled.
---

# UX Build

Use this skill to translate an approved design into production code without silently redesigning the feature.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This is an execution skill, not an interview phase. Consume approved behavior and visual decisions from the spec, visual direction, design system, and Figma. Make routine implementation choices autonomously and do not reopen settled decisions. If implementation uncovers a material product or engineering blocker that evidence cannot resolve, pause only the affected work and ask one concise question or route it to the appropriate discovery/planning phase.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Reload sources of truth

Resolve the active initiative and read:

- relevant `AGENTS.md` instructions;
- active `SPEC.md`;
- `product/CONTEXT.md` when relevant;
- `design/DESIGN_SYSTEM.md`;
- `engineering/ARCHITECTURE.md` when relevant;
- relevant Figma frame(s);
- existing code/components/tests around the implementation seam.

Do not implement from a screenshot or chat summary when structured Figma/spec context is available.

## 2. Inspect before coding

Before writing implementation code:

- inspect existing production components and styles;
- inspect Figma variables/tokens used by the target frame;
- inspect Figma component mappings / Code Connect when available;
- identify which existing code components map to Figma components;
- identify genuine gaps rather than recreating components prematurely;
- identify backend/API/data dependencies already present in the repo.

When using Figma MCP for design-to-code:

- get structured design context for the exact relevant node(s);
- if context is too large, inspect metadata and fetch smaller nodes;
- obtain a visual reference/screenshot when available for fidelity checking;
- retrieve relevant variables/tokens;
- use Code Connect mappings when available;
- adapt the returned context to this repository's framework and conventions rather than copying generic generated markup blindly.

## 3. Create an implementation mapping

Before editing, establish a concise mapping such as:

```text
Figma Button / primary / md → existing Button variant="primary" size="md"
Figma spacing/300 → existing semantic spacing token
Figma Modal → existing Dialog component
```

Record reusable mapping/gap information in `design/DESIGN_SYSTEM.md` when it will matter beyond this feature.

## 4. Implement the approved behavior

Follow the existing stack, architecture, and repository conventions.

Requirements:

- reuse existing design-system components and tokens where they fit;
- do not recreate an existing component using arbitrary CSS;
- preserve semantic HTML/control behavior;
- implement responsive behavior defined/required by the design;
- implement relevant loading/empty/error/permission/recovery states;
- preserve product copy language and canonical terminology;
- avoid unrelated refactors;
- add/update tests at appropriate behavior boundaries;
- keep accessibility behavior real, not merely visual.

Do not promote code from `prototype/<initiative>/prototype.html` directly into production merely because it looks correct. Treat the prototype as behavioral evidence; implement using the production stack and system.

## 5. Escalate material engineering gaps instead of inventing them

If implementation reveals a substantial unresolved decision involving, for example:

- data model/schema;
- authorization model;
- API contract;
- concurrency/idempotency;
- security/privacy;
- infrastructure;
- architectural boundaries;
- migration/rollout strategy;

then do not silently decide it inside a UX implementation.

Document the gap in `SPEC.md` and recommend `dev-discovery` / `dev-plan` for that concern. Continue only where the existing requirements make the answer clear or the user explicitly directs a choice.

## 6. Verify behavior and quality

Run the repository's relevant checks, such as:

- targeted tests;
- broader test suite when warranted;
- lint/format;
- typecheck;
- build;
- accessibility checks available in the project.

Test important interactions, states, and responsive behavior in the running application when tooling allows.

Do not claim a check passed unless it was actually run successfully.

## 7. Design QA

Compare the running implementation against the approved Figma/spec, looking for material mismatch in:

- hierarchy/layout;
- spacing/sizing;
- typography/color/tokens;
- component variants;
- content;
- interaction behavior;
- states;
- responsive behavior;
- focus/keyboard/accessibility behavior.

Fix confirmed implementation mismatches unless they require a new product/design decision. Record intentional deviations and rationale in `SPEC.md`.

## 8. Update status

Update the initiative `SPEC.md` with:

- implementation notes only when they are durable/relevant;
- intentional deviations;
- validation/QA status;
- build status.

Do not turn the spec into a commit log.

## 9. Finish the phase

Report concisely, in the conversation language:

- what was implemented;
- files/areas changed;
- verification actually run;
- design-system mappings/gaps;
- remaining product/design/engineering issues;
- whether the UX build is complete.
