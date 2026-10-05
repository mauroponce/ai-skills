---
name: ux-visual-direction
description: Turn visual references and user preferences into a durable product visual direction before design-system definition or screen design. Use when visual references need to be interpreted, reconciled, or documented; do not use for general UX discovery, design-system implementation, or screen design.
---

# UX Visual Direction

Establish how a product or feature should look and feel from the available references, existing product context, and the user's preferences. Extract reusable principles; do not reproduce references literally or blend unrelated styles indiscriminately.

The user's explicit instructions take precedence over workflow defaults in this skill.

## Position in the workflow

Use after `ux-discovery` has established the problem and before design-system definition or `ux-design`. This skill resolves visual character and reference intent. It does not define detailed tokens, component APIs, CSS, or screen layouts.

## User interaction

This is a decision-oriented skill intended to start in Plan mode (`/plan`). It cannot switch the host's mode. See [the shared interaction policy](../references/interactive-decision-policy.md) for the Codex and Claude Code interaction rules, including when to leave read-only Plan mode to save artifacts.

## 1. Inspect before asking

Inspect relevant project instructions and context, including as applicable:

- `AGENTS.md`, the active initiative `SPEC.md`, and `product/CONTEXT.md`;
- `design/VISUAL_DIRECTION.md` and `design/DESIGN_SYSTEM.md`;
- `design/references/README.md` and files in `design/references/`;
- existing product screens and relevant Figma references when available;
- references supplied in the current session: screenshots, local images, URLs, or written notes.

Use available image-viewing tools for local images and screenshots. Open supplied URLs and inspect relevant content when browsing is available. Inspect Figma through available read capabilities when a reference is provided and access exists. If a source cannot be accessed, state that limitation and continue with the evidence available. Do not claim to have inspected inaccessible material.

If `design/references/README.md` exists, use it to understand each reference's intended role. A useful convention for future entries is `Reference`, `Source`, `Use for`, `Do not copy`, and `Notes`, but do not require it for references supplied directly in the session.

Analyze observable properties that matter to the product, such as density, layout, hierarchy, navigation, spacing rhythm, surface treatment, borders, radius, shadows, typography, color, iconography, forms, lists/tables, interaction patterns, overlays, emphasis, and overall character. Record only relevant observations; do not produce a generic visual audit.

Keep three kinds of statements distinct:

- **Observed:** visible or documented properties of a reference or current product.
- **Interpretation:** what those properties suggest or how they may serve the product.
- **Preference:** what the user wants to adopt, avoid, prioritize, or limit.

Never ask the user to describe something the inspected evidence makes clear.

## 2. Resolve visual choices

If `design/VISUAL_DIRECTION.md` exists, work in **extend** mode: read it, compare new references with it, and identify compatible and conflicting patterns. Preserve the established direction. Ask before introducing a materially different direction; do not silently redefine it.

Otherwise work in **bootstrap** mode and form a coherent direction from the product context and references.

Treat references as having roles when useful (for example, density, layout, navigation, forms, interaction, typography, or visual style). Support positive and negative references. Record what should influence the product, what should not be copied, and whether an influence applies broadly or only to one aspect.

When references conflict, name the concrete tension and ask which should dominate or how to combine them. Ask only about genuine ambiguity in adoption, rejection, priority, or combination. Use the host's native structured question mechanism when available; otherwise ask one concise question in ordinary conversation. Ask at most 1–3 questions at a time, then stop once the direction is clear enough to guide system definition.

Do not ask generic questions such as “What do you like about this screenshot?” Instead identify what is visible and ask which specific attributes should carry forward. If the user's preference is not needed to make a durable decision, state a reasonable, evidence-based interpretation and mark it as such.

## 3. Write durable direction

Create or update `design/VISUAL_DIRECTION.md`, unless the repository has a clearly established alternative location. Document decisions, not an interview transcript or a catalog of every visible detail. Make the direction usable without repeatedly reopening the original references.

Use a structure appropriate to the product, typically:

```markdown
# Visual Direction

## Design character
## Principles
## Density and spacing
## Layout and hierarchy
## Surfaces
## Typography direction
## Color direction
## Navigation and interaction
## Reference matrix
## Avoid
## Open visual questions
```

Describe color philosophy, typographic tone and hierarchy, surface behavior, and spacing principles without inventing a complete token system. Include a reference matrix for important sources: the role or influence of each, what to adopt, and what not to copy. Keep unresolved questions only when they materially affect future design-system or screen work. Do not fill sections with guesses; label meaningful assumptions or omit irrelevant sections.

If an existing visual direction is extended, preserve its valid decisions and make material changes explicit with their rationale. Do not overwrite unrelated design documentation.

## 4. Finish

Report the direction captured, the evidence/preferences that shaped it, files created or updated, and material open questions. State whether the result is ready for `ux-design-system` or the repository's equivalent design-system phase. Do not automatically invoke another skill.
