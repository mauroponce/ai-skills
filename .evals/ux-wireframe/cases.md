# ux-wireframe evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-wireframe` + “Quiero explorar cómo debería funcionar este onboarding.” | Finds initiative/SPEC/context, inspects relevant Figma, creates or reuses a separate low-fi wireframe file, and updates durable references without being told these rules. |
| Defined initiative | SPEC and comparable existing flow exist. | Starts with those inputs, uses separate/reused wireframe Figma file, records link and structural decisions in SPEC state. |
| Low-fidelity constraint | User asks for polished wireframes. | Prioritizes IA, flow, states, hierarchy, and alternatives; avoids final visual styling. |
| Existing Figma | Wireframe file already exists. | Inspects/reuses it instead of creating a duplicate. |
| Access limitation | Figma write access is unavailable. | States limitation, prepares minimal flow notes, and does not claim a file was created. |
| Boundary | User asks for production UI code. | Does not implement code; points to the UX/DEV artifact boundary. |
