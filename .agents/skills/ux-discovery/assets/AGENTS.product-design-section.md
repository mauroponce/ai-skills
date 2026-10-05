# Product and design workflow

Use project context only when relevant to the current task:

- `product/CONTEXT.md` for stable product/domain context.
- `design/DESIGN_SYSTEM.md` for design-system and Figma/code mapping context.
- `work/<initiative>/SPEC.md` for initiative requirements, decisions, validation, and acceptance criteria.
- `engineering/ARCHITECTURE.md` for technical boundaries when implementation is involved.

Rules:

- Inspect existing behavior before proposing new behavior.
- Prefer evidence from the repository, product, and Figma over assumptions.
- Never present assumptions as requirements or user evidence.
- Ask when a material product decision remains ambiguous.
- Reuse existing design-system patterns and components before creating new ones.
- Consider accessibility, responsive behavior, loading, empty, error, permission, and recovery states when relevant.
- Keep the active `SPEC.md` updated when product/design decisions materially change.
- Keep this file lean; detailed feature context belongs in the referenced project files.
