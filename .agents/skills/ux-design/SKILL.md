---
name: ux-design
description: Turn an approved product problem/spec into a coherent product design. Work from structure and flows through interaction, states, visual design, design-system reuse, and native Figma output. Use after ux-discovery or when an existing SPEC is sufficiently defined.
---

# UX Design

Use this skill to design the solution, not to rediscover the product problem from scratch.

The user's explicit instructions take precedence over workflow defaults in this skill.

## User interaction

This skill applies established UX requirements and design-system direction to screens; it is not the requirements interview phase. Read the spec, visual direction, and design system first. Make ordinary design choices autonomously within those decisions. Ask only when a genuine product-behavior blocker cannot be resolved from repository evidence or prior decisions; do not reopen settled visual preferences.

## Language policy

- Detect the language of the user's current request.
- Use that language for conversation, questions, interview rounds, explanations, and summaries unless the user explicitly asks to switch.
- Determine repository artifact language in this order: (1) an explicit instruction in the current request, (2) an explicit initiative/workflow artifact language already recorded in the active `SPEC.md`, (3) English by default.
- When the user explicitly requests another artifact language for the whole initiative/workflow, record that preference in the active `SPEC.md` and preserve it in later phases. A clearly one-off language request applies only to the requested artifact.
- Never infer repository artifact language merely from the conversation language.
- Treat product UI/content language as independent from conversation and artifact language. Infer it from the existing product, repository, Figma, or product context. Ask only when it is materially ambiguous.
- Preserve existing code identifiers, domain terms, and established naming conventions; do not translate them merely because the conversation is in another language.
- For Figma names (components, variables, layers, pages), default to English unless the existing design system uses another convention, the active initiative records another artifact/naming convention, or the user explicitly requests otherwise.


## 1. Resolve the active initiative

Resolve the active `SPEC.md` from the user's request, current conversation, or a single clearly active initiative.

If multiple initiatives are plausible and selecting the wrong one would be material, ask which one to use.

Read, when relevant:

- root/local `AGENTS.md`;
- active `SPEC.md`;
- `product/CONTEXT.md`;
- `design/DESIGN_SYSTEM.md`;
- `engineering/ARCHITECTURE.md` when feasibility affects design;
- relevant existing UI/code;
- linked Figma files/frames.

Do not proceed from chat memory alone when durable project files exist.

## 2. Check the discovery gate

Before designing, verify that the spec establishes the problem, target user/context, desired outcome, and material scope/business rules.

Do not block on every open question. Classify open questions into:

- can design around safely;
- needs prototype/validation;
- blocks product behavior and must be answered now.

Ask only the blocking ones.

## 3. Inspect existing design context before creating

When Figma is available:

- inspect the target file/frames before editing;
- inspect subscribed/available libraries when relevant;
- search the existing design system before creating components or variables;
- inspect relevant tokens/variables;
- use existing components/variants/patterns whenever they fit;
- preserve existing naming and page organization.

When writing through Figma MCP, prefer native editable structure: frames, auto layout, variables, components, variants, text styles, and reusable instances rather than flattened/static approximations.

If no suitable Figma file exists and the connected environment exposes a native file-creation capability, create the minimal appropriate file. If it does not, do not pretend a file was created: ask for/provide the minimum setup needed and continue with everything else that can be done.

## 4. Design in layers

Do not jump directly to high-fidelity visual polish.

Work through these layers in order, iterating when needed:

### A. Outcome and structure

- confirm the outcome the design must enable;
- define information architecture/navigation impact;
- define the primary user flow and meaningful alternate paths;
- identify required content/data hierarchy.

### B. Explore alternatives

When there is meaningful design uncertainty, explore multiple materially different directions before converging.

Examples:

- inline vs modal vs dedicated page;
- progressive disclosure vs all-at-once;
- guided flow vs direct manipulation.

Do not create three cosmetically different versions merely to satisfy an alternatives rule.

Evaluate alternatives against:

- user outcome;
- clarity and cognitive load;
- consistency with existing patterns;
- accessibility;
- feasibility/constraints;
- reversibility and risk.

Record the selected direction and material rationale in the spec.

### C. Interaction design

Define behavior before polish:

- controls and affordances;
- navigation/transitions;
- form behavior and validation;
- feedback;
- recovery;
- permissions;
- keyboard/focus behavior where relevant.

### D. State coverage

Design the states that actually matter to the initiative, including as applicable:

- default;
- loading/skeleton/progress;
- empty;
- partial data;
- success;
- validation errors;
- system/network errors;
- permission denied;
- destructive confirmation;
- disabled/read-only;
- long content/overflow;
- responsive variants;
- relevant first-time/returning states.

Do not create irrelevant states mechanically.

### E. Visual system

Only after structure/behavior are coherent:

- use established typography, color, spacing, radius, grid, and elevation tokens;
- preserve hierarchy and contrast;
- avoid arbitrary values when semantic variables exist;
- create new design-system primitives only when the existing system genuinely lacks what the product needs.

## 5. Accessibility and responsive design are part of the design

Account for, when relevant:

- semantic control intent;
- focus order and visible focus;
- keyboard operation;
- contrast;
- target sizes;
- error identification;
- labels/instructions;
- reduced motion;
- zoom/text resizing;
- responsive layout and content priority.

Do not defer obvious accessibility problems to implementation.

## 6. Product copy

Preserve/infer the product UI language independently from the conversation language.

For new copy:

- optimize for clarity and action;
- match established product terminology;
- avoid inventing policy/legal claims;
- record unresolved content decisions rather than hiding them with placeholder copy.

## 7. Maintain the design-system contract

If design work introduces or changes a reusable token/component/pattern:

- update `design/DESIGN_SYSTEM.md` with the actual new contract;
- keep Figma naming aligned with existing code/design terminology;
- note Figma↔code drift rather than silently resolving it.

Do not duplicate an existing production component with raw styling just because a new Figma frame needs a similar visual.

## 8. Update the initiative spec

Keep `SPEC.md` current with:

- user flow and states;
- selected direction and material trade-offs;
- Figma file/frame/prototype links;
- design assumptions/open questions;
- accessibility/responsive requirements that affect acceptance;
- workflow status.

When design is ready for validation, set design status to complete and validation status to not-started/in-progress as appropriate.

## 9. Finish the phase

Report concisely, in the conversation language:

- the selected design direction;
- Figma work created/updated;
- design-system changes or gaps;
- unresolved risks/questions;
- whether `ux-validate` is the recommended next phase;
- whether `ux-prototype` would answer a remaining interaction question better than more discussion.

Do not automatically invoke another skill.
