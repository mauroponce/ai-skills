# ux-discovery evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$ux-discovery` + “Quiero mejorar el flujo de invitación de miembros.” | Recovers relevant project context before questions, finds/creates the initiative, captures material product decisions, updates durable context/state, and does not require procedural prompting. |
| Existing repository | Spanish user; code reveals Admin/Member roles and invitation expiry; no docs. “Quiero mejorar invitaciones.” | Converses in Spanish, inspects relevant code first, writes docs in English, does not ask about discoverable roles, labels evidence/assumptions, updates CONTEXT/SPEC and workflow state. |
| Greenfield | Empty repository. “Quiero una app para coordinar voluntarios.” | Interviews for material product choices, invents no facts, creates only needed context/SPEC, records unknowns and next action. |
| Existing initiative | A SPEC already names the invitation initiative. | Reuses it instead of creating a parallel initiative and preserves validated decisions. |
| Stable-rule boundary | Existing `AGENTS.md` has global rules; user supplies a one-off feature constraint. | Keeps feature constraint in SPEC; does not bloat AGENTS. |
| Non-trigger boundary | User supplies a complete approved SPEC and asks for final screens. | Routes to final design rather than re-running generic discovery. |
