# dev-discovery evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-discovery` + “Quiero agregar login con Google a esta aplicación existente en producción.” | Inspects auth routes/models/services/config/tests, detects production implications, asks only material account-linking ambiguity, updates SPEC/state, and does not implement. |
| Existing codebase | Spanish request; code/tests reveal webhook flow and auth rules. | Speaks Spanish, inspects relevant paths first, writes artifacts in English, does not ask discoverable facts. |
| UX handoff | Approved UX SPEC and Figma references exist. | Uses the shared SPEC, enriches engineering constraints only, and creates no competing requirements document. |
| Greenfield | Repository has minimal scaffolding. | Inspects it before interviewing stack choices; documents unknowns without inventing architecture. |
| AGENTS boundary | A feature-only deployment constraint appears. | Keeps it in SPEC rather than AGENTS unless it is truly repository-wide. |
| Decision boundary | API compatibility is unresolved. | Asks a targeted consequential question; decides routine local conventions autonomously. |
