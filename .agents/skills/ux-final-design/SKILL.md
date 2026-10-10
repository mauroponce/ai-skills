---
name: ux-final-design
description: Create production-intent high-fidelity Figma screens for a defined initiative, using confirmed requirements, visual direction, existing design system, wireframes, product context, and validation findings. Use when a flow is ready for detailed screen design.
---

# UX Final Design

Create or evolve high-fidelity Figma designs for an initiative. This produces a durable design artifact, not production application code.

## Invocation contract

The user only needs to state the initiative or desired final-design outcome. Recover active-chat or personal requirements, wireframes, references, validation, design system, and appropriate Figma destination internally.

## Language and decision boundaries

Use the user's current language for questions and explanations. Personal notes default to English unless the user explicitly selects another language now or personal initiative context records it. Determine product UI copy language independently from explicit instruction, existing product, Figma, and context. Inspect before asking; separate known, inferred, assumed, unknown, and conflicting information. Do not silently change product behavior settled in confirmed requirements; ask only when a real behavior blocker remains.

## Reload the durable context

Start with active-chat or personal requirements, applicable wireframes, validation findings, visual direction, design-system contract, saved references, and relevant Figma libraries. Load product context, existing UI, local instructions, or additional files only when needed to resolve the design. Use active conversation context when available; recheck personal notes in a new chat. Inspect Figma structure and available libraries before editing.

Follow [workflow governance](../references/workflow-governance.md). This skill owns the initiative final-design Figma artifact; it records final-design references and feature decisions in chat or useful personal notes, while reusable system changes belong to `ux-design-system`.

## Figma file and design execution

Use Figma MCP. Inspect and reuse an existing appropriate initiative final-design file; otherwise create a separate file named `<Product> — <Initiative> — Final Design`. Keep it separate from the wireframe file and design-system library. Never destroy or convert wireframes into final design. Build editable native Figma structure, reuse variables, library components, variants, and patterns, and avoid unnecessary detachment or duplicated components.

Use personal or existing project visual direction and saved screenshots/reference URLs as visual intent. Interpret each reference for its intended property; do not clone another product or independently invent an aesthetic when direction exists. If a new/ambiguous product has no established direction, recommend `ux-visual-direction` first. A mature product and system can provide sufficient direction without an extra step. If the design system materially conflicts with visual direction, report the drift. If a required component is missing, identify the gap and coordinate its reusable treatment with `ux-design-system`; do not create a parallel mini-system inside the feature file.

Cover applicable high-fidelity screens, responsive layouts, realistic copy, interaction states, loading/empty/success/error/permission states, edge cases, accessibility, and useful prototype connections. Preserve confirmed flow and requirements in chat or personal context. Report Figma links, frames, assumptions, system gaps, and status; save a personal note only when another chat needs it. Report what was designed, what remains unresolved, and whether `ux-validate` is the next useful step.

## Definition of Done

The task is complete when confirmed requirements and relevant Figma/design context have been inspected, the established visual direction and system are respected when available, production-intent screens and relevant states exist in the separate final-design file, and material decisions, gaps, and references are clear in chat or a useful personal handoff.
