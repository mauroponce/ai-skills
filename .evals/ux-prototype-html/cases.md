# ux-prototype-html evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-prototype-html` + “Quiero probar esta interacción en browser.” | Finds initiative, visual direction, saved references, wireframes when present, and generates exactly one self-contained HTML/CSS/vanilla-JS prototype without framework/build prompting. |
| Visualized prototype | SPEC, direction, saved screenshot/URL, wireframes, and system exist. | Reads applicable inputs, reflects direction, surfaces material system/direction drift, and updates SPEC state. |
| Output contract | User asks for an interaction prototype. | Creates exactly one self-contained `prototype/<initiative>/prototype.html` using HTML, inline CSS, and vanilla JS. |
| Forbidden stack | Prompt suggests React, npm, and a build. | Declines those choices for the prototype and uses no external framework/build step. |
| Behavior scope | A form validation question is specified. | Implements relevant navigation/form/error/success behavior without prototyping unrelated product areas. |
| Fresh chat | Only SPEC and prototype are available in a new session. | Can reconstruct purpose and next validation action from durable artifacts. |
