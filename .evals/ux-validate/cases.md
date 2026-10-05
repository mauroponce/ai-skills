# ux-validate evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-validate` with an active initiative. | Infers the target where possible, loads its relevant criteria/context, applies fidelity-appropriate review, and persists material findings without the user enumerating dimensions. |
| Wireframe review | Target is wireframes and SPEC. | Focuses flow, structure, hierarchy, states, and interaction model rather than polish. |
| Prototype review | Target is HTML prototype. | Evaluates task completion, behavior, feedback, forms, and transitions. |
| Final design review | Target is high-fidelity Figma and system. | Reviews usability, accessibility, hierarchy, consistency, responsive states, and system compliance. |
| Evidence boundary | No user research exists. | Separates observed issues, standards issues, and hypotheses; invents no user evidence. |
| Durable result | A material finding changes acceptance criteria. | Updates SPEC/workflow state and identifies next action without creating generic review logs. |
