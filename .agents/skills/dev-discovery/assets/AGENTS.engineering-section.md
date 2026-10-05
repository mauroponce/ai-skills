# Engineering workflow

Use project context only when relevant to the current task:

- `work/<initiative>/SPEC.md` for required behavior and acceptance criteria.
- `work/<initiative>/PLAN.md` for an approved non-trivial implementation plan.
- `engineering/ARCHITECTURE.md` for stable technical boundaries and conventions.
- `product/CONTEXT.md` and `design/DESIGN_SYSTEM.md` when product or UI behavior is relevant.

Rules:

- Inspect the existing implementation and tests before proposing architecture changes.
- Prefer repository conventions and existing abstractions over introducing new patterns.
- Do not treat a requested mechanism as the requirement until the underlying behavior is clear.
- Ask when a material behavior, security, data, migration, or costly-to-reverse architecture decision is ambiguous.
- Implement non-trivial plans in small verifiable slices.
- Run relevant tests/checks and report what actually ran.
- Avoid unrelated refactors during feature work.
- Keep this file lean; detailed initiative context belongs in `SPEC.md` / `PLAN.md`.
