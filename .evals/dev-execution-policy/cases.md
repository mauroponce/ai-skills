# DEV execution-policy evals

Score the **next task's** tier and reasoning recommendation, not the current Codex session's hidden model. Verify the recommendation respects currently exposed Codex models or uses tier only when availability is unknown. No public model-selector Codex skill is invoked.

| Case | Setup | Expected behavior |
| --- | --- | --- |
| Static copy/style change | Isolated UI text/CSS, existing pattern. | FAST or ROUTINE, Low; never HARD or DB/security/concurrency lecture. |
| Scoped system exploration | One Rails flow with known entry point. | ROUTINE; does not escalate solely because it traces several layers. |
| Broad legacy exploration | Cross-domain mapping with unclear tenancy and several integrations. | COMPLEX when uncertainty justifies it; avoids HARD by default. |
| Routine Rails CRUD | Known Active Record pattern and tests. | ROUTINE, Low or Medium. |
| OAuth account linking | Architecture still needs identity, security, and data decisions. | COMPLEX or HARD; never FAST. |
| Strong plan, mechanical implementation | Planning required COMPLEX; plan settles interfaces, migrations, tests. | Reassesses next step downward to ROUTINE or FAST; does not inherit planning tier. |
| Production deadlock | Multi-process locking and uncertain production cause. | HARD, with appropriately high reasoning only if evidence remains difficult. |
| Narrow N+1 correction | Query path identified and preload pattern established. | ROUTINE; no broad architecture analysis. |
| High-risk migration plan | Large table/backfill/rolling code compatibility. | COMPLEX or HARD with reason. |
| Unknown model availability | Codex environment exposes no reliable model list. | Tier/reasoning only; no invented model name. |
| Codex-only mapping | The next task needs COMPLEX capability and a current Codex model is exposed. | Recommends the mapped Codex model and reasoning effort; creates no Claude/Gemini mapping or provider abstraction. |
