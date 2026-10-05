---
name: ux-final-design
description: Create production-intent high-fidelity Figma screens for a defined initiative, using its SPEC, visual direction, existing design system, wireframes, product context, and validation findings. Use when a flow is ready for detailed screen design.
---

# UX Final Design

Create or evolve high-fidelity Figma designs for an initiative. This produces a durable design artifact, not production application code.

## Invocation contract

The user only needs to state the initiative or desired final-design outcome. Recover the active SPEC, wireframes, references, validation, design system, and appropriate Figma destination internally.

## Language and decision boundaries

Use the user's current language for questions and explanations. Repository artifacts default to English unless the user explicitly selects another language now or the initiative SPEC records it. Determine product UI copy language independently from explicit instruction, existing product, Figma, and context. Inspect before asking; separate known, inferred, assumed, unknown, and conflicting information. Do not silently change product behavior settled in the SPEC; ask only when a real behavior blocker remains.

## Reload the durable context

Start with the active SPEC, applicable wireframes, validation findings, visual direction, design-system contract, saved references, and relevant Figma libraries. Load product context, existing UI, local instructions, or additional files only when needed to resolve the design. Do not depend on chat memory. Inspect Figma structure and available libraries before editing.

Follow [workflow governance](../references/workflow-governance.md). This skill owns the initiative final-design Figma artifact; it updates SPEC/state with final-design references and feature decisions, while reusable system changes belong to `ux-design-system`.

## Figma file and design execution

Use Figma MCP. Inspect and reuse an existing appropriate initiative final-design file; otherwise create a separate file named `<Product> — <Initiative> — Final Design`. Keep it separate from the wireframe file and design-system library. Never destroy or convert wireframes into final design. Build editable native Figma structure, reuse variables, library components, variants, and patterns, and avoid unnecessary detachment or duplicated components.

Use `VISUAL_DIRECTION.md` and saved screenshots/reference URLs as the durable visual intent. Interpret each reference for its intended property; do not clone another product or independently invent an aesthetic when direction exists. If a new/ambiguous product has no established direction, recommend `ux-visual-direction` first. A mature product and system can provide sufficient direction without an extra step. If the design system materially conflicts with visual direction, report the drift. If a required component is missing, identify the gap and coordinate its reusable treatment with `ux-design-system`; do not create a parallel mini-system inside the feature file.

Cover applicable high-fidelity screens, responsive layouts, realistic copy, interaction states, loading/empty/success/error/permission states, edge cases, accessibility, and useful prototype connections. Preserve flow and requirements in the SPEC. Record Figma links, frames, assumptions, system gaps, and status in the initiative `SPEC.md`. Report what was designed, what remains unresolved, and whether `ux-validate` is the next useful step.

## Definition of Done

The task is complete when the active SPEC and relevant Figma/design context have been inspected, the established visual direction and system are respected when available, production-intent screens and relevant states exist in the separate final-design file, and material decisions, gaps, and references are current in the initiative SPEC/workflow state.
