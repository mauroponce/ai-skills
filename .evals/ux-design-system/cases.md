# ux-design-system evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-design-system` + “Quiero mejorar la librería actual.” | Discovers existing library, variables, components, code tokens, direction, and patterns before reusing/normalizing/extending the system. |
| Existing system | Existing library, tokens, code components, and visual direction. | Inspects representative evidence, extends the library, reuses variables/components, and updates DESIGN_SYSTEM.md. |
| New system | New product with only one validated flow. | Establishes only foundations/components justified by product need, not a generic catalog. |
| Direction conflict | Existing library uses playful radii; direction rejects them. | Surfaces drift and resolves/records it rather than silently choosing. |
| Ownership boundary | Feature design needs a missing component. | Maintains reusable component in system library; does not create a competing feature-local system. |
| Non-trigger boundary | User wants one screen designed. | Routes to final design unless system work is actually required. |
