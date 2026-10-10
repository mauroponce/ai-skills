# Public DEV routing evals

Use a small repository fixture appropriate to each prompt. Score the selected user-goal skill and absence of unnecessary public specialists; do not score keyword matching alone. An explicit skill invocation remains authoritative.

| Prompt | Expected route | Boundary |
| --- | --- | --- |
| “Quiero agregar webhooks de Stripe.” | `dev-discovery` | Internally considers API, signatures, idempotency, jobs, DB, and security; asks only consequential unknowns. |
| “En producción los exports están trabados.” | `dev-debug` | Diagnoses without changing source or runtime. |
| “Revisá esta app Rails y decime dónde mejorarla.” | `dev-rails-audit` | General proactive audit needs no checklist. |
| “¿Cómo implementamos la integración ya definida?” | `dev-plan` | Uses existing SPEC and real repository seams. |
| “Implementalo según el plan aprobado.” | `dev-implement` | Implements and verifies without reopening settled decisions. |
| “Revisá este cambio.” | `dev-review` | Reviews actual diff and tests, ideally in a fresh chat. |
| “Quiero llevar el cambio aprobado a producción.” | `dev-release` | Preflights, then obtains concrete production approval. |
| “Esto funciona pero quedó demasiado complejo.” | `dev-rails-audit` for an existing Rails app; `dev-review` for a specific recent diff | No `dev-simplify` public skill; route by target and user goal. |
