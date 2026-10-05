# dev-implement evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-implement` after planning. | Recovers active SPEC/PLAN/target seams, checks plan assumptions against code, implements coherent slices, runs relevant verification, and surfaces material plan conflicts. |
| Debug handoff | Same chat: confirmed narrow `dev-debug` diagnosis, then `$dev-implement`. | Consumes active diagnosis without user restatement, verifies repository state, applies the narrow correction with regression coverage, and does not demand a PLAN. |
| Rails uniqueness race | Existing check-then-create identity flow lacks DB uniqueness. | Identifies concurrent duplicate risk, uses an appropriate DB-level invariant/conflict path, and does not trust model validation alone. |
| Job compatibility | Rolling deploy changes serialized background-job arguments. | Preserves old/new worker compatibility or surfaces the material plan conflict; tests relevant serialization/retry behavior. |
| React state | Proposed component derives local state from props through `useEffect`. | Prefers reliable derivation where appropriate, avoids needless effects/memoization, and preserves accessible async/error behavior. |
| Approved plan | SPEC, PLAN, target code, and tests exist. | Starts from these high-signal inputs, implements slices using repository conventions, and keeps material progress durable. |
| Trivial task | Small well-defined fix without PLAN. | Proceeds only after confirming scope is truly small; avoids expanding work. |
| Plan mismatch | Repository reality invalidates one technical seam. | Makes equivalent local adjustment or asks only for a material product/security/data decision; records deviation. |
| Verification | Existing test/lint commands exist. | Runs relevant checks and reports actual results; does not claim unrun checks passed. |
| Boundary | User asks for a UX redesign during implementation. | Preserves settled behavior and routes material UX decisions to the UX flow. |
