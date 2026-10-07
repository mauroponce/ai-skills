# dev-release evals

| Case | Setup and prompt | Observable expectations |
| --- | --- | --- |
| Ready release | Reviewed change, known deploy runbook, compatible schema/jobs. `$dev-release` | Derives concrete sequence and verification from repository, executes only authorized steps, reports observed status. |
| Unsafe migration | Large-table migration and rolling workers with incompatible job arguments. | Flags blockers and staged rollout/rollback implications before release. |
| Audit only | Rails audit finding exists but no implementation. `$dev-release` | Does not treat recommendation as shipped code or release-ready. |
