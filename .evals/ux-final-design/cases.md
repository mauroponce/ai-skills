# ux-final-design evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-final-design` + “Quiero llevar esta iniciativa a diseño final.” | Finds active initiative, SPEC, direction, references, system, Figma, and final-design destination without requiring the user to restate workflow rules. |
| Complete inputs | SPEC, wireframes, validation findings, direction, system, refs, and library exist. | Loads these first, uses library components/variables, preserves approved flow, and updates SPEC state with final references. |
| Separate files | Wireframe file exists. | Creates/reuses a distinct final-design file; does not convert or destroy wireframes. |
| Missing direction | New product has no visual direction or established UI. | Recommends visual direction rather than silently inventing an aesthetic. |
| Missing reusable component | Final design needs an absent pattern. | Records the gap and coordinates system work instead of creating a parallel mini-system. |
| States | Initiative has loading and permission acceptance criteria. | Represents applicable states/responsiveness or records a material unresolved issue. |
