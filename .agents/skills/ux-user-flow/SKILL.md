---
name: ux-user-flow
description: Create or update a FigJam user flow for one user goal, task, entry point, decisions, and outcomes. Use before wireframes when a product journey needs alignment; do not use for screen wireframes, detailed UI flows, customer journeys, or internal process diagrams.
---

# UX User Flow

Create a concise, editable FigJam user flow that aligns the team on how a person completes one meaningful task. This skill maps behavior and decisions before screens are designed.

## Invocation contract

The user only needs to name the experience or task to map. Resolve the active initiative, product context, relevant existing flow, and FigJam destination internally. This is an optional step: use it when a flow needs alignment, not as a prerequisite for every initiative.

## Language and context

Use the user's current language in conversation. Personal notes default to English; precedence is an explicit current instruction, a personal initiative preference, then English. Infer product UI language separately from the existing product, repository, Figma, and supplied context.

Resolve the active initiative from the request, conversation, or an unambiguous personal initiative note or existing project-owned spec. Inspect the smallest useful set of active-chat or personal requirements, product context, relevant implementation, supplied references, and existing FigJam boards. Classify uncertain flow details as known, inferred, assumed, unknown, or conflicting. Ask only about ambiguity that changes the user's goal, entry point, decisions, result, or material alternate path.

Follow [workflow governance](../references/workflow-governance.md). This skill owns the FigJam user-flow artifact and records material decisions and links in chat or useful personal notes.

## Flow boundary

Map one user goal per flow. Include the entry point, meaningful user actions, decisions, alternate outcomes, recovery when it changes the journey, and a clear end state. Omit incidental clicks and implementation detail.

Do not create screen layouts or component-level interactions; hand those off to `ux-wireframe`. Do not broaden the artifact into a customer journey, sitemap, or internal system/process diagram. A detailed per-control UI flow is outside this skill unless it is required to express a material decision in the task.

## FigJam workflow

Use a dedicated FigJam board named `<Product> — <Initiative> — User Flow`. Reuse and update the initiative's existing board when it is present; otherwise create the dedicated board. Do not add the flow to a design-system, wireframe, or final-design file.

Before any FigJam write, load `figma-use` and `figma-use-figjam`; inspect the board with `get_figjam`. Before calling `create_new_file`, load `figma-create-new-file`. Follow those skills' API, font-loading, node-ID, validation, and recovery requirements.

Build an easily scannable board with these areas:

- `00 — Context`: user or role, goal, entry point, and a compact legend.
- `01 — Primary flow`: a left-to-right path. Use rounded rectangles for actions, diamonds for decisions, ellipses for start/end states, and directed connectors between nodes.
- `02 — Alternate paths`: only material branches, positioned below the decision they leave. Label connectors with the decision outcome when necessary.
- `03 — Assumptions / Open questions`: clearly separated notes for unresolved details that could change the flow.

Keep the visual vocabulary consistent. Use neutral styling for normal steps, distinguish success and failure or recovery outcomes clearly, and use space rather than decorative elements to preserve readability. Connectors must attach to their nodes and point in the direction of travel. Use a current screenshot or structural read to verify that the board is complete and legible before finishing.

If FigJam access or MCP operations are unavailable, report the smallest useful flow notes in chat, saving a personal note only if another chat needs it, including the primary flow, material branches, assumptions, and the access limitation. Do not claim that a board was created.

## Durable handoff

For cross-chat continuation, update a concise personal initiative note when the flow produces useful knowledge:

- add the FigJam link;
- record confirmed structural decisions and unresolved material questions in concise sections;
- update the recommended next action when the flow establishes readiness for wireframes or needs validation.

Send the work to `ux-wireframe` when screen structure, states, or responsive behavior need exploration. Send it to `ux-validate` when the flow itself needs an evidence-based review.

## Definition of Done

The initiative and its existing evidence have been inspected; the board or explicit access limitation exists; the artifact shows one coherent goal-oriented flow with meaningful branches and open assumptions; and any needed personal handoff has current links and next action.
