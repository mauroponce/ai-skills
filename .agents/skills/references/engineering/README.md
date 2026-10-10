# Engineering Context Router

The public DEV skills define goals and boundaries. For each task, inspect the relevant project path and detect its language, framework, frontend, database, queues, tests, and deployment model from dependency manifests and lockfiles, configuration, code, CI, and runbooks. Confirm installed versions when behavior depends on them; a manifest constraint may describe a range. Inspect configuration without exposing secrets.

Use current project code and tests to establish behavior, and follow its working conventions when they are safe. For a material version-specific claim or an unfamiliar API, consult installed source and authoritative documentation for the **detected version**; state uncertainty if it cannot be verified. Do not borrow conventions from another stack or treat the absence of a local technology guide as lack of support.

## Load only relevant cross-cutting references

| Task or risk | Reference |
| --- | --- |
| Authentication, authorization, tenancy, uploads, or sensitive data | [Web security](web-security.md) |
| Existing production app, schema, jobs, APIs, or rollout compatibility | [Production safety](production-safety.md) |
| Behavior change, failure path, or regression risk | [Testing](testing.md) |
| Explicit live/production evidence request | [Runtime diagnostics](runtime-diagnostics.md) |
| Version-sensitive framework or dependency behavior | [Source verification](source-verification.md) |
| Public API, webhook, or integration contract | [API design](api-design.md) |
| Diagnosis, asynchronous work, or release signals | [Observability](observability.md) |
| Demonstrated excess abstraction | [Code simplification](code-simplification.md) |
| Release readiness or execution | [Release safety](release-safety.md) |

`dev-explore` uses references only to clarify current behavior; `dev-audit` evaluates relevant risks and architecture from project evidence. A focused task needs only the affected paths and concerns. Use Git history selectively for unusual design, regression timing, or release identity; churn is a signal, not proof. Do not load every reference merely because a technology or risk category exists.
