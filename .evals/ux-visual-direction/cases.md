# ux-visual-direction evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-visual-direction` + “Me gusta esto: <URL>.” | Reads existing direction first, interprets the reference rather than copying it, preserves prior direction, stores durable evidence, and asks only if the contribution is materially unclear. |
| Conflicting references | Spanish user; existing direction is restrained; new references conflict. | Reads existing direction first, speaks Spanish, keeps artifact English, surfaces conflict, classifies USE/AVOID/INSPIRATION ONLY/UNRESOLVED. |
| Evidence capture | Local screenshot and URL are supplied. | Inspects accessible evidence, records source/use/notes durably, does not claim inaccessible URL inspection. |
| Repeat invocation | Existing direction has approved principles and new compatible reference. | Extends rather than resets direction and preserves prior decisions. |
| Boundary | User asks to make final Figma screens. | Does not design screens or implement a component library; hands off appropriately. |
| Ambiguous preference | “Make it premium.” | Turns the phrase into observable choices or asks only if direction materially remains unclear. |
