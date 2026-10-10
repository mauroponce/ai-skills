---
name: ux-visual-direction
description: Turn visual references and user preferences into a durable product visual direction before design-system definition or screen design. Use when visual references need to be interpreted, reconciled, or documented; do not use for general UX discovery, design-system implementation, or screen design.
---

# UX Visual Direction

Build and evolve the product's visual intent from references, screenshots, URLs, current UI, Figma, brand material, anti-references, and user preferences. This is a transversal skill: it may be used at any point and repeated as the direction evolves. It defines visual intent; it does not design screens, create a component library, or replace product discovery.

## Invocation contract

The user only needs to state visual intent and optionally attach references. Interpret provided screenshots, links, and Figma references; recover existing direction and durable visual context without requiring workflow instructions in the prompt.

## Language and evidence

Use the user's current language for conversation. Write personal notes in English unless the current request or a personal initiative preference selects another language. Product UI language is independent; infer it from explicit instruction, existing product, Figma, and product context, asking only if material and unresolved.

Start with relevant personal visual direction or existing project-owned direction, supplied references, relevant product UI, and brand context. Load initiative context, design-system detail, Figma, or broader documentation only when it constrains the visual decision. Use available image, browser, and Figma read tools; disclose inaccessible sources rather than claiming inspection. Separate observed properties, interpretation, preference, and unknowns. Ask only about consequential unresolved choices.

Follow [workflow governance](../references/workflow-governance.md). This skill produces visual direction in chat or personal notes and does not modify target repository process docs.

## Reconcile, do not reset

When direction exists, extend it. Compare new material with the current principles, preserve compatible decisions, and surface material conflicts. Do not average incompatible references into generic adjectives. Interpret each reference by its role: for example, use one for density, another for typography, and reject its navigation. Support positive references and anti-references with explicit classifications:

- **USE** — adopt the principle, adapted to this product.
- **AVOID** — explicitly reject the pattern or quality.
- **INSPIRATION ONLY** — useful mood or stimulus, not a product rule.
- **UNRESOLVED** — needs a decision or evidence.

Translate vague words such as “clean”, “premium”, or “modern” into visible, actionable qualities. Capture relevant density, hierarchy, navigation, spacing, surfaces, borders, shape, typography, color, iconography, motion, imagery, and what the product should not feel like. Do not invent a complete brand system or screen layouts.

## Durable output

When useful across chats, create or update a personal `visual-direction.md` note in the Codex workspace, recording overall intent, principles, reference interpretations, anti-references, hierarchy, typography/color/shape/density/spacing/motion/imagery direction, unresolved questions, and source links. Preserve useful supplied visual evidence in the personal workspace `references/` when it is available locally and appropriate; do not download or duplicate assets unnecessarily. Keep a personal `references/README.md` with source, intended use, what not to copy, and notes when storing assets. URLs and annotated observations are valid durable evidence when image capture is unavailable.

Keep personal visual direction consistent with confirmed initiative decisions; link rather than duplicate. Never silently turn an assumption into a rule. Report sources inspected, decisions captured, files updated, and unresolved conflicts.

## Definition of Done

The task is complete when relevant visual evidence and existing direction have been reconciled, actionable visual intent and material conflicts are reported in chat or a useful personal note, useful evidence is referenced or preserved appropriately, and cross-chat context is saved personally when needed.
