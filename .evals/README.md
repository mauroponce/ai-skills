# Skill Evals

These human-readable cases are regression contracts for the public skills. Each case gives a realistic setup, prompt, and observable expectations; it can later become automated without coupling the package to a custom test framework.

Run the relevant cases after changing a skill, its template, or shared governance. For an observed failure: reproduce it, add or revise the smallest case that captures it, make the smallest useful skill change, rerun that skill and adjacent-skill cases, then remove obsolete instructions. Do not score wording; evaluate behavior, artifacts, boundaries, and Definition of Done.

| Directory | Skill |
| --- | --- |
| `ux-discovery` | `ux-discovery` |
| `ux-visual-direction` | `ux-visual-direction` |
| `ux-wireframe` | `ux-wireframe` |
| `ux-prototype-html` | `ux-prototype-html` |
| `ux-design-system` | `ux-design-system` |
| `ux-final-design` | `ux-final-design` |
| `ux-validate` | `ux-validate` |
| `dev-discovery` | `dev-discovery` |
| `dev-plan` | `dev-plan` |
| `dev-implement` | `dev-implement` |
| `dev-review` | `dev-review` |

Each suite covers positive and negative behavior where relevant: trigger/boundary correctness, language, just-in-time context, ambiguity, artifact ownership, durable state, forbidden behavior, and completion.
