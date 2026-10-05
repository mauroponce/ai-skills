---
name: ux-wireframe
description: Explore low-fidelity information architecture, flows, hierarchy, interaction models, and states in a dedicated Figma wireframe file. Use when a sufficiently understood UX problem needs structural exploration before visual polish.
---

# UX Wireframe

Turn a sufficiently defined initiative into low-fidelity, editable Figma wireframes. This skill explores structure and behavior, not final visual styling or production code.

## Language and inputs

Use the user's current language in conversation. Durable artifacts default to English; precedence is explicit current instruction, initiative `SPEC.md`, then English. Infer product UI language separately from explicit instruction, product, Figma, and context. Inspect `AGENTS.md`, active `SPEC.md`, `product/CONTEXT.md`, relevant UI and existing Figma before asking; classify evidence as known, inferred, assumed, unknown, or conflicting. Ask only about decisions that change the flow or structure.

## Figma workflow

Use Figma MCP and its available read/write capabilities. Inspect existing product files, libraries, frames, and initiative-specific wireframes first. Reuse an appropriate existing wireframe file; otherwise create a dedicated file named `<Product> — <Initiative> — Wireframes`. Do not turn the design-system file or final-design file into the wireframe file. Organize as useful, for example: `00 — Context / Notes`, `01 — Flow`, `02 — Happy Path`, `03 — Alternate States`, `04 — Responsive`, `05 — Explorations`.

Explore only where uncertainty merits it. Focus on information architecture, screen structure, hierarchy, navigation, user flow, interactions, states, edge cases, and responsive structure. Stay deliberately low fidelity: avoid final brand color, polished typography, decorative styling, final component visuals, shadows, and visual identity. `VISUAL_DIRECTION.md` may inform restraint and broad context but must not be materialized as high-fidelity styling. Visual direction and design-system creation are not prerequisites.

If Figma access or MCP operations are unavailable, state the limitation and prepare the smallest useful structure/flow notes without claiming a Figma file was created. Record the Figma file/frame link, alternatives resolved, and structural assumptions in the initiative `SPEC.md`. Never implement production code. Report the resulting flow, file, unresolved decisions, and whether an interactive HTML prototype or validation is useful next.
