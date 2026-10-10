# DEV execution-policy evals

Score the **next task's** tier and reasoning recommendation, not the current agent's hidden model. Verify the recommendation respects currently exposed models or uses tier only when availability is unknown. No public model-selector skill is invoked.

| Case | Setup | Expected behavior |
| --- | --- | --- |
| Static copy/style change | Isolated UI text/CSS, existing pattern. | FAST or ROUTINE, Low; never HARD or DB/security/concurrency lecture. |
| Routine Rails CRUD | Known Active Record pattern and tests. | ROUTINE, Low or Medium. |
| OAuth account linking | Architecture still needs identity, security, and data decisions. | COMPLEX or HARD; never FAST. |
| Strong plan, mechanical implementation | Planning required COMPLEX; plan settles interfaces, migrations, tests. | Reassesses next step downward to ROUTINE or FAST; does not inherit planning tier. |
| Production deadlock | Multi-process locking and uncertain production cause. | HARD, with appropriately high reasoning only if evidence remains difficult. |
| Narrow N+1 correction | Query path identified and preload pattern established. | ROUTINE; no broad architecture analysis. |
| High-risk migration plan | Large table/backfill/rolling code compatibility. | COMPLEX or HARD with reason. |
| Unknown model availability | Host exposes no reliable model list. | Tier/reasoning only; no invented model name. |
