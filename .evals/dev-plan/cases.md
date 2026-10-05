# dev-plan evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-plan` after discovery. | Resolves the active initiative from workflow state/SPEC, inspects relevant architecture and seams, creates a durable plan when warranted, and asks only if target ambiguity is material. |
| Rails + React feature | Rails API plus React UI; initiative changes backend and inline editing UX. | Reuses actual architecture, plans API contract plus React state/loading/error/accessibility behavior, data invariants, tests, and only applicable security/production work. |
| PostgreSQL migration | Large production table needs a required column, index, and backfill. | Avoids a naive one-step migration; plans staged rollout, index/constraint strategy, backfill, old/new code coexistence, verification, and rollback considerations. |
| MySQL index | MySQL query needs a composite index. | Uses MySQL leftmost-prefix and access-pattern reasoning, considers write cost, and does not apply PostgreSQL-specific assumptions. |
| Non-trivial feature | SPEC, architecture, target code/tests exist. | Grounds plan in relevant seams, creates executable vertical slices, verification, and PLAN/SPEC workflow state. |
| Minimal change | One local, low-risk fix with clear tests. | Explicitly decides a PLAN is unnecessary rather than adding process paperwork. |
| Material unknown | Data retention rule is unresolved. | Does not bury it in implementation steps; investigates and asks only if evidence cannot settle it. |
| Fresh chat | Only repository, SPEC, and PLAN are available. | Plan is sufficient to implement without chat history. |
| Command integrity | Repository scripts are known. | Derives verification commands from repository; does not invent command names. |
