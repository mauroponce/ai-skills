# dev-plan evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-plan` after discovery. | Resolves the active initiative from workflow state/SPEC, inspects relevant architecture and seams, creates a durable plan when warranted, and asks only if target ambiguity is material. |
| Non-trivial feature | SPEC, architecture, target code/tests exist. | Grounds plan in relevant seams, creates executable vertical slices, verification, and PLAN/SPEC workflow state. |
| Minimal change | One local, low-risk fix with clear tests. | Explicitly decides a PLAN is unnecessary rather than adding process paperwork. |
| Material unknown | Data retention rule is unresolved. | Does not bury it in implementation steps; investigates and asks only if evidence cannot settle it. |
| Fresh chat | Only repository, SPEC, and PLAN are available. | Plan is sufficient to implement without chat history. |
| Command integrity | Repository scripts are known. | Derives verification commands from repository; does not invent command names. |
