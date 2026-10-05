---
name: ux-prototype-html
description: Create a standalone interactive browser prototype as one self-contained HTML file for a product-design question. Use when behavior is easier to evaluate in a browser than in static Figma; never treat it as production code.
---

# UX Prototype HTML

Answer a specific design question with one runnable browser artifact. This is an exploratory UX deliverable and never production application code.

## Language and context

Use the user's current language in conversation. Artifacts default to English unless explicitly changed now or in the initiative SPEC. Infer product UI language independently from explicit instruction, product, Figma, and context. Read relevant `AGENTS.md`, active `SPEC.md`, `product/CONTEXT.md`, design documentation, existing UI, and relevant Figma before building. Identify the question being explored; do not prototype an entire product when a smaller artifact suffices. Ask only for missing material behavior that cannot be inferred.

## Visual evidence is required

Before styling, inspect when available: `design/VISUAL_DIRECTION.md`, `design/references/` including saved screenshots and their notes, reference URLs recorded there or supplied in the request, existing product UI, `design/DESIGN_SYSTEM.md`, Figma, and optional wireframes. Use available image and browser tools to inspect screenshots and URLs; do not claim inaccessible sources were reviewed. Apply the stored visual principles rather than generic SaaS styling or literal reference cloning. Combine references by intended role (for example, one source for density, another for typography, and another for surface treatment). If a newly supplied reference conflicts materially with the durable visual direction, ask before changing the visual intent and keep `VISUAL_DIRECTION.md` consistent with any accepted durable change.

Use this precedence for visual decisions:

1. Explicit instruction in the current request.
2. Applicable established design-system rules.
3. `design/VISUAL_DIRECTION.md`.
4. Stored screenshots and annotated references.
5. Existing product UI.
6. Sensible fallback.

If the design system and visual direction materially conflict, surface the drift rather than silently choosing.

## Output and behavior

Create exactly one self-contained file at `prototype/<initiative>/prototype.html`, using only HTML, CSS in `<style>`, and vanilla JavaScript in `<script>`. No React, Vue, Svelte, package managers, build tools, framework CDNs, external dependencies, backend, network calls, or remote assets required for core behavior. Start from `assets/prototype-shell.html` when useful and adapt it; do not leave generic demo content.

Implement enough behavior to evaluate the question: navigation, forms, validation, dialogs, menus, transitions, simulated loading, errors, success, sample data, keyboard/focus, and responsive behavior as relevant. Use semantic HTML and label the artifact as a prototype. It must run from a basic local HTTP server, e.g. `python3 -m http.server 8000`.

Update the initiative `SPEC.md` with the prototype path, question, relevant visual sources, and status. Do not claim validation until actual evaluation evidence exists. Report how to run it and what to evaluate next, often with `ux-validate`.
