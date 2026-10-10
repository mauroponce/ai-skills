# dev-discovery evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-discovery` + “Quiero agregar login con Google a esta aplicación existente en producción.” | Inspects auth routes/models/services/config/tests, detects production implications, asks only material account-linking ambiguity, updates SPEC/state, and does not implement. |
| Rails OAuth profile | Rails app with email/password auth, PostgreSQL, existing users. `$dev-discovery` + “Quiero agregar login con Google.” | Detects Rails/PostgreSQL/auth stack, inspects identity invariant and sessions, activates security/production guidance, surfaces account-linking ambiguity, and persists relevant stable stack facts. |
| Multi-tenant data | Tenant-scoped models, background jobs, and a feature crossing accounts. | Detects tenancy from evidence and evaluates scoping, authorization, uniqueness, job context, and cache boundaries without assuming tenancy where absent. |
| Negative relevance | Static copy change in a React view. | Detects enough context to work safely without producing irrelevant migration, locking, or OAuth analysis. |
| Existing codebase | Spanish request; code/tests reveal webhook flow and auth rules. | Speaks Spanish, inspects relevant paths first, writes artifacts in English, does not ask discoverable facts. |
| UX handoff | Approved UX SPEC and Figma references exist. | Uses the shared SPEC, enriches engineering constraints only, and creates no competing requirements document. |
| Greenfield | Repository has minimal scaffolding. | Inspects it before interviewing stack choices; documents unknowns without inventing architecture. |
| AGENTS boundary | A feature-only deployment constraint appears. | Keeps it in SPEC rather than AGENTS unless it is truly repository-wide. |
| Decision boundary | API compatibility is unresolved. | Asks a targeted consequential question; decides routine local conventions autonomously. |
| Evidence gate | Request names a feature but current code already handles a related path. | Inspects repository and current behavior, identifies material constraints/unknowns, and defines testable requested behavior before claiming readiness. |
| Git explains convention | Unusual module boundary has relevant history. | Reads focused history before replacing it; treats commit rationale as evidence, not immutable policy. |
