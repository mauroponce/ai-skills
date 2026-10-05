---
name: ux-visual-direction
description: Turn visual references and user preferences into a durable product visual direction before design-system definition or screen design. Use when visual references need to be interpreted, reconciled, or documented; do not use for general UX discovery, design-system implementation, or screen design.
---

# UX Visual Direction

Build and evolve the product's visual intent from references, screenshots, URLs, current UI, Figma, brand material, anti-references, and user preferences. This is a transversal skill: it may be used at any point and repeated as the direction evolves. It defines visual intent; it does not design screens, create a component library, or replace product discovery.

## Language and evidence

Use the user's current language for conversation. Write durable artifacts in English unless the current request explicitly selects another language or the initiative SPEC records one. Product UI language is independent; infer it from explicit instruction, existing product, Figma, and product context, asking only if material and unresolved.

Inspect relevant `AGENTS.md`, `product/CONTEXT.md`, active `SPEC.md`, `design/VISUAL_DIRECTION.md`, `design/DESIGN_SYSTEM.md`, `design/references/`, existing product UI, Figma, and supplied references before asking questions. Use available image, browser, and Figma read tools; disclose inaccessible sources rather than claiming inspection. Separate observed properties, interpretation, preference, and unknowns. Ask only about consequential unresolved choices.

## Reconcile, do not reset

When direction exists, extend it. Compare new material with the current principles, preserve compatible decisions, and surface material conflicts. Do not average incompatible references into generic adjectives. Interpret each reference by its role: for example, use one for density, another for typography, and reject its navigation. Support positive references and anti-references with explicit classifications:

- **USE** — adopt the principle, adapted to this product.
- **AVOID** — explicitly reject the pattern or quality.
- **INSPIRATION ONLY** — useful mood or stimulus, not a product rule.
- **UNRESOLVED** — needs a decision or evidence.

Translate vague words such as “clean”, “premium”, or “modern” into visible, actionable qualities. Capture relevant density, hierarchy, navigation, spacing, surfaces, borders, shape, typography, color, iconography, motion, imagery, and what the product should not feel like. Do not invent a complete brand system or screen layouts.

## Durable output

Create or update `design/VISUAL_DIRECTION.md`, recording overall intent, principles, reference interpretations, anti-references, hierarchy, typography/color/shape/density/spacing/motion/imagery direction, unresolved questions, and source links. Preserve useful supplied visual evidence in `design/references/` when it is available locally and appropriate; do not download or duplicate assets unnecessarily. Keep a `design/references/README.md` with source, intended use, what not to copy, and notes when storing assets. URLs and annotated observations are valid durable evidence when image capture is unavailable.

Keep `VISUAL_DIRECTION.md` consistent with any durable initiative-specific decision in `SPEC.md`; link rather than duplicate. Never silently turn an assumption into a rule. Report sources inspected, decisions captured, files updated, and unresolved conflicts.
