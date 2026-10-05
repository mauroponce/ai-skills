---
name: ux-design-system
description: Create or evolve a reusable Figma design system and its repository-facing contract, independently of any one screen. Use when foundations, tokens, components, variants, patterns, or system documentation need focused work.
---

# UX Design System

Create or evolve the reusable system that supports the product. This work is independent of a particular initiative screen and does not implement production code.

## Invocation contract

The user only needs to state whether they want to establish or improve the system. Discover existing Figma, code, visual-direction, and product evidence before deciding whether to reuse, normalize, or extend it.

## Language and inspection

Use the user's current language for discussion; write artifacts in English unless explicitly overridden now or in the initiative SPEC. Product UI language is independent and inferred from explicit instruction, current product, Figma, and context. Start with visual direction, existing system documentation, relevant Figma libraries, representative UI, and existing tokens/components. Inspect code or active specs only when useful for consistency or demand. Distinguish known, inferred, assumed, unknown, and conflicting facts. Ask only about material system decisions that repository/Figma evidence cannot resolve.

Follow [workflow governance](../references/workflow-governance.md). This skill owns the reusable Figma library and `DESIGN_SYSTEM.md`; feature skills should surface gaps rather than silently creating a competing system.

## Work in the existing system

Use the existing Figma library/file when it can be extended. Otherwise create a dedicated `<Product> — Design System` file/library. Do not create a duplicate library because the current one is unfamiliar. Inspect available Figma components, variables, variants, and publication conventions before editing. Reuse before creating, preserve naming and existing structure, and make incremental changes.

When `design/VISUAL_DIRECTION.md` exists, read it before defining or materially changing foundations. Treat it as the durable visual intent and translate it into reusable rules; surface drift rather than silently contradicting it. Work from visual direction to foundations, variables/tokens, primitives, components, variants, patterns, and documentation. Build only what actual product needs justify, not a generic catalog. Possible foundations include color, typography, spacing, radius, elevation, grid, breakpoints, and motion.

Update `design/DESIGN_SYSTEM.md` to describe the actual Figma file/library, foundations and tokens, components/patterns, conventions, accessibility, code mappings, known gaps/drift, and links. Reuse existing documentation conventions and preserve useful content. Do not duplicate all Figma details in Markdown. If a visual direction is not established and the product is new or ambiguous, recommend `ux-visual-direction`; mature existing UI may already establish sufficient intent. Report changes, sources, missing components, and open questions. Do not design a feature screen or write production code.

## Definition of Done

The task is complete when relevant visual direction and existing system evidence have been inspected, reusable changes are made in the appropriate Figma library or a clear limitation is recorded, `DESIGN_SYSTEM.md` reflects the actual contract and drift, and material system decisions are durable without designing a feature screen or production code.
