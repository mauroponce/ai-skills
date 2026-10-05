# dev-review evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-review` after implementation. | Infers review target/base where safe, loads SPEC/PLAN/diff/tests/conventions, checks spec and plan compliance plus engineering quality, and remains review-only by default. |
| Bug-fix review | Fresh chat after a fix whose original diagnosis stayed in a prior chat. | Reconstructs the bug scenario from code/tests/durable context where possible, checks that the change addresses cause rather than masks the symptom, and asks only for minimal missing context. |
| Account linking | OAuth callback links accounts solely by matching email. | Activates security review, examines provider identity/ownership/session implications, and reports evidence-based risk rather than assuming linking is safe. |
| React effect | Changed component uses `useEffect` to synchronize derivable state. | Identifies duplicated state/effect risk when it is real, considers stale async behavior and accessibility, and does not demand memoization mechanically. |
| Production migration | PostgreSQL migration adds non-null default column on a large production table. | Reviews staged migration, locks/rewrites, backfill, deploy compatibility, and rollback evidence with appropriate severity. |
| Job rollout | Changed job argument format during rolling deploy. | Identifies concrete old/new worker compatibility risk and its recovery direction. |
| Negative relevance | CSS-only diff with no data/auth changes. | Does not emit irrelevant transaction, database, or security findings; reviews actual UI/accessibility/convention risk. |
| Ordinary review | Diff, base, SPEC, PLAN, and tests exist. | Inspects actual diff and relevant sources; evaluates both spec compliance and engineering quality. |
| Evidence threshold | Suspected race condition lacks plausible path. | Does not report it as a finding without concrete evidence. |
| Severity | One security issue and one minor concrete defect exist. | Prioritizes findings accurately with location, impact, and recommended direction. |
| No findings | Relevant checks and review show no material issue. | Says so clearly, reports verification and residual uncertainty, without padded praise. |
| Durable-state boundary | Confirmed finding changes accepted completion status. | Updates SPEC/PLAN workflow state only for that material change; default remains review-only. |
