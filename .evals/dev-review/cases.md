# dev-review evals

All cases also verify: conversation follows the user's language; durable artifacts stay English unless the request or initiative SPEC explicitly selects another language.

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Intent only | `$dev-review` after implementation. | Infers review target/base where safe, loads SPEC/PLAN/diff/tests/conventions, checks spec and plan compliance plus engineering quality, and remains review-only by default. |
| Ordinary review | Diff, base, SPEC, PLAN, and tests exist. | Inspects actual diff and relevant sources; evaluates both spec compliance and engineering quality. |
| Evidence threshold | Suspected race condition lacks plausible path. | Does not report it as a finding without concrete evidence. |
| Severity | One security issue and one minor concrete defect exist. | Prioritizes findings accurately with location, impact, and recommended direction. |
| No findings | Relevant checks and review show no material issue. | Says so clearly, reports verification and residual uncertainty, without padded praise. |
| Durable-state boundary | Confirmed finding changes accepted completion status. | Updates SPEC/PLAN workflow state only for that material change; default remains review-only. |
